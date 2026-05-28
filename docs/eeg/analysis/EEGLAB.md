# EEGLAB Quick Guide

!!! note
    This example demonstrates a simple local EEGLAB preprocessing workflow using MATLAB.

<b>This guide shows how to install and run EEGLAB locally using MATLAB.</b>

---

## Downloading EEGLAB

1. Go to the official [EEGLAB download page](https://eeglab.org/download/)
2. Download the latest version of EEGLAB (or Cloning EEGLAB from GitHub)
3. Extract the downloaded `.zip` file
4. Place the folder somewhere accessible

---

## Launching EEGLAB in MATLAB

Open MATLAB and add the EEGLAB folder to your MATLAB path.

You can use either the **GUI interface (recommended for beginners)** or **run scripts** directly.

```matlab
addpath('/Users/yourname/Documents/MATLAB/eeglab')
eeglab
```

This will open the EEGLAB graphical user interface, where you can:

- Import EEG data
- Filter signals
- Run ICA
- Reject artefacts interactively
- Epoch data
- Visualise data and components

---
## Processing flow diagram

```text
RECOMMENDED PIPELINE

Raw continuous EEG
        ↓
Filtering (HP / LP / Notch)
        ↓
ICA decomposition (runica)
        ↓
Remove artefactual components
        ↓
Epoching (event-related segmentation)
        ↓
Baseline correction
        ↓
Trial rejection / quality check
        ↓
Statistical analysis (ERP / time-frequency)
```

---

## Core preprocessing script

You can also run EEGLAB in script mode for reproducibility.

Save as `basic_preprocessing_eeglab.m`:

```matlab
%% Basic EEGLAB Preprocessing

eeglab;

%% Load Dataset
EEG = pop_loadset('example_data.set');
EEG = eeg_checkset(EEG);

%% Filtering
EEG = pop_eegfiltnew(EEG, 'locutoff', 1);   % high-pass
EEG = pop_eegfiltnew(EEG, 'hicutoff', 40);  % low-pass

%% Re-reference (recommended BEFORE ICA)
EEG = pop_reref(EEG, []);

%% Run ICA (on continuous data)
EEG = pop_runica(EEG, ...
    'icatype', 'runica', ...
    'extended', 1);

%% Remove ICA components (example)
EEG = pop_subcomp(EEG, [1 3], 0);

%% Epoch data (AFTER ICA cleaning)
EEG = pop_epoch(EEG, {'stimulus'}, [-0.2 0.8]);

%% Baseline correction
EEG = pop_rmbase(EEG, [-200 0]);

%% Save dataset
EEG = pop_saveset(EEG, ...
    'filename', 'example_data_preprocessed.set');

disp('Preprocessing complete.')
```

---

## Running the script

Open MATLAB and run:

```matlab
basic_preprocessing_eeglab
```

Or click the **Run** button inside the MATLAB editor.

---

## Simple ERP plotting

After epoching and baseline correction, you can compute and visualise ERP (Event-Related Potentials).

This approach computes the mean across trials and plots a selected channel.

```matlab
%% Compute ERP (average across trials)

% select channel of interest (example: Cz)
chan_idx = find(strcmp({EEG.chanlocs.labels}, 'Cz'));

% extract data: channels × time × trials
data = squeeze(EEG.data(chan_idx, :, :));

% compute ERP (average across trials)
erp = mean(data, 2);

% plot ERP
figure;
plot(EEG.times, erp, 'LineWidth', 2);
xline(0, '--k');
yline(0, ':k');

xlabel('Time (ms)');
ylabel('Amplitude (\muV)');
title('ERP at Cz');
```

---

## Useful EEGLAB functions

| Function | Purpose |
|---|---|
| `pop_loadset` | Load EEGLAB dataset |
| `pop_eegfiltnew` | Apply filters |
| `pop_epoch` | Create epochs |
| `pop_rmbase` | Baseline correction |
| `pop_runica` | Run ICA |
| `pop_reref` | Re-reference EEG |
| `pop_saveset` | Save dataset |

---

## Useful links

- [EEGLAB Official Website](https://eeglab.org)
- [EEGLAB Tutorials](https://eeglab.org/tutorials/)
- [MATLAB Documentation](https://www.mathworks.com/help/matlab/)