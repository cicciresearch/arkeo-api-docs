# LED Commands

The light (LED) target provides commands to control the multiLED control.

---

## Command Index

| Command | Description |
|----------|-------------|
| [GetStatus](#getstatus) | Returns the connection status of the light controller. |
| [SetValues](#setvalues) | Set the values of the light controller channels. |

---

### GetStatus

**Description**  
Returns the connection status of the light controller. The `boards` field is an array as there may be multiple boards present in the system. The boards are uniquely identified by their address.

**Example Request**  

```json
{
  "target": "LED",
  "command": "GetStatus",
  "request_id": 401
}
```

**Example Response**  

```json
{
  "status": "ok",
  "data": {
    "connected":true,
    "driver":"LVVISA",
    "boards":[
      {
        "address":1,
        "connected":true,
        "values":[0,0,0,0,0,0,0,0,0,0,0,0]
      }
    ]
    
  },
  "request_id": 401
}
```

---

### SetValues

**Description**  
Set the values of the light controller channels. Each value in the `values` array represents one channel’s desired output. Values must be between 0 (off) and 1 (maximum). Values provided outside this range will be coerced.

!!! Warning
    The size of the provided `values` array must match the number of channels. If not, the command is ignored and an error message is returned.

**Example Request**  

```json
{
  "target": "LED",
  "command": "SetValues",
  "parameter": {
    "address":1,
    "values":[0,0,0.8,0,0,0,0,0,0,0,0,0]
  },
  "request_id": 402
}
```

**Example Response**  

```json
{
  "status": "ok",
  "data": { "state":"ok" },
  "request_id": 402
}
```

```json
{
  "state":"error",
  "error":{
    "code":1001,
    "message":"Invalid array size: 1. Must match number of channels: 12"
  }
}
```
