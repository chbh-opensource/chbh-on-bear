# MEG Usage time

'' <span style="color:maroon">To see much MEG usage time you can obtain…</span>'''

* '''Open''' a terminal window (click on the “'''Command Line'''“ button, lower left of the IHR window), then type ...
** ''' <span style="color:red">cd /neuro/cryo/bin</span>'''
** ''' <span style="color:red">./plot 7d --cycles</span>'''  - lists cryocooler state changes and times (85=> turn off, 80=> turn on)
** ''' <span style="color:red">./plot 7d --wins</span>'''  - plots windows (on top are the boil-of times, the same cooler off times as with cycles.

'''See [[IHR Plot usage]] for other uses of the ''plot'' command.'''

<gallery widths=440x heights=220px>
Image:Cycles.png|IHR Cycles
</gallery>

* As the tanks get only half full during the day (~5bar), some extra capacity is achievable by letting the tank pressure accumulate Mon - Fri, so that the cryocooler can liquefy the full tanks over the weekend (or Sunday).

* The extra capacity varies 1-2.5 hr/day, depending on the gantry position and cold head performance.

''' <span style="color:maroon">What to set the Scheduler to, if acquisition not taking place e.g. Sundays.</span>'''

''“Instead of using those ‘None’ windows, nowadays we recommend to set the windows to their '''<span style="color:blue">minimum length of 1 hour</span>'''. The reason is that if you have multiple None days in a row, the system lets the tanks accumulate until 9 bars before starting to liquefy. Then if it happens that someone would happen to need the system earlier than expected, the tanks might get overfilled before the unexpected measurement finishes.”''

'''Antti Teliö, 09/01/2020'''


