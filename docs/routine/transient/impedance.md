# Impedance Routine Commands

This section lists the commands specific to the Impedance routine.  

## {{ headers.settings }}
```json
{
  "instrument":"SMU",
  "config":{
    "frequency":{
      "mode":"Ramp",
      "ramp":{
        "Start (Hz)":200,
        "Stop (Hz)":10000,
        "Steps":10
      },
      "Amplitude (V)":0.1,
      "Offset (V)":0,
      "Periods":10
    },
    "offset":{"mode":"Fixed","Offset (V)":0},
    "light":{"mode":"Off"}
  }
}
```

---

## {{ headers.data }}
```json
{
  "user":"User",
  "device":"Device",
  "temperature":0,
  "test":"Impedance",
  "time":"2026-02-09T16:04:47.538Z",
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
        200,
        308.890420989276,
        477.06646089466,
        736.806299728077,
        1137.96204055278,
        1757.52786888082,
        2714.41761659491,
        4192.28800165354,
        6474.78802869525,
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
        [123.822655,0,0,0,0,-Infinity],
        [200.188982,0,0,0,0,-Infinity],
        [287.12285,0,0,0,0,Infinity],
        [456.387042,0,0,0,0,-Infinity],
        [730.160017,0,0,0,0,Infinity],
        [1227.31876,0,0,0,0,Infinity],
        [1826.76732,0,0,0,0,-Infinity],
        [3334.42597,0,0,0,0,Infinity],
        [5787.06779,0,0,0,0,-Infinity],
        [9550.3184,0,0,0,0,-Infinity]
      ]
    }
  ]
}
```

---

## {{ headers.commands }}
No custom commands are available for the impedance routine