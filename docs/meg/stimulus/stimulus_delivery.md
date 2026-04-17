# Stimulus Delivery & Triggering

!!! info
	The Stim PC (**CHBH-ST-MEG-W02**) has no on-board parallel port. <br /> 
	It is utilising a **PCIe(x1) parallel port card** by **Delock**, with the **Oxford Chipset**. <br /> 
	This particular card (**#89219**) been shown to **work well with Presentation, PsychoPy, Psychtoolbox (MATLAB)**

To install, and use, a Delock 89219 PCIe Parallel Port card, see **[Delock Parallel Port Card](../stimulus/delock_pp_card.md)**

### <span style="color:blue">**Parallel Port Connections to MEG hardware**</span>

The **CHBH-ST-MEG-W02** parallel port is connected to the MEG acquisition electronics via the 37-pin multipole connector of **Stimulus Trigger Interface #1 ([STI101](../../images/meg/STI101.jpg))**. No BNC triggers are made from the parallel port.<br />
The **8 data lines** of the **parallel port** are connected to **Trigger Inputs 1-8** ("**In 1**", "**In 2**" etc.) of the **STI101**. Trigger line logic in the MEG is explained below.

!!! Warning "The Stimulus Trigger Interface BNC connectors and the 37-pin multipole connector are *internally connected* together.<br /> **DO NOT** connector the multipole connector if individual triggers via the BNC connectors are to be used."

**<span style="font-size:large">CHBH-ST-MEG-W02 Port memory base address: <span style="color:blue">0xCFF8 (LPT1)</span></span>**

### <span style="color:blue">**Within MATLAB (Psychtoolbox), 64bit**</span>
***<span style="color:maroon">(This has already been done for CHBH-ST-MEG-W02)</span>***

A **C++ extension (mex file)**, created by **Prof. Frank Schieber (Department of Psychology, The University of South Dakota)**, is used to accomplish **very fast port I/O, as a NO COST add-on to MATLAB, using native methods to access low-level hardware**. 
<br />

**Prof. Schieber has since retired**, and his website is down, but **[web.archive.org](https://web.archive.org/)** has a snapshot of it ...

**[Mex-File Utility for Fast MATLAB Port I/O (64-bit)](https://web.archive.org/web/20210903151747/http://apps.usd.edu/coglab/psyc770/IO64.html)**

This **mex-file is named** **[io64.mexw64](../../meg/files/io64.mexw64)**. It **uses a freeware self-installing system driver** named **[inpoutx64.dll](../../meg/files/inpoutx64.dll)**

!!! Note
	**Self-installation of the driver requires that the MATLAB runs with Administrator privileges.  The driver must have been previously installed in order to support non-Administrator users]**.

- **Download** the **io64.mexw64** module and **place it in the relevant stimulus delivery folder (or as necessary in the MATLAB path)**.<br />
**If not** done, then on useage **the following error will be generated ...**

```matlab
>> Undefined function or variable 'io64'
```

- **Download** the **inpoutx64.dll** module and **move it to the C:\Windows\System32 directory** (i.e., This **module must reside in the Windows system PATH**).

!!! Note
	Because the **inpoutx64.dll** was **compiled using Visual Studio**, the **Microsoft Visual C++ 2005 SP1 Redistributable (x64) Package must be installed on the computer**.<br />
	**Use the Control Panel** to see if it is already installed.<br />
	**Open Add and Remove Programs and look for *Microsoft Visual C++ Redistributable***. The installed versions will be listed there.<br/>
	If not, then **[vcredist_x64.exe](../../meg/files/vcredist_x64.exe)** needs to be downloaded and installed (*possibly via Administrator privileges*).

- **Add** the following line to the beginning of the MATLAB script.

```matlab
address = hex2dec('CFF8');    %CHBH-ST-MEG-W02 Stim PC LPT1 output port address
```

- The **following MATLAB command snippet** demonstrates how to use the **io64()** extension:

```matlab
%create an instance of the io64 object
ioObj = io64;
%
% initialize the interface to the inpoutx64 system driver
status = io64(ioObj);
%
% if status = 0, you are now ready to write and read to a hardware port
% let's try sending the value=1 to the parallel port (LPT1)
% address = hex2dec('378');    %standard LPT1 output port address
address = hex2dec('CFF8');     %CHBH-ST-MEG-W02 Stim PC LPT1 output port address
data_out=1;                    %sample data value
io64(ioObj,address,data_out);  %output command
%
% now, let's read that value back into MATLAB
data_in=io64(ioObj,address);
%
% when finished with the io64 object it can be discarded via
% 'clear all', 'clear mex', 'clear io64' or 'clear functions' command.
clear io64;
```

- **The following MATLAB command snippet** demonstrates how to **turn all the CHBH-ST-MEG-W02 Stim PC trigger lines on/off**.
!!! Note "```initialiseParallelPort.m``` MUST be in the relevant stimulus delivery folder."

```matlab
sendTrigger = initialiseParallelPort();

for ii = 0:7
    sendTrigger(power(2, ii));
    WaitSecs(0.2);
end

%% Reset Triggers to 0
sendTrigger(0);
```

**initialiseParallelPort.m**

```matlab
function sendTrigger = initialiseParallelPort()
% sendTrigger = initialiseParallelPort()
%
% Tries to initialise a parallel port using the inpoutx64.dll library.
% Returns the function sendTrigger, which takes a single 8-bit integer
% input and sends it to the parallel port. NB: no input checking is done!
% Make sure you only use values 1-255. Also, the trigger lines are not
% pulled down automatically, you need to do this manually by sending a 0:
%
% sendTrigger(15)  % send trigger 15
% ... do something ... e.g. a Screen('Flip')
% sendTrigger(0)  % pull all lines down
%
% If initialisation fails, returned sendTrigger-function simply prints
% out the input code; useful for developing/testing.

% Revision history:
% - created on 26 Jan 2018, cjb
%
% Copyright 2018 Christopher J. Bailey under the MIT License
%
% Permission is hereby granted, free of charge, to any person obtaining a
% copy of this software and associated documentation files (the
% "Software"), to deal in the Software without restriction, including
% without limitation the rights to use, copy, modify, merge, publish,
% distribute, sublicense, and/or sell copies of the Software, and to
% permit persons to whom the Software is furnished to do so, subject to
% the following conditions:
% 
% The above copyright notice and this permission notice shall be included
% in all copies or substantial portions of the Software.
% 
% THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
% OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
% MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
% IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
% CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
% TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
% SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


try
    % ------------------------------------------------------------------------
    % INITIALIZE PARALLEL PORT
    % ------------------------------------------------------------------------
    % Aarhus: based on InpOut-library, and C:\Windows\System\inpoutx64.dll
    % Aarhus: io64.mex in stimuser's Documents\MATLAB-folder (in path)
    % create an instance of the io64 object
    ioObj = io64;
    % initialize the interface to the inpoutx64 system driver
    status = io64(ioObj);
    % LPT1 memory port address
    % address = hex2dec('DFF8');
    address = hex2dec('CFF8');

    sendTrigger = @(code) io64(ioObj, address, code);
catch  % assume either drivers not found or running on non-stim PC
    fprintf(1, '############################################################\n');
    fprintf(1, 'WARNING: No parallel port access, triggers will not be sent!\n');
    fprintf(1, '############################################################\n');
    sendTrigger = @(code) fprintf(1, 'TRIG %d\n', code);
end
end
```

**<span style="color:blue">With many thanks to Dr. Chris Bailey, Aarhus Univeristy</span>**


### <span style="color:blue">**Trigger logic in MEG data**</span>

**By default**, only **one trigger channel is sampled** with the MEG data: **STI101**. <br />
This channel **contains all possible trigger combinations**, up to a theoretical maximum of over 65000 unique triggers.<br />
When **all trigger lines** are "**down**" (0), **STI101 reads zero**. When:

- A **trigger is sent to input 1**, height(STI101)= **1**
- A **trigger is sent to input 2**, height(STI101)= **2**
- A **trigger is sent to input 1 AND 2**, height(STI101)= **3**

- **Following a binary encoding scheme** in which **input 1 is 2<sup>0</sup>, input 2 is 2<sup>1</sup>, input 3 is 2<sup>2</sup>** and so on.

The following PDF, **[Triggering_through_the_Parallel_Port](../../meg/pdfs/Triggering_through_the_Parallel_Port.pdf)**, was **kindly provided by The Aston Neuroimaging Facility, Aston University**.

In **summary**, the **height of STI101 indicates the value of the trigger signal sent via the parallel port, with most values being encoded by multiple simultaneous trigger signals**.

**If desired, the individual trigger lines (1-16) can also be activated separately**, in which case **0 is no trigger and any positive value is a trigger**.

