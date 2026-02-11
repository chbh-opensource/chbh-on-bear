# Atypical MEG signals

"**Artifacts**" are **unwanted noise in the acquired data** that **may or may not interfere/mask the signal expected to be seen**. <br />
Any artifact found will **need to be removed from acquired data before any analysis is performed**, and obviously they are **needed to be identified** first.<br />
Artifacts can be **caused by the environment or by the participant**, and common examples are:

## **Pysiological**

- <span style="color:maroon">Eye blinks (**EOG**) - Electrooculogram.</span>
- <span style="color:maroon">Heart beats (**ECG**) - Electrocardiogram.</span>
- <span style="color:maroon">Muscle artifacts (**EMG**) - Electromyogram.</span>
- <span style="color:maroon">Head movements (*will include neck EMG artifacts*).</span>
- <span style="color:maroon">Dental artifacts (*large amalgam fillings, orthodontic applances*).</span>

## **Environmental / System**

- <span style="color:maroon">Power line noise (**Mains 50Hz**).</span>
- <span style="color:maroon">Squid Jumps.</span>

## **Example FIF data**

![Eyes open, Temporal set, 3sec Window](../../images/meg/Eyes_open_with_ECG_Temporal.png){width=30% align=left}

- **<span style="color:green">Good Data</span>**.<br />
An example of **good, clean, data**. Temporal set of sensors. Eyes open looking at a central cross on the projector screen.
**Even if the ECG hadn't been recorded, the heartbeat can still be detected in the acquired data**.
<br /><br /><br /><br /><br />

<br />
![Parietal set, 8sec Window](../../images/meg/Squid_Jumps.png)

- **<span style="color:red">Squid Jumps</span>**<br />
"***Squid jumps***" on channel **MEG1043**. Resetting the channel/warming the sensor had no effect, and its tuning curve was within normal parameters. Resetting the SSC card only caused a temporary respite for a few days.
At the time, the channel was **marked as "bad"**, and it was repaired during the PM Service Visit.<br />

<br />
![Eye blinks (every 2sec), Frontal set, 10sec Window](../../images/meg/Eye_blinks_Frontal_10sec.png){width=30% align=left}
![Eye blinks (every 2sec), Temporal set, 10sec Window](../../images/meg/Eye_blinks_Temporal_10sec.png){width=30% align=right}

- **<span style="color:red">Eye blinks</span>**.<br />
Eye blinks from two sets of sensors, Frontal (left image) and Temporal (right image).
The Participant was asked to **blink their eyes every two seconds**, producing approximately five blinks in each ten-second window. It is **recommended to record EOG channels** in acquired data, to **help remove blink artifacts**.

<br /><br />
![Eyes side-to-side, Temporal set, 8sec Window](../../images/meg/Eyes_side-to-side_Temporal_8sec.png){width=30% align=left}

- **<span style="color:red">Eyes side-to-side</span>**.<br />
The Participant was asked to **move their eyes between two markers on either side of the projector screen, about once every second**. There are about eight movements collected in the eight-second window. There may also be some head movement/neck EMG artifact incorporated in the example image.
<br /><br /><br />

<br />
![Head movement, Occipital set, 8sec Window](../../images/meg/Head_movement_Occipital_8sec.png){width=30% align=left}

- **<span style="color:red">Head Movement</span>**.<br />
The Participant was asked to make a **shaking their head "No!"** type movement, with each "shake" taking about two seconds to complete. There are about five movements in the eight-second window, so they were moving slightly faster than asked. There is probably some neck EMG involved, as well as some EOG as they kept their eyes fixated on the central cross as they shook their head.<br />
<br /><br />

![Shrug shoulders, Temporal set, 8sec Window](../../images/meg/Shrug_shoulders_Temporal_8seconds.png){width=30%}
![Shrug shoulders, Occipital set, 8sec Window](../../images/meg/Shrug_shoulders_Occipital_8seconds.png){width=30%}

<align=full>

- **<span style="color:red">Shrug Shoulders</span>**.<br />
The Participant was asked to **"shrug" their shoulders**, about once a second. Temporal (left image) and Occipital (right image). The majority of the artifact is probably muscle EMG; the Participant kept their head surprisingly still during the task.
<br /><br />


![Clench Teeth, Frontal set, 5sec Window](../../images/meg/Teeth_Clench_Frontal_5sec.png){width=30%}
![Clench Teeth, Parietal set, 5sec Window](../../images/meg/Teeth_Clench_Parietal_5sec.png){width=30%}
![Clench Teeth, Occipital set, 5sec Window](../../images/meg/Teeth_Clench_Occipital_5sec.png){width=30%}

<align=full>

- **<span style="color:red">Clench Teeth</span>**.<br />
The Participant was asked to **clench their teeth and then relax**. Frontal (left), Parietal (center) and Occipital (right). Majority of the artifact is jaw muscle EMG.

<span style="color:blue">***With many thanks to Davd L. Winter.***</span>
