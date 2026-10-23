# "Link to DACQ workstation is down"

### **<span style="color:maroon">Problem</span>**

If MEG Operators **inadvertently shutdown/restart the MEG DACQ Console/Workstation**, rather than logging off, **or the DACQ automatically reboots**, the IHR will send out the following error SMS text and email ...

**```Link to DACQ workstation is down```**

### **<span style="color:maroon">Solution</span>**

1. **Allow the DACQ to reboot** whilst **watching the bootloader/kernal initialisation process for any errors.**
	- **Allow any disk check to take place**.
	- **If errors are seen**, make a note/take 'phone image, and **contact MEG Support**, or **email chbh-help[@]contacts ...**, or **MEGIN** as necessary.
	- **After any advice**, reboot DACQ as necessary.
2. **Once** the Desktop/Login environment has loaded, log in.
3. **Perform** a **[RAP](../../meg/acquisition/rap.md)** (**R**estart **A**cquisition **P**rograms).
	- **```Applications -> Neuromag -> Maintenance -> Restart Acquisition Programs```**
4. Then **start Acquisition** and **Load** the latest Tuning file, see **[Loading a Tuning File](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**, to **make sure the correct Tuning file for acquisition is loaded**, and to **check for any sensor noise**.
	- **Check for any errors in the Message Box at the top of the Acquisition control window.**
5. See **[Restart Acquisition](../../meg/acquisition/restart_acquisition.md)** for full details.
6. **At some point after sucessful DACQ reboot**, the **IHR should send out** the following cleared SMS text and email ...

**```Link to DACQ workstation up again```**


