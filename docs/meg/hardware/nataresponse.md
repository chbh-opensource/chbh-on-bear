# Recovering responses via NAtA Interface

This '''<span style="color:maroon">MATLAB</span>''' script utilises the Psychtoolbox functions '''KbQueue''' to record the responses of our new 5- and 2-button NAtA Boxes

It uses information taken from ...

'''[ftp://ftp.tuebingen.mpg.de/pub/pub_dahl/stmdev10_D/Matlab6/Toolboxes/Psychtoolbox/PsychDocumentation/KbQueue.html ftp://ftp.tuebingen.mpg.de/pub/pub_dahl/stmdev10_D/Matlab6/Toolboxes/Psychtoolbox/PsychDocumentation/KbQueue.html]'''

and

'''[http://psychtoolbox.org/docs/KbQueueCheck http://psychtoolbox.org/docs/KbQueueCheck]'''


'''<span style="color:blue">NAtA_bbox.m</span>''' can be downloaded '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/NAtA_bbox.m HERE]'''.


'''''(Many thanks to Dr. Tjerk Gutteling / Dagmar Fraser for providing the code).'''''


'''<span style="color:maroon">The NAtA Response Boxes output button presses as Keyboard numbers via USB to the STIM PCs.</span>'''

<span style="color:blue">'''The NAtA Converter box uses the US Keyboard layout'''</span>, and since most modern keyboards have two ways to input a numerical value (standard row of numbered keys, and a number keypad) the correct key 'name' needs to be implemented correctly in your Psychtoolbox code.

'''<span style="color:red">NOTE:</span>''' This 'naming' could also apply to Python/E-Prime/Presentation (''citation needed'').

'''''(Many thanks to Dr. Tjerk Gutteling for pointing this out).'''''


 <nowiki> 5 Button      Keyboard number    [KbName ('xx')];

Left Little            1               1!                
Left Ring              2               2@
Left Middle            3               3#             
Left Index             4               4$
Left Thumb             5               5%

Right Thumb            6               6^           
Right Index            7               7&             
Right Middle           8               8*               
Right Ring             9               9(           
Right Little           0               0)

2 Button       Keyboard number    [KbName ('xx')];
(Could be either hand, left or right)

#1 L                   1               1!          
#1 R                   2               2@

#2 L                   3               3#               
#2 R                   4               4$ </nowiki>


The NAtA Converter Box has TTL outputs to enable recording of button presses in MEG data.

STI channels '''In 9''' to '''In 13''' in the Stimulus cabinet have been connected to '''Data Bit 0''' to '''Data Bit 4''' from the NAtA Converter box. 

These 5 channels provide unique TTL combinations for all 10 buttons, according to the following ...

[[File:NAtA_Button_pinouts.jpg|600px|thumb|left|NAtA Button Box TTL Output Combinations]]

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

Please select the relevant combination of the 5 channels in your '''Acquisition Settings''', '''Channel selection''', to record your participant's responses.


'''<span style="font-size:large;color:blue">NEW! August 2024</span>'''

The Original MEG Converter box has been removed and the original buttons swapped to a new set (buttons swapped again in October 2024), to allow the faulty "RR" button to be repaired or replaced. The '''new buttons are non-sticky''', and '''respond as before, LL => RL, 1 => 0''' <br />Unfortunately, the new Converter box maps the button's parallel port outputs differently to the above, and not all buttons respond with a continuous press.<br />For now, please use the diagram below when deciding which button data bits to select in MEG Acquisition.


[[File:NAtA Button_pinouts_August_2024.jpg]]
