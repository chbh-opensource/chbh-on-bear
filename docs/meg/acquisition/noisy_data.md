# Noisy Data

**If Acquired data is noisy during Acquisition, run a quick check to see if the artefacts can be easily removed using *MaxFilter*.<br />Collect ~1min or so of data, save, and then …**

1. Start **MaxFilter**.
	- **```Applications -> Neuromag -> MaxFilter.```**
	- Dismiss the "Welcome" splash screen, click "**Hide**"
2. **```File -> Working directory```**.
	- *Example settings files/.fif files, to try, are shown in ****<span style="color:blue">blue</span>***.
3. In the ***Select a new working directory*** window, type the name of the folder location e.g.
	- ***<span style="color:blue">/data/neuro-data/demo/221003/</span>*** - **<span style="color:red">don’t forget the “/” at the end!</span>**
4. Click “**OK**"
5. **```File -> Load data```**.
6. In the ***Files*** window, select the relevant .fif file e.g.
	- ***<span style="color:blue">watch_on_chair_30_sec.fif</span>***
7. In the ***Maxwell filtering task*** window, select ***Spatiotemporal tSSS***
	- <span style="color:maroon">"*to suppress nearby movement-related artefacts such as metal fillings/a magnetised tooth.*"</span>
8. Click “**OK**”.
9. Click “**Execute**”.
10. **```File -> Exit```**
11. Click “**Yes**”.
12. A file should now have been written to the ***working directory*** location, with the addition of “**_tsss**” to **the name of the .fif** file chosen in ***Step*** 6 above e.g.
	- ***<span style="color:blue">watch_on_chair_30_sec<span style="color:red">_tsss</span>.fif</span>***

!!! Info
	**For more detailed information on usage,<br /> please read pages 21 – 25 from [Guidelines to MEG Data Analysis Software](../../meg/pdfs/NM25775A-B1_DANA_Guidelines.pdf)**


**Compare the *before* and *after* MaxFilter files …</span>**

1. Start **Graph**.
	- **```Applications -> Neuromag -> Graph.```**
	- Dismiss the "Welcome" splash screen, click "**OK**".
2. **```File -> Load settings```**.
	- *Example settings files/.fif files, to try, are shown in ****<span style="color:blue">blue</span>***.
3. In the ***Directories*** window, double-click on the settings required e.g.
	- ***<span style="color:blue">/home/meguser/lisp/setup/local</span>***.
4. In the ***Files*** window, select ***compare.setup***
5. Click “**OK**”  - ***two synchronised Windows will appear.***
6. In the **top Window**, **```File -> Open Diskfile```**
7. In the ***Directories*** window, double-click ***/neuro/data/sinuhe***
8. In the next ***Directories*** window (*left-click on the RH window edge and drag to open the window wider if necessary*), scroll down and double-click on the Project e.g.
	- ***<span style="color:blue">/neuro/data/sinuhe/demo</span>***
9. In the next ***Directories*** window (*left-click on the RH window edge and drag to open the window wider if necessary*), scroll down and double-click on any relevant sub-directory e.g.
	 - ***<span style="color:blue">/neuro/data/sinuhe/demo/221003</span>***
10. In the ***Select disk file to open*** window, chose the **unfiltered** .fif file e.g.
	 - ***<span style="color:blue">watch_on_chair_30_sec.fif</span>***
11. Click “**OK**".
12. In the **top Window**, **```Displays -> Control Panel```**
13. **Open the filtered** .fif file by double-clicking the widget "**File2**" (*usually to be found bottom left of the Control Panel window*).
14. Repeat from ***Step 7*** to ***Step 10*** to select the "**… _tsss.fif**" file e.g.
	- ***<span style="color:blue">watch_on_chair_30_sec<span style="color:red">_tsss</span>.fif</span>***
15. Click “**OK**"
16. **[View](../../images/meg/Before_After_MaxFilter_watch_on_chair.jpg)** the **effect of *MaxFilter* on the original noisy** .fif file (*lower window/display2*).
17. In the **top Window**, "**Exit**", "**Exit**", "**Yes**", when finished.

!!! Info
	**For more detailed information on usage,<br /> please read from page 57 onwards, as necessary, from [Guidelines to MEG Data Analysis Software](../../meg/pdfs/NM25775A-B1_DANA_Guidelines.pdf)**

