# API Protocol

The ARKEO API uses a **TCP-based request-response protocol** with **length-prefixed JSON messages**.

External clients connect to a running ARKEO application and exchange structured JSON commands to control measurements, query state, and configure hardware-related subsystems.

This page describes the **wire-level protocol**, independent of any specific target or command.

---

## Transport and connection model

- **Transport**: TCP  
- **Default port**: `6360`  
- **Connection type**: persistent  

The ARKEO application acts as a TCP server. Clients establish a connection and keep it open for the duration of their interaction. The protocol is strictly **sequential**: One request is sent and one response is received. Only then may the next request be sent.

---

## Message framing

Every message exchanged over the connection is framed as:

```
[4-byte length][JSON payload]
```

The 4-byte length prefix is:

- **Unsigned**
- **Big-endian**
- Specifies the number of bytes of the JSON payload only  
- Does **not** include the 4 bytes of the length field itself

After reading the length prefix, the receiver reads exactly that number of bytes and interprets them as a UTF-8 encoded JSON object.

---

## Request message format

Each request consists of a single JSON object with the following structure:

```json
{
  "target": "<TARGET>",
  "command": "<COMMAND>",
  "parameter": { ... },
  "request_id": 42
}
```

### Request fields

| Field        | Required | Description |
|--------------|----------|-------------|
| `target`     | Yes      | Logical subsystem that handles the command |
| `command`    | Yes      | Command name for the selected target |
| `parameter`  | Yes      | Command parameters (may be an empty object) |
| `request_id` | No       | Client-defined identifier |

All fields except `request_id` are mandatory.

The `request_id` field is optional and, if present, is echoed back in the corresponding response. It allows clients to correlate requests and responses but does not affect command execution.

---

## Response message format

Each request produces exactly one response.

A successful response has the form:

```json
{
  "status": "ok",
  "data": { ... },
  "request_id": 42
}
```

An unsuccessful response has the form:

```json
{
  "status": "error",
  "error": {
    "code": 101,
    "message": "Invalid parameters"
  },
  "request_id": 42
}
```

### Response fields

| Field        | Description |
|--------------|-------------|
| `status`     | `"ok"` or `"error"` |
| `data`       | Command-specific response data (only if status = OK) |
| `error`      | Error information (only if status = ERROR) |
| `request_id` | Echoes the request ID, if provided |

---

## Error semantics

The API distinguishes between **protocol-level errors** and **command-level errors**.

- A response with `"status": "error"` indicates that the main JSON request structure is invalid and could not be processed correctly.
- A response containing an `"error"` object indicates that the request was syntactically valid, but the target rejected it, most commonly due to invalid or missing command parameters.

In both cases, the response is well-formed JSON and follows the standard framing rules.

Transport-level errors (such as connection loss) are not represented as API responses and must be handled by the client at the socket level.

---
