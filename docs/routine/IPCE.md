# IPCE Routine Commands

This section lists the commands specific to the IPCE routine.  

## ⚙️ Settings JSON
```json
{
  "wavelength":{"Start":300,"Step":10,"End":900},
  "acquisition":{
    "Acquisition time (s)":1,
    "Averaging":1,
    "Delay (s)":0,
    "Bias Voltage (V)":0,
    "LED Level":0,
    "Chopper Frequency (Hz)":0
  },
  "device":{
    "type":"Simulate",
    "configuration":{"foo":"bar"}
  }
}
```

---

## 🧾 Data JSON
```json
{
  "user":"Bas de Jong",
  "device":"Sample",
  "temperature":0,
  "test":"IPCE",
  "time":"2025-11-20T16:28:47.462Z",
  "file":"",
  "scan":{
    "name":"IPCE",
    "columns":[
      "Wavelength (nm)",
      "EQE (%)",
      "J_DUT (A/cm2)",
      "J_int (A/cm2)"
    ],
    "data":[
      [300,5.11127313120292,9.99914652862212E-11,NaN],
      [310,4.09082352975042,1.79786580603119E-10,2.66787817748082E-7],
      [320,4.18754042209682,4.80029375632581E-10,1.63639676014496E-6],
      [330,4.9068748237155,1.51960531556791E-9,5.82337871103985E-6],
	  ...
    ]
  }
}
```

---

## Command Index

| Command | Description |
|----------|-------------|
| [SetShutter](#setshutter) | Opens or closes the shutter. |
| [SetWavelength](#setwavelength) | Move the monochromator to the specified wavelength. |
| [StartCalibration](#startcalibration) | Start the lamp calibration with a photodiode. |
| [GetChopperFrequency](#getchopperfrequency) | Retreive the live chopper frequency. |
| [GetMonochromatorStatus](#getmonochromatorstatus) | Get the monochromator status. |

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
