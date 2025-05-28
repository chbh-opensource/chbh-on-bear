# Getting started on BEAR

This page collects tutorials and examples for neuroimaging analyses to run on BlueBEAR. This is intended to extend the main [BEAR Technical Documentation](https://docs.bear.bham.ac.uk/) pages.

Here we provide a set of links, tips and tricks for getting started.

## Step 0: Linux

Bear provide a [Introduction to Linux](https://www.birmingham.ac.uk/research/arc/bear/training/intro-linux) guide. Many computing services on bear rely on linux. There are in-person workshops and an online canvas courses available on this page.

## Step 1: BlueBEAR

BEAR also provide a [Introduction to BlueBEAR](https://www.birmingham.ac.uk/research/arc/bear/training/necessities) course. There are in person workshops and an online Canvas course.

## Step 2: RDS Projects

You'll need to be a member of a BEAR project and have a BEAR linux account to use BlueBEAR. Your PI and lab can help with this. A detailed guide for [accessing BEAR](https://docs.bear.bham.ac.uk/bluebear/accessing/) is provided on the technical docs.

## Step 3: BEAR Portal

[BEAR Portal](https://docs.bear.bham.ac.uk/portal/accessing/) provides web-based access to a range of BEAR services, such as JupyterLab, RStudio, and various other GUI applications. BEAR Portal is only available on campus or using the University Remote Access Service.

## Step 4: Launching interactive sessions

From BEAR Portal there are three options for launching an interactive analysis session.

- Some software packages have [GUI Apps](https://docs.bear.bham.ac.uk/portal/gui_apps/) installed on BlueBEAR that can be launched from the BEAR Portal - the main example for neuroimaging analysis is MATLAB.

- [JupyterLab](https://docs.bear.bham.ac.uk/portal/jupyterlab/) and [RStudio](https://docs.bear.bham.ac.uk/portal/rstudio/) are installed as standalone apps that can be launched from BEAR Portal. (ote that only packages installed on BEAR Apps are available to load in JupyterLab).

- A complete Linux Desktop can be launched as the [BlueBEAR GUI](https://docs.bear.bham.ac.uk/portal/gui/). BlueBEAR GUI is effectively a blank-slate Linux desktop, into which you can load the modules for various applications, specify environment variables etc. by using the built-in Terminal client (see image below), and then ultimately launch the interface for the application that you require.

## Step 5: Running cluster jobs with Slurm

There are two ways to submit a cluster job - the [BlueBEAR terminal](https://docs.bear.bham.ac.uk/bluebear/jobs/) and the [job submission page on BEAR Portal](https://docs.bear.bham.ac.uk/portal/jobs/)

**BlueBEAR Terminal** Once you have prepared a submission script, you can go to that location in the BEAR-Portal file browser and click 'Open in terminal' in the top. This will open a terminal session from which you can submit, monitor and (optionally) cancel your job using `sbatch`, `squeue` and `scontrol`.

!!! note
    These terminal sessions are ONLY intended for submitting and monitoring cluster jobs - not for active analyses. This should be carried out on the BEAR GUI or similar.

**BlueBEAR Job Composer** this is a GUI page which helps you to write a new job to submit to blue-bear using the [job composer](https://docs.bear.bham.ac.uk/portal/jobs/#creating-a-new-compute-job-through-the-bear-portal).

# Index of Neuroimaging Software

This is an incomplete list of the neuroimaging software that is available on BlueBEAR. The links in the 'Toolbox' column follow to CHBH-on-BEAR examples and the 'Bear Apps' links go to the module specifications provided by BEAR.

| Toolbox                           | GUI App          | Bear Apps Modules                                                           | Notes                         |
|:----------------------------------|:-----------------|:---------------------------------------------------------------------------|:------------------------------|
| **Programming Environments**      |                  |                                                                            |                               |
| [Python](software/python.md)     | JupyterLab       | [Bear Apps Python](https://bear-apps.bham.ac.uk/applications/Python/)     | Bear Apps or pip/venv         |
| [MATLAB](software/matlab.md)     | MATLAB           | [Bear Apps MATLAB](https://bear-apps.bham.ac.uk/applications/MATLAB/)     |                               |
| [R](software/R.md)               | RStudio          | [Bear Apps R](https://bear-apps.bham.ac.uk/applications/R/)               |                               |
| **MRI Analysis Tools**            |                  |                                                                            |                               |
| [FSL](mri/fsl.md)                | FSLeyes          | [Bear Apps FSL](https://bear-apps.bham.ac.uk/applications/FSL/)           | Pip install modules via venv  |
| [FreeSurfer](mri/freesurfer.md)  | FreeView         | [Bear Apps FreeSurfer](https://bear-apps.bham.ac.uk/applications/FreeSurfer/) |                           |
| [SPM](mri/spm.md)                | MATLAB           | None                                                                       | Load within MATLAB script     |
| **EEG/MEG Analysis Tools**        |                  |                                                                            |                               |
| [MNE-Python](meg/mne.md)         | JupyterLab       | [Bear Apps MNE](https://bear-apps.bham.ac.uk/applications/MNE-Python/)    | Bear Apps or pip/venv         |
| [FieldTrip](eeg/fieldtrip.md)    | MATLAB           | None                                                                       | Load within MATLAB script     |
| EEGLab                           | MATLAB           | None                                                                       | Load within MATLAB script     |