# VPixx X-Rite i1Display Pro Colourimeter


'''<span style="color:blue;font-size:medium">VPixx X-Rite i1Display Pro Colourimeter.</span>''' <span style="font-size:medium">The specifications can be found '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/i1Display_Pro_Specification.pdf HERE]'''</span>

* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/X-Rite_i1Display_Pro_Data_Sheet.pdf Data Sheet]'''
* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/X-Rite_i1Display_Pro_User_Manual.pdf User Manual]'''

The calibration information is now included as part of the ...
* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/ApplicationGuide_for_VPixx_Products.pdf Application Guide for VPixx Products]'''
... the relevant section has been printed and is kept with the i1Display Pro device.


''"<span style="color:maroon;font-size:medium">The i1Display Pro colorimeter features an advanced, high-end optical system with custom-designed filters. It provides a near-perfect match to the color perception of the human visual system, delivering superior color measurement results. <br />i1Display Pro supports all modern display technologies, including LED backlight and wide gamut displays. It is spectrally calibrated, making it fully field upgradeable to support future display technologies.</span>"''


'''<span style="color:green;font-size:medium">Borrowed: </span><span style="font-size:medium">26/01/2023: Dr. Dietmar Heinke, Hills, Room 235</span>''' 
* '''<span style="color:green;font-size:medium">Returned: </span><span style="font-size:medium">02/03/2023</span>'''
'''<span style="color:green;font-size:medium">Borrowed: </span><span style="font-size:medium">19/04/2024: Dr. Qiaoyu "Chloe" Chen, Dr. Dietmar Heinke, CHBH, Room 217</span>''' 
* '''<span style="color:green;font-size:medium">Returned: </span><span style="font-size:medium">June 2024</span>'''


The Colorimeter can be used as a '''standalone''' device or through '''MATLAB'''.


'''<span style="font-size:medium">1) Standalone.</span>''' (e.g. usage on own laptop to investigate stimuli generated via MEG-STIM1).

* Install '''VPixx ''Software Tools''''' from the provided USB stick (<span style="color:red">already done for MEG-STIM1 and CHBH-ST-MEG-W02</span>).
* '''Plug in''' the Colorimeter, attach to the back projection screen where required (wider ''Micropore'' tape is available).
* '''Start''' the ''VPutil'' application by clicking on its desktop shortcut. The ''VPutil'' menu will appear.
* Type “'''3'''” to initiate the Calibration commands.
* Type "'''i1d'''", and follow the instructions to take a measurement.
* Type "'''q'''" to quit.


'''<span style="font-size:medium">2) MATLAB.</span>''' (<span style="color:red">below instructions already done for MEG-STIM1 and CHBH-ST-MEG-W02</span>).

* Copy '''I1.mexw64''' ('''<span style="color:blue">15/06/2021 94KB, from the USB memory stick</span>''') to '''C:\toolbox\Psychtoolbox\PsychBasic\MatlabWindowsFilesR2007a'''.
* Copy the new '''Datapixx.mexw64''' (from '''<span style="color:blue">C:\Program Files\VPixx Technologies\Software Tools\DatapixxToolbox_trunk\mexdev\build\matlab\win64</span>''') to usage locations ...
** '''C:\toolbox\DataPixx''' - for '''<span style="color:maroon">MATLAB R2017A</span>.'''
** '''C:\toolbox\Psychtoolbox\PsychBasic\MatlabWindowsFilesR2007a''' - for '''<span style="color:maroon">MATLAB R2019B</span>.'''
*** <span style="color:red">'''NOTE:''' Previous versions of Datapixx MEX files renamed to Old_Datapixx... etc</span>


Starting MATLAB and typing '''I1 <Enter>''' lists the I1's functions… not all are usable as we have the i1Display Pro, ''not'' the i1Pro.

 <nowiki>
>> I1
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
</nowiki>


'''>> I1('IsConnected?');'''

 <nowiki>
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
</nowiki>

'''>> isConnected = I1('IsConnected');''' produces the result for ‘'''isConnected'''’ as "'''1'''" if the '''I1''' is connected, "'''0'''" otherwise.


'''>>  I1('SetMeasurementMode?');'''
 <nowiki>
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
</nowiki>

'''>>  I1('GetMeasurementMode?');'''
 <nowiki>
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
</nowiki>

'''>> mode = I1('GetMeasurementMode');''' produced the (default) result for ‘'''mode'''’ as '''VPixx'''.

Running <br />
'''>>  I1('SetMeasurementMode', 'RGBLED');'''<br />
then<br />
'''>>  mode = I1('GetMeasurementMode');'''<br />
produced the result for ‘'''mode'''’ as
 <nowiki>
mode =

    ‘RGBLED’
</nowiki>

'''>> I1('GetTriStimulus?');'''
 <nowiki>
Usage:

Lxy = I1('GetTriStimulus'); 

Returns CIE Lxy coordinates of last i1 measurement.
</nowiki>

Taking a sample measurement with ‘'''RGBLED'''’ as the '''mode'''....


'''>> Lxy = I1('GetTriStimulus');''' produces the result for ‘'''Lxy'''’ as 
 <nowiki>
>> Lxy =

     94.3362, 0.3781, 0.3791
</nowiki>

'''(<span style="color:red">NOTE:</span> VPIxx say you need a second or so exposure to collect a sample, so you will need to allow for this in your code)'''


'''>>  I1('SetIntegrationTime?');'''
 <nowiki>
Usage:

I1('SetIntegrationTime', time);

Sets the integration time used to take a measurement by the i1Display.
It represents the maximum time which could be taken by the i1Display to get a measurement.
The value must be > 0.2 seconds. Default is 0.2 seconds.
</nowiki>

'''>> I1('GetIntegrationTime?');'''
 <nowiki>
Usage:

time = I1('GetIntegrationTime');

Gets the integration time used for measurements by the i1Display.
It represents the maximum time which could be taken by the i1Display to get a measurement.
</nowiki>

So

'''>> time = I1('GetIntegrationTime');'''<br />
'''>> '''<br />
'''>> time'''<br />
 <nowiki>
time =

    0.2000
</nowiki>

So to set the integration time to '''1''' second ...

'''>>  I1('SetIntegrationTime', 1);'''

And to check it’s changed …

'''>> time = I1('GetIntegrationTime');'''<br />
'''>> '''<br />
'''>> time'''<br />
 <nowiki>
time =

    1
</nowiki>

