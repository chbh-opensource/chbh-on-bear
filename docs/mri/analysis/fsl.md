# FSL

**[FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki) is a comprehensive library of analysis tools for FMRI, MRI and DTI brain imaging data.**

## FSL Modules

A range of installed FSL versions are available as [modules on Bear Apps](https://bear-apps.bham.ac.uk/applications/FSL/).

## BEAR Portal GUI

The following code snippet can be executed in a terminal from within the Bear Portal GUI. It will load a pre-installed FSL version into the terminal where is can be used as normal.

```shell
module load bluebear
module load FSL/6.0.5.1-foss-2021a
```

We can then use FSL command line functions as normal:

```shell
fsl_anat --help
```

or open the FSL GUI:

```shell
fsl
```

## FSLEyes on BEAR Portal GUI

[FSLEyes](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSLeyes) is the MRI volume visualisation tool provided and maintained by the FSL team. This runs well in BEAR GUI and can be added to the local environment by adding the following module. (See the [FSLEyes page on BEAR Apps](https://bear-apps.bham.ac.uk/applications/FSLeyes/) for all available versions). 

```shell
module load FSLeyes/1.3.3-foss-2021a
```

Once the module has loaded you can run FSLEyes from the terminal as normal.

```shell
fsleyes
```

!!! info
    Note that it is currently not possible to have both FSL and FSLEyes in the environment in the same terminal. Until this is fixed, please use two separate terminal sessions, one for FSL and one for FSLEyes.

## FSL on the cluster

We can also run FSL jobs on the cluster using job scripts. The following can be saved as `run_fsl_bet.sh` and submitted to the cluster using `sbatch`. This will run a brain extraction on a single datafile.

```slurm
#!/bin/bash

#SBATCH --account quinna-camcan
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 5 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format

module purge
module load bluebear
module load FSL/6.0.5.1-foss-2021a

set -e

bet subject1.nii.gz subject1_brain.nii.gz
```

**If we have many datafiles to run BET on, we can extend our script into an array job.** This is a `slurm` script that actually creates many jobs that can be run in parallel. Here we add the `#SBATCH --array=1-48` line to our script to tell it that we want to parallelise our script across the range 1 to 48. This creates 48 separate jobs each with a value between 1 and 48 stored in the variable `${SLURM_ARRAY_TASK_ID}`. Our `BET` call changes the subject number with this variable for each job.

```slurm
#!/bin/bash
#SBATCH --account quinna-camcan
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 5 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format
#SBATCH --array=1-48

module purge
module load bluebear
module load FSL/6.0.5.1-foss-2021a

set -e

bet subject${SLURM_ARRAY_TASK_ID}.nii.gz subject${SLURM_ARRAY_TASK_ID}_brain.nii.gz
```

Submitting this script to the cluster will run BET 48 times on each input from `subject1.nii.gz` to `subject48.nii.gz`.

## FSL in a container

Sometime we may want more control over software versions that are supported by pre-compiled BEAR App. We can install FSL within a controlled container using the following job script. This creates a container file `FSL.sif` from the [NeuroDesk](https://www.neurodesk.org/) container specification.

```slurm
#!/bin/bash

#SBATCH --account quinna-example-project
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 10 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format
#SBATCH --constraint icelake

set -e

apptainer pull --name FSL.sif docker://vnmd/fsl_6.0.4
```

We can submit this job to the cluster using `sbatch` as normal. Once the `FSL.sif` has been created we can run future cluster jobs through it.

For example, this job script runs `fsl_anat` on a single dataset using our FSL container.

```slurm
#!/bin/bash

#SBATCH --account quinna-camcan
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 5 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format

module purge
module load bluebear

set -e

apptainer exec FSL.sif  fsl_anat -i subject1.nii.gz -o subject1
```

This can be combined with array jobs from the example above to run many container-based analyses together in parallel.
