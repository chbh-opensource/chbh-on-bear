# Getting started on BEAR

**This page collects tutorials and examples for neuroimaging analyses to run on BlueBEAR.** This is intended to extend the main [BEAR Technical Documentation](https://docs.bear.bham.ac.uk/) pages.

Here we provide a set of links, tips and tricks for getting started.

## Step 0: Linux

BEAR provide a [Introduction to Linux](https://www.birmingham.ac.uk/research/arc/bear/training/intro-linux) guide. **Many computing services on BEAR rely on Linux.** There are in-person workshops and an online Canvas courses available on this page.

## Step 1: BlueBEAR

BEAR also provide a [Introduction to BlueBEAR](https://www.birmingham.ac.uk/research/arc/bear/training/necessities) course. There are in person workshops and an online Canvas course.

## Step 2: RDS Projects

**You'll need to be a member of a BEAR project and have a BEAR linux account to use BlueBEAR.** Your PI and lab can help with this. A detailed guide for [accessing BEAR](https://docs.bear.bham.ac.uk/bluebear/accessing/) is provided on the technical docs.

## Step 3: BEAR Portal

**[BEAR Portal](https://docs.bear.bham.ac.uk/portal/accessing/) provides web-based access to a range of BEAR services**, such as JupyterLab, RStudio, and various other GUI applications. BEAR Portal is only available on campus or using the University Remote Access Service.

## Step 4: Launching interactive sessions

**From the BEAR Portal there are three options for launching an interactive analysis session.**

- Some software packages have [GUI Apps](https://docs.bear.bham.ac.uk/portal/gui_apps/) installed on BlueBEAR that can be launched from the BEAR Portal - the main example for neuroimaging analysis is MATLAB.

- [JupyterLab](https://docs.bear.bham.ac.uk/portal/jupyterlab/) and [RStudio](https://docs.bear.bham.ac.uk/portal/rstudio/) are installed as standalone apps that can be launched from the BEAR Portal (note that only packages installed on BEAR Apps are available to load in JupyterLab).

- A complete Linux Desktop can be launched as the [BlueBEAR GUI](https://docs.bear.bham.ac.uk/portal/gui/). BlueBEAR GUI is effectively a blank-slate Linux desktop, into which you can load the modules for various applications, specify environment variables etc. by using the built-in Terminal client, and then ultimately launch the interface for the application that you require.

## Step 5: Running cluster jobs with Slurm

There are two ways to submit a cluster job - the [BlueBEAR terminal](https://docs.bear.bham.ac.uk/bluebear/jobs/) and the [job submission page on BEAR Portal](https://docs.bear.bham.ac.uk/portal/jobs/)

**BlueBEAR Terminal** Once you have prepared a submission script, you can go to that location in the BEAR Portal file browser and click 'Open in terminal' in the top. This will open a terminal session from which you can submit, monitor and (optionally) cancel your job using `sbatch`, `squeue` and `scontrol`.

!!! note
    These terminal sessions are ONLY intended for submitting and monitoring cluster jobs - not for active analyses. This should be carried out on the BEAR GUI or similar.

**BlueBEAR Job Composer** this is a GUI page which helps you to write a new job to submit to BlueBEAR using the [job composer](https://docs.bear.bham.ac.uk/portal/jobs/#creating-a-new-compute-job-through-the-bear-portal).
