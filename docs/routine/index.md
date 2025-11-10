# ROUTINE Commands

Commands in this section are shared across all measurement routines.
Each routine can be started from the MAIN target, after which the commands below
control the measurement process, retrieve results, and manage settings.

---

## Command Index

| Command | Description |
|----------|-------------|
| [StartMeasurement](#startmeasurement) | Start a measurement within the active routine. |
| [StopMeasurement](#stopmeasurement) | Stop the current measurement. |
| [ApplySettings](#applysettings) | Apply configuration parameters to the routine. |
| [LoadSettings](#loadsettings) | Retrieve the current routine configuration. |
| [GetStatus](#getstatus) | Query the routine’s current operational state. |
| [GetTestData](#gettestdata) | Retrieve the most recent measurement data. |

---

## StartMeasurement

**Description**  
Starts a measurement using the currently active routine.

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "StartMeasurement",
  "params": {},
  "request_id": 20
}
````

### Example Response

```json
{
  "status": "OK",
  "data": {
    "routine_status": "Running",
    "started": true,
    "progress": 0
  },
  "request_id": 20
}
```

---

## StopMeasurement

**Description**
Stops the running measurement. If no measurement is active, the command will return without error.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "StopMeasurement",
  "params": {},
  "request_id": 21
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "routine_status": "Ready",
    "stopped": true
  },
  "request_id": 21
}
```

---

## ApplySettings

**Description**
Applies a set of configuration parameters to the active routine.
Parameters are specific to the routine and provided as a JSON object.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "ApplySettings",
  "params": {
    "voltage_range": [0.0, 1.2],
    "integration_time_ms": 500
  },
  "request_id": 22
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "applied": true },
  "request_id": 22
}
```

---

## LoadSettings

**Description**
Retrieves the current configuration of the routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "LoadSettings",
  "params": {},
  "request_id": 23
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "settings": {
      "voltage_range": [0.0, 1.2],
      "integration_time_ms": 500
    }
  },
  "request_id": 23
}
```

---

## GetStatus

**Description**
Retrieves the current operational state of the routine, including progress and error information.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetStatus",
  "params": {},
  "request_id": 24
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "routine_status": "Running",
    "progress": 42,
    "error": null,
    "details": {
      "current_voltage": 0.65,
      "points_acquired": 128
    }
  },
  "request_id": 24
}
```

### Routine Status Values

| Value          | Description                                                        |
| -------------- | ------------------------------------------------------------------ |
| `Initializing` | Routine is loading or configuring resources.                       |
| `Ready`        | Routine is idle and ready to start.                                |
| `Starting`     | Routine has received a start command and is preparing measurement. |
| `Running`      | Measurement is in progress.                                        |
| `Error`        | Routine encountered an error.                                      |

---

## GetTestData

**Description**
Retrieves the most recent test or measurement data from the active routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetTestData",
  "params": {},
  "request_id": 25
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "measurement_id": "batch_20251001_001",
    "columns": ["Voltage (V)", "Current (A)"],
    "data": [
      [0.0, 0.0],
      [0.1, 0.0012],
      [0.2, 0.0025]
    ]
  },
  "request_id": 25
}
```