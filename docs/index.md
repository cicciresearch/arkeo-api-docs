# Arkeo All-in-One API Documentation

The Arkeo All-in-One API allows external applications to control and query the Arkeo measurement software. Communication happens using the TCP protocol on port 6360, enabling users to perform a variety of commands manage measurements. Each connected client can send JSON-encoded requests and receive JSON responses.

All commands follow a standard message structure containing a **target**, a **command**, optional **parameters**, and a **request ID** to match responses.

---
## 🔧 Request Format

Every request message must contain the following JSON structure:

```json
{
  "target": "<TARGET>",
  "command": "<COMMAND>",
  "parameter": { ... },
  "request_id": 42  //optional
}
```

* **target**: Specifies which module should handle the command.
  Example targets: `"MAIN"`, `"ROUTINE"`, `"TMPCTL"`, `"MUX"`.
* **command**: The specific instruction for that target.
* **parameter**: Optional command parameters (may be empty `{}`).
* **request_id**: An integer identifier assigned by the client.

---

**Note**: Each command must be preceded by a 4-byte integer indicating the total length of the command.

## Response Format

Each command returns a structured JSON response. The response always includes a `status` field and the same `request_id` as the corresponding request. Similar to the request, each response is preceded by a 4-byte integer indicating the total length of the command.

```json
{
  "status": "OK" | "ERROR",
  "data": { ... },     // present if status = "OK"
  "error": { ... },    // present if status = "ERROR"
  "request_id": 42
}
```

### Response Keys

* **status**: Indicates success or failure (`"OK"` or `"ERROR"`).
* **data**: Command-specific response payload.
* **error**: Only present if an error occurred; contains fields such as:
  ```json
  { "code": 101, "message": "Invalid parameters" }
  ```
* **request_id**: Echoes the ID from the request.

---

## Targets Overview

| Target      | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| **MAIN**    | Controls system-wide operations, including routine activation.              |
| **ROUTINE** | Handles measurement routines such as JV, MPPT, Impedance, and Luminescence. |
| **TMPCTL**  | Controls and monitors temperature controllers.                              |
| **MUX**     | Manages multiplexer connections.                                            |

---