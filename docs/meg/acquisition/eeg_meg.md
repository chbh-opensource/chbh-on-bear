# Using EEG with MEG


**<span style="color:blue">We have a 64 Channel EEG system, use EASYCAPs specifically designed for our TRIUX system, purchased from Brain Products UK, and have 6 caps available in 4 different sizes. 
The caps use the 10/20 system of electrode placement.</span>**

- **1 x 54cm, 2 x 56cm, 2 x 58cm, 1 x 60cm**

**[64Ch BrainCap-MEG for Triux - Electrode Layout/Channel Assignment](../../meg/pdfs/CHBH_BC-MEG-64-X10.pdf)**

**[64Ch BrainCap-MEG for Triux - Table of Coordinates](../../meg/pdfs/CHBH_BC-MEG-64-X10_Coordinates.pdf)**

## Digitisation

To **digitise the 64 electrodes**, follow the **[Instructions for Digitisation](../../meg/pdfs/MEGIN_64Channel_EEG_Instructions_for_Digitisation.pdf)** copied from MEGIN's **[EEG Cap User's Manual](../../meg/pdfs/NM24405A-B_Triux_EEG_Cap.pdf)**<br />
**The EASYCAP layout closely follows** the MEGIN caps, **<span style="color:blue">but there are some differences in electrode usage (EASYCAPs have T9 & T10, but no PO5 & PO6) , and when certain electrodes are digitised, and be wary of the extra EOG electrodes built into the EASYCAPs</span>** <br />
- ***See the 64 BrainCap-MEG electrode layout above.***

!!! Note "**<span style="color:red">NOTE: </span>** One additional important difference between the two systems: the channel numbering (*channel index mapping*) is not the same.<br />For example, <span style="color:blue">channel Fpz</span> ...<br /> - Is registered as <span style="color:blue">EEG020 for the MEGIN caps</span>, whereas it is ...<br />- <span style="color:blue">EEG002 for the EASYCAP</span>.<br />(*The data is recorded as EEG001, EEG002, etc., rather than as Fp1, Fp2, and so on*)." 


#### **<span style="color:maroon">If using EASYCAPs ...</span>**

The **eeg_digit_maps** file in **```/neuro/dacq/setup```** has been edited to **create a new layout to help digitise the EASYCAPs**.

- Select **all EEG channels** in **```megacq```** (click the **```EEG on```** button). 
- After **Coordinate frame alignment** and **HPI Coils** digitisation, select **```EEG EasyCap 64```** from the dropdown sub-menu, then click on **```EEG ecectrodes```** to start digitising each electrode. 
	- The **REF** electrode is **always the first one to digitise** ("**0**").

The **new digitisation order** (taken from *eeg_digit_maps*) is as follows ...

```
# A map for 64-channel EASYCAP (05/02/2026 - JLW & CZ)
EEG EasyCap 64:0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15:16:17:19:20:21:22:18:23:24:25:26:27:28:29:30:31:32:33:34:35:36:37:41:42:43:44:45:46:47:48:49:53:54:55:56:57:58:59:60:61:64:38:39:40:62:50:51:52:63
```


#### **<span style="color:maroon">If using MEGIN Caps ...</span>**

To **help in digitisation, three pages have been copied from MEGIN's EEG Cap User's manual above** ...

- **[Electrode Locations and Channel Numbers](../../meg/pdfs/MEGIN_64Channel_EEG_Locations_and_Channel_Numbers.pdf)**

- **[Electrode layout (original)](../../meg/pdfs/MEGIN_64Channel_EEG_Layout_original.pdf)** - **Figure A.2**

- **[Electrode layout (new numbering)](../../meg/pdfs/MEGIN_64Channel_EEG_Layout_new.pdf)** - ***<span style="color:maroon">Many thanks to Malgorzata "Gosia" Wislowska.</span>***

**She says ...**

"*<span style="color:green">I exchanged numbers of green electrodes so that they go from 1-32 instead of 33-64.<br />
This new numbering is compatible with electrode numbering on SIGGI device.<br />
So one can save a little bit of grey matter energy and skip subtracting number 32 when checking the impedances.<br />
We should however not get rid of the old layout, which in turn is compatible with electrode numbering in the acquisition software (numbers going from 1 to 64).</span>*"


## Procedure

**<span style="color:blue">Not many MEG Operators have undertaken EEG & MEG, but those that have used the following procedure/digitisation order:</span>**<br />
***<span style="color:maroon">Many thanks to Oscar Ferrante & Tara Ghafari @2020</span>***

- **Attach BIO electrodes**.
- **Attach EEG cap**.
- **Attach HPI coils on EEG cap** (***EASYCAPs were purchased with built-in HPI coil holders***).
- **Gel EEG cap** (**[Correct Positioning & Usage of EEG Caps](position_usage_eeg_caps.md)**)
- **Digitise fiducial points**.
- **Digitise HPI coils**.
- **Digitise the 64 electrodes.** 
	 - **Use the SIGGI-II multimeter to measure electrode impedance** <br /> - **[Correct Positioning & Usage of EEG Caps#check-impedances](position_usage_eeg_caps.md#check-impedances)**
- **Digitise the head shape**. **<span style="color:red">Take care not to damage the coils/break any electrode wiring!</span>**

**They used the MEGIN caps**<br />
"*<span style="color:green">We attached the HPI coils to the MEGIN cap because that way we could easily reach them during digitisation.<br />
If they are placed on the head (as in normal usage), this needs to be done so that the Polhemus pointer can reach them under the EEG cap with a perpendicular orientation - it needs to be very well thought out.</span>*"

**When queried if it was possible to digitise the head shape *before* the 64 electrodes ...**<br />
"*<span style="color:green">I’m not sure it’s possible to digitise the head shape before doing it for the EEG electrodes in the MEGIN software.<br />
If so, it’s worth a try. But the HPI coils would then need to be attached to the head, adding the problems mentioned above.<br />
Doing the head shape digitisation once the cap is in place is not perfect as it introduces some noise, which can make the coregistration less accurate.<br />
It’s a trade-off. In our analysis (i.e., visual response in posterior and prefrontal areas), this extra noise did not have a strong impact, but I guess it depends on the specific experimental question.</span>*"


!!! note "<span style="color:red">NOTE: Autumn 2025:</span> Coen & Helena found that using the BIO GND electrode (which they're using for EMG recording), rather than the EASYCAP GND electrode, produced better signal quality overall when plugged into the gantry side panel.<br />The side panel REF connection was made using the EASYCAP REF electrode (no BIO REF electrode was attached to the participant)."

