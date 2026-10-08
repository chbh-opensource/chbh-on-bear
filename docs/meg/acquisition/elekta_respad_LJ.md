# Elekta Response Pads & LabJack U3-LV

**<span style="color:maroon">MATLAB</span> Functions to use Elekta Response Pads with a LabJack U3-LV**.

Before NAtA response pads were purchased, the Supplier-provided pads were used to recover participant responses. The code may still be useful when using a LabJack.

The **Elekta Response Pads** (*"Bilateral Finger Response System"*) were attached, **via BNC cables**, to the **Stimulus Interface #2 (STI102)** trigger inputs **In 15** (***Left Pad***) 
& **In 16** (***Right Pad***) located in the **Stimulus Cabinet**.

**Stimulus Interface #1 (STI101)** is situated **on the Control Room desk**, and **by default** the two Interface boxes **are operated in parallel**. <br />

!!! info "**In parallel operation the signals from Interface #2 are duplicated on Interface #1.**"

**To record** button presses on *CHBH-ST-MEG-W02*, **Out 15** and **Out 16** from **Interface #1** were attached, **via BNC cables** to the **LabJack U3-LV Interface Box**
inputs **CIO0** (***pin 9/bit 16***) and **CIO1** (***pin 2/bit 17***) respectively.

!!! note "**<span style="color:red">NOTE:</span><span style="color:blue"> Stimulus Interface #2 dipswitch orientation (*in Stimulus Cabinet*)</span>.**<br /> - **Input Pull Up Resistor: <span style="color:red">ON</span>**<br /> - **Input Polarity: <span style="color:red">Raising Edge</span>**"

**The following MATLAB code was used to initialise the LabJack and record a response from the pads.**

**<span style="color:maroon">int_buttonInitalise.m</span>**

```matlab
function lj = int_buttonInitalise()

%% Initalise Labjack
% Make the UD .NET assembly visible in MATLAB.
lj.ljasm = NET.addAssembly('LJUDDotNet');
lj.ljudObj = LabJack.LabJackUD.LJUD;

% Open the first found LabJack U3.
[lj.ljerror, lj.ljhandle] = lj.ljudObj.OpenLabJackS('LJ_dtU3', 'LJ_ctUSB', '0', true, 0);

% Start by using the pin_configuration_reset IOType so that all pin
% assignments are in the factory default condition.
lj.ljudObj.ePutS(lj.ljhandle, 'LJ_ioPIN_CONFIGURATION_RESET', 0, 0, 0);

% define voltage threshold for button press
lj.volt_thr = 0.1; 
```

**<span style="color:maroon">int_getResponse.m</span>**

```matlab
function [resp,t] = int_getResponse(cfg)

% loop till broken from
while true
    
    % cycle through buttons
    for button = 1 : 2
        
        % get current state      
        [~,cs]  = cfg.lj.ljudObj.eDI(cfg.lj.ljhandle, button+15, 1); % check digital bit 16 (CIO0) and digital bit 17 (CIO1)
        
        % get time
        t       = GetSecs();
        
        % check if voltage exceeds threshold
        if cs < 1
            resp = button;
            WaitSecs(0.25); % wait to avoid press overlap
            return
        end
    end
end
```

**<span style="color:blue">Many thanks to Dr. Ben Griffiths for providing the code</span>.**
