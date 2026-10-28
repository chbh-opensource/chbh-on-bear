# IHR Plot Usage

The control daemon runs independently of the plotter script, which only extracts the required data from the log files.<br />
Plotting can therefore be run at any time, plots can be left open, and multiple plot windows opened at the same time.<br />
Offline plotting is also available (with proper configuration of the file locations).

**<span style="color:maroon">Via the IHR PC (Tank Room, G24) - <span style="color:red">not remotely!!</span></span>**

- **Open** a terminal window (click on the **Konsole** Terminal button, lower left of the IHR window), then type ...

	- **megadmin@neptunus-20170801:/> <span style="color:red">cd /neuro/cryo/bin</span>**
	!!! note "The default Terminal window on the IHR now opens to ...<br/> "*megadmin@neptunus-20170801:/opt/neuromag/cryo/bin>*" <br />so the above "cd (change directory)" may not be needed."

``` 
Usage: ./plot <time_span_number_and_unit> [--all] [--temps] [--pressures]
                                          [-- wins] [--purity] [--slopes]
                                          [-- nodecim]
                                          [-- lessdecim] [--moredecim]
                                          [-- from=<yyyyMMdd>]
                                          [-- fullscreen] [--noanno] [--fit]
                                          [-- style=<gnuplot_style_string>]
       where unit can be 'm' for minutes
                         'h' for hours
                         'd' for days
                         'w' for weeks
                         'M' for months
E.g.: ./plot 8h
```

- **<span style="color:red">./plot 7d --gantry</span>**  - plots the tank pressures and gantry position (25, 60 68) for the current week.
- **<span style="color:red">./plot 7d --cycles</span>**  - lists cryocooler state changes and times (85 => turn off, 80 => turn on).
- **<span style="color:red">./plot 7d --wins</span>**  - plots windows (on top are the boil-off times, the same cooler-off times as with cycles).

**The plot command can also be run without changing the directory first e.g. ...**

- **<span style="color:red">/neuro/cryo/bin/./plot 5d --gantry</span>**

!!! note "Time spans longer than 2h will decimate data unless "*-- nodecim*" is used.<br />Time spans shorter than 3h will not fit the regression line properly!"

**The script uses gnuplot for plotting, and zooming is available via the right mouse button.**

**Main gnuplot mouse actions:**

```
   right click corners = select zoom area
         Shift + wheel = scroll x-axis
  Ctrl + Shift + wheel = zoom x-axis
```

**Supported key actions in gnuplot:**

```
left/right arrows scroll display
```

**Regression line fitting also available (for pressure and lHe only).**

**Data or application log files may also be gzipped (.gz suffix), and auto-decompression on-the-fly is supported (with some performance boost usually!).**

!!! note "Varying sampling rates (or decimated log files) is NOT supported properly."

**Description of flags:**

```
        --wins          paints window periods (red) and cryo on periods (blue) 
                        to pressure plot and dewar temp -plot (incl. liq rates and boil rates)
        --slopes        plots momentarily liquefaction/boiling rates 
                        on the pressure plot (in place of dewar pressure)
        --purity        plots the oxygen meter values
        --workgas       plots the cryocooler work gas pressure over time
        --conv          converts RuO ohms to Kelvins for plotting
        --heliumvolume  plots system total helium over time
        --dewar         plots dewar pressure on the 'wins' display (defaults to no with --wins)
        --gantry        plots gantry positions on the 'wins' display


 DEBUG: --cycles       for extracting duty cycle figures from the log files
 DEBUG: --rates        for extracting the adaptive boiling and liquefaction rates
 DEBUG: --debuggas     for plotting work gas pressure over time
 DEBUG: --debugest     for plotting tank pressure estimate over time
 DEBUG: --debugpsw     for plotting pressure switch values

        --keepoutput   indicate names of plot data output files (for external plotting purposes)
        --ratesonly    plots only performance metrics: liquef. rate, boiling rate and MEG window length
        --timebase
```


