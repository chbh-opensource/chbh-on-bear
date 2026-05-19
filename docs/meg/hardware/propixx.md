# VPixx PROPixx Lite

**[Data Sheet](../../meg/pdfs/ds_propixx_lite.pdf)** <br />
**[PROPixx UserManual v1.1](../../meg/pdfs/PROPixx_UserManual.pdf)**

CHBH MEG use a **[VPixx PROPixx projector](https://vpixx.com/products/propixx/)** (480 Hz RGB, 1440 Hz greyscale), utilising high brightness LEDs (providing a larger colour gamut) 
to display stimuli onto a back-projection screen inside the MSR. It features a native resolution of 1920 x 1080.<br /> 
**The projector is situated outside the MSR**, at 90<sup>o</sup> to the MSR wall, and the projected image through the wave guide is thrown onto the screen via 
a ceiling-mounted mirror system with the mirror set at a 45<sup>o</sup> angle with respect to the midline of the MSR.

**The projector is attached to the Stim PC through the PROPixx Controller, via a DVI to DP (Display Port) adapter**. 
The adapter is used due to the Controller having DVI connectors, as it is an older model (now rebranded as DATAPixx), and the Stim PC using DP graphical output.

!!! Note "The PROPixx Controller was updated from 'Lite' to 'Full' in 2023, and is now able to output audio stimuli (with deterministic timing)."

To **control the projector**, the **"VPutil" program shortcut on the Stim PC Desktop is accessed**.

To check the PROPixx projector is "awake" (*make sure lens cover is removed!*).

- **Start the VPutil program**, from the Stim Desktop shortcut, and **type**...
- (ANY DEVICE) > **`ppx a`** - **should respond with "<span style="color:blue">PROPixx is in awake mode</span>"**.
- To "sleep" the projector ...
- (ANY DEVICE) > **`ppx s`** - **should respond with "<span style="color:blue">PROPixx is in sleep mode</span>"**.

!!! warning "Please do not leave the PROPixx projector in *awake* mode when not in use e.g. overnight!"
!!! warning "`ppx a / ppx s` didn't work on one occasion. PROPixx needed a full power off/on to reset."