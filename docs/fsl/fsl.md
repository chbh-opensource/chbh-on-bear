# FSL

[FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki) is a comprehensive library of analysis tools for FMRI, MRI and DTI brain imaging data.


## FSL Modules

A range of installed FSL versions are available as [modules on Bear Apps](https://bear-apps.bham.ac.uk/applications/FSL/).

## Bear Portal GUI

The following code snippet can be executed in a terminal from within the Bear Portal GUI. It will load a pre-installed FSL version into the terminal where is can be used as normal.

```
module load FSL/6.0.5.1-foss-2021a-fslpython
```

We can then use FSL command line functions as normal.

```
fsl_anat --help
```

## Submitting FSL Jobs


```
#!/bin/bash
#SBATCH --ntasks 1
#SBATCH --time 30:0
#SBATCH --mem 50G
#SBATCH --qos bbdefault
#SBATCH --array=1-48

set -eu

module purge; module load bluebear
module load MATLAB/2019b					# load the MATLAB version you need


# apply matlab script to each index in the array (here, the MATLAB script is programmed such that the input ID is used as the subject ID)
matlab -nodisplay -r "run /rds/homes/d/dueckerk/startup.m, e1_fun_ICA(${SLURM_ARRAY_TASK_ID}), quit"
```

