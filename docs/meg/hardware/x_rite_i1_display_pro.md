# VPixx X-Rite i1Display Pro Colorimeter

**[Specifications](../../meg/pdfs/i1Display_Pro_Specifications.pdf)**<br />
**[Data Sheet](../../meg/pdfs/X-Rite_i1Display_Pro_Data_Sheet.pdf)**<br />
**[User Manual](../../meg/pdfs/X-Rite_i1Display_Pro_User_Manual.pdf)**

!!! Note
	The **calibration information is now included as part of** the ...<br />
	**[Application Guide for VPixx Products](../../meg/pdfs/ApplicationGuide_for_VPixx_Products.pdf)**<br />
	... and the **relevant section has been printed and is kept** with the **i1Display Pro device** in its **storage box in the MEG Side Room**.

!!! Info
	***<span style="color:maroon">"The i1Display Pro colorimeter features an advanced, high-end optical system with custom-designed filters. It provides a near-perfect match to the color perception of the human visual system, delivering superior color measurement results. <br />
	i1Display Pro supports all modern display technologies, including LED backlight and wide gamut displays. It is spectrally calibrated, making it fully field upgradeable to support future display technologies.</span>*** **- VPixx Technologies**

The Colorimeter can be used as a **Standalone** device or **through MATLAB**.

## **Standalone**
(e.g. usage on own laptop to investigate stimuli generated via Stim PC).

- Install **VPixx** ***Software Tools*** from the provided USB stick **(<span style="color:red">already done for CHBH-ST-MEG-W02</span>**).
- **Plug in the Colorimeter** to an availabe USB port, **attach it to the back projection screen** where required (wider **Micropore** tape is available).
- **Start the VPutil application** by clicking on its Desktop shortcut. The VPutil menu will appear.
- Type “**3**” to **initiate the Calibration commands**.
- Type "**i1d**", and **follow the instructions to take a measurement**.
- Type "**q**" to quit.


## **Through MATLAB** 
(**<span style="color:red">below instructions already done for CHBH-ST-MEG-W02</span>**).

- Copy **I1.mexw64** (**<span style="color:blue">15/06/2021 94KB, from the USB memory stick</span>**) to **C:\toolbox\Psychtoolbox\PsychBasic\MatlabWindowsFilesR2007a**.
- Copy the **new Datapixx.mexw64** (from **<span style="color:blue">C:\Program Files\VPixx Technologies\Software Tools\DatapixxToolbox_trunk\mexdev\build\matlab\win64</span>**) to the following usage locations depending on which version of MATLAB used ...
	- **C:\toolbox\DataPixx** - for **<span style="color:maroon">MATLAB R2017A</span>.**
	- **C:\toolbox\Psychtoolbox\PsychBasic\MatlabWindowsFilesR2007a** - for **<span style="color:maroon">MATLAB R2019B</span>.**

!!! Note "**<span style="color:red">Previous versions of Datapixx MEX files have been renamed to "Old_Datapixx..." etc</span>**"


Starting MATLAB and **typing "I1", ```Enter```, lists the I1's functions...** **not all are usable as we have the i1Display Pro, *not* the i1Pro.**

**>> I1**

```matlab
Usage:

% All I1 (Pro, Pro3, Display) functions:
isConnected = I1('IsConnected');
I1('Calibrate');
Lxy = I1('GetTriStimulus');

% I1Pro / I1Pro3 functions:
I1('TriggerMeasurement');
keyPressed = I1('KeyPressed');
spectrum = I1('GetSpectrum');

% I1 Display ONLY functions:
I1('SetIntegrationTime', time);
time = I1('GetIntegrationTime');
I1('SetMeasurementMode', 'mode');
mode = I1('GetMeasurementMode');
SERVER MODE VERSION: 3.9 [05/APR/2021]
```
<br />

**>> I1('IsConnected?');**

```matlab
Usage:

isConnected = I1('IsConnected', [device]);

Returns non-0 if an X-Rite I1 has been detected.
The argument 'device' can be used to choose a device should 2 different i1ProDev
be connected to the computer.
It should be noted that only 1 device can be used at the same time.
Device is one of the following value:
    - i1Pro
    - i1Pro3
    - i1Display
```

!!! Note 
	**>> isConnected = I1('IsConnected');** produces the result for **‘isConnected’** as "**1**" if the "**I1**" is connected, "**0**" otherwise.
<br />

**>> I1('SetMeasurementMode?');**

```matlab
Usage:

I1('SetMeasurementMode', ‘mode’);

Sets the calibration file and the measurement mode for the i1Display.
The measurement mode is one of the following value:
    - CCFL: Used for LCD monitors with CCFL backlight.
    - WLED : Used for LCD monitors with White LED backlight monitors.
    - RGBLED : Used for LCD monitors with RGB LED backlight monitors.
    - Phosphor : Used for CRT monitors.
    - Projector : Used for Projectors.
    - VPixx : Used for VIEWPixx, VIEWPixx /3D and PROPixx.
    - EEG : Used for VIEWPixx /EEG monitors.
```
<br />

**>> I1('GetMeasurementMode?');**

```matlab
Usage:

mode = I1('GetMeasurementMode');

Gets the measurement mode currently used by the i1Display.
The calibration mode is one of the following value:
    - CCFL: Used for LCD monitors with CCFL backlight.
    - WLED : Used for LCD monitors with White LED backlight monitors.
    - RGBLED : Used for LCD monitors with RGB LED backlight monitors.
    - Phosphor : Used for CRT monitors.
    - Projector : Used for Projectors.
    - VPixx : Used for VIEWPixx, VIEWPixx /3D and PROPixx.
    - EEG : Used for VIEWPixx /EEG monitors.
```

So to change ...(*default* vaule is '**VPixx**' as a PROPixx is used in the CHBH MEG Lab)

```matlab
mode = I1('GetMeasurementMode');
mode
mode = 

	'VPixx'
I1('SetMeasurementMode', 'RGBLED');
mode = I1('GetMeasurementMode');
mode
mode =

	'RGBLED'
```
<br />

**>> I1('GetTriStimulus?');**

```matlab
Usage:

Lxy = I1('GetTriStimulus'); 

Returns CIE Lxy coordinates of last i1 measurement.
```

Taking a sample measurement with **‘RGBLED'** as the **'mode'** ...

```matlab
Lxy = I1('GetTriStimulus');
Lxy
Lxy =

     94.3362, 0.3781, 0.3791
```

!!! Note "VPIxx say a second or so exposure is needed to collect a sample, so allow for this time in the code."
<br />

**>>  I1('SetIntegrationTime?');**

```matlab
Usage:

I1('SetIntegrationTime', time);

Sets the integration time used to take a measurement by the i1Display.
It represents the maximum time which could be taken by the i1Display to get a measurement.
The value must be > 0.2 seconds. Default is 0.2 seconds.
```
<br />

**>> I1('GetIntegrationTime?');**

```matlab
Usage:

time = I1('GetIntegrationTime');

Gets the integration time used for measurements by the i1Display.
It represents the maximum time which could be taken by the i1Display to get a measurement.
```

So

```matlab
time = I1('GetIntegrationTime');
time
time =

    0.2000
```

So to set the **integration time** to **1 second** ...

```matlab
I1('SetIntegrationTime', 1);
```

And to check it’s changed …

```matlab
time = I1('GetIntegrationTime');
time
time =

    1
```

