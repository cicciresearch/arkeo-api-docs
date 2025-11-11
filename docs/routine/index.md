# ROUTINE Commands

Commands in this section are shared across all measurement routines.
Each routine can be started from the MAIN target, after which the commands below control the measurement process, retrieve results, and manage settings. They can only be called if a routine is active. If no routine is active, any of these commands return `error 4006: no active routine` as an error object.
---

## Command Index

| Command | Description |
|----------|-------------|
| [StartMeasurement](#startmeasurement) | Start a measurement within the active routine. |
| [StopMeasurement](#stopmeasurement) | Stop the current measurement. |
| [CloseRoutine](#closeroutine) | Stops any ongoing measurement and close the routine. |
| [ApplySettings](#applysettings) | Apply configuration parameters to the routine. |
| [GetSettings](#getsettings) | Retrieve the current routine configuration. |
| [GetStatus](#getstatus) | Query the routine’s current operational state. |
| [GetTestData](#gettestdata) | Retrieve the most recent measurement data. |
| [SetInfo](#setinfo) | Applies user and device name. |
| [ClearErrors](#clearerrors) | Clears any errors when the routine is in the error state. |
| [GetCustomCommands](#getcustomcommands) | Returns a list of custom commands available for the active routine. |

---

## StartMeasurement

**Description**  
Starts a measurement. This command returns an error when the routine is not in the Ready state.

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "StartMeasurement",
  "request_id": 20
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state":"OK"
  },
  "request_id": 20
}
```

---

## StopMeasurement

**Description**
Stops the measurements. This command returns an error when the routine is not in the Starting or Running state.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "StopMeasurement",
  "request_id": 21
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state":"OK"
  },
  "request_id": 21
}
```

---

## CloseRoutine

**Description**
Stops any ongoing measurement, clears all errors and close the routine. 

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "CloseRoutine",
  "request_id": 21
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state":"OK"
  },
  "request_id": 21
}
```

---

## GetSettings

**Description**
Returns the routine configuration. The format depends on the active routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetSettings",
  "request_id": 23
}
```

---

## ApplySettings

**Description**
Applies a configuration. The configuration JSON must match the active routine. It is recommended to use GetSettings to obtain the correct JSON.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "ApplySettings",
  "parameter": {
    "device_type":"NI-SMU",
    "device_settings":{"Compliance (A)":0.01},
    "scan_settings":{
      "scan":{
        "Start (V)":-0.2,
        "End (V)":1,
        "Step (V)":0.02,
        ...
      }
    }
  },
  "request_id": 22
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 22
}
```

---

## GetTestStatus

**Description**
Returns the current status of the routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetTestStatus",
  "request_id": 24
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "routine_status":"Running" },
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
Retrieves the most recent test or measurement data from the active routine. The response depends on the active routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetTestData",
  "request_id": 25
}
```

---

## SetInfo

**Description**
Set the user name, device name and device area. 

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "SetInfo",
  "parameter": {"user_name": "User",
                "device_name": "Sample",
                "device_area": 1.23 },
  "request_id": 26
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state":"OK"
  },
  "request_id": 26
}
```

---

## ClearErrors

**Description**
Clears any errors when the routine is in error. After this command, the routine returns to the Ready state.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "ClearErrors",
  "request_id": 27
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "state":"OK"
  },
  "request_id": 27
}
```

---

## GetCustomCommands

**Description**
Returns a list of custom commands available for the active routine.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "GetCustomCommands",
  "request_id": 28
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {"CustomCommands":["AcquireDark","AcquireReference","AcquireSingle","SetLaser","AutoExposure"]},
  "request_id": 28
}
```