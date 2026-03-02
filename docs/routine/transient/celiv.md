# CELIV Routine Commands

This section lists the commands specific to the CELIV routine.  

## {{ headers.settings }}
```json
{
  "output":{
    "Pulse Delay":{
      "Start (s)":0,
      "Step (s)":1E-5,
      "End (s)":1E-4
    },
    "Pulse Width (s)":1E-6,
    "V Ramp":{
      "Duration (s)":2E-4,
      "Start (V)":0,
      "End (V)":-1
    },
    "Delay (s)":0.001,
    "Averages":100,
  },
  "device_thickness_m":2E-5,
  "instrument":{
    "type":"Fast",
    "config":{
      "range":{"value":0.05,"unit":"A"}
    }
  }
}
```

**`device_type`**  
The `instrument.config` object changes based on the `instrument.type` selected:

=== "`"instrument.type":"Slow"`"

    <div class="grid" markdown>
    ```json
    "device_settings":{
      "compliance":{"value":0.01,"unit":"A"}
    },
    ```
    </div>

=== "`"instrument.type":"Fast"`"

    <div class="grid" markdown>
    ```json
    "device_settings":{
      "range":{"value":0.1,"unit":"A"}
    },
    ```
    </div>
---

## {{ headers.data }}
```json
{
  "delay":{"value":1E-4,"unit":"s"},
  "data_scheme":[
    {"name":"Voltage","unit":"V"},
    {"name":"Current","unit":"A"}
  ],
  "data":[
    [2.19706854771811,-2.22762695659185E-5],
    [2.19749007802445,-1.38456634391332E-5],
    [2.19741104109201,-1.54264020879054E-5],
    [2.19712782541744,-2.10907155793393E-5],
    ...
  ],
  "parameters":{
    "delay":{"value":1E-4,"unit":"s"},
    "t_max":{"value":7.53E-5,"unit":"s"},
    "deltaJ":{"value":1.92323202267289E-5,"unit":"A"},
    "J0":{"value":-2.72819419536972E-5,"unit":"A"},
    "A":{"value":5000,"unit":"V/s"},
    "mobility":{"value":3.15124676318999E-18,"unit":"m^2/Vs"}
  }
}
```

---

## {{ headers.progress }}

```json
{
  "routine_status":"Running",
  "routine_name":"CELIV",
  "progress":{
    "total_delays":11,
    "delays_done":4,
    "averaging_pct":40.98
  },
  "error":null
}
```

---

## {{ headers.commands }}

No custom commands are available for the Photo-CELIV routine

---

## {{ headers.example }}

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "Photo-CELIV"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status == "Ready"
{ "target": "ROUTINE", "command": "ApplySettings", "parameter": { ... Settings JSON ... } }
{ "target": "ROUTINE", "command": "StartMeasurement" }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status != "Running"
{ "target": "ROUTINE", "command": "GetTestData" } 
{ "target": "ROUTINE", "command": "CloseRoutine" }
```

---