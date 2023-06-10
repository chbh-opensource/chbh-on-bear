# Use Conda to Manage Your Own Python Environments

Managing software dependencies can be one of the most annoying thing in scientific computing, 
especially when dealing with complex systems with multiple packages and libraries. 
This is where conda comes in - a package management system that simplifies the task of installing, configuring, 
and managing software packages and their dependencies.

BEAR systems does offer a default Python environment, but it must be loaded beforehand, 
and it does not allow you to install additional packages that are not already provided.
After creating your own Conda environment, you don't have to load them everytime. 
Submitting cluster jobs becomes straightforward with simple scripts, as demonstrated in this example:
```python
#!/bin/bash
set -e
#SBATCH settings

python your_script.py
```

If this seems interesting to you, let's get started!

## What is conda
Conda is a platform-agnostic package management system that can be used to install and manage software packages and their dependencies.
It is designed to work with multiple programming languages, including Python, R, and others.

Advantages of using conda:
* Build your own python env when you don't have `sudo` access
* Conda simplifies managing software packages and dependencies
* Conda allows for isolated environments for different projects or applications
* Conda facilitates switching between different package versions
* Conda provides access to a vast range of pre-built packages and libraries.

## How to install conda
First go to your home directory, and type:
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
# start installation
bash Miniconda3-latest-Linux-x86_64.sh
```
Follow the instructions on the screen to complete the installation (**You can just leave everything as default and it should be fine most of the time**).
After the installation is complete, you need to restart you kernel to load it, type:
```bash
exec bash
```
And you should see your terminal changed, for example from `[<usr>@bb-pg-login04 ~]$` to `(base) [<usr>@bb-pg-login04 ~]$`. 
This means you have a python environment called `base` is now active.
**Every time you logged in to BEAR this environment will be loaded automatically.** 
Now you can start using conda to manage your own python environments!

## Use `base` environment
If you accepted default setting when installing, the `base` environment is the default environment 
that is loaded everytime you start a terminal session.

You can install any packages you need in the `base` environment with `pip` or `conda` command.
For example, to install `numpy` and `scipy`:
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
**Congratulations! Now you can start use your own environments to do anything you like!** Simply type:
```bash
(base) [<usr>@bb-pg-login04 ~]$python your_script.py
# or 
(base) [<usr>@bb-pg-login04 ~]$python # to start a python shell
# or 
(base) [<usr>@bb-pg-login04 ~]$ipython # to start a ipython shell
```

## Crate Virtual Environments with Conda
In most cases, the `base` environment should be enough. 
But if you are working on multiple projects, especially when you have deep learning projects or you are developing a toolbox 
which might be sensitive to specific environmental conditions , it is important to take measures to ensure consistency and prevent any problems that could arise from changes in the environment.

Type the following command to create and enter a new environment:
```bash
conda create -n <name> python=3.10 ipykernel
conda activate <name>
# Now you will see your terminal became:
(<name>) [<usr>@bb-pg-login04 ~]$
# install the packages use the commands provided above
(<name>) [<usr>@bb-pg-login04 ~]$ pip install -r requirements.txt
# run your python scripts
(<name>) [<usr>@bb-pg-login04 ~]$ python your_script.py

# go back to base enviroment
(<name>) [<usr>@bb-pg-login04 ~]$ conda deactivate
(base) [<usr>@bb-pg-login04 ~]$ 
```

## Run your job on cluster
As I have indicated before, your bash script is very simple:
```bash
#!/bin/bash
# run_python.sh
set -e
#SBATCH --account <your account>
#other settings

python your_script.py
```
Then choose your perferred enviroment, let's say a enviroment called `neuroimaging`, type the following command:
```bash
(base) [<usr>@bb-pg-login04 ~]$ conda activate neuroimaging
(neuroimaging) [<usr>@bb-pg-login04 ~]$ sbatch run_python.sh
# check your output:
(neuroimaging) [<usr>@bb-pg-login04 ~]$ tail -f slurm-<id>.out 
Processing subj_id: CC222555:  24%|██▎       | 153/651 [08:42<28:37,  3.45
```
