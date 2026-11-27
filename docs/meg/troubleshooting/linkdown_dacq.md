# Link to DACQ workstation is down

### **<span style="color:maroon">Problem #1</span>**

If MEG Operators **inadvertently shutdown/restart the MEG DACQ Console/Workstation**, rather than logging off, **or the DACQ reboots unexpectedly**, the IHR will send out the following error SMS text and email ...

**```Link to DACQ workstation is down```**

### **<span style="color:maroon">Solution</span>**

1. **If powered off completely, switch on the DACQ PC**.
	- **If DACQ is on, but Link is lost** - press **```Ctrl-Alt-Delete```** at least **once, possibly twice, to soft boot**.
2. **Allow the DACQ to reboot** whilst **watching the bootloader/kernal initialisation process for any errors.**
	- **Allow any disk check to take place**.
	- **If errors are seen**, make a note/take 'phone image, and **contact MEG Support**, or **email chbh-help[@]contacts ...**, or **MEGIN** as necessary.
	- **After any advice**, reboot DACQ as necessary.
3. **Once** the Desktop/Login environment has loaded, log in.
4. **Perform** a **[RAP](../../meg/acquisition/rap.md)** (**R**estart **A**cquisition **P**rograms).
	- **```Applications -> Neuromag -> Maintenance -> Restart Acquisition Programs```**
5. **<span style="color:blue">Move the gantry to an "in use" position e.g. Upright (60)</span>**
6. Then **start Acquisition** and **Load** the latest Tuning file, see **[Loading a Tuning File](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**, to **make sure the correct Tuning file for acquisition is loaded**, and to **check for any sensor noise**.
	-  !!! note "If the sensors are still noisy, more than one [RAP](../../meg/acquisition/rap.md) might be required and also maybe a [soft boot of the electronics](../../meg/acquisition/restart_acquisition.md/#resetting-the-electronics)"
	- **Check for any errors in the Message Box at the top of the Acquisition control window, or in any of the Acquisition settings e.g. [Gantry Position](../../meg/troubleshooting/gantry_position.md)**
7. See **[Restart Acquisition](../../meg/acquisition/restart_acquisition.md)** for full details.
8. **At some point after sucessful DACQ reboot**, the **IHR should send out** the following cleared SMS text and email ...

**```Link to DACQ workstation up again```**

### **<span style="color:maroon">Problem #2</span>**

A MEG Support SMS/email was received on a Saturday during OPM usage of the MSR.

**```
Link to DACQ workstation is down
```**

A device (*faulty Laptop adapter?*) was **plugged into one of the 3 x double Mains sockets, marked "UPS 20"**.<br />
These sockets are UPS-supported for USE ONLY by the MEG DACQ Console and its components (monitor, speakers) and **not for general use**.<br />
The device overloaded the UPS causing it to fail and shut down the Console unexpectedly.

### **<span style="color:maroon">Solution</span>**

The UPS was recoverable (see below), and the DACQ Console rebooted without incident.<br />
**<span style="color:red">Operators have been informed NOT to use these 3 x 2 sockets for any purpose, other than that specified e.g. for MEG DACQ Console and it's components</span>**.

1. **Enter IHR Tank Room** (G24), UPS 20 *may* be heard beeping.
	- The UPS may already be in Standby mode (“**UPS on standby ...**”).
		- If not, **Switch off, then on** the Mains socket powering the UPS 20.
		- The UPS 20 front panel should show a status of “**UPS initializing ...**”
		- The UPS 20 should then transfer to Standby mode (“**UPS on standby ...**”).
2. **Press the On/Off button** on the front panel for at least one second.
	- The UPS front panel display changes status to “**UPS starting ...**”.
4. **Check the UPS front panel display** for active alarms or notices. Resolve any active alarms before continuing.
5. **Verify** that the **<span style="color:green">green</span> Power On** LED **illuminates solid**, indicating that the UPS is operating normally.
4. Return to MEG Control Room, and power on DACQ Console.
	- **Press** the Power button on the front of the DACQ system unit.
4. **Follow the boot sequence for any erors** - ***startup may initialise a disk check, let it proceed***. 
5. Wait for Linux to load and the Login screen to appear.
6. **Once the Login screen appears**, log in and run a **[RAP](../../meg/acquisition/rap.md)**, followed by **[Loading the latest Tuning file](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**
7. **At some point after sucessful DACQ reboot**, the **IHR should send out** the following cleared SMS text and email ...

**```Link to DACQ workstation up again```**