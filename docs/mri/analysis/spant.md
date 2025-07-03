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

Or the the development version from GitHub (requires the devtools package):

```
install.packages("devtools")
devtools::install_github("martin3141/spant", ref = "devel", dependencies = TRUE)
```

Note, installing for the first time will require compilation of various packages and will take some time.

## Batch use

TODO