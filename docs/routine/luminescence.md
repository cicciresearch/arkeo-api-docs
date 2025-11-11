# Luminescence Routine Commands

This section lists the commands specific to the Luminescence routine.  
These commands allow acquisition of luminescence spectra, automatic exposure adjustment, and control of laser excitation.

## ⚙ Settings JSON
```json
{"integration_time":100,"averages":1,"pixel_smoothing":1}
```

---

## 🔢 Data JSON

---

## Command Index

| Command | Description |
|----------|-------------|
| [AcquireDark / AcquireReference / AcquireSingle](#acquire) | Capture a spectrum. |
| [AutoExposure](#autoexposure) | Automatically determine optimal integration time. |
| [SetLaser](#setlaser) | Enable or disable the excitation laser. |

---

## AcquireDark / AcquireReference / AcquireSingle

**Description**  
Captures a spectrum and stores it in memory either as Dark / Reference / Spectrum based on the command type. The current spectrumeter settings are used.

**Note**: a new dark/reference must be acquired each time the integration time changes

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "AcquireDark",
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "stored": true },
  "request_id": 201
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
  "parameter": { },
  "request_id": 203
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {"integration_time":50, "averages":5},
  "request_id": 203
}
```

---

## SetLaser

**Description**
Controls the excitation laser used during luminescence measurements. Set the PWM frequency and duty cycle of the selected laser channel.

### Example Request

```json
{
  "target": "ROUTINE",
  "command": "SetLaser",
  "parameter": {"channel":0, "frequency":10000, "duty_cycle":50},
  "request_id": 204
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 204
}
```
