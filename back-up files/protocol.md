Request Format

Every request message must contain the following JSON structure:

All commands follow a standard message structure containing a **target**, a **command**, optional **parameters**, and a **request ID** to match responses.

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