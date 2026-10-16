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
#### Powering Down the Main Electronics Cabinet (T2)

<span style="color:red">'''NOTE:'''</span> ''The Main Electronics Cabinet (T2) is protected by a UPS ('''UPS21''').''

The [https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/DSP_Electronics.jpg '''Power Control'''] of the Main Electronics Cabinet has three switches. These '''MUST''' be powered off in the correct sequence.

* '''Main switch''' (''with no-mains release''). '''(Switch 1)''' <br />
* '''Main (DSP) Electronics''' (''MEG & Bioamplifier/EEG'') <span style="color:green">'''green'''</span> rocker switch. '''(Switch 2)''' <br />
* '''Preamplfiers''' (''MEG & Bioamplifier/EEG'') <span style="color:green">'''green'''</span> rocker switch. '''(Switch 3)'''

''' Procedure '''

# '''Switch off''' the '''Preamplifiers (3)''' rocker switch first, followed by the '''Main Electronics rocker switch (2)''' from the mains control panel.
# Turn the '''Main switch (1)''' on the Mains Control Panel to '''Off''' position. This will turn off the ethernet switch, the Watchguard Firewall, the UoB Switch, the roof fans and eventual equipment connected to the auxiliary sockets, e.g. the optional intercom.
#: '''NOTE:''' ''It may take a while before the LED indicators go off. A main electronic power supply unit will not restart before all indicators are off.''
# Power off the Eaton UPS, labelled "'''UPS21'''" - '''<span style="color:red">On the floor, at back of IHR Tank Room</span>'''
#* '''Turn off''' the equipment that is connected to the UPS (''see above'').
#* Press and hold the '''On/Off''' button on the front panel for approximately three seconds. <br /> The UPS starts to beep and shows a status of “'''UPS off pending…'''” <br /> The UPS transfers to Standby mode (if utility power is available) and removes power to the equipment. The green Power On LED turns off.
#* '''Switch off''' the mains socket powering the UPS.

<br />
#### Powering Down the contents of the STIM Cabinet (T1)

# '''Turn off''' equipment in the STIM Cabinet (T1) e.g. Digitimer Stimulator, via their power buttons/switches.
# '''Switch off''' the filtered powerbar (green rocker switch).
#* This will power down the MSR Patient Camera/IR Light.

<br />
#### Powering Down DACQ & Participant Logging Computer (PLC)
<span style="color:red">'''NOTE:'''</span>  ''Both the DACQ, it's Speakers, and the PLC are plugged into double power sockets protected by a UPS ('''UPS20''').''

''' Powering Down the DACQ Console "''Sinuhe''" '''
# ''From Login Screen''.
#* Bottom right corner, left mouse click, select "'''Shut Down'''".
# ''If logged In''
#* Exit Acquisition program, close Terminal windows etc.
#* Bottom left corner, left click.
#* Hover over "'''Leave'''", select "'''Shutdown'''".
# '''Power off''' Monitor and Speakers.
# '''Switch off''' the mains socket powering the DACQ.

''' Powering Down the Participant Logging Computer (PLC)'''

# '''Press''' the power button on the front of the PC.
# '''Power off''' the Monitor.
# '''Switch off''' the mains sockets powering the PC and Monitor.

''' Power off the associated Eaton UPS, labelled "UPS20" ''' - '''<span style="color:red">On the floor, at back of IHR Tank Room</span>'''.

# '''Turn off''' the equipment that is connected to the UPS (''see above'').
# '''Press''' and hold the '''Off''' button on the front panel for approximately three seconds. <br /> The UPS starts to beep and shows a status of “'''UPS off pending…'''” <br /> The UPS transfers to Standby mode (if utility power is available) and removes power to the equipment. The green Power On LED turns off.
# '''Switch off''' the mains socket powering the UPS.

<br />
#### Powering Down the MEG-STIM-01 and CHBH-ST-MEG-W02 PCs

# '''Shutdown the PCs''' as you would normally ('''Windows 10''').
# Switch off the '''Monitor'''
# Switch off the '''PROPixx Controller'''.
# ''(Switch off '''SOUNDPixx Controller''' and '''PC Speakers''' if used)''
# Switch off the attached 8-way bar plug powering the KVM and network mini hub.
# Shut down both '''APC Back-UPS 1400s.'''
#* Press and hold the POWER button for at least 2 seconds. At the first beep, release the button and the UPS will turn off. A 2-second delay has been added to mitigate unintentional contact with the POWER button.
#* '''''<span style="color:red">NOTE:</span>''' Make sure '''other equipment''' e.g. PROPixx Projector, EyeLink PC, '''is powered off BEFORE switching off ''' the APCs.''
# Switch off the '''mains sockets''' powering the '''APCs'''.
#* '''''NOTE:''' Mains sockets can be left '''switched on''' during normal, daily usage.''
#* '''''NOTE:''' Only switch off '''in emergency''', or if equipment is being moved.''

<br />
#### Powering Down the EyeLink 1000 Plus PC

# After Data Acquisition etc., click/select "'''Exit EyeLink'''" on Host PC.
#* Or click/select "'''Shutdown Host'''", click/select "'''YES'''" <span style="font-size:large">&rarr;</span> Point 3.
# Click red "'''<span style="color:red">Shutdown</span>'''" button.
# Turn off '''Monitor'''.
# '''Turn off EyeLink battery''', unplug power cables from battery and FO Camera Head/IR Illuminator.
# Replace lens cap, '''move FO Camera Head/IR Illuminator''' back to MSR white cabinet, carefully tidy up '''<span style="color:orange">orange</span>''' FO lead and place in cabinet.
# '''Remove EyeLink battery''' from MSR and '''put battery on charge''' ''(if able to)''.
#* '''Unplug''' battery once fully charged. '''Do not''' leave attached to the charger.
# '''Switch off bar plug on table''' by EyeLink Host PC
#* This ensures the ''actual'' '''EyeLink camera is powered down'''.
# Shut down both '''APC Back-UPS 1400s.'''
#* Press and hold the POWER button for at least 2 seconds. At the first beep, release the button and the UPS will turn off. A 2-second delay has been added to mitigate unintentional contact with the POWER button.
#* '''''<span style="color:red">NOTE:</span>''' Make sure '''other equipment''' e.g. PROPixx Projector, EyeLink PC, '''is powered off BEFORE switching off ''' the APCs.''
# Switch off the '''mains sockets''' powering the '''APCs'''.
#* '''''NOTE:''' Mains sockets can be left '''switched on''' during normal, daily usage.''
#* '''''NOTE:''' Only switch off '''in emergency''', or if equipment is being moved.''

