# Python Example

This example demonstrates how to communicate with the Arkeo All-in-One API
using Python over TCP sockets.  
It shows how to send JSON commands, receive responses, and handle basic errors.

---

## Example Overview

The script:

1. Connects to the API over TCP.
2. Sends a `StartRoutine` command.
3. Waits for the response.
4. Closes the socket connection.

---

## Example Code

```python
import socket
import json
import struct

HOST = "127.0.0.1"     # IP address of the Arkeo API server
PORT = 6360            # Default TCP port

def send_command(sock, message):
    """Send a JSON message with a 4-byte length prefix."""
    data = json.dumps(message).encode("utf-8")
    length = struct.pack(">I", len(data))
    sock.sendall(length + data)

def receive_response(sock):
    """Receive a JSON response with a 4-byte length prefix."""
    header = sock.recv(4)
    if len(header) < 4:
        raise ConnectionError("Incomplete header received.")
    msg_len = struct.unpack(">I", header)[0]
    payload = sock.recv(msg_len)
    return json.loads(payload.decode("utf-8"))

def main():
    # Connect to the API
    with socket.create_connection((HOST, PORT)) as sock:
        print(f"Connected to {HOST}:{PORT}")

        # Example command: start a routine
        command = {
            "target": "MAIN",
            "command": "StartRoutine",
            "params": {"routine": "Luminescence"},
            "request_id": 1001
        }

        # Send the command
        send_command(sock, command)
        print("Command sent:", json.dumps(command, indent=2))

        # Wait for and print the response
        response = receive_response(sock)
        print("Response received:", json.dumps(response, indent=2))

if __name__ == "__main__":
    main()
```

---

## Example Output

A typical session looks like this:
```text
Connected to 127.0.0.1:6360
Command sent:
{
  "target": "MAIN",
  "command": "StartRoutine",
  "params": {"routine": "Luminescence"},
  "request_id": 1001
}

Response received:
{
  "status": "OK",
  "data": {"status": "OK"},
  "request_id": 1001
}
```
## Notes

- The API uses a **4-byte big-endian header** that specifies the message length.
- Each request and response is transmitted as a **UTF-8 encoded JSON string**.
- The `request_id` field ensures that each response can be matched with its originating command.
- When an error occurs, the API responds with `"status": "ERROR"` and includes an `"error"` object describing the issue.
- Communication is stateless beyond the active TCP session; each message is self-contained and includes all required parameters.
- Commands and responses are not compressed or encrypted by default; if required, encryption must be implemented at the transport layer.
- The connection is persistent — multiple commands can be sent sequentially without reconnecting.


---
