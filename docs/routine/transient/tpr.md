# Transient Photo Response Routine Commands

This section lists the commands specific to the Transient Photo Response (TPR) routine.  

## {{ headers.settings }}
```json
{
  "test":"TPV",
  "device_type":"Oscilloscope Real-Time",
  "device_settings":{
    "range":{"value":0.1,"unit":"A"}
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
      "bias":0.7
    },
    "additional":{"step_delay":0.5},
    "transient":{"high":80,"mid":50,"low":20}
  }
}
```

**`test`** *(enum)*  
Allowed values: `TPV`, `TPC`

**`device_type`**  
The `device_settings` object changes based on the `device_type` selected:

=== "`"device_type":"SMU"`"

    <div class="grid" markdown>
    ```json
    "device_settings":{
      "compliance":{"value":0.01,"unit":"A"}
    },
    ```
    </div>

=== "`"type":"Oscilloscope Real-Time"`"

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
  "test":"TPV",
  "scans":[
    {
    "name":"light:0",
    "data_schema":[
      {"value":"Voltage","unit":"V"},
      {"value":"Current","unit":"A"}
    ],
    "data":[
      [2.98263548080926,-5.22751659154892E-5],
      [2.98140850876458,-5.94769650138915E-5],
      [2.98276884749415,-4.90743663161993E-5],
      [2.98240875851712,-4.13391006179154E-5],
      [2.98164856814081,-6.37446978129446E-5],
      ...
    ],
    "dt (s)":1,
    "rise_time (s)":0,
    "fall_time (s)":0
    }
  ],
  "processed_schema":[
    {"value":"Voltage","unit":"V"},
    {"value":"Recombination Time","unit":"s"}
  ],
  "processed_data":[
    [5.98278102733661,0.001],
    [6.87851028592209,0.001],
    [7.77527980193263,0.001],
    [8.67275616167695,0.001],
    [9.56888551881537,0.001],
    ...
  ]
}
```

!!! warning "`processed_schema`" 
    The `#!json "processed_schema"` object changes based on the selected test.  
    
**TPV**  
```json
{
  "processed_schema":[
    {"value":"Voltage","unit":"V"},
    {"value":"Recombination Time","unit":"s"}
  ]
}
```

**TPC**  
```json
{
  "processed_schema":[
    {"value":"Current Density","unit":"A/cm^2"},
    {"value":"Charge","unit":"C"}
  ]
}
```

---

## {{ headers.commands }}

No custom commands are available for the TPR routine

---

