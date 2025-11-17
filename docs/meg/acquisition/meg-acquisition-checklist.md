# MEG Data Acquisition Checklist

Click on the checklists to mark your progress through data collection.

## Prepare Control Room & MSR

-  [ ] Check functioning of stimulus and response equipment.

    === "Select the stim PC"

        - Select the correct Stim PC via KVM.
            - Press button 1 to connect to the OLD Stim PC.
            - Press button 3 to connect to the NEW Stim PC.
                - LED Meanings
                - <b><span style="color:green">Green</span></b>/<b>Dark</b> for connected PCs, but not active.
                - <b><span style="color:green">Green</span></b>/<b><span style="color:red">Red</span></b> for connected PCs actively using the KVM.
                - <b>Dark/Dark</b> for no connection.

    === "Select the parallel port"

        - Select the correct Parallel Port via the Parallel Port (PP) Switch Box.
            - PP Switch position A to connect STI101 to the OLD Stim PC (PP Base Memory Address: BFF8)
            - PP Switch position B to connect STI101 to the NEW Stim PC (PP Base Memory Address: CFF8)
            - PP Switch position C to connect STI101 to the [LabJack U3-LV](../hardware/meg-labjack.md) connected via USB to the NEW Stim PC

- [ ] Check Gantry position. Move from liquefaction (25) position to usage position.
	* **[Moving the Gantry](moving-the-gantry.md)**

- [ ] Check experimental paradigm.

    === "Check the PROPixx projector"

        - Check the PROPixx projector is "awake" (make sure lens cover is removed).
            - Start the VPutil program, from the Stim Desktop shortcut, and **type**...
            - (ANY DEVICE) > **`ppx a`** - should respond with "PROPixx is in awake mode"
            - To "sleep" the projector ...
            - (ANY DEVICE) > **`ppx s`** - should respond with "PROPixx is in sleep mode"
            - Please do not leave the PROPixx projector in "awake" mode when not in use e.g. overnight!
			!!! Note
			    **`ppx a / ppx s`** didn't work on one occasion. PROPixx needed a full power off/on to reset.
				

    === "Check Stimuli, Responses and Triggers"

        - Check that the stimuli and responses are as expected.
        - Check arrival of triggers in MEG recording.
		!!! note "New Stim PC PP card has a different Base Memory Address than the OLD Stim PC PP card."
			Change any, e.g. MATLAB, code on the NEW Stim PC, referencing the PP Base Memory Address to...<br />
			**CFF8** ... e.g. in `initialiseParallelPort.m`

- [ ] Start subject preparation - items to have ready/available.
 
	!!! info "Reusable and disposable electrodes are available for use as required."
	- Label 4 electrodes for EOG, 2 electrodes for ECG and any other (i.e. EMG) electrodes as required. Have some additional electrodes ready in case you have to redo them.
    - Electrode gel (in 20ml syringes - use the caulking gun to fill them.) We also have 12ml *curved tip* syringes available.
    - Cut tape ready for attaching electrodes to skin (*Tegaderm* tape)
    - Cut tape for securing electrodes (*Micropore* tape) and *Blenderm* tape for attaching cHPI coils.
	- Small double-sided sticky discs used to secure reusable electrodes.
    - If using an EEG cap, check it over for damaged electrodes. Makes sure it's clean and dry.
    - Set up the Digitiser chair, away from any metal. Attach the transmitter cube to the back of the chair. The **cable has to point downwards**.
    - See this page for our various consumable items - **[MEG Consumables](meg-consumables.md)**

- [ ] Check the MSR, yourself, and participant, for any unwanted items that could cause artefacts and remove them.
	- See this PDF... **[Metal items Checklist](../../meg/pdfs/Metal_items_checklist.pdf)**

- [ ] Check that the participant monitoring camera and microphone are working correctly.

## Prepare MEG system

- [ ] Login to the Console, start MEG Acquisition program (***megacq***).
- [ ] Load latest Tuning file, check quality of channels.<br /> "***Heat Sensor***", "***Reset Channels***" as necessary.
    - See this flowchart **[Noisy Channels](noisy_channels.md)**, or for a more detailed process see this walkthrough **[To fix noisy channels](to_fix_noisy_channels.md)**.
- [ ] Exit Tuner and return to ***megacq***. Adjust **Settings**
    - Select Project, or create new.
	- Input pseudonymised Subject details from Participant Logging Computer (PLC).
	- Adjust Acquisition parameters or load settings...<br /> **```File -> Load settings```** 
    - Create or adjutst stimulus generation, on-line averaging (as necessary).

## Prepare subject
 
- [ ] Offer bathroom break.
- [ ] Explain preparation procedure.
- [ ] Explain experiment.
- [ ] Let subject read and sign ethics consent and screening questionaire.
- [ ] Have subject remove metal objects, and do **a comprehensive check with both metal detectors**. Subject to change into scrubs if necessary (show subject to Changing Room and show scrubs sizes that are available).

!!! note "We are trying to reduce our laundry bill so only use scrubs if necessary e.g. metal in clothing."

## Attach electrodes

!!! info "Reusable and disposable electrodes available for use as required."

- [ ] Clean hands with provided Alcohol Gel Sanitizer.

When ready **to attach a reusable electrode:**

- [ ] Carefully attach a sticky disc to the electrode, centering the hole over the grey Ag/AgCl. Remove the paper protective cover, exposing the disc adhesive.
- [ ] Using a gel-filled syringe and blunt needle, place a drop of gel in the electrode center and place the electrode on the prepared site.
- [ ] Do not pull on the cable when applying it or when attached. Apply *Micropore* tape as necessary to help secure it in place.

If using the **[NeuroTab](https://www.unimed-electrodes.co.uk/15x20mm-Disposable-solid-gel-electrode-150cm-Lead-TP-connector-Box-of-120/151)** **disposable electrodes**.

- [ ] Remove the transparent backing from the electrode and place the electrode on the prepared site.
- [ ] To ensure good contact, apply pressure to the center of the electrode and move to the edges.
- [ ] Do not pull on the cable when applying it or when attached. Apply *Micropore* tape as necessary to help secure it in place.

**For either electrode type:**

- [ ] Where necessary, remove makeup with the provided Micellar water and cotton pads.
- [ ] Rub skin with alcohol pads where the electrodes and HPI coils will be attached (see **Figure 1** below). 

!!! note "Don't overdo it as the skin can become sensitive."

- [ ] Some Operators also like to then abrade the skin with *NuPrep* paste. 
	- Using one of our small stainless steel bowls, squeeze out some *NuPrep* and rub it onto the skin using a cotton bud.
    - Use tissues to gently wipe-off excess *NuPrep* as it is non-conducting (some Operators then like to re-wipe the skin with an alcohol pad).
- [ ] **hEOG**: Attach an electrode on the outside of the subject's left eye (**hEOG left**) and on the outside of the subject's right eye (**hEOG right**). 
- [ ] **vEOG**: Attach an electrode above subject's right eye (**vEOG up**) and below the subject's right eye (**vEOG down**). 

!!! note "In both cases, **make sure that the electrodes are in line with the eyes - horizonally & vertically**."

- [ ] **ECG**: Attach an electrode on the left collarbone (**ECG left**) and on the right collarbone (**ECG right**).
- [ ] **GND**: Attach an electrode on the back of the subject's neck (**GND**).
- [ ] **REF**: Attach an electrode on the subject's right cheekbone (**REF**).

![Figure 1](../../images/meg/Electrode_placement.png)
**Figure 1: Standard locations of EOG and ECG electrodes**

!!! Note
	REF may not be required for the bipolar EOG, ECG, but use as necessary if channels are noisy.<br />
	For EMG, site REF electrode where required/as per your paradigm.<br />
	Use *Micropore* tape over the electrodes to help hold them in place.
	
    Our Electrode input on the gantry is to the **right of the subject**, so we use the **right eye for vEOG**.

## Check impedance of electrodes

Use the **[SIGGI II impedance meter](../../meg/pdfs/SIGGI_II_User_Manual.pdf)**

- [ ] Press the white button, labelled *Enter/Esc*, on the jog-shuttle to turn on.
- [ ] Press the white button *again* to enter *Impedance Meter* menu.
- [ ] On the top side of the SIGGI ("***Single-Ch-In***") plug **GND** electrode into **"N"**.
- [ ] On the top side of the SIGGI plug **REF** electrode into **"-"**.
- [ ] On the top side of the SIGGI plug the **electrode of interest** into **"+"**

!!! note "If measuring EEG cap impedance, use the provided adapter."

- [ ] **Cycle through all electrodes**, and make sure the **impedance is <10kOhm**.
- [ ] Quit *Impedance Meter* by selecting *Return* symbol and press *Enter/Esc*. 
- [ ] Select *Power off* via the jog-shuttle and press *Enter/Esc*.

## Attach HPI coils

![Figure 2](../../images/meg/HPI_placement.png)
**Figure 2: Standard locations of HPI coils**

## Digitize head-coordinate system

## Digitize HPI coils

## Digitize head shape

## Prepare the subject in the MSR

## If using the EyeLink 1000 Plus

## Start recording

## Finishing recording session

## Tidying Up
