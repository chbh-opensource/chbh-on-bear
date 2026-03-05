# Restart Acquisition

<span style="color:maroon">
**Problem:**<br />
  - SQUID controller (SQC), Signal Acquisition Module (SAM), System Controller (SCC) 
    dropped out during acquisition.<br />
  - SQC, SAM, SCC previously disconnected.<br />
**Solution:**<br />
  - SCC reset (Main Electronics Cabinet, SCC card, Reset button).<br />
  - Restart Acquisition Programs (Neuromag applications, Maintenance folder).<br />
  - Download the latest Tuning file with Tuner (**```Acquisition > Tools > Tuner```**).<br />
**If nothing else helps**<br />
  - Switch off/on the power in the Main Electronics Cabinet (<span style="color:red">**by MEG Support!**</span>).<br />
  - Restart Acquisition Programs (Neuromag applications, Maintenance folder).<br />
  - Download the latest Tuning file with Tuner (**```Acquisition > Tools > Tuner```**).
</span>

### **<span style="color:blue">Resetting the electronics</span>**

The MEGIN TRIUX has four different Digital Signal Processing (**DSP**) electronics boards:

* SQUID controller (SQC) board, used for MEG channels, HPI and Internal Active Shielding.
* Signal acquisition module (SAM) board, used for bioamplifiers, EEG, and analog signal input.
* System controller (SCC) board, a master board for the main electronics.
* Front end controller (FEC) board, used for controlling the preamplifiers.

Each main electronics board has a recessed **Reset** button on its front panel. <br />
If the board becomes locked up (e.g. showing a red <span style="color:red">**Fail**</span> LED, or it is reported by the acquisition sofware (***megacq***) as been dropped from acquisition) press the **Reset** button. <br />
Boot-up of the boards starts automatically. <br />
Wait until the board shows a steady green <span style="color:green">**Run**</span> LED and the <span style="color:red">**Fail**</span> LED is off. <br />
Boot-up takes about 30—60 seconds. <br />
**If the bootup fails, open the back door of the main electronics cabinet and check the indicator LEDs of individual power supplies.** <br /> 

!!! note
    <span style="color:red">**If several boards fail simultaneously**</span>, **all boards can be reset simultaneously** by pressing the **Reset** button of the **System Controller Card** **[[SCC](../../images/meg/SCC.jpg)]**
	which, in our installation, is located 5th slot from the right in the middle rack in the electronics cabinet. Most MEG sites detail this slot with a label/arrow.<br />
	
After resetting the boards, run **Restart Acquisition Programs** by double-clicking its icon in the **Maintenance** toolbox on the acquisition workstation. See the specific **[RAP](rap.md)** page for the full procedure. <br />

The **[SCC](../../images/meg/SCC.jpg)** and FEC boards also have status LEDs for the optical links of the stimulus trigger interface units and MEG and Bio/EEG preamplifiers.
The Link LEDs should be lit <span style="color:green">**green**</span> after resetting the boards.<br />

!!! note 
    Each time the MEG front-end electronics are reset, or powered off/on, they **must** be initialized by invoking the **Restart Acquisition Programs**, a **[RAP](rap.md)**, and **the correct/up-to-date Tuning File must be reloaded**.

### **<span style="color:blue">Restarting the software</span>**

**When to restart**

The data acquisition may under some circumstances either stop prematurely or freeze with the following symptoms:

* ***Megacq*** becomes non-responsive for a long time. When windows covering ***megacq*** are moved, the exposed areas are not repainted.
* When ***megacq*** is started it fails to contact the data server.

The most common reasons for this are **networking problems**.<br />
Recover the system by restarting the acquisition software modules.

If the front-end **DSP** boards hang up, a complete power cycle is ***not*** normally required. It is enough to ...

* Stop/Close the Acquisition program (***megacq***).
* Reset the DPS boards (See the **[Resetting the electronics](restart_acquisition.md/#resetting-the-electronics)** section above).
* Perform a **[RAP](rap.md)**
* Restart the Acquisition program again.
 
The DSP boards are reset by pressing the **Reset** button on the **[SCC](../../images/meg/SCC.jpg)** board panel in the electronics cabinet and waiting until all **DSP** boards boot-up to green <span style="color:green">**Run**</span>-status. <br />
See the **[Resetting the electronics](restart_acquisition.md/#resetting-the-electronics)** section above.

**Procedure to restart the software** (perform a **[RAP](rap.md)**)

1. Stop/Close the Acquisition program (***megacq***).
2. Open the **Maintenance** folder under the **Neuromag** folder in the Desktop’s Applications menu to see the available actions.
3. Select the **Restart Acquisition Programs** icon ("**RAP**").
4. Confirm that you really want to proceed by answering "**Y**" to the question appearing in the **Restart Acquisition Programs** terminal window.
5. Observe the messages in the window during the restarting. 
	- Should the restart operation fail, verify all physical power and data connections, as well as network connections, are working. Then ...
	- Close the terminal window, and try from point #2 again. If successful, then...
6. Wait until the message...<br />
**```Restart complete. Press <Enter> to close the window```**<br />
...appears and press **Enter** on the keyboard.
7. If you had collected data and ***megacq*** ceased to work after you pressed **Stop**, you can rescue your data by double-clicking the **Rescue Data** icon in the **Maintenance** folder.
	- If there is some data to be saved, you will first see a dialog to confirm that you would really like to proceed. Thereafter, a standard ***megacq*** saving dialog will appear. The rescued data will be 
	saved under the project directory called **unknown** if the real project name could not be retrieved.
8. Restart ***megacq*** by selecting the **Acquisition** icon in the **Neuromag** folder.

### **<span style="color:blue">Loading a Tuning File</span>**

**Procedure to load a tuning file, to check sensor noise levels, and to make sure the correct file is loaded after a Console reboot/MEG front-end reset or power off/on.**

1. Start the **Acquisition** program (***megacq***) on the DACQ Console.
2. Select **```Tools > Tuner```** from the menu bar at the top of the **Acquisition** window.
3. Select **```File > Load tunings```** from the menu bar. A dialog window will pop up...<br /><br />
	**```OK to load state file /neuro/dacq/tunings/tnp/He_90.tnp```**<br /><br />
4. If this is the file wanted, click **OK**. Otherwise, click **Load other** to pop up an ordinary file selection box and browse for the file required. 
Click **OK** once the required file to be loaded has been found.
5. Click on the **Measure noise** button, to start a noise check.
6. Look at the generated "**Manhatten Skyline**", warm any sensors that are reaching atypical levels...
	- CTRL + left click on the noisy sensor "building"
	- **```Commands > Heat sensor```**, trace should reduce in height/noise level reduce
	- CTRL + left click to return to the "**all sensor**" view
	- Once happy, click **```Stop measurement```**, followed by **```Stop Collector```**
7. To exit Tuner, select **```File > Exit```**. A dialog window will pop up, select "**Yes**"

!!! Note
	**He_90.tnp** is the default filename expected by **megacq** when the software is started.
	After a completed tuning session, ensure that the new tuning file is saved under this name. A backup copy can then be made by
	selecting **```File > Save Tunings > Save elsewhere```** and chosing a different filename e.g. date of tuning/gantry position.
