# EyeLink Demo Code

**<span style="color:maroon">Demo code for EyeLink setup, calibration, validation, drift checking and trigger sent during data acquiring.</span>** <br />
**Edited by Dr. Yali Pan.**

## MATLAB Code

```matlab
function Eyelink_Demo
%%%% Demo for eyelink setup, calibration, validation, drift checking and trigger sent during data acquiring
%%%%% edited by Yali Pan (Y.Pan.1@bham.ac.uk) 

%%%=====Open screen, the same screen for eyelink
screens = Screen('Screens'); % Get the screen numbers
cfg.screenNumber = max(screens); %select screen
cfg.ScrBgc = [0.5 0.5 0.5];
cfg.TextColor = [1 1 1];
%%%open PTB window
[window] = PsychImaging('OpenWindow', cfg.screenNumber, cfg.ScrBgc);
cfg.window = window;
%%%  Get the size of the on screen window and set resolution
sc_info = Screen('Resolution', cfg.screenNumber);
resx = sc_info.width;
resy = sc_info.height;
cfg.resx = resx;
cfg.resy = resy;

%%%=====Parameters for eyelink
cfg.el.Eyeused = 'LEFT_EYE';      %eye used
cfg.el.edffile = 'sub1.edf'; %EDF filename
%%% check file
%add eyelink script folder (should be in main experiment folder)
addpath([exp_dir filesep 'Eyelink']);
%make directory if it doesn't already exist (local computer)
cfg.el.eyedir = [exp_dir filesep 'Eyelink' filesep ];
if ~exist(cfg.el.eyedir, 'dir')
    mkdir(cfg.el.eyedir);
end
%check whether files already exist for this subject/session
if exist([exp_dir filesep 'Eyelink' filesep 'Data' filesep  cfg.el.edffile '.edf'],'file')>0
    cont = input('Warning! Eyelink file will be overwritten, do you want to continue? (y/n) ','s');
    if cont == 'n'
        error('Session aborted')
    end
end
cfg.el_rect = [0 0 resx resy]; %% needed for the el_Set_Params function

%%%=====Eyelink setup, calibration and validation
cfg = el_calib_valid(cfg,0);

%%%%===== Trigger: Experiment start message to eyelink
Eyelink('Message', 'sub1: Exp_start');

%%%%===== Trigger: Experiment triggers to eyelink
sendTrigger(cfg,1); %%% here the trigger is '1'

%%%=====Redo calibration and validation
cfg = el_calib_valid(cfg,1);

%%%=====Run EyelinkDoDriftCorrection
%%% enable eye drift checking !!!
Eyelink('Command', 'driftcorrect_cr_disable = NO');
el_calib_valid(cfg,2);
WaitSecs(0.1)

%%%======Stop eyelink & transfer file
Eyelink('Message', 'end of block');
el_Stop(cfg);

end

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function cfg = el_calib_valid(cfg,mode)
if mode == 0 %% run the eye-tracker setup for the first time
    %%% run el_Start
    cfg = el_Start_SameWindow(cfg);
    cfg.el.defaults.ScrBgc = cfg.ScrBgc;
    cfg.el.defaults.TextColor = cfg.TextColor;
elseif mode == 1 %% run the eye-tracker setup for the non-first time
    %%% re-calibration and re-validation and re-drift correction
    EyelinkDoTrackerSetup(cfg.el.defaults);
elseif mode == 2
    EyelinkDoDriftCorrection_pan(cfg.el.defaults);
    Eyelink('StartRecording');
    % record a few samples before we actually start displaying
    WaitSecs(0.1);
    % mark zero-plot time in data file
    disp('Sending message')
    Eyelink('Message', 'SYNCTIME');
end
%%% set screen to experiment background color
Screen('FillRect', cfg.window, cfg.ScrBgc)
Screen('Flip', cfg.window);
end

function cfg = el_Start_SameWindow(cfg)
% Used in FG experiment
% Using the main screen for calibration, calibrate and start recording

% STEP 1
% Provide Eyelink with details about the graphics environment
% and perform some initializations. The information is returned
% in a structure that also contains useful defaults
% and control codes (e.g. tracker state bit and Eyelink key values).
% Psychtoolbox defaults function
cfg.el.defaults = EyelinkInitDefaults(cfg.window);

% Disable key output to Matlab window:
ListenChar(2);

% STEP 2
% Initialization of the connection with the Eyelink Gazetracker.
% exit program if this fails.
if ~EyelinkInit
    fprintf('Eyelink Init aborted.\n');
    cleanup;  % cleanup function
    return;
else
    disp('Eyelink initizalized')
end

% open file to record data to
disp('Opening EDF file');
status = Eyelink('Openfile', cfg.el.edffile);

if ~status
    disp('EDF file opened on Eyelink computer')
else
    error(['Could not open EDF file on Eyelink computer, error: ' int2str(status)])
end

% set custom parameters
disp('Setting parameters')
cfg = el_Set_Params(cfg);

% STEP 3
% start recording eye position
disp('Start recording')
%sca
Eyelink('StartRecording');
% record a few samples before we actually start displaying
WaitSecs(0.1);
% mark zero-plot time in data file
disp('Sending message')
Eyelink('Message', 'SYNCTIME');
ListenChar(0);
end

function [cfg] = el_Set_Params(cfg)
%el_Set_Params 
%Custom parameter file for eyelink
el=cfg.el.defaults;
el.eye_used                = cfg.el.Eyeused;
el.calibrationtargetsize   = 1;
el.calibrationtargetwidth  = 0.5;
el.targetbeep              = 0;
el.feedbackbeep            = 0;
el.displayCalResults       = 1;
el.eyeimagesize            = 50;  % percentage of screen
el.backgroundcolour        = cfg.ScrBgc;

disp('Updating Parameters')
EyelinkUpdateDefaults(el);

cfg.el.defaults=el;
% make sure we're still connected.
if Eyelink('IsConnected')~=1
    warning('eyelink is not connected! restart the tracker');
    cleanup;
    return;
end
% make sure that we get gaze data from the Eyelink
Eyelink('Command', 'link_sample_data = LEFT,RIGHT,GAZE,GAZERES,AREA,STATUS,INPUT'); 

% This Command is crucial to map the gaze positions from the tracker to
% screen pixel positions to determine fixation
Eyelink('Command','screen_pixel_coords = %ld %ld %ld %ld',  cfg.el_rect(1)-cfg.el_rect(1), cfg.el_rect(2)-cfg.el_rect(2), cfg.el_rect(3)-cfg.el_rect(1), cfg.el_rect(4)-cfg.el_rect(2));
Eyelink('message','DISPLAY_COORDS %ld %ld %ld %ld',         cfg.el_rect(1)-cfg.el_rect(1), cfg.el_rect(2)-cfg.el_rect(2), cfg.el_rect(3)-cfg.el_rect(1), cfg.el_rect(4)-cfg.el_rect(2));

% Use Psychophysical setting
Eyelink('Command', 'recording_parse_type = GAZE');
Eyelink('Command', 'saccade_motion_threshold = 0.0');
Eyelink('Command', 'saccade_pursuit_fixup = 60');
Eyelink('Command', 'fixation_update_interval = 0');
%%% normal visual experiments
Eyelink('Command', 'saccade_velocity_threshold = 22');
Eyelink('Command', 'saccade_acceleration_threshold = 3800');
% % %%% YPan: changed accoording to the user mannual to be better for reading study
% % Eyelink('Command', 'saccade_velocity_threshold = 30');
% % Eyelink('Command', 'saccade_acceleration_threshold = 8000');

% Other tracker configurations
%% these might crash:
Eyelink('Command', 'heuristic_filter = 0');
Eyelink('Command', 'pupil_size_diameter = YES');

%use 9 point calibration (Default)
Eyelink('Command', 'calibration_type = HV9'); %%HV5,HV3

Eyelink('Command', 'generate_default_targets = YES');
Eyelink('Command', 'enable_automatic_calibration = YES');
Eyelink('Command', 'automatic_calibration_pacing = 1000');
Eyelink('Command', 'binocular_enabled = NO');
Eyelink('Command', 'use_ellipse_fitter = NO');
Eyelink('Command', 'sample_rate = 1000');
%Eyelink('Command', 'elcl_tt_power = %d', 2); % illumination, 1 = 100%, 2 = 75%, 3 = 50%

switch cfg.el.Eyeused
    case 'RIGHT_EYE'
        Eyelink('Command', 'file_event_filter = RIGHT,FIXATION,SACCADE,BLINK,MESSAGE,INPUT');
        Eyelink('Command', 'link_event_filter = RIGHT,FIXATION,FIXUPDATE,SACCADE,BLINK,MESSAGE,INPUT');
    case  'LEFT_EYE'
        Eyelink('Command', 'file_event_filter = LEFT,FIXATION,SACCADE,BLINK,MESSAGE,INPUT');
        Eyelink('Command', 'link_event_filter = LEFT,FIXATION,FIXUPDATE,SACCADE,BLINK,MESSAGE,INPUT');
end
Eyelink('Command', 'file_sample_data  = GAZE,GAZERES,HREF,PUPIL,AREA,STATUS,INPUT');

% Cleanup routine:
function cleanup
% Shutdown Eyelink:
    Eyelink('Shutdown');
    el.online = 0;
end
end

%function to send eyelink triggers
function [cfg] = sendTrigger(cfg,trig)
%send trigger to eyelink
if cfg.el.eyelink
    Eyelink('Message', ['Trigger_' int2str(trig)]);
end
end

function el_Stop(cfg)
el=cfg.el;
% finish up: stop recording eye-movements,
% close graphics window, close data file and shut down tracker
Eyelink('StopRecording');
Eyelink('CloseFile');
% download data file
fprintf('Receiving data file ''%s''\n', cfg.el.edffile);
%status=Eyelink('ReceiveFile');
status=Eyelink('ReceiveFile',cfg.el.edffile,cfg.el.eyedir,1); %transfer file to experiment directory
if status > 0
    fprintf('ReceiveFile status %d\n', status);
end
if 2==exist(cfg.el.edffile, 'file')
    fprintf('Data file ''%s'' can be found in ''%s''\n', cfg.el.edffile, cfg.el.eyedir );
end
cleanup;
end

% Cleanup routine:
function cleanup
% Shutdown Eyelink:
Eyelink('Shutdown');
% Restore keyboard output to Matlab:
ListenChar(0);
end
```