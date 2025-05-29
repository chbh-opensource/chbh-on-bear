# Troubleshooting

## VPixx Device FPGA device appears unprogrammed

Problem

If you get the error 'VPixx Device FPGA device appears unprogrammed' this means the USB connection to the Projector has failed.

Solution

Switch the KVM to 2 or and then back to 1, or vice versa, for 10 seconds to restore the connection. You can switch between Windows 10 and the NeuroDebian CEP using the KVM, whilst the projector is live, and the projector will display the selected desktop.

Instructions with detailed trouble shooting steps are found HERE.
UPDATED SEPT 2021 - if the projector / console screen is flickering for more than a minute after booting you may need to reboot.

## Siemens Room audio

Problem

When the Siemens Room audio is all that is required the patch panel should be left in the standard position to avoid a ground loops developing - which delivers a rumbling bassy noise.

Solution

Should you experience this noise switch the Audio patch from 23-24 or vice versa.

## Amplifier Out of synch, Barker words missing!

Problem

This error was encountered when using the Brain Products MR EEG caps and amplifiers in the PTL (G08).
The user was having issues keeping the impedance low as well as the software cutting out with the error "Amplifier out of sync, Barker words missing!"

Possible Solution

The so-called 'Barker words' are part of a watchdog mechanism that assures the integrity of the communication between the amp and PC interface. The error message likely originates from the BrainAmp driver.
The error message suggests that the optical path is impaired.
Check the following ...

Correct connection between fiber optic and amp/USB-adapter.
Clean optical plugs/slots.
If cleaning doesn't help, use another fiber optic cable for testing
Clean ribbon cables, plugs, and sockets. Make sure the cut ends of the ribbon cable are cleaned of any dried gel.
Update your BrainVision Recorder .

NOTE: For a combined EEG-fMRI measurement only: If the "Barker words missing!" error coincides with the start of an fMRI sequence, it can also be a sign of an RF overload. An amp experiencing RF overload can produce arbitrary error messages in Recorder.

## The Participant Logging Computer (PLC) isn't working

If the Participant Logging Computer (PLC) is faulty, or if there is some other Service/Network issue, but our intranet is working, you should be able to use the logging software via a browser.

Links are shown below. The second log screen should automatically show after participant details are entered into the first screen, but the second link is provided below if needed.

NOTE: The links will only work on the MRI Stim PCs.


https://www.chbh.bham.ac.uk/log/log-screen1.html


https://www.chbh.bham.ac.uk/log/log-screen2.html

## In bore projector screen out of focus

Problem

On occasion, the in bore projector screen is out of focus.

Solution

Most commonly the projector screen has been moved in the bore and not replaced in the correct locale.
You can remedy this by ensuring the red stabilisers (pictured below) are aligned with the black circles inscribed in the scanner bore.
General users and operators are free to move the screen to recover focus themselves.
Deploy caution as the screen has a deformable membrane, and costs £ks to replace.
Move it only via the solid base.


Much more rarely the Projector in the Equipment room has been moved.
Resetting the focus in that room should be the province of the CHBH technical staff.