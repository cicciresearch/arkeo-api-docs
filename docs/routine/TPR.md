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
{"Voltage (V)":0,"Current (A)":0}
```

---