<!-- --8<-- [start:device-configuration] -->
The `device.specific` object changes based on the `device.type` selected:

=== "`"type":"SMU"`"

    <div class="grid" markdown>
    ```json
    "specific":{
      "current_compliance":0.02,  //in A
      "voltage_compliance":6,     //in V
      "sense":"4-wire"
    }
    ```
    </div>

=== "`"type":"Keithley24xx"`"

    <div class="grid" markdown>
    ```json
    "specific":{
      "port":"GPIB0::24::INSTR",
      "shutter":true,
      "remote_sense":true
    }
    ```
    </div>

=== "`"type":"Keithley26xx"`"

    <div class="grid" markdown>
    ```json
    "specific":{
      "port":"KE2600",
      "Hi-C Mode":0,
      "Sense":"4 Wire"
    }
    ```
    </div>
<!-- --8<-- [end:device-configuration] -->