# Power Up Equipment

<big>
**<span style="color:maroon">Cold start power up after mains failure / Service Operations / or at Start-of-Day</span>**
</big>

!!! note "<span style="color:red">NOTE:</span> "*The main electronics cabinet has been equipped with a power failure release main switch to ensure proper boot-up sequence of the computers. The following instructions are to be used  after mains power to the main electronics cabinet has been off due to mains failure or because the power to the three isolation transformers in the IHR tank room has been disconnected e.g. for service operations*"."
 
#### <span style="color:maroon">Powering Up the Internal Helium Recycler (IHR) (cabinet T3)</span>

1. **Make sure** the valves are as per this **[Figure 7.38](../../meg/pdfs/Figure_7-38.pdf)**.
	- *The valves shouldn't have been changed from their defaults since MEG installation.*
2. **Make sure** the small **Mode** switch on the cryocooler compressor is set to **remote control** mode (position 2).
3. **Turn the main power switch** on the cryocooler compressor to **On**.
4. In the Helium Recycler cabinet, keep the **UPS power button** pressed **down** for a few seconds.
5. Wait for the control PC to **power up automatically**.
	- *The control PC power-up takes about one minute.*
6. To **verify** that the system started up, **monitor the LEDs** on the door of the helium recycler cabinet.
	- *The LED/s indicating the latest active operating mode come/s on.*
8. To continue normal operations, click the **Normal Mode** button on the Service GUI.

<br />
#### <span style="color:maroon">Powering Up the Main Electronics Cabinet (cabinet T2)</span>

!!! note "<span style="color:red">NOTE:</span> The Main Electronics Cabinet (T2) is protected by a UPS (UPS21), situated in the IHR tank room (G24)."

The **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)** of the Main Electronics Cabinet has three switches. These **MUST** be powered on in the correct sequence.

1. **Main switch** (*with no-mains release*). <br />
2. **Main (DSP) Electronics** (*MEG & Bioamplifier/EEG*) **<span style="color:green">green</span>** rocker switch. <br />
3. **Preamplfiers** (*MEG & Bio/EEG*) **<span style="color:green">green</span>** rocker switch.

**Procedure**

1. **Boot/Power Up** the DACQ Workstation ("***Sinuhe***") as shown below. Wait until it **boots normally** (*shows Log In prompt*).
2. **Power on** the Eaton UPS, labelled **"UPS21"**.
	- **Switch on** the mains socket powering the UPS21.
		- The UPS front panel display illuminates, and shows a status of “**UPS initializing ...**”.
	- **Verify** that the UPS then transfers to Standby mode (“**UPS on standby**”).
	- **Press the "On/Off" button** on the front panel for **at least one second**.
		- The UPS front panel display changes status to “**UPS starting ...**”.
	- **Check** the UPS front panel display for active alarms or notices. **Resolve** any active alarms before continuing.
	- **Verify** that the **<span style="color:green">green</span> Power On** LED **illuminates solid**, indicating that the UPS is operating normally.
	- **Switch on** the equipment that is connected to the UPS21 (*see below*).
3. **Switch on** the **Watchguard Firewall and Network Switch**, in the **Side Room Comms cabinet**. Wait until both have started up, indicated by any **Self test** and **Fail** LEDs extinguishing. 
4. On the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)** of the Main Electronics Cabinet, ensure that the **<span style="color:green">green</span>** rocker switches, **Preamplifiers (3)**, **Main (DSP) Electronics (2)**, are in **Off** position.
5. Inside the Main Electronics Cabinet, the individual power supply units are connected to outlet socket strips located in the rear of the cabinet. **Ensure** that the power cords are **in place**.
6. Switch on the Main Electronics Cabinet power by turning the **Main switch (1)** on the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)** to the **On** position. The switch will automatically turn back into the **Off** position if Mains voltage **is too low**.
7. After turning the **Main switch (1)** to the **On** position, wait until the ethernet switch has started up, indicated by the **Self test** and **Fail** LEDs extinguishing. 
	- Bootup takes about one minute. The cabinet roof fans and auxiliary equipment, e.g the intercom, should also now power up. 
8. Switch **On** the **Main (DSP) Electronics green rocker switch (2)** from the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)**.
	- **Wait** until all the controller cards in the racks show **<span style="color:green">steady green</span> Run** LEDs and the **<span style="color:red">red</span> Fail** LEDs are off.
	- Boot-up takes about 30—60 seconds. 
	!!! info "If the bootup fails, open the back door of the main electronics cabinet and check the indicator LEDs of individual power supplies.<br /> The Main (DSP) Electronics racks must be booted *before* the Preamplifiers because the Preamplifiers are controlled by one of the main electronics boards."
9. Switch **On** the **Preamplifier green rocker switch (3)** from the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)**.
10. Run a **Restart Acquisition Programs** (**[RAP](../../meg/acquisition/rap.md)**) by double-clicking its icon in the Maintenance toolbox on the DACQ Workstation ("***Sinuhe***").

!!! note "<span style=color:red>NOTE:</span> Each time the MEG front end is powered it must be initialized by running a [RAP](../../meg/acquisition/rap.md).<br /> Also the latest tuning file must be loaded, via Tuner.<br /><span style=color:red>**NOTE:**</span> For optimum noise performance, let the Preamplifiers stabilize for approximately 1-2 hours before commencing MEG measurements."

<br />
#### <span style="color:maroon">Powering Up the contents of the STIM Cabinet (cabinet T1)</span>

1. **Switch on** the filtered 6way Mains extension (**<span style="color:green">green</span>** rocker switch).
	 - This will power on the MSR Patient Camera/IR Light and the STI102 box.
2. **Turn on** equipment in the STIM Cabinet (T1) e.g. Digitimer Stimulator, via their power buttons/switches as required. 

<br />
#### <span style="color:maroon">Powering Up DACQ & Participant Logging Computer (PLC)</span>

!!! note "<span style="color:red">NOTE:</span> The DACQ and its speakers are plugged into Control Room double power sockets protected by a UPS (UPS20), situated in the IHR tank room (G24).<br /> The PLC is plugged into the UPSs found on the floor of the Control Room (2 x APC Back-UPS 1400s)."

**Power on the Eaton UPS, labelled "UPS20", in the IHR tank room**

1. **Switch on** the Mains socket powering the UPS.
	- The UPS front panel display illuminates and shows a status of “**UPS initializing ...**”
2. **Verify** that the UPS transfers to Standby mode (“**UPS on standby ...**”).
3. **Press the On/Off button** on the front panel for at least one second.
	- The UPS front panel display changes status to “**UPS starting ...**”.
4. **Check the UPS front panel display** for active alarms or notices. Resolve any active alarms before continuing.
5. **Verify** that the **<span style="color:green">green</span> Power On** LED **illuminates solid**, indicating that the UPS is operating normally.
6. **Turn on** the equipment that is connected to the UPS (*see below*).

!!! Note 
	- **<span style="color:red">TO BE PERFORMED BY MEG SUPPORT ONLY!!</span>**
	 - **On one occasion, after power on, UPS20 was *shown to be On*, but the double sockets appeared to have no power (DACQ wouldn't power up). To fix ...**
		- ***Make sure DACQ & Monitor are off.***
		- **Trip (*and reset*) the UPS20 trip switch in the grey fuse box in the IHR Tank Room (*Incomer 1, L2*)**
			- ***UPS20 may beep, and switch to internal battery power briefly.***
		- **Check to see if power is now getting to the protected double power sockets.**
			- ***Turn on DACQ Speakers, <span style="color:green">green</span> Power LED should light.***
		- **If not, move DACQ & Speakers to unprotected sockets and power on.** 
		- **Have UPS examined for possible fault.**

**Powering up the DACQ Console, "Sinuhe"**

1. **Switch on** the Mains sockets powering the DACQ, Monitor & Speakers.
2. **Power on** the Monitor and Speakers.
3. **Press** the Power button on the right side of the DACQ system unit.
4. **Follow the boot sequence for any erors** - ***startup may initialise a disk check, let it proceed***. 
5. **Once the Login screen appears**, log in and run a **[RAP](../../meg/acquisition/rap.md)**, followed by **[Loading the latest Tuning file](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**

**Powering Up the Participant Logging Computer (PLC).**

1. **Turn on the two UPS (2 x APC Back-UPS 1400s) on the Control Room floor**.
	- **Switch on** the **Mains supply** at the **wall sockets for the two UPSs.**
	- **Press** and **hold the Power button** for **approximately 0.5 to 1 second**. The Unit **should beep, indicating it is turning on**.
	- **Front panel **<span style="color:green">green</span>** "On Line" LED should light, confirming the UPS is powered and operating normally**.
2. **Switch on** the Monitor.
3. **Press** the power button on the front of the PLC.
4. After a while the Monitor should **display** the **first** Participant Logging **information screen**.

<br />
#### <span style="color:maroon">Powering Up the Stim PC (CHBH-ST-MEG-W02)</span>

!!! info "2 x APC Back-UPS 1400s may already be powered, if PLC has been turned on already."

1. **Turn on the two UPS (2 x APC Back-UPS 1400s) on the Control Room floor**.
	- **Switch on** the **Mains supply** at the **wall sockets for the two UPSs.**
	- **Press** and **hold the Power button** for **approximately 0.5 to 1 second**. The Unit **should beep, indicating it is turning on**.
	- **Front panel **<span style="color:green">green</span>** "On Line" LED should light, confirming the UPS is powered and operating normally**.
2. **Switch on/check** (as required) associated equipment plugged into the UPSs.
	- **PROPixx Controller** (*Monitor is attached to this*)
	- **KVM** (*for keyboard/Mouse*)
	- **Network Mini Hub** (*EyeLink connection*)
	- **SOUNDPixx** (*if required*)
3. **Switch on** the Monitor.
4. **Switch on** the PC.
5. **CHBH-ST-MEG-W02** should boot into Windows automatically, no password required.

!!! note "As the DP PROPixx Adapter is negotiating with the KVM, the Monitor screen will flash 8 times at 2sec intervals then settle down. <br /> This is expected functionality and will happpen every time the Adapter, or PC, are repowered/rebooted."

<br />
#### <span style="color:maroon">Powering Up the EyeLink 1000 Plus PC</span>

!!! note "Stim PC will need to be powered up to allow network communication to the EyeLink PC (both APC Back-UPS 1400s will need to be powered)."

1. **Switch on 6-way bar plug on  table** alongside EyeLink Host PC (*to power Host PC and EyeLink camera*).
2. **Turn on** EyeLink 1000 Plus Host PC & Monitor.
3. Select "**EyeLink**" with mouse, or just wait.
4. **Confirm** EyeLink software starts.
5. **If only a Power Up check was required**, exit to EyeLink Manager and shutdown Host PC.
6. **Switch off** Monitor and 6-way bar plug.
7. **If EyeLink is to be used** when Acquiring data, follow up until Step 4., then follow ...

**[EyeLink Operations Guide](../../meg/acquisition/eyelink_operations_guide.md)**, and **[Charging EyeLink batteries](../../meg/acquisition/charging_eyelink_batteries.md)** as required.
