# Power Up Equipment

<big>
**Cold start power up after mains failure / Service Operations / or at Start-of-Day**
</big>

!!! note "<span style="color:red">NOTE:</span> "*The main electronics cabinet has been equipped with a power failure release main switch to ensure proper boot-up sequence of the computers. The following instructions are to be used  after mains power to the main electronics cabinet has been off due to mains failure or because the power to the three isolation transformers in the IHR tank room has been disconnected e.g. for service operations*"."
 
#### Powering Up the Internal Helium Recycler (IHR) (cabinet T3)

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
#### Powering Up the Main Electronics Cabinet (cabinet T2)

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
#### Powering Up the contents of the STIM Cabinet (cabinet T1)

1. **Switch on** the filtered 6way Mains extension (**<span style="color:green">green</span>** rocker switch).
	 - This will power on the MSR Patient Camera/IR Light and the STI102 box.
2. **Turn on** equipment in the STIM Cabinet (T1) e.g. Digitimer Stimulator, via their power buttons/switches as required. 

<br />
#### Powering Up DACQ & Participant Logging Computer (PLC)

!!! note "<span style="color:red">NOTE:</span> Both the DACQ, it's speakers, and the PLC are plugged into double power sockets protected by a UPS (UPS20), situated in the IHR tank room (G24)."

''' Power on the Eaton UPS, labelled "UPS20" '''

# '''Switch on''' the mains socket powering the UPS. <br /> The UPS front panel display illuminates and shows a status of “'''UPS initializing…'''”
# Verify that the UPS transfers to Standby mode (“'''UPS on standby'''”).
# Press the '''On/Off''' button on the front panel for at least one second. <br /> The UPS front panel display changes status to “'''UPS starting…'''”.
# Check the UPS front panel display for active alarms or notices. Resolve any active alarms before continuing.
# '''Verify''' that the '''green Power On''' LED '''illuminates solid''', indicating that the UPS is operating normally.
# Turn on the equipment that is connected to the UPS (''see below'').
#* <span style="color:red">'''NOTE:'''</span> On '''one''' occasion the UPS was shown to be on, but the double sockets appeared to have no power. If this happens again...
#** Make sure DACQ & PLC are powered down.
#** Trip (and reset) the '''UPS20''' trip switch in the grey fuse box in the IHR tank room (Incomer 1, L2).
#** Check to see if power is now getting to the protected double power sockets.
#*** ''Turn on DACQ PC Speakers, green Power LED should light.''
#** If not, move DACQ & PLC to unprotected sockets and have UPS examined for possible fault.

''' Powering up the DACQ Console "''Sinuhe''" '''
# '''Switch on''' the mains sockets powering the DACQ, Monitor & Speakers.
# '''Power on''' the Monitor and Speakers.
# '''Press''' the Power button on the right side of the DACQ system unit.
# After a while the Monitor should display the Log In screen.
#* ''Any member of Ole's group knows the DACQ username/password.''

''' Powering Up the Participant Logging Computer (PLC)  '''

# '''Switch on''' the mains sockets powering the PLC and Monitor.
# '''Power on''' the Monitor.
# '''Press''' the power button on the front of the PLC.
# After a while the Monitor should '''display''' the Participant Logging '''information screen'''.
<br />

#### Powering Up the MEG-STIM-01 and CHBH-ST-MEG-W02 PCs 

# '''Switch on both APC Back-UPS 1400s''', and wait until they are on and operational.
# Switch on the associated 8-way bar plug (powers KVM and network mini hub).
# Switch on the blue '''PROPixx Controller''' (''the PC Monitor is attached to this''), and '''SOUNDPixx Controller''' (if it is to be used).
# Switch on the '''Monitor'''.
# Switch on the '''PCs'''.
#* ''If a PC doesn't power up, its PSU power switch back right has been unnecessarily turned off. Turn it on again''. 
# '''MEG-STIM-01''' requires a password ("TheCHBH"), '''CHBH-ST-MEG-W02''' boots to Windows automatically.
# If '''KVM switched to "NEW"''' (switch 3) when PCs booted, the Monitor screen '''will flash 8 times at 2-sec intervals''' (as expected) and then settle down.
<br />

#### Powering Up the EyeLink 1000 Plus PC ===

''' <span style="color:red">NOTE: </span> Relevant STIM PC will need to be powered up to allow network communication to the EyeLink PC (both APC Back-UPS 1400s will need to be powered).'''

# '''Switch on bar plug on  table''' alongside  EyeLink host PC (to '''power EyeLink camera & PC monitor'''). <br /> 
# '''EyeLink Batteries:''' Press '''TEST''' button to check power level, '''use a fully-charged battery''' if possible. 
#* '''Put''' the second battery '''on charge''' (if required). 
#**<span style="color:blue">Make sure '''battery''' is '''switched OFF''' when '''charging'''</span>
#* '''Swap batteries''' between acquisitions. '''Put''' first battery '''on charge'''.
#* '''"Charge"''' LED will '''go out''' when battery is fully charged / '''"Complete"'''.
#* '''Unplug''' battery once fully charged. '''Do not''' leave attached to the charger.
#** '''DO NOT''' leave on charge over night.'''
#** '''<span style="color:blue">If necessary leave a note for Jonathan, to put battery on charge first thing in the morning.</span>'''
#* <span style="color:maroon">'''''"A battery with 2-3 hours left should be fine for a short experiment. Do not risk using it for a 2-hour experiment."''''' </span>'''(SR Research)'''
# Take battery into MSR. Place in '''front right corner''' (''front left corner, if viewed from gantry'') 
# '''Arrange''' power cable around the edge of the MSR, '''avoiding any loops'''. '''Attach power cable''' to battery and to '''FO Camera Head/IR Illuminator'''. Switch on battery. 
#*'''<span style="color:maroon">Note: if you don’t power the camera head/IR Illuminator first, the Host PC will complain when "EyeLink” starts up.</span>''' 
# '''Place''' FO Camera Head/IR Illuminator on '''small table.''' Position table as required.
# '''Turn on''' EyeLink 1000 Plus Host PC & monitor.
# Select "'''EyeLink'''" with mouse, or just wait.
# '''Set up''' EyeLink FO Camera Head/IR Iluminator as usual...
#* ''Position Camera Head, remove lens cap, adjust focus/thresholds etc.'' 

'''<span style="color:red">NOTE: </span> You can view the EyeLink IR lamp via the MSR camera monitor on the wall in the Control Room - helps in checking lamp alignment on participant.'''

<gallery mode="traditional">
Image:EyeLink_Battery_TEST.jpg|EyeLink Battery fully charged
Image:EyeLink_Battery_Charger.jpg|EyeLink Battery Charger
Image:EyeLink_Battery.jpg|EyeLink Battery cable connections / ON-OFF Switch
</gallery>
