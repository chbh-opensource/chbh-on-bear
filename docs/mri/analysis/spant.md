# Using spant on BEAR

## Interactive use

- Navigate to : [https://portal.bear.bham.ac.uk](https://portal.bear.bham.ac.uk)
- Navigate to the "Interactive Apps" tab and select "RStudio Server".
- Set "Number of hours" to the duration of the session.
- Set "Number of cores" to 4 to allocate 16 GB of memory.
- Press "Launch".

### Installing spant for the first time

Type the following in the Console (lower left panel) to install the latest stable version of spant:

```
install.packages("spant", dependencies = TRUE)
```

Or the development version from GitHub (requires the devtools package):

```
install.packages("remotes")
remotes::install_github("martin3141/spant", ref = "devel", dependencies = TRUE)
```

Note, installing for the first time will require compilation of various packages and will take some time.

The following commands should also be run to install the requried dependencies for voxel tissue segmentation:

```
spant::install_ants()
spant::install_oasis_template()
spant::install_faceoff()
```


## Batch use

The following modules are required to use spant on BlueBEAR:

```
module load bear-apps/2024a
module load R/4.5.0-gfbf-2024a
module load R-bundle-CRAN/2025.06-foss-2024a
```

The following command bash command should be run once to reduce the chances of write errors:

```
echo "TMPDIR=/scratch/$USER" >> $HOME/.Renviron
```

