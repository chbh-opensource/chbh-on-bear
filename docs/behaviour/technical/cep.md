# Common Experimental Platform PCs

Currently the Brain Stim Lab, the fMRI, the Mock, the MEGs, fNIRS, the OPM and some Cubicles have identical stimulus presentation / response recovery PCs built specifically for research grade timing, durability and redundancy.

We intend to install such CEP (common experimental platform) Stimulus machines in all suitable modalities. This will encourage paradigm mobility between the modalities (write once, run anywhere), and allow enhanced response from CHBH IT personnel.

## The CEP PC

!!! note

    Information on log-ins, network names and administration of CEP PCs is covered on the CHBH sharepoint pages which require UoB SSO log in.

### Hardware

High end Intel CPUs and 16GB of RAM on ASUS PRIME Z370-A II (or it's predecessor Z270-A) motherboards. Graphics are provided by AMD WX (4100 or 7100) series of workstation graphics cards, as specifically recommended by the author of the PsychoPhysics Toolbox (PTB) under Neurodebian.

AMD WX 4100 & WX7100 graphics cards. The WX7100 cards will be in the MEG (in transition from NVIDIA), MOCK and fMRI. 4100s in the cubicles and other modalities. (2023 will see new PCs equipped with the newer W7500 cards)

Onboard audio is the recommended solution for the PTB, replacing the previous ASIO recommendation (which has been fully retired in recent version of PTB).

AOC 24" monitor 1920x1080@120Hz (to match the standard operation of the VPIxx projector in the MEG and fMRI chambers). Check that desktop refresh rate is set to 120Hz and that AMD FreeSync is disabled - otherwise the PTB will fail the SimpleMovieDemo test. Some PCs will now be equipped with 360Hz monitors in the EEG lab.

Single monitors are indicated for precise timing control in the PTB. In Labs where multiple monitors are indicated, experimenters should use a hardware splitter and not a second output port on the AMD WX card (especially under Windows 10). The VPIXX Projector provides it's own pass through that preserves timing control.

### Software

Generally Windows 10; MATLAB 2018a *and* 2019b, with the most recent PTB. PsychoPy 3.0.3. National Instruments DAQmx. LABJACK U3 package. Every machine should have an identical OS installation. We will be updating the MATLAB versions in the beginning of 2024.

To provide a consistent experience. MATLAB will clean it's path of any non basic paths on restart. Please add suitable code to the beginning of your experiment, such as addpath(genpath(‘yourfolder)); . As this is a multi-user machine this allows us to avoid namespace clashes for inbuilt and bespoke scripts.

All CEPs are capable of running Neurodebian 18 LTS; MATLAB 2018a, with the most recent PTB. This is the preferred platform for precise timing.

See this article, from the author of PsychoPy, for a discussion of timing reliability betwixt PsychoPy/PTB and Windows/Linux.

Some Labs may request that their CEP not be constantly connected to the Network.

### Paradigm Location (Windows)

The C: boot drive is not for the storage of responses or paradigms. The C: boot drive is not backed up. The C: boot drive can and will be re-imaged at any time. A remote drive R: Remote Paradigms is provided to offer a shared repository of paradigms and your data. This will allow access from any other CEP PC. This is backed up. - How to Map the Remote Paradigms Drive. A second drive L: LOCAL is provided for paradigms to be hosted locally if your paradigm is impacted running from a network resource. This is not backed up.
