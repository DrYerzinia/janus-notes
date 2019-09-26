# Janus : ESC Repair (9/16/2019)

ESC was discovered to be defective during inital bench testing.  FET visibly smoked.  Due to a lack of a replacment it was used in inital pool testing and failed completly.

New ESCs were ordered and one was modified to replace the broken ESC.

ESC programming was done with a EMAX Femto F3.

![Programming Setup](img/janus/Programming_Setup.jpg)

Settings from old ESC where read using BLHeli Configuration and can be seen below.

![ESC Settings](img/janus/ESC_Settings.png)

It was observed that the damaged ESC pulled 200mA of current with no motor connected with a 7.2V input.  Considerably more than a non-damaged ESC which pulls 4mA.

Below we see the old ESC.

| ![ESC Old Top](img/janus/ESC_Old_Top.jpg) | ![ESC Old Top](img/janus/ESC_Old_Bot.jpg) |
|:---:|:---:|
|Top|Bottom|

Below we see the new ESC as delivered.

| ![ESC Old Top](img/janus/ESC_New_Top.jpg) | ![ESC Old Top](img/janus/ESC_New_Bot.jpg) |
|:---:|:---:|
|Top|Bottom|

The heatshrink sheath and unneeded wires are removed.

| ![ESC Old Top](img/janus/ESC_New_Top_NC.jpg) | ![ESC Old Top](img/janus/ESC_New_Bot_NC.jpg) |
|:---:|:---:|
|Top|Bottom|

The connectors are transfered from the damaged ESC.

| ![ESC Old Top](img/janus/ESC_New_Top_Complete.jpg) | ![ESC Old Top](img/janus/ESC_New_Bot_Complete.jpg) |
|:---:|:---:|
|Top|Bottom|

ESC was installed into Janus.  Medium power was run into system for 1 minute and no escess current or smoke were observed.  ESC drew about 400mA with a PWM input of 1650uS.

![ESC Installed](img/janus/Installed_ESC.jpg)

## TODOs
* Need to linearize inputs to ESCs to remove dead zones and make control effort linearly proportional to thrust.  We can start with just removing the deadzones as I do not have a way to measure motor thrust.