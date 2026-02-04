# Impedance Routine Commands

This section lists the commands specific to the Impedance routine.  

## {{ headers.settings }}
```json
{
  "Freq":{
    "FreqType":"Ramp",
    "Frequency":{
      "Start (Hz)":100,
      "Stop (Hz)":10000,
      "Steps":10
    },
    "Amplitude (V)":0.1,
    "Offset (V)":0,
    "Periods":10
  },
  "Offset":{
    "Type":"Fixed",
    "Start (V)":0,
    "Stop (V)":1,
    "Steps":10
  },
  "Light":{
    "LightType":"Off",
    "LED Type":"Fast LED",
    "Start":0,
    "Stop":1,
    "Steps":10
  },
  "LED":{"LED Level":0}
}
```

---

## {{ headers.data }}
```json
{
  "user":"Cicci Research",
  "device":"Sample",
  "temperature":0,
  "test":"Impedance",
  "time":"2025-11-12T13:21:36.021Z",
  "output_values":{
    "light":{
      "unit":"a.u.",
      "values":[0]
    },
    "offset":{
      "unit":"V",
      "values":[0]
    },
    "frequency":{
      "unit":"Hz",
      "values":[
        100,
        166.810053720006,
        278.255940220713,
        464.158883361278,
        774.263682681127,
        1291.54966501488,
        2154.43469003188,
        3593.81366380463,
        5994.84250318941,
        10000
      ]
    }
  },
  "data_columns":[
    {"name":"Frequency","unit":"Hz"},
    {"name":"Impedance_Re","unit":"Ohm"},
    {"name":"Impedance_Im","unit":"Ohm"},
    {"name":"Magnitude","unit":"Ohm"},
    {"name":"Phase","unit":"deg"},
    {"name":"Capacitance","unit":"C"}
  ],
  "scans":[
    {
      "iteration":{"light":0,"offset":0,"frequency":0},
      "data":[
        ["72.80","0.00","-0.00","-0.00","-0.00","Inf"],
        ["91.20","-0.00","-0.00","-0.00","-0.00","Inf"],
        ["163.01","-0.00","-0.00","-0.00","-0.00","Inf"],
        ["280.12","-0.00","-0.00","-0.00","-0.00","Inf"],
        ["475.39","0.00","0.00","0.00","0.00","-Inf"],
        ["723.83","-0.00","0.00","0.00","0.00","-Inf"],
        ["1265.24","-0.00","-0.00","-0.00","-0.00","Inf"],
        ["3035.43","-0.00","-0.00","-0.00","-0.00","Inf"],
        ["5547.07","0.00","0.00","0.00","0.00","-Inf"],
        ["9550.32","0.00","0.00","0.00","0.00","-Inf"]
      ]
    }
  ]
}
```

---

## {{ headers.commands }}
No custom commands are available for the JV routine