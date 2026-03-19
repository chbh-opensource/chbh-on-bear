# Gantry Position not detected

=== Problem ===

After the gantry was unintentionally moved beyond FU (68 degrees) the '''Acquisition''' program failed to detect the gantry position.<br />
Gantry position detection failure may also occur if the DACQ Console ("Sinuhe") has been rebooted.

 <nowiki> CHANGE: Gantry position: Detected: illegal value(0), Manual:Supine(0)</nowiki>

'''<span style="color:maroon">Summer 2019</span>'''<br />
Before proceeding further, check first that the '''MSR traffic light''' is showing '''<span style="color:green">green</span>''' in the "in use"  position you're wanting to use e.g. 60 (The '''60 position sensor''' may need '''adjusting''' during our first Service next year).
* If it isn't showing '''<span style="color:green">green</span>''', adjust the '''up/down''' buttons until it does, then check to see if the position is now recognized in '''Acquisition'''. If not ...

=== Solution/s ===

1. Perform a '''soft boot/reset of the electronics'''. '''<span style="color:red">(press the [https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/SCC.jpg[SCC]]board Reset button in the electronics cabinet).</span>'''
* [[RESTART_ACQUISITION#Resetting_the_electronics]]
2. Perform a '''Restart Acquisition Programs''' ('''[[RAP]]''').
* [[RESTART_ACQUISITION#Restarting_the_software]]
3. Start the '''Acquisition''' program.<br />
4. Hopefully the gantry position should now show ...

 <nowiki> CHANGE: Gantry position: Detected: Upright(60)</nowiki>

5. Repeat from Step 1. if the gantry position is still failing to be detected.

6. Once detected correctly, check sensor noise levels if necessary.
* [[RESTART_ACQUISITION#Loading_a_Tuning_File]]



or

* '''Power cycle the gantry lifting motor'''.
*: The motor is plugged into a 13amp mains socket located behind the MSR, as shown '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/GantryLiftingMotorSocket.jpg[here]].'''
* Switch off the socket that is housing the ''''Black'''' plug with the ''''<span style="color:grey>grey</span>'''' power lead.
* Wait a few moments, then switch back on.<br />
* May then still require a '''soft boot/[[RAP]]''' (as above).

<span style="color:red>'''NOTE:'''</span> ''You can tell if you've switched off the correct socket as the 'traffic light' in the MSR will not be lit. <br /> (The other plug powers the Oxygen level monitor - '''<span style="color:blue> which has now been removed (November 2020)</span>''').''


* As a last resort, trying '''Powering down''' then '''Restarting the electronics'''. <span style="color:red"> (MEG Support Officer to do this).</span> 
** [[POWER_DOWN_EQUIPMENT#Powering_Down_the_Main_Electronics_Cabinet_.28T2.29]] (but not the UPS!)
** [[POWER_UP_EQUIPMENT#Powering_Up_the_Main_Electronics_Cabinet_.28T2.29]]
* Then '''[[RAP]]/ Acquisition''' etc.


* If gantry is still not detected, contact MEGIN Support.


<span style="color:red">'''NOTE:'''</span> '''''<span style="color:blue"> If the gantry position is not detected during an Acquisition, you will still be able to acquire data. Enter the position manually for now (chose the correct position value from the menu provided).</span>'''''
