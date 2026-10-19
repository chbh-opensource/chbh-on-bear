# Power Down Equipment

<big>
**<span style="color:maroon">In fault situations, planned (UoB) power outages, or End-of-Day, equipment will need to be shutdown</span>**
</big>

!!! warning "<span style="font-size:medium"><span style="color:red">NOTE:</span> In normal, End-of-Day usage, not ALL equipment needs to be powered down.</span><br /><span style="font-size:medium"><span style="color:red">NOTE:</span> e.g. DO NOT power down IHR, Main Electronics, DACQ etc. on a daily basis!!! </span>"

#### <span style="color:maroon">Powering Down the Internal Helium Recycler (IHR) (cabinet T3)</span>

1. In the **IHR cabinet**, keep the **UPS power button pressed down** for a few seconds.
2. Turn the Main Power Switch on the cryocooler compressor is set to **Off**.
	- *the cryocooler shouldn't be running, but stop liquefaction first if it is*
3. **Turn off** the **IHR Mains power** (**<span style="color:red">large red switch</span>** on the wall to the right of the cabinet).

<br />
#### <span style="color:maroon">Powering Down the Main Electronics Cabinet (cabinet T2)</span>

!!! note "<span style="color:red">NOTE:</span> The Main Electronics Cabinet (T2) is protected by a UPS (UPS21), situated in the IHR tank room (G24)."

The **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)** of the Main Electronics Cabinet has three switches. These **MUST** be powered down in the correct sequence.

**INDEX**<br />
1. **Main switch** (*with no-mains release*). <br />
2. **Main (DSP) Electronics** (*MEG & Bioamplifier/EEG*) **<span style="color:green">green</span>** rocker switch. <br />
3. **Preamplfiers** (*MEG & Bio/EEG*) **<span style="color:green">green</span>** rocker switch.

**Procedure**

1. **Switch off** the **Watchguard Firewall and Network Switch**, in the **Side Room Comms cabinet**.
	- **Both Mains plugs** are attached to sockets protected by **UPS21**. Make sure **both socket switches are turned off**.
2. **Switch off** the **Preamplifiers (3)** rocker switch first, followed by the **Main (DSP) Electronics rocker switch (2)** from the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)**
3. Turn the **Main switch (1)** on the **[Power Control Panel](../../images/meg/DSP_Electronics.jpg)** to **Off** position. 
	- This will turn off the ethernet switch, the roof fans, and the intercom.
	!!! Note "It may take a while before the LED indicators go off. A [Power Control Panel](../../images/meg/DSP_Electronics.jpg) will not restart before all indicators are off."
4. Power off the Eaton UPS, labelled **UPS21**, situated in the IHR Tank Room (G24).
	- First **power down** equipment that is connected to the UPS (*see above*).
	- **Press and hold the On/Off** button on the front panel for **approximately three seconds**. <br /> The UPS starts to beep and shows a status of “**UPS off pending**”. <br /> The UPS transfers to Standby mode (“**UPS on standby**”) (*if utility power is available*) and removes power to the equipment. The **<span style="color:green">green</span> Power On** LED turns **off**.
	- The **Watchguard Firewall and Network Switch**, in the **Side Room Comms cabinet**, will also power down - *if not switched off already*.
	- **Switch off** the Mains socket powering **UPS21**.

<br />
#### <span style="color:maroon">Powering Down the contents of the STIM Cabinet (cabinet T1)</span>

1. **Turn off** equipment in the STIM Cabinet (T1) e.g. Digitimer Stimulator, via their power buttons/switches.
2. **Switch off** the filtered 6way Mains extension (**<span style="color:green">green</span>** rocker switch).
	- This will power down the MSR Patient Camera/IR Light, and the STI102 box.

<br />
#### <span style="color:maroon">Powering Down DACQ & Participant Logging Computer (PLC)</span>

!!! note "<span style="color:red">NOTE:</span> The DACQ and its speakers are plugged into Control Room double power sockets protected by a UPS (UPS20), situated in the IHR tank room (G24).<br /> The PLC is plugged into the UPSs found on the floor of the Control Room (2 x APC Back-UPS 1400s)."

**Powering Down the DACQ Console, "Sinuhe"**

1. ''From Login Screen''.
	- Bottom right corner, left mouse click, select "'''Shut Down'''".
2.  ''If logged In''
	- Exit Acquisition program, close Terminal windows etc.
	- Bottom left corner, left click.
	- Hover over "'''Leave'''", select "'''Shutdown'''".
3. Power off''' Monitor and Speakers.
4. Switch off''' the mains socket powering the DACQ.

**Powering Down the Participant Logging Computer (PLC)**

1. '''Press''' the power button on the front of the PC.
2. '''Power off''' the Monitor.
3. '''Switch off''' the mains sockets powering the PC and Monitor.

**Power off the associated Eaton UPS, labelled "UPS20" - <span style="color:red">On the floor, at back of IHR Tank Room</span>**.

1.  '''Turn off''' the equipment that is connected to the UPS (''see above'').
2. '''Press''' and hold the '''Off''' button on the front panel for approximately three seconds. <br /> The UPS starts to beep and shows a status of “'''UPS off pending…'''” <br /> The UPS transfers to Standby mode (if utility power is available) and removes power to the equipment. The green Power On LED turns off.
3. '''Switch off''' the mains socket powering the UPS.

<br />
#### <span style="color:maroon">Powering Down the Stim PC (CHBH-ST-MEG-W02)</span>

1.  '''Shutdown the PCs''' as you would normally ('''Windows 10''').
2. Switch off the '''Monitor'''
3. Switch off the '''PROPixx Controller'''.
4. ''(Switch off '''SOUNDPixx Controller''' and '''PC Speakers''' if used)''
5. Switch off the attached 8-way bar plug powering the KVM and network mini hub.
6. Shut down both '''APC Back-UPS 1400s.'''
	- Press and hold the POWER button for at least 2 seconds. At the first beep, release the button and the UPS will turn off. A 2-second delay has been added to mitigate unintentional contact with the POWER button.
	- '''''<span style="color:red">NOTE:</span>''' Make sure '''other equipment''' e.g. PROPixx Projector, EyeLink PC, '''is powered off BEFORE switching off ''' the APCs.''
7. Switch off the '''mains sockets''' powering the '''APCs'''.
	- '''''NOTE:''' Mains sockets can be left '''switched on''' during normal, daily usage.''
	- '''''NOTE:''' Only switch off '''in emergency''', or if equipment is being moved.''

<br />
#### <span style="color:maroon">Powering Down the EyeLink 1000 Plus PC</span>

1. After Data Acquisition etc., click/select "'''Exit EyeLink'''" on Host PC.
	- Or click/select "'''Shutdown Host'''", click/select "'''YES'''" <span style="font-size:large">&rarr;</span> Point 3.
2. Click red "'''<span style="color:red">Shutdown</span>'''" button.
3. Turn off '''Monitor'''.
4.  '''Turn off EyeLink battery''', unplug power cables from battery and FO Camera Head/IR Illuminator.
5. Replace lens cap, '''move FO Camera Head/IR Illuminator''' back to MSR white cabinet, carefully tidy up '''<span style="color:orange">orange</span>''' FO lead and place in cabinet.
6.  '''Remove EyeLink battery''' from MSR and '''put battery on charge''' ''(if able to)''.
	- '''Unplug''' battery once fully charged. '''Do not''' leave attached to the charger.
7. '''Switch off bar plug on table''' by EyeLink Host PC
	- This ensures the ''actual'' '''EyeLink camera is powered down'''.
8. Shut down both '''APC Back-UPS 1400s.'''
	- Press and hold the POWER button for at least 2 seconds. At the first beep, release the button and the UPS will turn off. A 2-second delay has been added to mitigate unintentional contact with the POWER button.
	- '''''<span style="color:red">NOTE:</span>''' Make sure '''other equipment''' e.g. PROPixx Projector, EyeLink PC, '''is powered off BEFORE switching off ''' the APCs.''
9. Switch off the '''mains sockets''' powering the '''APCs'''.
	- '''''NOTE:''' Mains sockets can be left '''switched on''' during normal, daily usage.''
	- '''''NOTE:''' Only switch off '''in emergency''', or if equipment is being moved.''

