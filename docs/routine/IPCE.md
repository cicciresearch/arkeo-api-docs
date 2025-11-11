# IPCE Routine Commands

This section lists the commands specific to the IPCE routine.  

## ⚙ Settings JSON
```json

```

---

## 🔢 Data JSON
```json

```
---

## Command Index

| Command | Description |
|----------|-------------|
| [SetShutter](#acquire) | Opens or closes the shutter. |
| [SetWavelength](#setwavelength) | Move the monochromator to the specified wavelength. |
| [StartCalibration](#startcalibration) | Start the lamp calibration with a photodiode. |
| [GetChopperFrequency](#getchopperfrequency) | Retreive the live chopper frequency. |
| [GetMonochromatorStatus](#getmonostatus) | Get the monochromator status. |

---

## SetShutter

**Description**  
Open or close the shutter 

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "SetShutter",
  "parameter": { "shutter_status": true},
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 201
}
```

---

## SetWavelength

**Description**  
Move the monochromator to the specified wavelength in nm

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "SetWavelength",
  "parameter": { "wavelength": 550.0},
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 201
}
```

---

## StartCalibration

**Description**  
Start the lamp calibration with a photodiode

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "StartCalibration",
  "parameter": { "path": "C:\\Arkeo\\calibration\\photodiode.txt"},
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 201
}
```

---

## GetChopperFrequency

**Description**  
Retreive the live chopper frequency in Hz.

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "GetChopperFrequency",
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": { "frequency":13.35 },
  "request_id": 201
}
```

---

## GetMonochromatorStatus

**Description**  
Returns the status and configuration of the monochromator.

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "SetShutter",
  "parameter": { "shutter_status": true},
  "request_id": 201
}
```

### Example Response

```json
{
  "status": "OK",
  "data": {
    "type":"Serial Monochromator",
    "connected":true,
    "wavelength":550.1,
    "shutter":"Open",
    "filter":2,
    "grating":1,
    "config":{
      "gratwave":[0,1000],
      "gratpos":[1,2],
      "fltrwave":[100,355,625,1115,1580,Infinity],
      "fltrpos":[1,2,3,4,5,6],
      "autofilter":true,
      "autograting":true
    }
  },
  "request_id": 201
}
```

---
