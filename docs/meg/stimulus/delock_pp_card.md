# Delock Parallel Port Card

***<span style="color:maroon">(This has already done for CHBH-ST-MEG-W02)</span>***

### <span style="color:blue">**Presentation**</span>

Once the card is installed in a PCIe x1 slot, boot the computer.

- Open **```Device Manager```**
- Find the **```Ports (COM & LPT)```**, open sub-menu.
- **```Printer Port (LPT1)```**, right click.
- **```Update Driver Software...```**
- **Point Windows** to the location of the contents of the **<span style="color:maroon"> Delock driver installation CD</span>** and it should find the **Oxford Chipset** drivers. <br /> 
**Copies of the driver** (and other required files) can also **be found on the Stim LOCAL (L:\) drive**, in a directory  called **Drivers**
	- The LPT port should get relabelled as **PCI Express ECP Parallel Port (LPT1)**.

On starting, Presentation should detect the card as an LPT-port, and be able to send triggers.

Under **```Device Manager```**, right-click on the LPT port.

- Select **```Properties```**, **```Change settings```**, **```Port Settings```** (*may require an* ***Admin*** *account*).
	- Change the port number to **```LPT1```** (for convenience) (***may already be set to LPT1***).
- Select **```Properties```**, **```Resources```**.
	- Shows the **physical port address** of the card.
		- In **64-bit Windows**, this will be something like **<span style="font-size:medium;color:maroon">0xCFF8</span>**
		- The **physical address is needed for *PsychoPy***.

### <span style="color:blue">**PsychoPy**</span>

For PsychoPy, some drivers are still needed as described at ...

-  **[http://www.highrez.co.uk/Downloads/InpOut32/default.htm](https://www.highrez.co.uk/Downloads/InpOut32/default.htm)** 
	- Select **[https://www.highrez.co.uk/scripts/download.asp?package=InpOutBinaries](https://www.highrez.co.uk/scripts/download.asp?package=InpOutBinaries)** to download the ZIP file
	- **Extract**, and then run **<span style="color:maroon">InstallDriver.exe</span>** from the **```Win32```** sub-directory .

**The reason is PsychoPy is still a 32-bit application**.

Running the **<span style="color:maroon">InstallDriver.exe</span>** application (*as instructed on the webpage*) only **installs 64-bit libs**, whereas the 32-bit version is still required for PsychoPy. Therefore ...

- **Extract** the archive.
- Copy the file **<span style="color:maroon">Win32/inpout32.dll</span>** ...
- ... to **<span style="color:maroon">C:\Windows\SysWOW64</span>**

### <span style="color:blue">**Psychtoolbox (64bit Matlab)**</span>

The same **InpOut Binaries** (**[http://www.highrez.co.uk/Downloads/InpOut32/default.htm](https://www.highrez.co.uk/Downloads/InpOut32/default.htm)** are used here (64-bit).

Running the **<span style="color:maroon">InstallDriver.exe</span>** application (*as instructed on the webpage*) only **installs 64-bit drivers, not the DLL**, which will have to be copied in manually.

- **Extract** the archive.
- Copy the file **<span style="color:maroon">x64/inpoutx64.dll</span>** ...
- ... to **<span style="color:maroon">C:\Windows\System32</span>**
