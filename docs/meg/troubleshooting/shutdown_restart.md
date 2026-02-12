# MEG Power Shutdown / Restart

### **<span style="color:maroon">Problem</span>**

CHBH was informed by Estates of a **whole building shutdown on Saturday 15th January 2022, for High Voltage maintenance**. The shutdown was to **last at least 6 hours.** <br />
A **Measurement Window was set to start ~30min/60min before shutdown**, to make sure **liquefaction wasn't taking place**.

### **<span style="color:maroon">Solution</span>**

After liasing with MEGIN, the **shutdown/startup procedure was agreed as follows**...

<br />
**<span style="font-size:large;color:blue">To shutdown beforehand, say ~30min before the agreed time...</span>**

-  **Power down the Stim PC/s, Participant Logging Computer, EyeLink Host Computer (*as necessary*).<br />
Turn off the monitors.<br /> Power down the two UPS on the Control Room floor (*make sure they don't restart!*)**.
	- **Press** and **hold the Power button** for **approximately 0.5 to 1 second**. The unit **should beep, indicating it is turning off. Front panel LED should go out**.
	- **Switch off** the **Mains** at the wall socket.
- ***May be prudent to power off above equipment the day before, to reduce workload on the day.***
- Set the **Internal Helium Recycler (IHR)** to **Maintenance Mode** using the **Service GUI**.
- **Close valve BV4** on the pressure regulator panel in the Internal Helium Recycler cabinet.
- **Open valve BV13** (***Refill Bypass Valve - on the wall behind the MSR***) to let any excess Helium **exit outside via Helium exhaust pipe**.
- **Make sure** that the **Main Power Switch on the cryocooler compressor** is set to **OFF** (***the cryocooler shouldn't be running, but stop liquefaction first if it is***).
- **Turn off** the **Electronics cabinet** components... **in order (left to right)**.
	- **1st - Preamps.**
	- **2nd - SQC Cards.**
	- **3rd - Mains.**
- **Turn off** the **IHR cabinet** (***press the UPS Power button** for a few seconds*).
	- **Turn off** the **IHR Mains power** (**<span style="color:red">large red switch</span>** on the wall to the right of the cabinet).
- **Turn off** any **Stimulus cabinet devices**, **power off the bar plug**.
- **Turn off** the **gantry lifting motor/traffic lights** (*Mains plug on the back wall, behind the MSR*).
- **Shutdown** the **DACQ console & monitor**.
- **Switch off** the **Watchguard Firewall and Network Switch**, in the **Side Room Comms cabinet**.
- **Switch off** the **MSR lighting UPS**...
	- **Press** the **Power button** on the front panel for **2 seconds**, **release** at first beep.
	- **Switch off** the **Mains** at the wall socket.
- **Switch off** the MSR **Jun-Air air compressor** (*in the IHR Tank room, found* ***behind the tanks***).
- **Power down** the **two Eaton UPS** located at the **back of the IHR Tank room**...
	 - **Press** the **Power button** on the front panel for **3 seconds**.
	 - The UPS should **start to beep** and show a **status of "UPS off pending..."**. The UPS then transfers to **Standby mode**, and the Mains indicator **turns off**.
	 - **Switch off** the **Mains** for each UPS (*Sockets on back wall, to the right of both UPS*).


**<span style="font-size:large;color:blue">To startup, after confirmation that Mains power is fully restored...</span>**

- **Switch on** the **Mains** sockets for the **two Eaton UPS**.
	- **Both UPS front panel displays illuminate** and **show a status of "UPS initializing..."**.
	- ...both should then **transfer to Standby mode ("UPS on standby")**.
- Press the **Power buttons** on both front panels for **at least 1 second**.
	- The UPS front panel displays **change status to "UPS starting..."**.
	- **Confirm the Power On indicator are lit** and showing **<span style="color:green">solid green</span>**, indicating that both UPS are **operating normally** and **any loads are powered** (***or will be once they are turned on***).
	- The UPS should **now be in Normal mode**.
	- **Press** the **ESC button** until the **start screen appears**.
- **Switch on** the MSR **Jun-Air air compressor** (*in the IHR tank room, found* ***behind the tanks***).
- **Switch on** the **MSR lighting UPS...**
	- **Switch on** the **Mains** socket.
	- **Press** the **Power button** on the front panel.
	- The **<span style="color:green">green "On Line"</span>** indicator **flashes**.
	- The **<span style="color:#E4D00A">yellow "On Battery"</span>** indicator **lights** while the **Self-test** is being performed.
	- When **Self-Test** has **successfully** completed, **only the <span style="color:green">green "On Line"</span> indicator** will be lit.
	- **Check** the MSR lights **come on** when the **light switch is depressed**.
- **Switch on** the **Watchguard Firewall and Network Switch**, in the **Side Room Comms cabinet**.
- **Turn on** the **gantry lifting motor/traffic lights** (*Mains plug on the back wall, behind the MSR*).
- **Turn on** the **Electronics cabinet** components... **in order (right to left)**.
	- **1st - Mains**.
- **Power up** the **DACQ console and monitor**, wait until login splash screen appears on the monitor.
	- **2nd - SQC Cards**.
	- **3rd - preamps**.
- **Run** a **[RAP](../../meg/acquisition/rap.md)** (**R**estart **A**cquisition **P**rograms) on the **DACQ**.
- **Turn on** the **IHR Mains power** (**<span style="color:red">large red switch</span>** on the wall to the right of the cabinet).
- **Turn on** the **IHR cabinet** (***press the UPS Power button** for a few seconds*).
- **Turn on** the **Main Power Switch on the cryocooler compressor**.
- **Turn on** the bar plug in the **Stimulus cabinet**, **power on** any **devices**.
- **Open valve BV4** on the pressure regulator panel in the Internal Helium Recycler cabinet.
	- **Wait for 1 minute**.
- **Close valve BV13** (***Refill Bypass Valve - on the wall behind the MSR***).
- **Set** the IHR to **Normal Mode/Cooldown Mode** (as necessary) using the **Service GUI**.
	- **Check** the **correct LED combination** is **showing on the IHR cabinet door**.
- **Turn on the two UPS on the Control Room floor; power on Stim PC, Participant Logging Computer, EyeLink Host Computer (as necessary)**.
- **<span style="font-size:large;color:maroon">Phew, Well done! Have a well-deserved cup of coffee!</span>**


