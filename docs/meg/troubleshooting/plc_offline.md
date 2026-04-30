# "The Participant Logging Computer isn't working!"

### **<span style="color:maroon">Problem</span>**

If the CHBH Intranet is down for any reason (e.g. faulty certificate), the Participant Logging software (via the standalone PC, or via a browser webpage) won't be available.

### **<span style="color:maroon">Solution</span>**

To generate a pseudonymised PL code for an up-and-coming Acquisition session, please use the following format...

- **YYYYMMDD#B**, and then a **3 digit Hex encoding** of the **slot booking time** e.g **1500 which is "5DC"** (*use dec2hex in MATLAB, or just Google for a Hex converter*).

- **18th January 2022**, at (*exactly*) **1500 (3pm)** would be **"20220118#B5DC"**.


Any manually-created PL code will need to be added to the PL database. Please email CHBH Lead Computing Officer with any that are created.
<br />
For current MEG session slot times, the following Hex codes can be used ...
<br /><br />
**<span style="font-size:large;color:blue">0900 => "384"<br /> 1100 => "44C"<br />1300 => "514"<br />1500 => "5DC"<br />1700 => "6A4"<br /></span>**

If the **P**articipant **L**ogging **C**omputer (**PLC**) is faulty, or there is some other Service/Network issue, but CHBH Intranet is working, the logging software can be accessed via a browser.

!!! Info "FireFox may be required, instead of Chrome, if there are still certificate issues."

Links are shown below. The second log screen should automatically show after participant details are entered into the first screen, but the second link is provided if needed to be used individually .</span>

!!! warning "<span style="color:red">The URLs are MEG-specific, please do not use them in the MRI.<br /> MRI have their own PLC webpages, added to their Stim PCs.<br /> **[MRI Troubleshooting, PLC isn't working](../../../mri/hardware/troubleshooting/#the-participant-logging-computer-plc-isnt-working)**</span>"


**<span style="font-size:large">https://www.chbh.bham.ac.uk/meg-log/log-screen1.html</span>**

**<span style="font-size:large">https://www.chbh.bham.ac.uk/meg-log/log-screen2.html</span>**

A spare PLC is available, and it should just be a straight swap out if the in-use PLC fails... *potentially*.

!!! Note "The power supply RESET switch (*back of the case/part of the PSU*) may need to be held down for a few seconds, before pressing the power button, if the PLC fails to start up after swapping over."


