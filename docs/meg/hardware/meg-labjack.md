# Using LabJack to send MEG triggers

The following code can be used to send triggers to the MEG using a LabJack. The current setup uses a LabJack U3-LV, although the code can easily be modified for other versions.

!!! note
    There is a small delay sending triggers via a LabJack compared to directly from the PC (see <https://support.labjack.com/docs/3-1-command-response-u3-datasheet>). For many, this delay (~0.6-1 ms) is probably negligible, but if super accurate timing is important for your experiment you may need to look on LabJack's website for more information and/or run your own timing tests.

LabJack main website: <https://labjack.com/>

LabJack U3-LV documentation: <https://support.labjack.com/docs/u3-datasheet>

Example code for controlling LabJack U3: <https://support.labjack.com/docs/ud-example-code-u3-u6-ue9>

## Matlab code to initialise LabJack

Matlab-specific examples on LabJack support website: <https://support.labjack.com/docs/matlab-for-ud-windows>

The following code uses digital I/O to set ports to high or low (i.e., on or off) to send triggers to the MEG via a parallel port.

To connect to LabJack:

```matlab
function [ljudObj, ljhandle] = initialiseLabJack()

% Make the UD .NET assembly visible in MATLAB.
ljasm = NET.addAssembly('LJUDDotNet');
ljudObj = LabJack.LabJackUD.LJUD;

% Read and display the UD version.
disp(['UD Driver Version = ' num2str(ljudObj.GetDriverVersion())])

% Open the first found LabJack U3.
[ljerror, ljhandle] = ljudObj.OpenLabJackS('LJ_dtU3', 'LJ_ctUSB', '0', true, 0);

% Start by using the pin_configuration_reset IOType so that all pin
% assignments are in the factory default condition.
ljudObj.ePutS(ljhandle, 'LJ_ioPIN_CONFIGURATION_RESET', 0, 0, 0);

end
```

To send a trigger to the MEG:

```matlab
trigger_code = 255;
ljudObj.AddRequestS(ljhandle, 'LJ_ioPUT_DIGITAL_PORT', 0, trigger_code, 8, 0); % assign code to 0-7 ports
ljudObj.GoOne(ljhandle); % send the code
```

The 'LJ_ioPUT_DIGITAL_PORT' command will convert the trigger_code from decimal to binary (e.g., "87" becomes "01010111" in binary) and set the corresponding ports as low or high (0 or 1). The trigger is then sent via the parallel port when goOne() is called. To reset the ports back to low (i.e., all 0s), do the same as above but set `trigger_code = 0`.

For ease of use, you can wrap the code above in a function that quickly sends a trigger and resets to zero:

```matlab
function triggerSpike(ljudObj, ljhandle, trigger_code)

ljudObj.AddRequestS(ljhandle, 'LJ_ioPUT_DIGITAL_PORT', 0, trigger_code, 8, 0); %assign code to 0-7 ports
ljudObj.GoOne(ljhandle); %send the code
WaitSecs(0.002); % Psychtoolbox function. Should be more accurate, but can use pause(0.002) if not using psychtoolbox
ljudObj.AddRequestS(ljhandle, 'LJ_ioPUT_DIGITAL_PORT', 0, 0, 8, 0); %reset to zero
ljudObj.GoOne(ljhandle);

end
```

Then just call `triggerSpike(ljudObj, ljhandle, trigger_code)` in your scripts to send a trigger to the MEG (make sure to initialise the LabJack first, otherwise the `ljudObj` and `ljhandle` variables won't exist).
