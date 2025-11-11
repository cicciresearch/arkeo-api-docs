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

---

## StartRoutine

**Description**  
Starts a measurement routine by name. Only one routine can be active at a time.

### Example Request
```json
{
  "target": "MAIN",
  "command": "StartRoutine",
  "parameter": { "routine_name": "JV" },
  "request_id": 10
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state": "OK"
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