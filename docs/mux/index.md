# MUX Commands

The multiplexer (MUX) target provides commands to control channel connections.
Each channel can be individually connected or disconnected, or all channels can be updated simultaneously.

---

## Command Index

| Command | Description |
|----------|-------------|
| [Connect](#connect) | Connects the multiplexer. |
| [Disconnect](#disconnect) | Disconnects the multiplexer. |
| [GetStatus](#getstatus) | Gets the status of the multiplexer. |
| [SetStatus](#setstatus) | Set the state of each multiplexer channel. |

---

### Connect

**Description**  
Connect to the multiplexer

**Example Request**  
```json
{
  "target": "MUX",
  "command": "Connect",
  "request_id": 401
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 401
}
```

---

### Disconnect

**Description**  
Disconnect from the multiplexer

**Example Request**  

```json
{
  "target": "MUX",
  "command": "Disconnect",
  "request_id": 402
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 402
}
```

---

### GetStatus

**Description**  
Returns the connection status of all multiplexer channels as a Boolean array.
Each element represents one channel, where `true` means connected and `false` means disconnected.

**Example Request**  

```json
{
  "target": "MUX",
  "command": "GetStatus",
  "request_id": 401
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": {
    "connected":true,
    "firmware":"Multiplexer_v1.1",
    "nrRelays":4,
    "status":[false, false, false, true]
  },
  "request_id": 403
}
```

---

### SetStatus

**Description**  
Sets the connection status for all channels simultaneously.
Each Boolean value in the `channels` array represents one channel’s desired state.

**Example Request**  

```json
{
  "target": "MUX",
  "command": "SetStatus",
  "parameter": {
    "state": [true, false, false, true, true, false]
  },
  "request_id": 404
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 404
}
```
