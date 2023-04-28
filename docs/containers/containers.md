# Containers

A container is a lightweight software package that contains both the software, and all of the required dependencies to run the contained software.

BlueBEAR supports running analyses on containers using [Apptainer](https://docs.bear.bham.ac.uk/bluebear/software/container/). The Bear Technical docs contain extensive tutorals

> **_NOTE:_** BlueBEAR does not directly support Docker as it requires administratr privalages to run. Apptainer is able to read and execute Docker images without admin rights. Apptainer is the successor to the Singularty project - please see [this article](https://apptainer.org/news/community-announcement-20211130/) for more information on the transition.

## Downloading a Container

[Docker](https://hub.docker.com/) has a wide selection of containers available to download. Bear Technical docs contains some examples on how to [download and execute a simple python container](https://docs.bear.bham.ac.uk/bluebear/software/container/#pull-and-run).

The following bash code provides an example of how to download the [fMRIPrep](https://hub.docker.com/r/nipreps/fmriprep) container, which includes a variety of neuroimaging software, including freesurfer, FSL, and ANTS. This can be run on a terminal in the Bear GUI.

```shell
singularity pull --name fMRIPrep.sif docker://nipreps/fmriprep:latest
```

and this version can be submitted as a cluster script.

```slurm
#!/bin/bash

#SBATCH --account bagshaap-eeg-fmri-hmm
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 10 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format
#SBATCH --constraint icelake

set -e

singularity pull --name fMRIPrep.sif docker://nipreps/fmriprep:latest
```

### Running Software using a Container

The `singularity exec` command is used to run the contained software. The following bash codes demonstrates how to run the FSL command `fslroi` contained within the fMRIPrep container.

```slurm
#!/bin/bash
#SBATCH --account bagshaap-eeg-fmri-hmm
#SBATCH --qos bbdefault

module purge; module load bluebear

singularity exec fMRIPrep.sif fslroi --help
```
