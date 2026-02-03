# Transient Photo Response Routine Commands

This section lists the commands specific to the Time-Correlated Single Photon Counting (TCSPC) routine.  

## {{ icons.settings }} Settings JSON
```json
{}
```

---

## {{ icons.data }} Data JSON

**Note** `Offset` and `Resolution` are expressed in ns. Histogram is the counts per bin.

```json
{"Offset":0,"Resolution":0.025,"Histogram":[6,7,11,8,3,6,9, ... ]}
```

---

## {{ icons.commands }} Custom Commands

| Command | Description |
|----------|-------------|
| [GetRates](#getrates) | Get the actual sync and input rates. |
| [SetLaser](#setlaser) | Enable or disable the excitation laser. |

---

### GetRates

**Description**  
Get the actual sync and input rates.

**Example Request**
```json
{
  "target": "ROUTINE",
  "command": "GetRates",
  "request_id": 201
}
```

**Example Response**  
Rates are expressed in counts per second

```json
{
  "status": "OK",
  "data": {"sync_rate":10000370,"input_rate":193650,"ratio":0.0193642835215097},
  "request_id": 204
}
```

---

### SetLaser

**Description**  
Control the excitation laser

**Example Request**

```json
{
  "target": "ROUTINE",
  "command": "SetLaser",
  "parameter": {"laser":true},
  "request_id": 204
}
```

**Example Response**

```json
{
  "status": "OK",
  "data": { "state":"OK" },
  "request_id": 204
}
```

---

## Example command sequence

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "TCSPC"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until state == "Ready"
{ "target": "ROUTINE", "command": "SetLaser", "parameter": {"laser":true},}
{ "target": "ROUTINE", "command": "GetRates" } //Check that sync rate != 0 and Ratio is 1-5%
{ "target": "ROUTINE", "command": "StartMeasurement" }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until state == "Ready"
{ "target": "ROUTINE", "command": "GetTestData" }
{ "target": "ROUTINE", "command": "CloseRoutine" }
```

---