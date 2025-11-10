# MAIN Commands

Commands in this section control the high-level state of the Arkeo All-in-One application.  
They are responsible for selecting and managing routines.

---

## Command Index

| Command | Description |
|----------|-------------|
| [StartRoutine](#startroutine) | Launch a measurement routine by name. |
| [GetActiveRoutine](#getactiveroutine) | Query which routine is currently active. |
| [GetAvailableRoutines](#getavailableroutines) | Retrieve the list of available routine plugins. |
| [CloseRoutine](#closeroutine) | Stop and unload the active routine. |

---

## StartRoutine

**Description**  
Starts a measurement routine by name. Only one routine can be active at a time.

### Example Request
```json
{
  "target": "MAIN",
  "command": "StartRoutine",
  "params": { "routine_name": "JV" },
  "request_id": 10
}
````

### Example Response

```json
{
  "status": "OK",
  "data": {
    "started": true,
    "routine": "JV"
  },
  "request_id": 10
}
```

---

## GetActiveRoutine

**Description**
Returns the name of the currently active routine. If no routine is active, an empty string is returned.

### Example Request

```json
{
  "target": "MAIN",
  "command": "GetActiveRoutine",
  "params": {},
  "request_id": 11
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "routine": "JV" },
  "request_id": 11
}
```

---

## GetAvailableRoutines

**Description**
Returns a list of all available routine plugins that can be loaded.

### Example Request

```json
{
  "target": "MAIN",
  "command": "GetAvailableRoutines",
  "params": {},
  "request_id": 12
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "routines": ["JV", "MPPT", "Impedance", "Luminescence"]
  },
  "request_id": 12
}
```

---

## CloseRoutine

**Description**
Stops and unloads the currently active routine. The system will return to the idle state.

### Example Request

```json
{
  "target": "MAIN",
  "command": "CloseRoutine",
  "params": {},
  "request_id": 13
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "closed": true },
  "request_id": 13
}
```

```
