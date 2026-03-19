# STI101 AC Adapter Outage

'''<span style="font-size:large;color:maroon">Problem</span>'''<br />
<big>
An issue was reported (24th June 2025) that '''''megacq''''' had suddenly stopped receiving triggers. Triggers had been previously recorded that session, but after a new PRESENTATION paradigm was started, no triggers were observed. '''No trigger LEDS were observed lighting up <span style="color:green">GREEN</span> on STI101'''.


'''<span style="font-size:large;color:maroon">Fix</span>'''<br />
The AC Adapter, powering the trigger interface STI101, '''was found to be off''' (the '''<span style="color:green">GREEN</span>''' power LED '''wasn't lit''').<br /> Powering off its Mains socket for a few seconds, then switching back on, repowered the AC Adapter, and triggers were again observed in '''''megacq'''''.


'''<span style="font-size:large;color:maroon">Solution</span>'''<br />
No other UPS-protected sockets appeared to be affected, so hopefully this was just a one-off occurrence. <br />
Operators are now, as part of their setup procedure moving forward, to '''check that the AC Adapter power-on LED is showing <span style="color:green">GREEN</span>'''.


[[File:ACAdapter.png]]


A '''"TRIGGER_TEST" batch file''' has also been created to '''test whether the triggers are being generated correctly, and show on STI101'''.<br />

Double-clicking the batch file will ...<br />
* Start a new instance of MATLAB (won't interfere with any MATLAB already open).
* Run a check/test, twice, that all 8 triggers work (the '''<span style="color:green">GREEN</span> LEDs on STI101 In 1 => In 8 switch on then off in sequence''').
* Then exit MATLAB gracefully.


