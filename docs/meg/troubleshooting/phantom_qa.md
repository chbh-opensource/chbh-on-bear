# Phantom QA

**<span style="font-size:large;color:maroon">Problem</span>**

Whilst attempting to run a Phantom QA measurement, no dipoles were seen to activate in the raw data display.<br />
The Phantom cHPI cable and dipole cable were plugged into the gantry correctly.

**<span style="font-size:large;color:maroon">Solution</span>**

The ribbon cable from the PCB connector under the EEG hatch at the base of the gantry evidently wasn't reattached during a recent Service visit.

1. **Power down the Preamplifiers** in the **Electronics cabinet** - rocker switch 3 on the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)**
2. **Undo** brass screws holding EEG hatch in place.
3. **Whilst** wearing an electrostatic discharge (ESD) bracelet clipped to the rack, **route the ribbon cable to the far side of the EEG rack and reattach**.
4. **Unclip** ESD bracelet, screw back the EEG hatch.
5. **Power on Premplifiers** (rocker switch 3)

**<span style="font-size:large;color:maroon">Finally ...</span>**

1. **Reset the Electronics** by pressing the **Reset** of the **System Controller card [[SCC](../../images/meg/SCC.jpg)]**
2. **Restart Acquisition Programs** as shown here - perform a **[RAP](../../meg/acquisition/rap.md)**
3. **Reload a Tuning file** to check noise levels by following **[Loading a Tuning File](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**

**<span style="font-size:large;color:blue">Perform a full Phantom test at the earliest opportunity to check all the dipoles are now activating as expected.</span>**
