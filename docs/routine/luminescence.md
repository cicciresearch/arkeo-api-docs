# Luminescence Routine Commands

This section lists the commands specific to the Luminescence routine.  
These commands allow acquisition of luminescence spectra, automatic exposure adjustment, and control of laser excitation.

---

## Command Index

| Command | Description |
|----------|-------------|
| [AcquireDark / AcquireReference](#acquiredark--acquirereference) | Capture a dark or reference spectrum. |
| [AcquireSingle](#acquiresingle) | Acquire a single luminescence spectrum. |
| [AutoExposure](#autoexposure) | Automatically determine optimal integration time. |
| [SetLaser](#setlaser) | Enable or disable the excitation laser. |

---

## AcquireDark / AcquireReference

**Description**  
Captures a dark or reference spectrum and stores it in memory.  
If `reference` is set to `false`, a dark spectrum is acquired.  
If `reference` is set to `true`, a reference spectrum is acquired.

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "AcquireDark",
  "params": { "reference": false },
  "request_id": 201
}
````

### Example Response

```json
{
  "status": "OK",
  "data": { "stored": true },
  "request_id": 201
}
```

---

## AcquireSingle

**Description**
Performs a single luminescence measurement using the current settings.
The resulting spectrum is returned as an array of intensity values.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "AcquireSingle",
  "params": {},
  "request_id": 202
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "spectrum": [0, 123, 456, 789, 655, 421],
    "units": "counts"
  },
  "request_id": 202
}
```

---

## AutoExposure

**Description**
Determines the optimal integration time for luminescence acquisition by iteratively measuring signal intensity.
The result includes the selected exposure time in milliseconds.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "AutoExposure",
  "params": { "target_level": 0.8 },
  "request_id": 203
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "integration_time_ms": 650 },
  "request_id": 203
}
```

---

## SetLaser

**Description**
Controls the excitation laser used during luminescence measurements.
Setting `enabled` to `true` turns the laser on, while `false` turns it off.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "SetLaser",
  "params": { "enabled": true },
  "request_id": 204
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "laser_state": "on" },
  "request_id": 204
}
```
