# Containers

A container is a lightweight enviroment that contains both the software, and all of the depencies needed to run the software. This makes containers great for reproducability. Containers are packaged enviroments containing both code and all the required dependencies. On Bluebear, a program called Singularity is used to both manage and run containers.

## Where to find containers


## Downloading a Container
Containers can be found  here... In this example we will download the fMRI prep container.  This container includes all of the neuroimaging software required to run fMRIprep, such as freesurfer, FSL, and ANTS. 
https://hub.docker.com/r/nipreps/fmriprep

The following script can be used to download the container.

```
This is some code that i ne
```

### Running Code within the Container

singularity shell
singularity run
singularity exec
singularity pull
singularity clone

## Creating your own container
Sometimes you may want to build a container yourself that contains all the analysis software required. One option is to use a program called `Neurodocker`. This allows you to select from a list of various neuroimaing packages, as well as installing python packages etc. 


