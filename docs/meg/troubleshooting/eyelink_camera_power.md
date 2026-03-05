# No Power to EyeLink Camera

### **<span style="color:maroon">Problem</span>**

On Monday 17th April 2023, it was reported to MEG Support that the **EyeLink camera wasn't being detected by the Host PC software**.<br />
A "***Gige Camera not found***", or similar, error was reported when booting the EyeLink 1000 Plus Host PC, 
or when starting the Host Application software.<br />
**Switching** battery power on/off, or **swapping** to AC power, to the MSR camera head/illuminator **didn't resolve** the issue, and **disconnecting/remaking the FO cable connection also had no effect**.


### **<span style="color:maroon">Solution</span>**

This **error** is usually caused by the **lack of power to the camera unit** itself, or if the **ethernet cable linking the camera to the Host PC is unplugged**.

- **Check** the AC Adaptor power cable is **attached to the camera unit** (the camera is **lying on the desk next to the *Polhemus***), 
and that the **ethernet port LEDs on the camera are glowing**.

If the Adapter power pin plug is **correctly plugged in but the issue is still seen**...

- **Check the ethernet cable connecting the camera and the Host PC**.
	- **Remove and replug** the cable into the **camera** ensuring a **firm connection**.
	- **Remove and replug** the cable connection to the **Host PC** - making sure the **relevant** (***black***) **cable** is **firmly plugged into the correct ethernet port**
(***the standalone ethernet card on the Host PC, not the one on the motherboard***).

### **<span style="color:maroon">Fix</span>**

The **camera power pin plug was found on the floor**, probably **accidentally disconnected by moving the camera** to make desk space and catching the power connector on the table edge. 
<br />**Replacing** the power pin plug into the camera **solved the problem**.



