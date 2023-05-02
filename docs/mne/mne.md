# MNE Python

[MNE-Python](https://mne.tools/stable/index.html) is a Python package for analysing electrophysiology (MEG, EEG, sEEG, ECoG, NIRS, etc) data.

## MNE-Python Versions

[Bear Apps](https://bear-apps.bham.ac.uk/applications/MNE-Python/) has several versions of MNE-Python as modules.

## JupyterLab

Interactive python notebooks are available to run as a [JupyterLab GUI App](https://docs.bear.bham.ac.uk/portal/jupyterlab/) through the Bear Portal. The pre-installed MNE python versions can be [loaded as modules](https://docs.bear.bham.ac.uk/portal/jupyterlab/#loading-modules) in the notebook session.

Only the pre-installed modules available in [Bear Apps](https://bear-apps.bham.ac.uk/index) are installable in the JupyterLab GUI App.

## Bear GUI

The following bash loads mne version 1.3.1 and its dependencies.

``` shell
module load bear-apps/2022a
module load MNE-Python/1.3.1-foss-2022a
```

``` slurm
#!/bin/bash

module purge; module load bluebear
module load bear-apps/2021a/live
module load Python/3.9.5-GCCcore-10.3.0
module load IPython/7.25.0-GCCcore-10.3.0

export VENV_DIR="${HOME}/virtual-environments"
export VENV_PATH="${VENV_DIR}/osl-bigmeg-${BB_CPU}"

# Create master dir if necessary
mkdir -p ${VENV_DIR}
echo ${VENV_PATH}

# Check if virtual environment exists and create it if not
if [[ ! -d ${VENV_PATH} ]]; then
    python3 -m venv --system-site-packages ${VENV_PATH}
fi

# Activate virtual environment
source ${VENV_PATH}/bin/activate

# Any additional installations
pip install mne
```
