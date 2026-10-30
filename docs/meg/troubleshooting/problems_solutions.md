# Usual Problems, Probable Solutions

== '''<span style="color:red">"Abnormal liquefaction rate" </span>''' ==

- '''''<span style="color:blue">helium level in the storage tanks not decreasing as expected.</span>'''''

== '''<span style="color:red">"Link to DACQ workstation is down" </span>''' ==

- '''''<span style="color:blue">control software cannot send notifications or detect measurement schedule. Liquefaction could start in the middle of a MEG Acquisition.</span>'''''

== '''<span style="color:red">"Error in cryocooler! Recycler is now in fail-safe mode" </span>''' ==

- '''''<span style="color:blue">cryocooler compressor is not operating correctly, it is not safe for the IHR to continue operating. Helium loss will occur if problem persists.</span>'''''

## **<span style="color:red">Any other issues</span>**

### **Abnormal boil-off rate**
 - ***<span style="color:blue">The helium boil-off rate is higher than expected, or abnormally low.</span>***
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Unlikely to happen out-of-hours, only during daily usage.**

The boil-off rate can temporarily rise if the probe unit position is changed repeatedly many times. In this case, the boiling rate typically returns to the normal level within 15-30 minutes.

 - Attend the MEG Lab and query the current Operator about any unnecessary gantry changes.
 - Examine the history plots on the IHR Console to see how the situation has developed re: previous Operator's usage. 
The plots will provide clues - changes in boil-off rate (plotted pressure slope has greater or less angle than normal) - as to possible cause e.g. gantry left at Upright (60), 
rather than being returned to Liquefaction (25) if there are a number of hours between the next acquisition session.
	- **Open** a terminal window (click on the **Konsole** Terminal button, lower left of the IHR window), then type ...
	- **megadmin@neptunus-20170801:/opt/neuromag/cryo/bin> <span style="color:red">./plot 7d --gantry</span>**
	- **gantry angle** plots as **<span style="color:blue">blue squares</span>**, using the right-hand scale for position (25, 60, 68).
	- **Close the plot** and re-run the command with more days, e.g. **<span style="color:red">14d</span>**, to see further back in time.
 - **<span style="color:maroon">Boil-off rate is normal again</span>**, is reported by the IHR once the situation is resolved e.g. gantry moved to 25.
 
### **The recycler is now on battery power**
 - ***<span style="color:blue">The helium recycler cabinet has lost the line power. The UPS keeps the cabinet powered up for 5-30 minutes, but will then run out of battery.</span>***
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Could happen at any time, day or night. Usually just a couple of seconds at most.**

Indicates that the Internal Helium Recycler experienced a temporary loss of mains power, and switched to its backup battery as designed.
This could have been due to brief building power interruption or voltage dip, a momentary interruption to the circuit supplying the recycler, or a brief power supply glitch within the recycler itself.<br />
If it was a single occurrence, then it's most likely just a brief, transient power interruption that the Internal Helium Recycler handled correctly.<br />
If there are no further alarms, the recycler remains in normal operation, and this only happened once, it's usually not cause for concern.

 - Save the resulting IHR email messages, which will note the date and time of the incident. If Estates reports a momentary power dip around the same time, that would explain it.
 - If the pair of messages are seen repeatedly, e.g. several times a day or week, report it to Estates and/or MEGIN, as it could indicate an unstable Tank Room Mains power supply or a developing fault with the recycler's power input or UPS.
 - **<span style="color:maroon">Line power has been restored</span>**, is reported by the IHR once it detects that Mains power has returned indicating the alarm condition has ended, and it has resumed normal operation.