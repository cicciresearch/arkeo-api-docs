# Transient Photo Response Routine Commands

This section lists the commands specific to the Transient Photo Response routine.  

## ⚙️ Settings JSON
```json
{
  "test":"TPC",
  "device_type":0,
  "device_settings":{
    "Voltage Compliance":2,
    "Current Compliance":0.01
  },
  "output_settings":{
    "pulse":{
      "duration":0.002,
      "duty_cycle":30,
      "delay":1E-4,
      "averaging":100,
      "points":1000
    },
    "level":{
      "start":0.25,
      "start_unit":"a.u.",
      "end":1,
      "end_unit":"a.u.",
      "steps":30,
      "ramp":true,
      "dark":false,
      "offset":0.5,
      "bias":0.5
    },
    "additional":{"step_delay":0.5},
    "transient":{"high":80,"mid":50,"low":20}
  }
}
```

---

## 🧾 Data JSON
```json
{
  "test":"TPV",
  "scans":[
    {
    "name":"light:0",
    "data_scheme":[
      {"value":"Voltage","unit":"V"},
      {"value":"Current","unit":"A"}
    ],
    "data":[[],[]],
    "dt (s)":1,
    "rise_time (s)":0,
    "fall_time (s)":0
    }
  ],
  "processed_scheme":[
    {"value":"Voltage","unit":"V"},
    {"value":"Recombination Time","unit":"s"}
  ],
  "processed_data":[[],[]]
}

```

---

## Command Index

| Command | Description |
|----------|-------------|
| [SetMode](#setmode) | Set the mode to TPV or TPC. |

---

### SetMode

**Description**  
Set the mode to TPV or TPC.

**Example Request**
```json
{
  "target": "ROUTINE",
  "command": "SetMode",
  "data": {"test":"TPV"},
}
```

**Example Response**

```json
{ "status": "OK" }
```

---

