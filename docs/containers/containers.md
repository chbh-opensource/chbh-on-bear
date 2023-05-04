# Containers

A container is a lightweight software package that contains both the software, and all of the required dependencies to run the contained software.

BlueBEAR supports running analyses on containers using [Apptainer](https://docs.bear.bham.ac.uk/bluebear/software/container/). The Bear Technical docs contain extensive tutorals

!!! note
    BlueBEAR does not directly support Docker as it requires administratr privalages to run. Apptainer is able to read and execute Docker images without admin rights. Apptainer is the successor to the Singularty project - please see [this article](https://apptainer.org/news/community-announcement-20211130/) for more information on the transition.

## Downloading a Container

[Docker](https://hub.docker.com/) has a wide selection of containers available to download. Bear Technical docs contains some examples on how to [download and execute a simple python container](https://docs.bear.bham.ac.uk/bluebear/software/container/#pull-and-run).

The following bash code provides an example of how to download the [fMRIPrep](https://hub.docker.com/r/nipreps/fmriprep) container, which includes a variety of neuroimaging software, including freesurfer, FSL, and ANTS. This can be executed on an interactive or batch job.

```shell
apptainer pull --name fMRIPrep.sif docker://nipreps/fmriprep:latest
```

and this version can be submitted as a cluster script.

```slurm
#!/bin/bash

#SBATCH --account bagshaap-example-project
#SBATCH --qos bbdefault
#SBATCH --time 60
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 10 # this will give you circa 40G RAM and will ensure faster conversion to the .sif format
#SBATCH --constraint icelake

set -e

apptainer pull --name fMRIPrep.sif docker://nipreps/fmriprep:latest
```

save the code above into a bash script called `create-container_fmriprep.sh` (make sure you update the `account` name on line 3 to a project that you have access to!) inside the directory where you would like to save the container file. This can then be submitted to the cluster by running `sbatch create-container_fmriprep.sh` in a terminal, or creating a job in the 'job composer'. This will take several minutes to run to completion with the `fmriprep` image.

Once the job has completed, you should be able to find a file called `fMRIPrep.sif` in your working directory (alongside the cluster log files). This is the container file.

### Running Software using a Container

The `apptainer exec` command is used to run the contained software. The following bash codes demonstrates how to run the FSL command `fslroi` contained within the fMRIPrep container.

```slurm
#!/bin/bash
#SBATCH --account bagshaap-example-project
#SBATCH --qos bbdefault

module purge; module load bluebear

apptainer exec fMRIPrep.sif fslroi --help
```

This code can be saved into a bash script called `check-container_fmriprep.sh` inside the same directory used above. You can run the job as above and check the cluster logfiles to see that the help text for the `fslroi` function was printed from within the container. This is a very simple example but can be adapted to run any command using the software inside the container.

Let's break this down so we can build a more complex command. There are four parts to running a command with Apptainer. This is the core line:

```shell
apptainer exec fMRIPrep.sif fslroi --help
```

We could visualise this as

```shell
<apptainer call> <apptainer command> <container image> <user command>
```

where

- `<apptainer call>` is simply `apptainer`. This specifies that we're using apptainer.
- `<apptainer command>` is `exec`. This tells apptainer that we want to run a command.
- `<container image>` is `fMRIPrep.sif`. This should point to an existing `.sif` file containing our container.
- `<user command>` is `fslroi --help`. This is the command we actually want to run and the part that we'll most frequently be changing.

So, to run a more complex command we'd simply need to update our `<user command>` to the function that we need to compute. You'll need to be sure that the appropriate command is included in the container with all its dependencies. The command can point to files and directories within RDS as usual. You can combine array jobs and container commands to run many parallel analyses all within equivalent containers.
