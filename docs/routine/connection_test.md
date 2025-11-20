# Connection Test Routine Commands

This section lists the commands specific to the Connection Test routine.  

## ⚙️ Settings JSON
```json
{
  "Device Name":"SMU",
  "Device_General":{
    "Mode":"Constant Voltage",
    "Sample Rate (S/s)":10,
    "Autorange":true
  },
  "Device_Specific":{
    "Current limit (A)":0.01,
    "Voltage Limit (V)":6
  }
}
```

---

## 🧾 Data JSON
```json
{"Voltage (V)":0,"Current (A)":0}
```

---

## Command Index

| Command | Description |
|----------|-------------|
| [SetOutput](#setoutput) | Sets the voltage/current in their respective modes. |

---

## SetOutput

**Description**  
Sets the voltage/current in their respective modes. This function only has an effect when the measurement is running

### Example Request
```json
{
  "target": "ROUTINE",
  "command": "SetOutput",
  "parameter": { "output": 0.123},
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