# Liquefaction started unexpectedly

**<span style="font-size:large;color:maroon">Problem</span>**

MEG Support was informed that liquefaction started up as preparation was taking place for an afternoon acquisition session.<br />
No warning/information messages were received from the IHR, either by SMS text or email.<br />
Opening the IHR Scheduler, **showed a Measurement Window of 9:00-10:00**, rather than the default 9:00-17:00.

**<span style="font-size:large;color:maroon">Solution</span>**

The IHR Scheduler was opened and the Measurement Window for the day was selected.<br />
Clicking on the "**Default**" button, reverted the Measurement Window to the daily default, so liquefaction stopped. Acquisition then proceeded as normal.

**<span style="font-size:large;color:maroon">Fix</span>**

Measurement Windows are **now being changed to 9:00-10:00 every Sunday**, as suggested by MEGIN. See **[MEG Usage Time](../../meg/troubleshooting/usage_time.md)**

Evidently Monday 19th October was inadvertently set to 9:00-10:00 by mistake.<br />
**Liquefaction could have then started at 10:00, but the IHR decided to wait until approx. 14:30 to power on the Cryocooler**.

Operators should routinely check the Scheduler as part of normal MEG usage, checking that daily (and future) Measurement Windows aren't adversely affected by any increase in Helium pressure in the tanks.

**<span style="color:maroon"> If the Scheduler had been checked when the Operator arrived, the incorrect Measurement Window would have been spotted and reverted back to Default hours.**
