# fMRIPrep

<b>[fMRIPrep](https://fmriprep.org/) is an open-source tool for preprocessing functional MRI (fMRI) data.</b> It automates the early stages of MRI data preprocessing, including motion correction, susceptibility distortion correction, and slice-timing correction, providing a standardised and reproducible analysis pipeline. Unlike other preprocessing pipelines, fMRIPrep utilizes functions from many popular neuroimaging tools, including FSL, FreeSurfer, and AFNI, ensuring that each step in the pipeline uses the most reliable and validated methods available, resulting in higher-quality outputs.

## Downloading fMRIPrep

The simplest way of running fMRIPrep is using a container. Instructions for downloading the fMRIPrep container are detailed [here](../software/containers.md).

## Running fMRIPrep

In order to run fMRIPrep, your data must first be organised according the Brain Imaging Data Structure [BIDS](https://bids.neuroimaging.io/) guidlines. Once organised into BIDS, the default fMRIPrep can be run using the following script:

``` bash
#!/bin/bash

#SBATCH --account example-project
#SBATCH --qos bbdefault
#SBATCH --time 1440
#SBATCH --ntasks 4
#SBATCH --mem 18G

bids_directory=camcan_bids/
output_directory=camcan_fmriprep/

apptainer run fmriprep_24_1_1.sif ${bids_directory} ${output_directory} participant -w work/ --participant-label 01 --fs-license-file ~/license.txt 
```

This script can then be submitted using the following command:

``` bash
sbatch fmriprep.sh
```

Descriptions of the variables and arguments:

| Variables / Arguments       | Description                                                           |
|-----------------------------|-----------------------------------------------------------------------|
| `bids_dir`                  | First positional argument. Path to the BIDS-formatted dataset.       |
| `analysis_level`            | Second positional argument. Should be set to "participant" (required).|
| `output_dir`                | Third positional argument. Sets the output directory.                |
| `-w`                        | Specifies the working directory to store intermediate files during preprocessing. |
| `--participant-label`       | Specifies the BIDS subject ID, enabling fMRIPrep to run on a single subject or a subset of subjects. |
| `--fs-license-file`         | Path to the FreeSurfer license file (see [FreeSurfer](../mri/freesurfer.md)). By default, fMRIPrep uses FreeSurfer for anatomical co-registration. |
| `--nprocs`                  | Number of CPU cores to use for processing.                           |
| `--mem`                     | Amount of memory available in GB.                                    |

These arguments represent only a selection of the available options.

## Running fMRIPrep Across all Subjects

It is also possible to run all subjects within a BIDS directory by using the following modified script:

``` bash
#!/bin/bash

#SBATCH --account example-project
#SBATCH --qos bbdefault
#SBATCH --time 1440
#SBATCH --ntasks 4
#SBATCH --mem 18G
#SBATCH --array=0-20 # Number of subjects in the BIDS directory.

SUBJECTS=($(find camcan_bids -maxdepth 1 -type d -name 'sub-*' | sort | xargs -n 1 basename))
SUBJECT_ID=${SUBJECTS[$SLURM_ARRAY_TASK_ID]}
bids_directory=camcan_bids/
output_directory=camcan_fmriprep/

apptainer run fmriprep_24_1_1.sif ${bids_directory} ${output_directory} participant -w work/ --participant-label ${SUBJECT_ID} --fs-license-file ~/license.txt 
```

The number at the end fo the "#SBATCH --array=0-20" should be replaced with the number of subjects within the BIDS directory.
