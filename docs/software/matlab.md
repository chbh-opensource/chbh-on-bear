# MATLAB

Interactive MATLAB sessions run as a [GUI App](https://docs.bear.bham.ac.uk/portal/gui_apps/) accessible from the [BEAR Portal](https://docs.bear.bham.ac.uk/portal/accessing/). Please follow the information on the BEAR Technical Docs to start up an interactive MATLAB session.

Some parallelisation is available through [parfor](https://www.mathworks.com/help/MATLAB/ref/parfor.html) loops within single MATLAB but users looking for to run many individual MATLAB scripts in parallel are likely to want to use the [Slurm job submissions](https://docs.bear.bham.ac.uk/bluebear/jobs/). Examples of both are included below.

## Neuroimaging toolboxes

Neuroimaging toolboxes can be added to the MATLAB path on BlueBEAR in the normal way. Toolboxes can be downloaded from the developer and stored on an [RDS](https://docs.bear.bham.ac.uk/rds/accessing/) space. These folders can be added to the path within a MATLAB session using `addpath`.

``` MATLAB
addpath(genpath('/rds/q/quinna-example-project/code/fieldtrip'))
```

These pages include some specific examples using popular MATLAB toolboxes:

- [Fieldtrip](../eeg/fieldtrip.md)
- [SPM](../mri/spm.md)

## Parallel for-loop

!!! info
    Example contributed by Dagmar Fraser

Simple parallelisation of a for-loop can be performed using [parfor](https://www.mathworks.com/help/MATLAB/ref/parfor.html). This functionality is provided by MATLAB and enables faster processing of `for` loops simply by changing the syntax at the start to say `parfor` rather than `for`.

The following MATLAB code performs some matrix calculations on simulated data. The inclusion of a `parfor` loop means that the code can take advantage of computers with multiple CPUs to accelerate processing.

```MATLAB
tic
n = 200;
A= 500;
a = zeros(1,n);
parfor i = 1:n
    a(i) = max(abs(eig(rand(A))));
end
toc
```

Run this a few times replacing `parfor` with `for` to get an idea of the time difference.

!!! note
    Make sure you specify the appropriate number of cores when starting the MATLAB GUI App, you may not notice a substantial speed-up if you run MATLAB using the default of 4 cores. Do try to avoid asking for substantially more than you might need however - BlueBEAR is a shared resource!

## Submitting MATLAB jobs with parfor to Bear

You can run this code in an interactive MATLAB session, or save it as a script that can be executed on the big cluster. If we save the code in the previous example as `parforDemo.m`, we can write a second 'submission' script to execute it on the cluster.

``` slurm
#!/bin/bash
#SBATCH --ntasks 8
#SBATCH --time 5:0
#SBATCH --qos bbshort
#SBATCH --mail-type ALL

set -e

module purge
module load bluebear
module load MATLAB/2020a

MATLAB -nodisplay -r parforDemo
```

If we save that second script as `RunMyCode.sh` it can be run using `sbatch RunMyCode.sh` on a terminal to send the job to the cluster. We can monitor the progress of the job using the 'Active Jobs' tab in BlueBEAR portal.

The `ntasks` line specifies we are looking to use 8 cores. The last line contains the filename we are sending to MATLAB to execute.

## Submitting multiple MATLAB jobs

!!! info
    Example contributed by Katharina Deucker

The previous example submits a single MATLAB job that uses `parfor` BlueBEAR, for larger analyses we may want to parallelise jobs across entire MATLAB instances. This can be done by submitting MATLAB jobs to BEAR using Slurm. The BEAR Technical Docs contain a simple example on [submitting a MATLAB job to BEAR](https://docs.bear.bham.ac.uk/bluebear/jobs/#an-example-job-script).

For neuroimaging analyses, you'll generally need to organise your scripts so that each part that you want to parallelise runs from a single function that takes a single ID as an argument. Here is a specific example that runs a function `e1_fun_ICA` on each of 48 datasets.

``` slurm
#!/bin/bash
#SBATCH --ntasks 1
#SBATCH --time 30:0
#SBATCH --mem 50G
#SBATCH --qos bbdefault
#SBATCH --array=1-48

set -eu

module purge; module load bluebear

# load the MATLAB version you need
module load MATLAB/2019b

# apply MATLAB script to each index in the array
# (the MATLAB script is programmed such that the input ID is used as the subject ID)
MATLAB -nodisplay -r "run /rds/homes/d/dueckerk/startup.m, e1_fun_ICA(${SLURM_ARRAY_TASK_ID}), quit"
```
