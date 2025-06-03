# MEG Data Acquisition Checklist

## Prepare Control Room, MSR

1. Check functioning of stimulus and response equipment.
  - Select the correct Stim PC via KVM.
    - Press button 1 to connect to the OLD Stim PC.
    - Press button 3 to connect to the NEW Stim PC.
        - LED Meanings
        - Green/Dark for connected PCs, but not active.
        - Green/Red for connected PCs actively using the KVM.
        - Dark/Dark for no connection.
  - Select the correct Parallel Port via the Parallel Port (PP) Switch Box.
    - Use PP Switch position A to connect STI101 to the OLD Stim PC (PP Base Memory Address: BFF8)
    - Use PP Switch position B to connect STI101 to the NEW Stim PC (PP Base Memory Address: CFF8)

2. Check Gantry position. Move from Liquefaction (25) position to usage position - [Moving the Gantry]

3. Check experimental paradigm.
    - Check the PROPixx projector is "awake" (make sure lens cover is removed).
        - Start the VPutil program, from the Stim Desktop shortcut, and type...
        - (ANY DEVICE) > `ppx a` - should respond with "PROPixx is in awake mode"
        - To "sleep" the projector ...
        - (ANY DEVICE) > `ppx s` - should respond with "PROPixx is in sleep mode"
        - Please do not leave the PROPixx projector in "awake" mode when not in use e.g. overnight!
            - NOTE: `ppx a / ppx s` didn't work on one occasion. PROPixx needed a full power off/on to reset.
    - Check that the stimuli and responses are as expected.
    - Check arrival of triggers in MEG recording.
        - NOTE: New Stim PC PP card has a different Base Memory Address than the OLD Stim PC.
            - Change any, e.g. MATLAB, code on the NEW Stim PC, referencing the PP Base Memory Address to...
                - CFF8 ... e.g. in `initialiseParallelPort.m`

4. Start subject preparation, items to have ready/available.
    - Label electrodes for EOG (2), ECG (2) and any other (i.e. EMG) electrodes. Have some additional ready in case you have to redo them.
    - NOTE: Reusable and disposable electrodes are available.
    - Electrode gel (in 20ml syringes - use the caulking gun to fill them.) We also have 12ml curved tip syringes now available.
    - Cut tape ready for attaching electrodes to skin (Tegaderm tape)
    - Tape for securing electrodes (Micropore tape) and small double-sided discs.
    - If using an EEG cap, check it over for damaged electrodes. Makes sure it's clean and dry.
    - Set up the Digitizer chair, away from any metal. Attach the receiver cube to the back of the chair. The cable has to point downwards.
    - The locations of our various consumable items can be found [here]()

5. Check the MSR for any unwanted items that could cause artefacts and remove them.

6. Check that the participant monitoring camera and microphone are working correctly.

## Prepare MEG system

## Prepare subject

## Attach electrodes

## Check impedance of electrodes

## Attach HPI coils

## Digitize head-coordinate system

## Digitize HPI coils

## Digitize headshape

## Prepare the subject in the MSR

## If using the EyeLink 1000 Plus

## Start recording

## Finishing recording session

## Tidying Up