# Luminescence Routine Commands

This section lists the commands specific to the Luminescence routine.  

## {{ icons.settings }} Settings JSON
```json
{"integration_time":100,"averages":1,"pixel_smoothing":1}
```

---

## {{ icons.data }} Data JSON
```json

```
---

## {{ icons.commands }} Custom Commands

| Command | Description |
|----------|-------------|
| AcquireDark / AcquireReference | Capture a reference spectrum. |
| [AcquireSingle](#acquiresingle) | Capture a spectrum. |
| [AutoExposure](#autoexposure) | Automatically determine optimal integration time. |
| [SetLaser](#setlaser) | Enable or disable the excitation laser. |

---

### AcquireDark / AcquireReference

**Description**  
Captures a spectrum and stores it in memory either as Dark / Reference. The current spectrometer settings are used. Returns a 2D array with 2 rows: Wavelength in nm and raw spectrum

!!! warning
    A new dark/reference must be acquired each time the integration time changes

**Example Request**
```json
{
  "target": "ROUTINE",
  "command": "AcquireDark",
  "request_id": 201
}
```

**Example Response**

```json
{
  "status": "OK",
  "data": { 
    "spectrum": [[144.6012,145.207,145.8128, ...],  //wavelength in nm
                 [80.49375,93.57708,102.1604, ...]] //spectrum in a.u.
    },
  "request_id": 201
}
```

---

### AcquireSingle

**Description**  
Captures a spectrum. Returns a 2D array with 3 rows: Wavelength in nm, raw spectrum, irradiance in µW/cm².

!!! info
    The 2nd row is the raw spectrum of the spectrometer and does not include the dark subtraction.

!!! info
    Irradiance is only valid when a dark spectrum is acquired before this function is called.

**Example Request**
```json
{
  "target": "ROUTINE",
  "command": "AcquireSingle",
  "request_id": 201
}
```

**Example Response**

```json
{
  "status": "OK",
  "data": { 
    "spectrum": [[144.6012,145.207,145.8128, ...],  //wavelength in nm
                 [80.49375,93.57708,102.1604, ...], //spectrum in a.u.
                 [0.24535,0.2544,0.34538, ...]]     //irradiance in µW/cm²
    },
  "request_id": 201
}
```

---

### AutoExposure

**Description**  
Determines the optimal integration time for luminescence acquisition by iteratively measuring signal intensity.
The result includes the selected exposure time in milliseconds.

**Example Request**

```json
{
  "target": "ROUTINE",
  "command": "AutoExposure",
  "parameter": { },
  "request_id": 203
}
```

**Example Response**

```json
{
  "status": "OK",
  "data": {"integration_time":50, "averages":5},
  "request_id": 203
}
```

---

### SetLaser

**Description**  
Controls the excitation laser used during luminescence measurements. Set the PWM frequency and duty cycle of the selected laser channel.

**Example Request**

```json
{
  "target": "ROUTINE",
  "command": "SetLaser",
  "parameter": {"channel":0, "frequency":10000, "duty_cycle":50},
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

## {{ icons.example }} Example command sequence

!!! note
    For the following examples, it is assumed that a light source is attached to the spectrometer at channel 0.

### PL measurement

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "Luminescence"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status == "Ready"
{ "target": "ROUTINE", "command": "SetLaser", "parameter": { "channel":0, "duty_cycle":100 } }
{ "target": "ROUTINE", "command": "AutoExposure" }
{ "target": "ROUTINE", "command": "AcquireSingle" }
{ "target": "ROUTINE", "command": "SetLaser", "parameter": { "channel":0, "duty_cycle":0 } }
{ "target": "ROUTINE", "command": "AcquireDark" }
{ "target": "ROUTINE", "command": "GetTestData" } 
{ "target": "ROUTINE", "command": "CloseRoutine" }
```

### Transmittance/Absorbance measurement

```json
{ "target": "MAIN",    "command": "StartRoutine", "parameter": { "routine": "Luminescence"} }
{ "target": "ROUTINE", "command": "GetTestStatus" } // repeat until routine_status == "Ready"

//Place Reference Device

{ "target": "ROUTINE", "command": "SetLaser", "parameter": { "channel":0, "duty_cycle":100 } }
{ "target": "ROUTINE", "command": "AutoExposure" }
{ "target": "ROUTINE", "command": "AcquireReference" }
{ "target": "ROUTINE", "command": "SetLaser", "parameter": { "channel":0, "duty_cycle":0 } }
{ "target": "ROUTINE", "command": "AcquireDark" }

// Place Device

{ "target": "ROUTINE", "command": "SetLaser", "parameter": { "channel":0, "duty_cycle":100 } }
{ "target": "ROUTINE", "command": "AcquireSingle" }
{ "target": "ROUTINE", "command": "GetTestData" } 
{ "target": "ROUTINE", "command": "CloseRoutine" }
```
??? info "Transmittance Calculation"
    Transmittance = Spectrum / Reference

    Absorbance = -log10(Transmittance)


---