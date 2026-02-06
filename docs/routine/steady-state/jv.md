# JV Routine Commands

This section lists the commands specific to the JV routine.  

## {{ headers.settings }}
```json
{
  "device_type":"NI-SMU",
  "device_settings":{"Compliance (A)":0.1},
  "scan_settings":{
    "scan":{
      "Start (V)":-0.2,
      "End (V)":1.2,
      "Step (V)":0.02,
      "Rate (V/s)":0.2,
      "Order":"Forward then Reverse",
      "Auto Voc":true,
      "Exceed Voc (%)":0
    },
    "precondition":{
      "Condition":"None",
      "Value":1,
      "Hold Time (s)":1,
      "Hold Voltage (V)":-0.2
    },
    "device":{"Area (cm2)":1,"Inverted":false},
    "light":{
      "Source":"None",
      "Irradiance (mW/cm2)":100,
      "Level (%)":100
    },
    "light_config":{"LED Level":1}
  },
  "sweep_settings":[]
}

```

---

## {{ headers.data }}
```json
{
  "user":"Cicci Research",
  "device":"Sample",
  "area_cm2":1,
  "temperature":23.8,
  "acquisition_time":"2026-01-26T12:22:07.461Z",
  "scans":[
    {
      "name":"forward",
      "sweep_indices":[-1],
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"mA/cm^2"}
      ],
      "data":[
        [-0.10164886713028,1.17926585553872E-4],
        [-0.0819301605224609,1.18105399488199E-4],
        [-0.0628146529197693,1.16118577995686E-4],
        [-0.0403454899787903,1.15959632276285E-4],
        ...
      ],
      "parameters":{
        "voc":{"value":0.326015792543873,"unit":"V"},
        "jsc":{"value":0.115310649809229,"unit":"mA/cm^2"},
        "v_mpp":{"value":0.217405427060398,"unit":"V"},
        "j_mpp":{"value":0.0843552348199183,"unit":"mA/cm^2"},
        "p_mpp":{"value":0.0183392858508045,"unit":"mW/cm^2"},
        "r_series":{"value":764.409924295598,"unit":"Ohm"},
        "r_shunt":{"value":107060.329453377,"unit":"Ohm"},
        "fill factor":{"value":48.7836579615014,"unit":"%"},
        "efficiency":{"value":0.0183392858508045,"unit":"%"}
      }
    },
    {
      "name":"reverse",
      "sweep_indices":[-1],
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"mA/cm^2"}
      ],
      "data":[
        [0.375275015830994,-1.03358969543919E-4],
        [0.356238186359406,-5.41851376042222E-5],
        [0.336988270282745,-1.99588260265312E-5],
        [0.31677782535553,9.65143695022121E-6],
        ...
      ],
      "parameters":{
        "voc":{"value":0.323545980753277,"unit":"V"},
        "jsc":{"value":0.115167594537622,"unit":"mA/cm^2"},
        "v_mpp":{"value":0.222084747509015,"unit":"V"},
        "j_mpp":{"value":0.0836156568083621,"unit":"mA/cm^2"},
        "p_mpp":{"value":0.0185697620300856,"unit":"mW/cm^2"},
        "r_series":{"value":705.15973836992,"unit":"Ohm"},
        "r_shunt":{"value":87558.7731630702,"unit":"Ohm"},
        "fill factor":{"value":49.8356392236295,"unit":"%"},
        "efficiency":{"value":0.0185697620300856,"unit":"%"}
      }
    }
  ]
}
```

---

## {{ headers.progress}}

```json
{
  "routine_status":"Running",
  "routine_name":"JV",
  "progress":{
    "voltage":{"value":-0.16,"unit":"V"},
    "current":{"value":-1E-4,"unit":"A/cmÂ²"},
    "direction":"Forward",
    "points done":3,
    "total points":142,
    "progres_pct":2.12,
    "sweep_index":0,
    "total_scans":5
  },
  "error":null
}
```

---

## {{ headers.commands}}

No custom commands are available for the JV routine

---

## {{ headers.example }}

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "JV"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status == "Ready"
{ "target": "ROUTINE", "command": "ApplySettings", "parameter": { ... Settings JSON ... } }
{ "target": "ROUTINE", "command": "StartMeasurement" }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status != "Running"
{ "target": "ROUTINE", "command": "GetTestData" } 
{ "target": "ROUTINE", "command": "CloseRoutine" }
```

---