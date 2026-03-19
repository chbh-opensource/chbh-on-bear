# HPI Digitisation/Preparation error

=== '''<span style="font-size:large;color:maroon">Problem</span>''' ===

<span style="font-size:medium">On Thursday 16th February, Operators reported seeing the following message pop up when starting Acquisition ...</span>

[[File:Error_message.jpg]]

<span style="font-size:medium">Apparantly the Index file used to save/list HPI digitisations was corrupt. It's possible that a HPI check was stopped halfway through, causing the file to be corrupted as it hadn't finished writing to disk correctly, perhaps during the digitisation of extra points for the fitting of an MRI T1. The Polhemus stylus has previously been reported as problematic when registering points/cHPI coils.</span>

'''<span style="font-size:large;color:maroon">Solution</span>'''

<span style="font-size:medium">The Index file, found in '''/neuro/dacq/prepared''', was deleted. </span>

 <nowiki>[Meguser@sinuhe /]$ cd /neuro/dacq/prepared
[Meguser@sinuhe prepared]$ rm Index</nowiki>

<span style="font-size:medium">Currently, HPI digitisations/preparations are only taken during the current Acquisition session. <br /> Participants aren't prepared a day or more beforehand, nor are the digitisations taken via a separate Workstation in another room. A previously-saved head preparation has never needed to be loaded, so it was safe to remove the Index file. <br /> After deletion, a HPI digitisation was taken using the Phantom, and all was fine. The preparation was saved, Acquisition was exited/restarted, saying 'no' to using the previous existing preparation. The saved preparation was then loaded successfully. <br /> On checking /neuro/dacq/prepared the Index file was found to be recreated, but no more error messages were seen when starting Acquisition.</span>

