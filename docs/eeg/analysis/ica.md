# Automated ICA labelling

!!! note
    Example contributed by [Simon Marchant](https://github.com/simonmarchant).

A standard part of EEG pre-processing is removal of artefacts using ICA. Independent Component Analysis (ICA) decomposes the EEG signal into components (hence the name) which can be labelled as originating from the brain or originating from noise. You can label these manually, and [this](https://labeling.ucsd.edu/tutorial/labels) tutorial can be helpful for that. Alternatively, you can label components automatically. Several algorithms are available for this; below is a script which runs the MNE implementation of the ICAlabel algorithm.

## Automatic component labelling

You can run the script with the command `python ICAlabeller.py <subject ID>` (replacing `<subject ID>` with the ID you use for your participant). The script finds all of the runs in the folder you give in `run_naming_pattern` (this may just be one, depending on how you structured your experiment). It re-labels some channels that the CHBH EEG system records but that MNE mis-labels. It concatenates the runs together and runs ICA on the concatenated EEG, then it runs the ICAlabel classifier on these components. Finally, it saves the components and the labels so that you can check them yourself.

``` python
import mne
from mne.preprocessing import ICA
import mne_icalabel
import argparse
import pandas as pd
import glob

# This part just deals with your input argument (should be the participant ID)
parser = argparse.ArgumentParser(
                    prog='ICAlabeller',
                    description='Fits ICA and classifies artefacts in EEG files.')
parser.add_argument('subjID', type=str, help='Subject ID (3 digits)')

# Load EEG file(s)
data_path = '<your_project_folder_here>/Data/'
subjID = parser.parse_args().subjID
montage = mne.channels.make_standard_montage('biosemi128')
run_naming_pattern = f'{data_path}{subjID}/results/eeg/{subjID}_*.bdf'
BDF_FILES = sorted(glob.glob(run_naming_pattern))

all_raws = []
for file_idx, bdf_file in enumerate(BDF_FILES):
    print(f"Started processing {bdf_file}")
    raw = mne.io.read_raw_bdf(bdf_file, preload=True, verbose=False)
    raw.set_channel_types({'EXG1': 'misc','EXG2': 'misc','EXG3': 'misc','EXG4': 'misc',
                            'EXG5': 'misc','EXG6': 'misc','EXG7': 'misc','EXG8': 'misc',
                            'GSR1': 'misc', 'GSR2': 'misc', 'Erg1': 'misc', 'Erg2': 'misc',
                            'Resp': 'misc', 'Plet': 'misc', 'Temp': 'misc'})
    raw.set_montage(montage, on_missing='warn')
    raw.set_eeg_reference('average', projection=False, verbose=False) # projection=False applies re-ref immediately, no separate save
    all_raws.append(raw)

raw_concat = mne.concatenate_raws(all_raws)
filtered = raw_concat.copy().filter(l_freq=1.0, h_freq=100.0)

# Fit ICA, run classification
ica = ICA(n_components=60, max_iter='auto', method='infomax', random_state=97, fit_params=dict(extended=True))
ica.fit(filtered)
ic_labels = mne_icalabel.label_components(filtered, ica, method="iclabel")

# Save 
ica.save(f'./{subjID}-ica.fif', overwrite=True)
components_df = pd.DataFrame({ # Alternatively icalabel includes a write_components_tsv method if you have a full BIDS directory
    'component': range(ica.n_components_),
    'type': ic_labels['labels'],
    'description': [f"ICLabel confidence: {prob:.3f}" 
                    for prob in ic_labels['y_pred_proba']],
    'status': ['bad' if i in ica.exclude else 'good' 
               for i in range(ica.n_components_)],
    'ic_type_confidence': ic_labels['y_pred_proba'],
    'manual_notes': [''] * ica.n_components_
})
components_df.to_csv(f'{subjID}_components.tsv', sep='\t', index=False)
```

## Cluster submit script

ICA can be computationally expensive, and so you may want to run it on BEAR by using Slurm. The following example shows a shell script that you can use to run `ICAlabeller.py` on BEAR. It installs ICAlabel in a virtual environment before running the python file. You can save this as run_ICAlabel.sh and then run it on BEAR using the command `sbatch run_ICAlabel.sh <subject_ID>`.

``` bash
#!/bin/bash

#SBATCH --qos bbdefault
#SBATCH --time 90
#SBATCH --nodes 1 # ensure the job runs on a single node
#SBATCH --ntasks 40

if [ "$#" -ne 1 ]; then
    echo "Must provide the subject ID to $0. Example: $0 001"
    exit 1
fi

set -e

module purge; module load bluebear
module load bear-apps/2023a
module load MNE-Python/1.7.1-foss-2023a
module load PyTorch/2.1.2-foss-2023a

# Create & activate virtual environment
export VENV_DIR="${HOME}/<your_project_folder_here>/Preprocessing/EEG_ICA/virtual-environments"
export VENV_PATH="${VENV_DIR}/EEG-ICA-python3-11-3-${BB_CPU}"
mkdir -p ${VENV_DIR}
if [[ ! -d ${VENV_PATH} ]]; then
    python3 -m venv --system-site-packages ${VENV_PATH}
fi
source ${VENV_PATH}/bin/activate

# Install ICAlabel (fix the version so that it uses existing install, if present)
PIP_CACHE_DIR="/scratch/${USER}/pip"
pip install mne-icalabel[ica,gui]==0.8.1

# Check that everything compiled correctly (outputs to terminal; errors in case of problem)
mne_icalabel-sys_info
echo "Using virtual environment at $VENV_PATH"

python ICAlabeller.py "$1"

echo "Done."
```

## Checking your labels
Once you have your components and labels saved, you can check them using the following code. This is not computationally intensive so you can do this in a python prompt or jupyter notebook on your own computer.

``` python
import mne
import pandas as pd

# Load everything (replace the appropriate bits with your own filenames)
ica = mne.preprocessing.read_ica('<subject ID>.-ica.fif')
components_df = pd.read_csv('<subject ID>_components.tsv', sep='\t')
eeg = mne.io.read_raw_bdf('<filename>.bdf', preload=True)

# Plot properties for each component individually (change picks to display different components)
ica.plot_properties(eeg, picks=range(30))
```