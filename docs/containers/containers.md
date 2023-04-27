# Containers

A container is a lightweight software package that contains both the software, and all of the required dependencies to run the contained software.

## Downloading a Container

[Docker](https://hub.docker.com/) has a wide selection of containers available to download. The following bash code provides an example of how to download the [fMRIPrep](https://hub.docker.com/r/nipreps/fmriprep) container, which includes a variety of neuroimaging software, including freesurfer, FSL, and ANTS.

```

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

```
#!/bin/bash
#SBATCH --account bagshaap-eeg-fmri-hmm
#SBATCH --qos bbdefault

module purge; module load bluebear

singularity exec fMRIPrep.sif fslroi --help
```





