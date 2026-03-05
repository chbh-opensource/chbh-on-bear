# Audio Delay Testing

**Tie-Clip microphones are available** to help **measure the audio delay from a sound being triggered** to **hitting the participant's ear or ears**.

**Two are identical** and were purchased (October 2022), and the **third is the original one provided during MEG training** (February/March 2018).

**<span style="color:maroon">Specifications</span>**


| 			     |  Original  |  2 x New  |
| -------------  |  -------  |  ------  |
| **Transducer Principle**  |  Condenser  |  Condenser  |
| **Frequency Response**  |  20 - 16000 Hz  |  50 - 18000 Hz  |
| **Pickup Pattern**  |  Omnidirectional  |  Omnidirectional  |
| **Sensitivity**  |  -64dB +/- 3dB  |  -62dB  |
| **Impedance**  |  1 k&Omega;  |  1 k&Omega;  |
| **Battery Power**  |  1.5V DC, "AAA"  |  1.5V DC, LR-44 Button  |
| **Output Connector**  |  6.35mm / &#188;" mono Plug  |  6.35mm / &#188;" mono Plug  |
| **Microphone Connection/lead length**  |  3.5mm mono Plug, 4M  |  3.5mm mono Plug, 4M  |

- **Connect** Stim PC or the PROPixx Controller (DATAPixx) audio output, to whichever sound system is being tested - **[MEG Audio Connections](../../meg/pdfs/MEG_Audio_Connections.pdf)**
- **Decide** which microphone/s to use and insert the relevant battery. **Remove battery after use** (*plastic forceps available to help remove LR-44 battery from new microphone/s*). 

!!! info
	- If using two microphones, best to not mix the Original and New microphones - to avoid possible inconsistencies - see **Specifications** above.
	- New microphone/s require/s microswitch on microphone case to be switched **ON**.

- **Uncoil** the microphone cable/s and lay it/them out neatly/safely on Control Room floor, to **avoid tripping use the provided Cable Protection Cover Mat**.<br /> **Insert** the 3.5mm mono Plug/s into the microphone case/s.
- **Insert** the &#188;" mono Plugs attached to the microphone case/s to the relevant &#188;" socket-to-socket adapter/s.<br /> The **socket adapter/s** should **already be attached** to the correct &#188;" Plug-to-BNC cable/s already connected to the MISC input box.
	 - Check **[MISC Channels](misc_channels.md)** for the **correct** BNC connection/s to use on the MISC Input Box.
		- ***Microphone Input - Left Response - MISC #8***
		- ***Microphone Input - Right Response - MISC #9***
- **Carefully** push the microphone/s (*minus the Tie Clips*) **halfway** into the provided small piece/s of **silicone tubing**.
- **Roll up the relevant eartip/s** and **push** into the **opposite end/s of the tubing**.
	- **<span style="color:maroon">NATUS:</span>**
		- Attach the Natus cabling to the gantry side panel as usual.<br /> Lay out the Transducers on the gantry chair, on the floor, or on a chair outside the MSR.<br /> Attach the microphone/s + eartip/s to the Left or Right, or both, Transducer/s as required.
	- **<span style="color:maroon">SOUNDPixx:</span>** 
		- Unravel the clear SOUNDPixx tubing from the MSR shelving.<br /> Attach the black Participant tubing correctly.<br /> Attach the microphone/s + eartip/s to the Left or Right, or both, red-coiled connector/s as required.

!!! Note "If only listening from one audio channel, to avoid possible spurious noise being picked up attach the relevant "squashed"/blocked eartip to whichever audio channel not recording from."

!!! note "<span style="color:red">Don't close the MSR door, or don't close it fully, to avoid cutting cable!</span>"

- In **Acquisition Settings**, select the relevant **[MISC Channels](misc_channels.md)** as well as the trigger channels associated with the audio test stimulus.

!!! note "<span style="color:blue">To reduce the resulting file size, turn off the MEG channels.<br />Increase the "Sample freq (Hz)" to *3000* or *4000* to increase file resolution (more points) to make subsequent cursor line start point selection easier/more defined.</span>"

- Press "**GO**", "**Record**", and start audio test stimulus.

- <span style="color:maroon">**Recording** the triggers, the audio output/s (*used for reference, and should be almost instantaneous but delays may be due to how the test sound is being generated in PTB*), and the microphone output/s - **should now show the audio delay between the sound-onset trigger and the microphone response**.</span>
- **Save** the resultant .FIF file and **read** into **Graph** to **find the delay/s**.

<big>
**To check the delay using "Graph"**
</big>

1. Start **Graph**.
	- **```Applications -> Neuromag -> Graph.```**
	- Dismiss the "Welcome" splash screen, click "**OK**".
2. **```File -> Load settings```**.
	- *Example settings files/.fif files, to try, are shown in ****<span style="color:blue">blue</span>***.
3. In the ***Directories*** window, double-click on the settings required e.g.
	- ***<span style="color:blue">/home/meguser/lisp/setup/examples</span>***.
4. In the ***Files*** window, select ***basic.setup***.
5. Click "**OK**".
6. **```File -> Open Diskfile```**.
7. In the ***Directories*** window, double-click ***/neuro/data/sinuhe***.
8. In the next ***Directories*** window (*left-click on the RH window edge and drag to open the window wider if necessary*), scroll down and double-click on the Project e.g.
	 - ***<span style="color:blue">/neuro/data/sinuhe/demo</span>***.
9. In the next ***Directories*** window (*left-click on the RH window edge and drag to open the window wider if necessary*), scroll down and double-click on the relevant sub-directory e.g.
	 - ***<span style="color:blue">/neuro/data/sinuhe/demo/221013</span>***.
10. In the ***Select disk file to open*** window, chose the ***.fif*** file to view e.g.
	- ***<span style="color:blue">Hyojin_audio_test_code_new_Stim.fif</span>***.
11. Click "**OK**".
12. **Graph** will respond with "**No data available**" - *if the MEG Channels were turned off during data collection to reduce file size*.
13. **```Displays -> Control Panel```**.
14. **Double-click** the widget labelled "**Stim**" to add in the **MISC** and **STI** channels used during the Acquisition.
15. In the "**Common to widgets**", "**names**" window, type in each channel name, in **<span style="color:red">CAPITAL</span>** letters, one channel per line, pressing the **Return** key after each entry e.g.<br />
**<span style="color:maroon">MISC 6<br />MISC 7<br />MISC 8<br />STI 2<span>**
16. Click "**Apply**", “**OK**”
17. **Right-click** on the "**Stim**" widget, and drag/draw a line to the "**display**" widget.<br /> **Release the mouse button**.
18. The **four channels** should now appear.
19. In the "**Start & length**" window, type a reasonable value in the "**length**" (lower) box, e.g. **10**
20. **Left-click** on each channel in turn (channel turns "**white**"). Click on **Autoscale** for both "**Scale**" and "**Offset**".
21. **Adjust** the bottom slider to **choose the best** section to measure.
22. **Right-click** on a position near e.g. **the STI trigger** and **drag right** to open a section to view (selected section turns "**white**").
23. **```Displays -> zoom in```**
24. **Repeat as necessary** from ***Step 22***.
25. **Once happy** with the zoomed view...
26. "**Shift + right-click**" on a channel at a **relevant starting point** e.g. the **start of the STI trigger**.<br /> A **vertical white line is displayed**, along with a **cursor box** showing the **Port number** and **which channel selected** e.g. one from ...<br />
**<span style="color:maroon">Port: 0 MISC006<br />Port: 1 MISC007<br />Port: 2 MISC008<br />Port: 3 STI002</span>**<br /> 
and the "**X**" and "**Y**" **axis values** at the point selected e.g. **X: 13.688** (***Time scale in Seconds to 3 decimal places***).
27. **Make a note** of this "**X**" time value.
28. **Release the "Shift" key** and whilst **still right-clicking**, **drag the mouse to the right** to the **start** of the **desired time-delayed channel e.g. the microphone response**.<br /> **Move** the line to the **start of the response** and **note the time** e.g. **X: 13.711**.
29. The **time difference** is the **delay (in msec)** from **trigger onset to microphone response**<br /> e.g. in this example, ***23msec***. 
30. **Repeat as necessary from** ***Step 21*** to **take more readings** from **different triggers/different sections** of the file, to **ensure a reliable/repeatable value is collected for the delay**.
31.  “**Exit**”, “**Exit**”, “**Yes**” when finished.
