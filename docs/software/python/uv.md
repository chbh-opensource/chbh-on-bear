# Using uv to manage dependencies and environments

[uv](https://docs.astral.sh/uv/) is a python package and project management tool that helps with consistency and reproducibility. It makes it easier for others (and yourself) to setup and run your code without worrying about differences between versions and dependency issues. 

Instead of using `pip` and a `requirements.txt`, uv creates a `uv.lock` and `pyproject.toml` file to keep track and manage package versions. These files can be version controlled using git.

uv is compatible with `pip` but is 10x-100x faster. It aims to replace similar dependency management tools (`pip`, `pyenv`, `poetry`, `virtualenv`, etc.) 

## Installing uv

If you are running things on BEAR, you can [install uv to your home folder](https://docs.bear.bham.ac.uk/bluebear/software/self_installs_python/).

For example, go to your home folder (`cd ~/` in the terminal) and then run:

```shell
curl -LsSf https://astral.sh/uv/install.sh | sh` 
```

Further installation instructions, e.g., for Mac or Windows, can be found on the [uv website](https://docs.astral.sh/uv/getting-started/installation/).

## Initial setup

Once you have uv installed, you need to setup a project in your project's folder. 

In the terminal run:

```shell
uv init
```

This will create a universal lock file `uv.lock` and a `pyproject.toml` file to help manage the packages and dependencies used.

The [`pyproject.toml`](https://docs.astral.sh/uv/guides/projects/) contains metadata about your project, such as the packages required, project name and description, development tools used (e.g., formatters), etc.

The [`uv.lock`](https://docs.astral.sh/uv/concepts/projects/sync/) file keeps a record of all the packages used and their specific versions and dependencies.

> uv.lock is a cross-platform lockfile that contains exact information about your project's dependencies. Unlike the pyproject.toml which is used to specify the broad requirements of your project, the lockfile contains the exact resolved versions that are installed in the project environment. This file should be checked into version control, allowing for consistent and reproducible installations across machines.

These files can be version controlled using git, so you can keep track of when you changed versions, added packages, etc.

## Installing packages

To install packages, use `uv add <package-name>`, for example `uv add numpy`. This will automatically install the package and any dependencies, and make sure that it does not conflict with other packages installed.

## Syncing/creating virtual environments

To create a virtual environment based on the uv.lock and pyproject.toml files, run in the terminal:

```shell
uv sync
```

This will create a virutal environment and install the required packages (defaults to `.venv`) .

If a `.venv` folder already exists, it will sync/update the packages to match the versions required.

To activate the virtual environment, run `source .venv/bin/activate`.

!!!Note
    A virtual environment created on Linux will not work on Mac or Windows. In this case, delete the .venv folder and use `uv sync` to rebuild it on your local machine.

## Running a python file

To run a python file, use `uv run <python-file>.py` where "python-file" is the name of the file you want to run (e.g., `main.py`).

Using uv to run the file, rather than `python <python-file>.py`, will check that all the correct packages are installed and the correct version. It will even create and setup the virtual environment if it doesn't exist!

## Running files on BEAR

When running scripts on BEAR, you will first need to load any modules you will be using. For example, in the terminal:

```bash
module purge
module load bluebear
module load bear-apps/2024a
module load Python/3.12.3-GCCcore-13.3.0
```

You can put this into a script, for example called `setup_bear.sh`:

```bash
#!/bin/bash

# set up bluebear
set -e
module purge
module load bluebear
module load bear-apps/2024a
module load Python/3.12.3-GCCcore-13.3.0
```

You can then run `source setup_bear.sh` in the terminal and it will setup setup the modules for you.

```bash
[vogelt@bear-pg0201u17a example-project]$ source setup_project_bear.sh 
Detected OS: RedHatEnterprise 8.10
GCCcore/13.3.0
zlib/1.3.1-GCCcore-13.3.0
binutils/2.42-GCCcore-13.3.0
bzip2/1.0.8-GCCcore-13.3.0
ncurses/6.5-GCCcore-13.3.0
libreadline/8.2-GCCcore-13.3.0
Tcl/8.6.14-GCCcore-13.3.0
SQLite/3.45.3-GCCcore-13.3.0
XZ/5.4.5-GCCcore-13.3.0
libffi/3.4.5-GCCcore-13.3.0
OpenSSL/3
Python/3.12.3-GCCcore-13.3.0
```

Once the modules are loaded, you can activate the virtual environment and edit/run your code, e.g., in an interactive session.

More commonly, you will want to submit a job using to the cluster and run it through a sbatch script. An example may look like:

```bash
#!/bin/bash
#SBATCH --account vogelt-example-project
#SBATCH --qos bbdefault

# set up bluebear
set -e
module purge
module load bluebear
module load bear-apps/2024a
module load Python/3.12.3-GCCcore-13.3.0

uv run main.py
```

`uv run` will automatially activate the virtual environment, install/sync any packages if necessary (matching the versions listed in the pyproject.toml and uv.lock files), and run the python script.
