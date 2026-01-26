# Using EEG with MEG

<big>
'''<span style="color:blue">We have the 64 Channel EEG system, use BrainCap EEG easycaps specifically designed for our TRIUX system, purchased from Brain Products UK, and have 6 caps available in 4 different sizes. The caps use the 10/20 system of electrode placement.</span>'''


* '''1 x 54cm, 2 x 56cm, 2 x 58cm, 1 x 60cm'''


A PDF copy of our 64Ch BrainCap easycap electrode layout, channel assignment, etc, can be found here - '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/CHBH_BC-MEG-64-X10.pdf 64Ch BrainCap-MEG for Triux]'''

The Table of Coordinates from the above can be found here - '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/CHBH_BC-MEG-64-X10_Coordinates.pdf BrainCap electrode coordinates]'''</big>

== Digitisation ==

<big>
To ''' digitise the 64 electrodes''', follow the '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/MEGIN_64Channel_EEG_Instructions_for_Digitisation.pdf Instructions for Digitisation]''' copied from MEGIN's '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/NM24405A-B_Triux_EEG_Cap.pdf EEG Cap User's Manual]''' .

Our BrainCaps should follow the layout of the MEGIN caps, '''<span style="color:blue">but be wary of the extra EOG electrodes built into the BrainCaps</span>''' (See the 64 BrainCap-MEG layout above).<br />
To '''help in digitisation''', three pages have been copied from MEGIN's EEG Cap User's manual above ...

* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/MEGIN_64Channel_EEG_Locations_and_Channel_Numbers.pdf[Electrode Locations and Channel Numbers]]''' 

* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/MEGIN_64Channel_EEG_Layout_original.pdf[Electrode layout (original)]]''' '''Figure A.2'''

* '''[https://www.chbh.bham.ac.uk/wiki/buic-files/MEG/MEGIN_64Channel_EEG_Layout_new.pdf[Electrode layout (new)]]''' - '''<span style="color:maroon">''Many thanks to Malgorzata "Gosia" Wislowska''.</span>'''

'''She says ...'''

"''I exchanged numbers of green electrodes so that they go from 1-32 instead of 33-64.<br />''
''This new numbering is compatible with electrode numbering on SIGGI device.<br />''
''So one can save a little bit of grey matter energy and skip subtracting number 32 when checking the impedances.<br />''

''We should however not get rid of the old layout, which in turn is compatible with electrode numbering in the acquisition software (numbers going from 1 to 64).''"
</big>

== Procedure ==

<big>
'''<span style="color:blue">Not many MEG Operators have undertaken EEG & MEG, but those that have used the following procedure/digitisation order:</span>'''<br />
('''''<span style="color:maroon">Many thanks to Oscar Ferrante & Tara Ghafari @2020</span>''''')

* Attach BIO electrodes.
* Attach EEG cap.
* Attach HPI coils on EEG cap (''possibly using the BrainCap built-in HPI coil holders?'').
* Gel EEG cap (see '''[[Correct Positioning/Usage of EEG Caps]]''').
* Digitise fiducial points.
* Digitise HPI coils.
* Digitise the 64 electrodes 
** Use the SIGGI multimeter to measure electrode impedance ('''[[Correct_Positioning/Usage_of_EEG_Caps#Check_impedances]]''').
* Digitise the head shape. '''<span style="color:red">Take care not to damage the coils/break any electrode wiring!</span>'''

('''They used the MEGIN caps''')<br />
"''We attached the HPI coils to the MEGIN cap because that way we could easily reach them during digitization.<br /> If they are placed on the head (as in normal usage), this needs to be done so that the Polhemus pointer can reach them under the EEG cap with a perpendicular orientation - it needs to be very well thought out.''"

'''When queried if it was possible to digitize the head shape ''before'' the 64 electrodes ...'''<br />
"''I’m not sure it’s possible to digitize the head shape before doing it for the EEG electrodes in the MEGIN software.<br /> If so, it’s worth a try. But the HPI coils would then need to be attached to the head, adding the problems mentioned above.<br /> Doing the head shape digitization once the cap is in place is not perfect as it introduces some noise, which can make the coregistration less accurate.<br /> It’s a trade-off. In our analysis (i.e., visual response in posterior and prefrontal areas), this extra noise did not have a strong impact, but I guess it depends on the specific experimental question.''"


'''<span style="color:red">NOTE: @2025:</span>''' Coen & Helena found that using the BIO GND electrode (which they're using for EMG recording), rather than the BrainCap GND electrode, produced better signal quality overall when plugged into the gantry side panel. <br />The side panel REF connection was made using the BrainCap REF electrode (no BIO REF electrode was attached to the participant).
</big>




