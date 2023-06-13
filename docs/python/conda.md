# Use Conda to Manage Your Own Python Environments

Managing software dependencies can be one of the most annoying things in scientific computing,
especially when dealing with complex systems with multiple packages and libraries.
This is where conda comes in - a package management system that simplifies the task of installing, configuring,
and managing software packages and their dependencies.

BEAR system does offer a default Python environment, but it must be loaded beforehand,
and it does not allow you to install additional packages that are not already provided.
After creating your own Conda environment, you don't have to load them every time.
Submitting cluster jobs becomes straightforward with simple scripts, as demonstrated in this example:

```bash
#!/bin/bash
set -e
#SBATCH settings
python your_script.py
```

!!! note BEAR [do not currently recommend using conda for installing Python packages](https://docs.bear.bham.ac.uk/bluebear/software/self_installs_python/#tips). This is due to possible performance issues when installing packages with conda. BEAR recommend that you get in touch with them prior via an IT-ticket to performing intensive analyses using conda environments.

If this seems interesting to you, or you need to use a custom environment, let's get started!

## What is conda

Conda is a platform-agnostic package management system that can be used to install and manage software packages and their dependencies.
It is designed to work with multiple programming languages, including Python, R, and others.

Advantages of using conda:

* Build your own Python env when you don't have `sudo` access
* Conda simplifies managing software packages and dependencies
* Conda allows for isolated environments for different projects or applications
* Conda facilitates switching between different package versions
* Conda provides access to a vast range of pre-built packages and libraries.

## How to install conda

First, go to your home directory and type:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
# start installation
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the instructions on the screen to complete the installation (**You can just leave everything as default, it should be fine most of the time**).
After the installation is complete, you need to restart your kernel to load it, type:

```bash
exec bash
```

And you should see your terminal changed, for example from `[<usr>@bb-pg-login04 ~]$` to `(base) [<usr>@bb-pg-login04 ~]$`.
This means you have a Python environment called `base` that is now active.
Now you can start using conda to manage your own Python environments!

## Use `base` environment

If you accepted the default setting when installing, the `base` environment is the default environment,
**Every time you logged in to BEAR this environment will be loaded automatically.**

You can install any packages you need in the `base` environment with `pip` or `conda` command.
For example, to install `matplotlib` and `scipy`:

```bash
conda install -c conda-forge matplotlib=3.5.2 scipy
# or
pip install matplotlib==3.5.2 scipy
```

If you have the requirements.txt from the projects you are working with:

```bash
pip install -r requirements.txt
# or 
conda install --file requirements.txt
```

After installing the packages, you can check the list of packages installed in the `base` environment with:

```bash
conda list
# or 
pip list
```

**Congratulations! Now you can start using your own environment to do anything you like!** Simply type:

```bash
(base) [<usr>@bb-pg-login04 ~]$ python your_script.py
# or 
(base) [<usr>@bb-pg-login04 ~]$ python # to start a python shell
# or 
(base) [<usr>@bb-pg-login04 ~]$ ipython # to start a ipython shell
```

## Crate Virtual Environments with Conda

In most cases, the `base` environment should be enough.
But if you are working on multiple projects, especially when you have deep learning projects or developing a toolbox
that might be sensitive to specific environmental conditions, it is important to take measures to ensure consistency and prevent any problems that could arise from changes in the environment.

Type the following command to create and enter a new environment:

```bash
(base) [<usr>@bb-pg-login04 ~]$ conda create -n <name> python=3.10 ipykernel
(base) [<usr>@bb-pg-login04 ~]$ conda activate <name>
# Now you will see your terminal became:
(<name>) [<usr>@bb-pg-login04 ~]$
# install the packages using the commands provided above
(<name>) [<usr>@bb-pg-login04 ~]$ pip install -r requirements.txt
# run your Python scripts
(<name>) [<usr>@bb-pg-login04 ~]$ python your_script.py

# Go back to the base environment
(<name>) [<usr>@bb-pg-login04 ~]$ conda deactivate
(base) [<usr>@bb-pg-login04 ~]$ 
```

## Run your job on the cluster

As I have indicated before, your bash script is very simple:

```bash
#!/bin/bash
# run_python.sh
set -e
#SBATCH --account <your account>
#other settings

python your_script.py
```

Then choose your preferred environment, let's say an environment called `neuroimaging`, and type the following command:

```bash
(base) [<usr>@bb-pg-login04 ~]$ conda activate neuroimaging
(neuroimaging) [<usr>@bb-pg-login04 ~]$ sbatch run_python.sh
# check your output:
(neuroimaging) [<usr>@bb-pg-login04 ~]$ tail -f slurm-<id>.out 
Processing subj_id: CC222555:  24%|██▎       | 153/651 [08:42<28:37,  3.45
```
