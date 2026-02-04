# TMPCTL Commands

The temperature controller (TMPCTL) target provides commands to control the temperature of the stage.

---

## Command Index

| Command | Description |
|----------|-------------|
| [GetStatus](#getstatus) | Gets the status of the controller. |
| [SetTemperature](#settemperature) | Set the target temperature. |
| [SetEnable](#setenable) | Enable the temperature controller. |

---

### SetController

**Description**  
Select the specified controller. The following commands then refer to this controller:  
[SetTemperature](#settemperature)  
[SetEnable](#setenable)  

**Example Request**  

```json
{
  "target": "TMPCTL",
  "command": "SetController",
  "parameter": { "address": 1, "channel": 1},
  "request_id": 402
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 402
}
```

---

### GetStatus

**Description**  
Returns the status of all temperature controllers.

**Example Request**  

```json
{
  "target": "TMPCTL",
  "command": "GetStatus",
  "request_id": 401
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": [
    {
    "address":0,
    "channel":0,
    "name":"",
    "DeviceStatus":{
      "State":"Initializing",
      "Error Number":0,
      "Error Instance":0,
      "Error Parameter":0
    },
    "LatestMeasurement":{
      "Time Stamp":"1904-01-01T00:00:00.000Z",
      "Temp. Measurement":{
        "Object Temperature":0,
        "Sink Temperature":0,
        "Stable":"Not Active"
      },
      "Temp. Control":{
        "Target Object Temperature":0,
        "(Ramp) Nominal Object Temperature":0,
        "Thermal Power Model Current":0
      },
      "Output Stage Monitoring":{"Output Current":0,"Output Voltage":0},
      "Sink Temp. General":{
        "Temperature Selection":"External",
        "Fixed Temperature":0
      },
      "Fan Controller":{
        "Relative Cooling Power":0,
        "Nominal FAN Speed":0,
        "Actual FAN Speed":0,
        "FAN PWM Level":0,
        "Enabled":0,
        "Target Temperature":0,
        "0% Speed":0,
        "100% Speed":0
      }
    }
  }
  ],
  "request_id": 401
}
```

---

### SetTemperature

**Description**  
Set the target temperature of the selected controller.

**Example Request**  

```json
{
  "target": "TMPCTL",
  "command": "SetTemperature",
  "parameter": { "temperature": 30.0 },
  "request_id": 402
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 402
}
```

---

### SetEnable

**Description**  
Enable the output status of the selected temperature controller.

**Example Request**  

```json
{
  "target": "TMPCTL",
  "command": "SetEnable",
  "parameter": { "enable": true },
  "request_id": 403
}
```

**Example Response**  

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 403
}
```