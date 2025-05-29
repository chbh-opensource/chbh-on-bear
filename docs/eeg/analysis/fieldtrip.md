# Fieldtrip on Slurm

!!! note
    Example contributed by [Ben Griffiths](https://www.benjaminjamesgriffiths.com/).

<b>This is an example script running a fieldtrip analysis on EEG data acqurired during a visual flicker task.</b>

The data is read in, filtered, epoched, ICA'd, re-referenced, then plotted. The core function can be executed on the [MATLAB GUI App](https://docs.bear.bham.ac.uk/portal/gui_apps/) during an interactive session, or submitted to BlueEBAR using the `bash` script below.

## Core processing script

The following code can be saved as `basic_preprocessing.m`.

``` matlab
%% Basic Preprocessing
% A script to demonstrate how one can (superficially) preprocessing EEG
% data using Fieldtrip, Matlab and BlueBEAR.
%
% Benjamin J. Griffiths (b.griffiths.1 [at] bham.ac.uk)
% 28th March 2023

%% Prepare Workspace
% define root directory where data is stored
root_dir = '/rds/projects/g/griffibz-example-project/msc-eeg-23/';

% add fieldtrip to path
addpath('/rds/projects/g/griffibz-example-project/fieldtrip/')
ft_defaults

% define participant number
subj = 1;

%% Filter Raw Data
% load data
cfg         = [];
cfg.dataset = sprintf('%s/bids/sub-%02.0f/eeg/sub-%02.0f_task-eeg-flicker_eeg.eeg', root_dir, subj, subj); % dynamically determine dataset name
data        = ft_preprocessing(cfg);

% remove external and trigger channels
cfg         = [];
cfg.channel = {'all', '-EX*', '-Status'}; % select all channels except any external (-EX*) or trigger (-Status) channel
data        = ft_selectdata(cfg, data);

% filter data
cfg             = [];
%cfg.hpfilter    = 'yes';   % apply high-pass filter
%cfg.hpfreq      = 0.8;     % use high-pass to suppress frequencies < 0.8Hz
cfg.lpfilter    = 'yes';   % apply low-pass filter
cfg.lpfreq      = 120;     % use low-pass to suppress frequencies > 120Hz
cfg.bsfilter    = 'yes';   % apply band-pass filter
cfg.bsfreq      = [49 51]; % use band-pass to suppress frequencies netween 49Hz and 51Hz
data            = ft_preprocessing(cfg, data);

%% Epoch Data
% load in BIDS event file
events = readtable(sprintf('%s/bids/sub-%02.0f/eeg/sub-%02.0f_task-eeg-flicker_events.tsv', root_dir, subj, subj),'Filetype','text'); % dynamically determine dataset name

% define Fieldtrip-style event structure
trl_start = -2; % start trial 2 seconds before trigger
trl_end = 4; % end trial 4 seconds after trigger
trl_def(:,1) = events.sample + (trl_start * data.fsample); % define samples to start trial
trl_def(:,2) = events.sample + (trl_end * data.fsample); % define samples to end trial
trl_def(:,3) = trl_start * data.fsample; % define when time = 0 occurs relative to start of trial

% epoch data
cfg = [];
cfg.trl = trl_def;
data = ft_redefinetrial(cfg, data);

% load in trialinfo
load(sprintf('%s/bids/sourcedata/sub-%02.0f_trialinfo.mat', root_dir, subj))
data.trialinfo = trialinfo; % add trialinfo to data structure

% tidy workspace
clear events trl_start trl_end trl_def trialinfo

%% Run ICA
% restrict to retrieval trials
cfg         = [];
cfg.trials  = find(cellfun(@(x) strcmpi(x.trl_type, 'retrieval'), data.trialinfo));
data        = ft_selectdata(cfg, data);

% reduce sample rate
cfg = [];
cfg.resamplefs = 256; % drop sample rate from 1024Hz to 256Hz
data = ft_resampledata(cfg, data);

% run ica
rng(subj) % set random seed to ensure reproducible outputs every time the function is run
ica = ft_componentanalysis([], data); % "cfg" need not be defined if using default settings

% visualise first 20 components (commented to stop execution when running via Slurm)
%ft_topoplotIC(struct('component',1:20,'layout','biosemi128.lay'), ica)

% remove components
cfg             = [];
cfg.component   = [1 3]; % 1 = eyeblink, 3 = saccade
data            = ft_rejectcomponent(cfg, ica);

%% Re-reference Data
% re-reference to the average of all channels
cfg = [];
cfg.reref = 'yes';
cfg.refchannel = 'all';
data = ft_preprocessing(cfg, data);

%% Plot Results
% get timelocked average of data
cfg = [];
cfg.channel = 'A*'; % restrict to posterior quadrant of channels
tml = ft_timelockanalysis(cfg, data);

% baseline correct timelocked average
cfg = [];
cfg.baseline = [-0.25 -0.05]; % set baseline as -250ms to -50ms
tml = ft_timelockbaseline(cfg, tml);

% plot ERP
h = figure;
subplot(2,1,1); hold on
plot(tml.time, mean(tml.avg))
xlim([-0.5 2.5])
xline(0,'k--')
yline(0,'k-')
xlabel('Time (s)')
ylabel('Amplitude (uV)')
title('Visual Evoked Potential')

% cycle through trials
pow = cell(8, 1); % create empty cells for eight conditions
for trl = 1 : numel(data.trial)
    condition = data.trialinfo{trl}.ret_freq; % determine flicker condition
    channels_A = cellfun(@(x) strncmpi(x, 'A', 1), data.label); % identify posterior channels
    signal = data.trial{trl}(channels_A, :); % extract signal over posterior channels
    pow{condition}(end+1,:) = mean(abs(fft(signal')')); % compute FFT
end

% determine frequencies of FFT
freqs = linspace(0, data.fsample, size(pow{1},2));

% plot FFT for each condition
subplot(2,1,2); hold on
for condition = 1 : numel(pow)
    plot(freqs,mean(pow{condition}));
end
xlim([6, 42])
ylim([0, 700])
title('Power Spectrum')
xlabel('Frequency (Hz)')
ylabel('Power (arb. units)')
legend({'60Hz','40Hz','30Hz','24Hz','20Hz','17.1Hz','15Hz','Baseline'})

% save figure in root directory
saveas(h, sprintf('%s/basic_preproc_output.jpg', root_dir))
```

## Cluster submit script

The following can be saved as a shell script and submitted to the cluster using `sbatch`.

``` bash
#!/bin/bash

#SBATCH --ntasks 10
#SBATCH --nodes 1
#SBATCH --time 1:0:0
#SBATCH --qos bbdefault
#SBATCH --mail-type ALL

set -e

module purge; module load bluebear
module load MATLAB/2021b

matlab -nodisplay -r "basic_preprocessing; exit;"
```
