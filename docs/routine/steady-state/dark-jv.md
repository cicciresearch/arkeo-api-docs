# Dark JV Routine Commands

This section lists the commands specific to the Dark JV routine.  

## {{ headers.settings }}
```json
{
  "scan_settings":{
    "V start (V)":-0.1,
    "V end (V)":0.5,
    "dV (V)":0.01,
    "Scan rate (V/s)":0.1,
    "Scan Order":"FW -> RV",
    "Precondition (s)":1,
    "Turn Hold (s)":0
  },
  "device":{
    "type":"SMU",
    "general":{
      "mode":"Constant Voltage",
      "sample_rate":10,
      "autorange":false
    },
    "specific":{
      "current_compliance":0.02,
      "voltage_compliance":6,
      "sense":"4-wire"
    }
  },
  "photodetector":{
    "type":"Spectrometer",
    "settings":{
      "integration_time_s":0.1,
      "averages":1,
      "smoothing":1
    }
  },
  "sweep_settings":[]
}
```

### Notes

**`scan_settings.Scan Order`** *(enum)*  
Allowed values: `FW -> RV`, `RV -> FW`, `FW Only`, `RV Only`, 

**`device.specifc`**  
--8<-- "embeds/spice-json.md:device-configuration"

**`photodetector.settings`**  
The `photodetector.settings` object changes based on the `photodetector.type` selected:

=== "`"type":"None"`"

    <div class="grid" markdown>
    ```json
    "settings":{ }
    ```
    </div>

=== "`"type":"Spectrometer"`"

    <div class="grid" markdown>
    ```json
    "settings":{
      "integration_time_s":0.01,
      "averages":10,
      "smoothing":1
    }
    ```
    </div>

---

## {{ headers.data }}
```json
{
  "measurement":[
    {
      "sweep_direction":"forward",
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"A"}
      ],
      "data":[
        [0.5,1E-4],
        [0.49,1E-4],
        [0.48,1E-4],
        [0.47,1E-4]
      ],
      "spectral_data":{
        "wavelengths_nm":[336.1982,336.7949,337.3916,337.9883],
        "spectra":[
          {"data_point":{"voltage":{"value":-0.1,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[81.43687,77.80354,79.80354,80.02021],"integrated_irradiance":{"value":0.01333607343767,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":-0.09,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[81.46875,79.97708,81.32708,80.48542],"integrated_irradiance":{"value":0.0134262674463728,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":-0.08,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[84.09125,79.69958,79.58292,80.09125],"integrated_irradiance":{"value":0.0133268793241002,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":-0.07,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[81.59,79.315,80.29,80.14833],"integrated_irradiance":{"value":0.0132556837644618,"unit":"W/cm^2"}}
        ]
      }
    },
    {
      "sweep_direction":"reverse",
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"A"}
      ],
      "data":[
        [-0.1,1E-4],
        [-0.09,1E-4],
        [-0.08,1E-4],
        [-0.07,1E-4]
      ],
      "spectral_data":{
        "wavelengths_nm":[336.1982,336.7949,337.3916,337.9883],
        "spectra":[
          {"data_point":{"voltage":{"value":0.5,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[82.2675,79.2425,79.85083,79.12583],"integrated_irradiance":{"value":0.0134023001641542,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":0.5,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[81.98813,79.03812,80.55479,80.50479],"integrated_irradiance":{"value":0.0133804762362235,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":0.49,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[81.55625,79.18958,80.07291,79.86459],"integrated_irradiance":{"value":0.0133407251182057,"unit":"W/cm^2"}},
          {"data_point":{"voltage":{"value":0.48,"unit":"V"},"current":{"value":1E-4,"unit":"A"}},"spectrum":[80.6525,77.96917,79.26917,80.38583],"integrated_irradiance":{"value":0.0133075743331856,"unit":"W/cm^2"}}
        ]
      }
    }
  ]
}
```

---

## {{ headers.progress}}

```json

```

---

## {{ headers.commands }}

No custom commands are available for the Dark JV routine

---

## {{ headers.example }}

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "Dark JV"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status == "Ready"
{ "target": "ROUTINE", "command": "ApplySettings", "parameter": { ... Settings JSON ... } }
{ "target": "ROUTINE", "command": "StartMeasurement" }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status != "Running"
{ "target": "ROUTINE", "command": "GetTestData" } 
{ "target": "ROUTINE", "command": "CloseRoutine" }
```

---