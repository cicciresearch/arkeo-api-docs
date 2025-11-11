# JV Routine Commands

This section lists the commands specific to the JV routine.  

## ⚙ Settings JSON
```json
{
  "device_type":"NI-SMU",
  "device_settings":{"Compliance (A)":0.01},
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

## 🔢 Data JSON
```json
{
  "user":"User",
  "device":"Sample",
  "temperature":0,
  "test":"",
  "time":"1904-01-01T00:00:00.000Z",
  "sweep":[],
  "data_schema":[
    {"name":"Voltage","unit":"V"},
    {"name":"Current","unit":"mA/cm2"}
  ],
  "parameter_schema":[
    {"name":"Voc","unit":"V"},
    {"name":"Jsc","unit":"mA/cm2"},
    {"name":"V_MPP","unit":"V"},
    {"name":"J_MPP","unit":"mA/cm2"},
    {"name":"P_MPP","unit":"mW/cm2"},
    {"name":"Rseries","unit":"Ohm"},
    {"name":"Rshunt","unit":"Ohm"},
    {"name":"Fill Factor","unit":"%"},
    {"name":"Efficiency","unit":"%"}
  ],
  "scans":[
    {
      "name":"forward",
      "file":"D:\\Arkeo\\Results\\Cicci Research\\2025_10_30\\Sample\\JV\\2025-10-30_14.51.57_JV_Sample.txt",
      "data":[
        [-0.100211457860631,1.14872582495027E-5],
        [-0.0800413256365645,1.19740465092449E-5],
        [-0.0600455286506167,1.18040040349514E-5],...
      ],
      "parameters":[
        0.199957825294649,
        0.0112409373200826,
        0.128680169428345,
        0.00767840281811049,
        9.88058175573541E-4,
        7141.88672920349,
        89045.9727026382,
        43.9583704939779,
        9.88058175573541E-4
      ],
      "sweep_indices":[-1]
    },
    {
      "name":"reverse",
      "file":"D:\\Arkeo\\Results\\Cicci Research\\2025_10_30\\Sample\\JV\\2025-10-30_14.51.57_JV_Sample.txt",
      "data":[
        [0.199999938425143,7.00119324713674E-7],
        [0.18004202880006,3.61618105053908E-6],
        [0.160041917080911,5.6967007360125E-6],...
      ],
      "parameters":[
        0.199999938425143,
        0.0115814924533883,
        0.129775601459748,
        0.00794798653972136,
        0.00103145473358632,
        6632.67377340069,
        94258.7456476277,
        44.5303165933094,
        0.00103145473358632
      ],
      "sweep_indices":[-1]
    }
  ]
}
```

---

## Command Index
No custom commands are available for the JV routine