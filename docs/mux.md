# MUX Commands

The multiplexer (MUX) target provides commands to control channel connections.
Each channel can be individually connected or disconnected, or all channels can be updated simultaneously.

---

## Command Index

| Command | Description |
|----------|-------------|
| [Connect](#connect) | Connect a specific channel. |
| [Disconnect](#disconnect) | Disconnect a specific channel. |
| [GetStatus](#getstatus) | Retrieve the connection status of all channels. |
| [SetStatus](#setstatus) | Set the connection state for all channels at once. |

---

## Connect

**Description**  
Connects a specific channel on the multiplexer.  
If the channel is already connected, this command has no effect.

### Example Request
```json
{
  "target": "MUX",
  "command": "Connect",
  "parameter": { "channel": 3 },
  "request_id": 401
}
````

### Example Response

```json
{
  "status": "OK",
  "data": {
    "connected": true,
    "channel": 3
  },
  "request_id": 401
}
```

---

## Disconnect

**Description**
Disconnects a specific channel on the multiplexer.
If the channel is already disconnected, the command has no effect.

### Example Request

```json
{
  "target": "MUX",
  "command": "Disconnect",
  "parameter": { "channel": 3 },
  "request_id": 402
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "disconnected": true,
    "channel": 3
  },
  "request_id": 402
}
```

---

## GetStatus

**Description**
Returns the connection status of all multiplexer channels as a Boolean array.
Each element represents one channel, where `true` means connected and `false` means disconnected.

### Example Request

```json
{
  "target": "MUX",
  "command": "GetStatus",
  "parameter": {},
  "request_id": 403
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "channels": [true, false, true, false, false, true]
  },
  "request_id": 403
}
```

---

## SetStatus

**Description**
Sets the connection status for all channels simultaneously.
Each Boolean value in the `channels` array represents one channel’s desired state.

### Example Request

```json
{
  "target": "MUX",
  "command": "SetStatus",
  "parameter": {
    "channels": [true, false, false, true, true, false]
  },
  "request_id": 404
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "channels": [true, false, false, true, true, false]
  },
  "request_id": 404
}
```
