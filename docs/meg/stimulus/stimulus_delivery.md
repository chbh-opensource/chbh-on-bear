# Stimulus Delivery & Triggering

!!! info
	The Stim PC (**CHBH-ST-MEG-W02**) has no on-board parallel port. <br /> 
	It is utilising a **PCIe(x1) parallel port card** by **Delock**, with the **Oxford Chipset**. <br /> 
	This particular card (**#89219**) been shown to **work well with Presentation, PsychoPy, Psychtoolbox (MATLAB)**

To install, and use, a Delock 89219 PCIe Parallel Port card, see **[Delock Parallel Port Card](../stimulus/delock_pp_card.md)**

'''<span style="font-size:xx-large">Triggers</span>'''

'''<span style="font-size:x-large">Parallel port settings</span>'''

The '''MEG STIM PC''' parallel port is connected to the MEG acquisition electronics via the 37-pin multipole connector of '''Stimulus Trigger Interface #1'''. The '''8 data lines''' of the '''parallel port''' are connected to '''Trigger Inputs 1-8''' (''''In 1'''', ''''In 2'''' etc.) of the MEG system. See below for description of trigger line logic in the MEG.

'''<span style="color:red">NOTE:</span>''' ''<span style="color:maroon">The Trigger Interface BNC connectors and the multipole connector are internally connected together. '''DO NOT''' connector the multipole connector simutaneously with the BNC connectors.</span>''

'''<span style="font-size:large">Port address: <span style="color:blue">0xBFF8 (LPT1)</span></span>'''<br />
'''<span style="font-size:large"><span style="color:red">NOTE: December 2022:</span> NEW Stim PC Port address: <span style="color:blue">0xCFF8 (LPT1)</span></span>'''

The parallel port to use for trigger output is LPT1, with the port address <samp>0xBFF8</samp> on the OLD Stim PC, port address <samp>0xCFF8</samp> on the NEW Stim PC.

'''<span style="font-size:x-large">Psychtoolbox</span>

Parallel port interface based on [https://github.com/Psychtoolbox-3/Psychtoolbox-3/wiki/FAQ:-TTL-Triggers-in-Windows '''this page'''], specifically [http://apps.usd.edu/coglab/psyc770/IO64.html '''this link (where usage is also demonstrated)'''].<br />

'''<span style="font-size:large">Usage</span>

* Download the file <samp>io64.mexw64</samp> from the link above ('''<span style="color:maroon">Already done for MEG-STIM-1 and the NEW, CHBH-ST-MEG-W02</span>).
** <samp>io64.mexw64</samp> and <samp>initialiseParallelPort.m</samp> can also be downloaded from our '''[[Audio/Visual Task]]''' page.

* Place the mex-file in the folder with your stimulus delivery script (or elsewhere in your MATLAB path).
** '''<span style="color:red">NOTE: <samp>io64.mexw64</samp> MUST be in your folder/MATLAB path.</span>'''
** If it isn't, you'll get the following error...

 <nowiki>>> Undefined function or variable 'io64'.</nowiki>

* Add the following lines to the beginning of your script.
* '''<span style="color:red">NOTE: Remember to set address to CFF8 if using the NEW Stim - <br /> <samp>address = hex2dec('CFF8');</samp></span>'''

 <nowiki>%create an instance of the io64 object
ioObj = io64;
%
% initialize the interface to the inpoutx64 system driver
status = io64(ioObj);

% LPT1 memory port address
address = hex2dec('BFF8');</nowiki>

* In conjunction with your stimulus (i.e. a 'Flip' of the screen), use the syntax

 <nowiki>io64(ioObj,address,1)  % trigger code from 1 to 255 </nowiki>

* '''You can pull the trigger down to zero to reset as necessary.'''

 <nowiki>io64(ioObj,address,0); %trigger 0 (reset)</nowiki>

* The following MATLAB command snippet demonstrates how to use the io64() extension:

 <nowiki>%create an instance of the io64 object
ioObj = io64;
%
% initialize the interface to the inpoutx64 system driver
status = io64(ioObj);
%
% if status = 0, you are now ready to write and read to a hardware port
% let's try sending the value=1 to the parallel port (LPT1)
address = hex2dec('BFF8');       %CHBH MEG Stim PC LPT1 output port address
data_out=1;                      %sample data value
io64(ioObj,address,data_out);    %output command
%
% now, let's read that value back into MATLAB
data_in=io64(ioObj,address);
%
% when finished with the io64 object it can be discarded via
% 'clear all', 'clear mex', 'clear io64' or 'clear functions' command.</nowiki>

* The following MATLAB command snippet from '''<samp>basicAudioVisualTask.m</samp>''' demonstrates how to turn all our triggers on/off.
** '''<span style="color:red">NOTE: <samp>initialiseParallelPort.m</samp> MUST be in your Paradigm folder.</span>'''

 <nowiki>sendTrigger = intialiseParallelPort();

for ii = 0:7
    sendTrigger(power(2, ii));
    WaitSecs(0.1);
end

%% Reset Triggers to 0
sendTrigger(0);</nowiki>

'''<span style="font-size:x-large">Trigger logic in MEG data</span>

By default, only one trigger channel is sampled with the MEG data: '''STI101'''. <br /> This channel contains all possible trigger combinations, up to a theoretical maximum of over 65000 unique triggers.<br /> When all trigger lines are "down" (0), STI101 reads zero. When:

* A trigger is sent to input 1, height(STI101)=1
* A trigger is sent to input 2, height(STI101)=2
* A trigger is sent to input 1 AND 2, height(STI101)=3
* ...
* Following a binary encoding scheme in which input 1 is 2^0, input 2 is 2^1, input 3 is 2^2 and so on.

''<span style="color:maroon">('''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/Triggering%20through%20the%20Parallel%20Port.docx HERE]''' you will find a useful '''Word''' Docx about "Triggering through the Parallel Port")</span>''.<br />
''(With thanks to the ABC, Aston University).''

In summary, the height of STI101 indicates the value of the trigger signal sent via the parallel port, with most values being encoded by multiple simultaneous trigger signals.

If desired, the individual trigger lines (1-16) can also be activated separately, in which case 0 is no trigger and any positive value is a trigger.

----


'''In response''' to a query about '''bits 15 and 16''', (see '''[[Elekta Response Pads & LabJack U3-LV]]'''), and their impact on the '''composite trigger channel STI101''' when both Interface Units are operating in '''''parallel''''' mode, one of our MEG Trainers had the following to say...

<span style="font-family:Times New Roman;font-size:medium">"The recommended practice would be to use the combined mode (i.e. STI101 represents the inputs of both interfaces) and then mask the bits corresponding to the response buttons before searching for stimulus events. You can do that in the on-line averager event setup by clicking the old and new states of bits 15 and 16 to the ”don’t care” state (denoted by an asterisk in the user interface). The MaxFilter averager will also obey this setting. In Graph you can apply a binary mask to the trigger channel values before extracting the codes. The possibilities in 3rd party analysis software packages vary but at least in MNE and MNE Python such masking is straightforward."</span><br />
Lauri Parkkonen: 27th May 2018.


