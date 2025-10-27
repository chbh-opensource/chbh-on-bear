# Stimulus Equipment

## Stimulus PCs

The CHBH has a rack of Stimulus PCs in the Console Room. The individual PCs are addressed by a single keyboard mouse & local screen via the KVM Switch (Keyboard/Video/Mouse Switch) mounted at the top of the rack.

Choose which Stimulus PC you want to run your experiment on and select that via the KVM Switch. KVM1 for Windows 10, KVM 2 for NeuroDebian. you can freely switch between the two, though MATLAB may need to be relaunched if it was active during switching.

What is seen on the local screen in the console room, is seen on the projector screen (when the wake command has been issued to the projector). Both local terminal screen and VPixx Projector are 1920x1080@120Hz for Ubuntu, and 1920x1080@100Hz for Windows 10 (not the 100Hz for Windows, 120Hz is not stable and will cause flickering). Note that only the central element of the Console Screen will be visible on the in bore projection screen. The Projector overfills the rear projection screen and the useful resolution is closer to ~4:3 ~1440x1080 visible. Always verify your paradigm's visual elements are not only visible on the projector screen and stimulus machine monitor, but remain so via the participant's superior mirror.

The KVM is not configured to route Audio, therefore to choose a specific Stimulus PC, as audio source, employ the plugs on the Audio Patch Panel.

Available Stimulus PCs are;

- KVM 1 - Windows 10 - PsychoPy, MATLAB 2018B with the PTB, Presentation, EPrime and NIDAQ Hardware [[6]]

- KVM 2 - Ubuntu 18.04.1 LTS with Neurodebian - PsychoPy, MATLAB 2018B with the PTB [[7]]

These have near identical hardware, INTEL i7, AMD WX7100. The Windows 10 machine has an additional National Instruments DAQ and BNC breakout attached. If one machine fails, the other can boot to Windows 10 / Ubuntu with intervention of the Technician. Identical Common Experimental Platform PCs are also installed in other modalities, several cubicles and the Mock Scanner room. You are invited to test your paradigms there.

There are also legacy Stimulus PCs at the foot of the rack.

- KVM 3 - Windows 7 - this is a former BUIC STIM PC and should function as before, except a difference in screen resolution* {Currently disabled and soon to be retired}

- KVM 4 - Windows XP - QUALISYS, ROBOT, other legacy.

When any CHBH Stimulus PC is selected via the KVM it will receive reports from the Keyboard, Mouse at the local screen, and from the NATA Response Interface and the LABJACK U3. Other devices may be plugged directly into the fascia of the desired Stimulus PC.

## vPixx Projector

The commands needed to enable the projector are as follows;

- launch the VPUtil command line interface (click the desktop icon in Windows / under Linux; click to open the desktop VPUtil folder, and in the folder pane that opens rightclick on the white space and Launch A Terminal From That Location, then type ./vputil and press enter).

- In that VPUtil interface type *ppx a* and return to awaken the projector.

- In that VPUtil interface type *ppx s* and return to deactivate.

- Do not leave the projector awakened.

- If you get the error 'VPixx Device FPGA device appears unprogrammed' this means the USB connection to the Projector has failed. Switch the KVM to 2 or and then back to 1, or vice versa, for 10 seconds to restore connection. You can switch between Windows 10 and the NeuroDebian CEP using the KVM, whilst the projector is live, and the projector will display the selected desktop.

These should be all you need for basic use of the VPixx. Instructions with detailed trouble shooting steps are found here. UPDATED SEPT 2021 - if the projector / console screen is flickering for more than a minute after booting you may need to reboot.

The projector should be set at 16:9 1920x1080@120Hz. The Projector overfills the rear projection screen and the useful resolution is closer to 4:3 1440x1080 visible. Always verify your paradigm's visual elements are; not only visible on the projector screen and stimulus machine monitor, but also remain so via the participant superior mirror.

## Recovering responses/triggers via NATA Interface

### Recovering Triggers

Scanner volume timing is delivered to the CEP Stimulus machines by the detection of the letter 't' (as if from a USB keyboard, spoofed by the NAtA interface box). This will echo into any command windows you use for running stimulus. Consider using the 'commandwindow' command at the beginning of MATLAB scripts to direct key presses away from the script editor! Alternatively switch off the NAtA interface box when troubleshooting, or open a notepad window to redirect these.

When a Stim PC is selected via the KVM [[9]] and the 2x5 NATA Response Interface is on, [[10]], then scanner volume triggers will echo as 't' keypress (at ~7ms after the volume begins). Consider using the suggested trigger code snippet on github, linked below, to recover this timing. If you are recovering other keypresses (e.g. 0-9) make sure you ignore ensuing 't's. Beware also, that if CAPSLOCK is on any keyboard attached to the current Stim PC, the NAtA will report 'T'. So always check CAPS LOCK is off, or program defensively to respond to 't' or 'T'.

KbCheck on Windows, and KbCheck(-3) on Linux should suffice to recover the 't' press. When you want to ignore successive 't' during recovery of Response Box keypresses use DisableKeysForKbCheck.

Example code using the more complex KbQueue is provided on [Github](https://github.com/theCHBH/fMRI/blob/master/SampleTriggerCodeCHBH_Windows).

The SIEMENS Prisma produces a 1us impulse which is delivered fibre-optically to the SIEMENS Interface Box behind the console PC. This has two settings, TOGGLE and IMPULSE, and requires USB power. Ensure IMPULSE is selected. The BNC output of this SIEMENS Interface Box is relayed to the NATA Response Interface, with potential breakout for other devices. 

The NAtA is connected directly to the KVM and reports a 't' via USB connection, which also reports 1,2,3,4,5 & ,6,7,8,9.0 for NATA response peripheral. The NATA Interface Box also passes the signal via a DB25 breakout, and <1ms delay. This is DB25 breakout is normally connected to the legacy Windows 7 BUIC Stimulus PC. This enables legacy BUIC experiments to be run without alteration on the legacy Stimulus PC (besides screen size considerations). The DB25 breakout may also be connected to the LABJACK U3, the National Instruments DAQ or the BlackBoxToolKit.

### Recovering Participant Responses in Linux

The NAtA Response Pads are installed in the scanner chamber in two configurations. 2x2 which report 12 34 and 2x5 which report 12345 67890 as if they were cut down USB keyboards. (NB Responding as US keyboards in PTB, not UK configuration.)

The 2x2 Interface and 2x5 are always on and connected. Both are connected via the KVM. if you switch between Windows and Linux whilst MATLAB is open, you may need to re-open MATLAB for to detect the NAtA.

Under Neurodebian use the following device names when setting up your KbQueue in PTB MATLAB;

```MATLAB
DeviceName = 'NAtA Technologies LxPAD PK080219 v6.11'  % 2x5 and trigger 't'

DeviceName = 'NAtA Technologies LxNK Keypad' % 2x2 only

DeviceName = 'Dell Dell QuietKey Keyboard'  % Experimenter Keyboard
```

Here is example [code](https://github.com/artaxerxes/TheCHBH/blob/master/twoDevice_KbQueue) that demonstrates gathering Experimenter Keyboard Responses and Participant 2x5 / Scanner volume triggers from the NAtA 2x5.

Always ensure the NAtA boxes respond before placing your participant in the scanner. They will illuminate the red LEDs on the front of the NATA Interface Box, so observe these. If they illuminate and there is no response from the stimulus PC then reset the PC as the USB hub has been sent to sleep and not awoke with the PC.

## Participant audio - Siemens / SoundPIXX

For Operator/Participant contact we rely on the inbuilt Siemens audio console. This broadcasts into the Room, and optionally via the mono pneumatic in-ear headphones that can be attached to the base of the participant bed.

For experimental audio, routed from the CEP stimulus machines the Siemens Room Audio / In-Ear Headphones may be suitable. However if you require Stereo reproductions or and higher fidelity audio reproduction there is the SoundPIXX system. This requires the use of a second set of headphones, stored to the left hand side of the head of the scanner bed.

As noted above, the KVM is not configured to route Audio, therefore to choose a specific Stimulus PC, as audio source, employ the plugs on the Audio Patch Panel.To switch between the two audio systems there is a patch panel (bank of ports for large audio cables) below the CEP Stimulus machines on the main rack. These allow audio to be routed from the CEP Stimulus Machines to the two available audio outputs. Sources are the Windows and the Neurodebian CEP Stim, outputs are the Siemens (Room + Participant Headphones), or the SoundPIXX (Participant Headphones only).

When utilising the SoundPIXX Audio the Siemens Room audio may suffice for participant communication still, but there is a secondary black desktop Microphone that you can use to speak directly into the SoundPIXX headphones.

!!! warning
    The SoundPIXX headphones have a much higher range of available volume than the Siemens in-Ear headphones and participants may be overwhelmed. Before any experiment involving their use check the settings are suitable, and that they have not been changed since your last scan. Additionally check the volume setting on our CEP Stimulus machine has not changed as the interaction of these two can produce surprisingly high volumes of noise which will be delivered directly into the SoundPIXX in ear headphones.

## Troubleshooting

When the Siemens Room audio is all that is required the patch panel should be left in the standard position to avoid a ground loops developing - which delivers a rumbling bassy noise. Should you experience this noise switch the Audio patch from 23-24 or vice versa.
