# R for statistical computing

**The [R project](https://www.r-project.org/) is a free software environment for statistical computing and graphics.**

## R Versions

[BEAR Apps](https://bear-apps.bham.ac.uk/applications/R/) has several versions of `R` as loadable modules.

## R-Studio GUI App

[RStudio](https://posit.co/products/open-source/rstudio/#rstudio-server) is an integrated development environment (IDE) for `R`. It includes a console, syntax-highlighting editor that supports direct code execution, and tools for plotting, history, debugging, and workspace management.

You can open an interactive RStudio session through the BEAR Portal. The pre-installed `R` versions can be loaded.

## Neuroimaging specific R packages

Here is a list of `R` packages commonly used for neuroimaging analysis.

### [FSLR](https://bear-apps.bham.ac.uk/applications/fslr/)

Wrapper functions that interface with 'FSL', a powerful and commonly-used 'neuroimaging' software, using system commands.

## R Example for BEAR

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(ggplot2)

# Simulate some data
time     <- 0:99
set.seed(1)
noise    <- rnorm(100)
disorder <- time * 4 + 100 + noise * 20
dis_df   <- data.frame(time, disorder)

# Create a plot
ggplot(dis_df, aes(x = time, y = disorder)) + geom_point() +
  geom_smooth(method = "lm")

# Fit model
lm_fit <- lm(disorder ~ time, dis_df)
summary(lm_fit)
```
