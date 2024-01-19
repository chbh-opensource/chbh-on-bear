# FreeSurfer

[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/) is an open-source package for the analysis and visualization of structural, functional, and diffusion neuroimaging data from cross-sectional and longitudinal studies.

## FreeSurfer License
FreeSurfer requires a license registration key in order to be used. This can be obtained from [here](https://surfer.nmr.mgh.harvard.edu/registration.html). Once downloaded, the file should be uploaded to your home directory on Bear. This can be done using "Files" tab on the [BlueBEAR portal](https://portal.bear.bham.ac.uk/), or using file transfer software, such as [WinSCP](https://winscp.net/eng/index.php), or [FileZilla](https://filezilla-project.org/). 

## Running recon-all
The `recon-all` command performs all, or any part of, the FreeSurfer cortical reconstruction process. The outputs of `recon-all` can be used to define the surfaces required for the boundary estimate model (BEM) required when performing source reconstruction on M/EEG data. The function can be run via BlueBEAR using the example script (recon_all.sh) below:

``` bash
#!/usr/bin/env bash
#SBATCH --qos bbdefault
#SBATCH --time 1440
#SBATCH --ntasks 4
#SBATCH --mem-per-cpu 2

module purge
module load bear-apps/2019a/live
module load FreeSurfer/6.0.1-centos6_x86_64

export FS_LICENSE=${HOME}/license.txt
export SUBJECTS_DIR=/rds/projects/b/bagshaap-eeg-fmri-hmm/fs_outputs

recon-all -s sub-01 -i /rds/projects/b/bagshaap-eeg-fmri-hmm/T1_vol_v1_5.nii.gz \
-all \ 
-log logfile \ 
-all \
-parallel -openmp 4
```

This script can then be submitted using the following command:

``` bash
sbatch recon_all.sh
```

Descriptions of the variables and arguments:

| Variables / Arguments       | Description                                                           |
|----------------|-----------------------------------------------------------------------|
| `FS_LICENSE`   | Sets the path to the FreeSurfer license file.                         |
| `SUBJECTS_DIR` | Sets the output directory for the analysis.                           |
| `-s`           | Sets the name of the output folder.                                   |
| `-i`           | Specifies the full path to the T1-weighted MRI image.                 |
| `-all`         | Instructs FreeSurfer to run all processing steps.                     |
| `-log`         | Creates a log file named "logfile" upon completion of the processing. |
| `-parallel`    | Enables parallel processing in FreeSurfer.                            |
| `-openmp`      | Defines the number of CPU cores available for parallel processing.    |

For the above script to work for you, several of the variables and arguments need to be changed to match your filenames and directories. Specifically, the `SUBJECT_DIR` variable needs to be changed to the path where you want the outputs to be saved, the `-s` argument needs to be changed to the desired name of the output folder, and the `-i` argument needs to be changed to a path to your T1 file. 

## Running recon-all on Multiple Subjects

Alternatively, if you need to run recon-all for multiple subjects at once, for example, on an entire BIDS dataset, it is possible to submit all jobs using the below script (recon_all_bids.sh):

``` bash
#!/usr/bin/env bash
#SBATCH --qos bbdefault
#SBATCH --time 1440
#SBATCH --ntasks 4
#SBATCH --mem-per-cpu 2
#SBATCH --array=1-20 # 20 represents the total number of subjects

module purge
module load bear-apps/2019a/live
module load FreeSurfer/6.0.1-centos6_x86_64

export FS_LICENSE=${HOME}/license.txt
export SUBJECTS_DIR=/rds/projects/b/bagshaap-eeg-fmri-hmm/fs_outputs

subject_id_number=$(printf "%02d" ${SLURM_ARRAY_TASK_ID})

recon-all -s sub-${subject_id_number} \
-i /rds/projects/b/bagshaap-eeg-fmri-hmm/bids_dataset/sub-${}/anat/sub-${subject_id_number}_T1w.nii.gz  \
-all \ 
-log logfile \ 
-all \
-parallel -openmp 4
```

## Running FreeSurfer in a Container
Running FreeSurfer within a container allows for greater control over the software versions and improves the reproducibility of the analysis. FreeSurfer containers are available on [dockerhub](https://hub.docker.com/r/freesurfer/freesurfer/tags), or can be created using [NeuroDocker](https://github.com/ReproNim/neurodocker) (see the [Containers](../containers/containers.md) page for details on downloading containers). In the example below we assume a container named 'freesurfer.sif' has been downloaded:

``` bash
#!/usr/bin/env bash
#SBATCH --qos bbdefault
#SBATCH --time 1440
#SBATCH --ntasks 4
#SBATCH --mem-per-cpu 2

FS_LICENSE=${HOME}/license.txt
SUBJECTS_DIR=/rds/projects/b/bagshaap-eeg-fmri-hmm/Projects/Visual_Response_Variability/fs_outputs

apptainer exec --env FS_LICENSE=${FS_LICENSE} --env SUBJECTS_DIR=${SUBJECTS_DIR} \
freesurfer.sif \
recon-all -s sub-01 -i /rds/projects/b/bagshaap-eeg-fmri-hmm/T1_vol_v1_5.nii.gz \
-log logfile \ 
-all \
-parallel -openmp 4
```
