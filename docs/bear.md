# Getting started on BEAR

This page collects tutorials and examples for neuroimaging analyses to run on BlueBEAR. This is intended to extend the main [Bear Technical Documentation](https://docs.bear.bham.ac.uk/) pages.

Here we provide a set of links, tips and tricks for getting started. Mostly linking out to other places.

## Step 0: Linux

Bear provide a [Introduction to Linux](https://intranet.birmingham.ac.uk/it/teams/infrastructure/research/bear/bear-training/intro-linux.aspx) guide. Many computing services on bear rely on linux. There are in-person workshops and an online canvas courses available on this page.

## Step 1: BlueBEAR

Bear also provide a [Introduction to BlueBEAR](https://intranet.birmingham.ac.uk/it/teams/infrastructure/research/bear/bear-training/necessities.aspx) course. There are in person workshops and an online canvas course.

## Step 2: RDS Projects

You'll need to be a member of a Bear project and have a Bear linux account to use BlueBEAR. Your PI and lab can help with this. A detailed guide for [accessing BEAR](https://docs.bear.bham.ac.uk/bluebear/accessing/) is provided on the technical docs.

## Step 3: Bear Portal

[BEAR Portal](https://docs.bear.bham.ac.uk/portal/accessing/)  provides web-based access to a range of BEAR services, such as JupyterLab, RStudio, and various other GUI applications. BEAR Portal is only available on campus or using the University Remote Access Service.

## Step 4: Launching interactive sessions

From BEAR Portal there are three options for launching an interactive analysis session.

- Some software packages have [GUI Apps](https://docs.bear.bham.ac.uk/portal/gui_apps/)  installed on BlueBEAR that can be launched from the Bear Portal - the main example for neuroimaging analysis is Matlab.

- [JupyterLab](https://docs.bear.bham.ac.uk/portal/jupyterlab/) and [RStudio](https://docs.bear.bham.ac.uk/portal/rstudio/) are installed as standalone apps that can be launched from BEAR Portal. (ote that only packages installed on Bear Apps are available to load in JupyterLab).

- A complete Linux Desktop can be launched as the [BlueBEAR GUI](https://docs.bear.bham.ac.uk/portal/gui/). BlueBEAR GUI is effectively a blank-slate linux desktop, into which you can load the modules for various applications, specify environment variables etc. by using the built-in Terminal client (see image below), and then ultimately launch the interface for the application that you require.


## Step 5: Running cluster jobs with Slurm

There are two ways to submit a cluster job - the bluebear terminal or the Bear Portal

https://docs.bear.bham.ac.uk/bluebear/jobs/
https://docs.bear.bham.ac.uk/portal/jobs/

## Step 6: Neuroimaging analysis software on Bear

The following software is available on BlueBEAR.


| Toolbox                      |      GUI App          |  Bear Apps Modules                                                     | Notes                         |
|:-----------------------------|:----------------------|:-----------------------------------------------------------------------|:------------------------------|
| [FSL](fsl/fsl.md)            | N/A                   | [Bear Apps FSL](https://bear-apps.bham.ac.uk/applications/FSL/)        | Pip install modules via venv  |
| [Python](mne/mne.md)         | JupyterLab            | [Bear Apps Python](https://bear-apps.bham.ac.uk/applications/Python/)  | Bear Apps or pip/venv         |
| [MNE-Python](mne/mne.md)     | JupyterLab            | [Bear Apps MNE](https://bear-apps.bham.ac.uk/applications/MNE-Python/) | Bear Apps or pip/venv         |
| [Matlab](matlab/matlab.md)   | MatLab                | [Bear Apps MatLab](https://bear-apps.bham.ac.uk/applications/MATLAB/)  |                               |
| Fieldtrip                    | MatLab                | None                                                                   | Load within MatLab script     |
| EEGLab                       | MatLab                | None                                                                   | Load within MatLab script     |
| SPM                          | MatLab                | None                                                                   | Load within MatLab script     |
| [R](R/R.md)                  | Rstudio               | [Bear Apps R](https://bear-apps.bham.ac.uk/applications/R/)            |                               |
| Freesurfer                   | N/A                   | [Bear Apps Freesurfer](https://bear-apps.bham.ac.uk/applications/FreeSurfer/)   |     |



