# MEG Contraindications

The signal measured by a MEG system is extremely low (10^-15^ T), and is susceptible to many potentially artifact-inducing elements.

None of the contraindications listed below will cause the MEG system to harm the participant or harm the device: a MEG is a fully passive device.

The contraindications will only impact the signal quality.

If your population of participants is limited or rare, you may have to run Acquisition sessions with subjects that might induce noise/reduce signal quality.

Depending on the artifact, it may well be possible to correct the Acquired data/remove the noise in postprocessing through the use of MaxFilter/Spatiotemporal SSS (tSSS) and/or MATLAB/FieldTrip.

!!! Note
    MRI compatibility is not equivalent to MEG compatibility. An MRI-compatible object might still contain some amount of ferromagnetic material which does not discount it from allowing an MRI scan but will induce artifacts that will show in the MEG signal.

!!! Info
    The majority of the contraindications, if not all, will have been mentioned in both our MRI and MEG screening forms. Remember to go over both screening forms when recruiting participants, to make sure you're able to obtain T1 scans (if you require them for your study).

## Known contraindications

(***not listed in any specific order of signal degradation***)

- Pacemaker, or any kind of cardiac stimulator
- Insulin pump, bladder neurostimulator, deep-brain neurostimulator, or any kind of implanted device
- Cardiac valves, both mechanical or animal
- Hearing aid, hearing implant
- Joint prosthesis (hip, knee, shoulder, etc)[^1]
- Neurosurgical clip for brain aneurysm
- Orthodontic implants, dental prosthesis, dental retainer/bridge work[^2]
- Sutures with metal wires or staples
- Non-removable piercings, earings, etc
- Tattoos[^1]
- Permanent makeup and eye makeup[^3]
- Coloured contact lenses, "Quick Attach" false eyelashes
- Recently-dyed hair, or any kind of hair extension
- Dreadlocks (gantry helmet is quite narrow)[^5]
- Foreign object in the eye
- Shrapnel or metal object in the body
- Vena cava filter, to prevent pulmonary embolism
- Metal workers or construction workers who work with metal (welders, etc)[^6]

### **Additionally, it's better if the participant:**

- Arrives with clean hair and/or beard[^4]
- Has not had an MRI scan, or been close to an MRI field, in the previous 72 hours[^6]
- Has not had any recent surgery[^6]

[^1]: May depend on the material and localisation. It's safer to avoid including participants with this contraindication, but if your participant population is limited, bring her/him into the lab for a brief screening test before booking the actual MEG slot. If the lab is free for ~10min or so, demetal your participant (where possible) and position them in the gantry chair. Start Acquisition, and look at the sensor noise. Based on your prior usage, make an informed decision as to whether it's worth your while Acquirng from this participant. If you're not sure, consult a colleague or ask MEG support. Remember MaxFilter and/or FieldTrip may be able to clean up your data afterward.Tattoos below the elbow do not usually cause artifacts.

[^2]: Any kind of dental work should be avoided, but some of the more modern dental work/dental retainers may be compatible. If your participant population is limited, bring her/him into the lab for a brief screening test before booking the actual MEG slot. If the lab is free for ~10min or so, demetal your participant (where possible) and position them in the gantry chair. Start Acquisition, and look at the sensor noise. Based on your prior usage, make an informed decision as to whether it's worth your while Acquirng from this participant. If you're not sure, consult a colleague or ask MEG support. Remember MaxFilter and/or FieldTrip may be able to clean up your data afterward.

[^3]: Makeup remover is available in the lab, but your setup will be quicker if the participant arrives without any makeup.

[^4]: A sink with a showerhead and hairdryer/towels are available in the lab, but your setup will be quicker if the participant arrives with clean hair/beard.

[^5]: We have a plastic helmet mimicing the gantry helmet. If the participant can wear the helmet comfortably, they will fit comfortably in the gantry helmet.

[^6]: If you're in any doubt, and your participant population is limited, bring her/him into the lab for a brief screening test before booking the actual MEG slot. If the lab is free for ~10min or so, demetal your participant (where possible) and position them in the gantry chair. Start Acquisition, and look at the sensor noise. Based on your prior usage, make an informed decision as to whether it's worth your while acquiring from this participant. If you're not sure, consult a colleague or ask MEG support. Remember MaxFilter and/or FieldTrip may be able to clean up your data afterward.
