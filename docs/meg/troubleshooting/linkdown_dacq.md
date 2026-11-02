# Link to DACQ workstation is down

### **<span style="color:maroon">Problem</span>**

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


