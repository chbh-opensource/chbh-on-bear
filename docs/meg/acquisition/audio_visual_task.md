# Audio/Visual Task

This **<span style="color:maroon">MATLAB</span>** function is a simple test of the audio-visual setup in **Psychotoolbox(PTB)** using the **io64-module** for **parallel port triggering**.

It uses information taken from **[Stimulus Delivery & Triggering](../stimulus/stimulus_delivery.md)**

**<span style="color:maroon">basicAudioVisualTask</span>** - code below.

<span style="color:maroon">"As the name implies, it’s very ‘basic’. The ’task’ is simply to count the number of times the red fixation cross changes colour to green (trigger=32). 
But this is just to keep the subject occupied, the main objective is to acquire simple **ERF**’s (**E**vent-**R**elated **F**ields's) to the 4 visual quadrant checkerboards (triggers 3-6) and the L/R auditory bips (triggers 1/2)"</span>

!!! Info "The MEG Stim PC, *CHBH-ST-MEG-W02*, is running Windows 10 (64-bit), so 64-bit versions of the following files are used.<br /> 32-bit versions are available if required - contact MEG Support."

The following files are also required ...

* **[io64.mexw64](../../meg/files/io64.mexw64)**
* **[inpoutx64.dll](../../meg/files/inpoutx64.dll)**
* **<span style="color:blue">intialiseParallelPort.m</span>** - code found in **[Stimulus Delivery & Triggering](../stimulus/stimulus_delivery.md)**
* **[Tone_1kHz_100ms_hanning_left.wav](../../meg/files/Tone_1kHz_100ms_hanning_left.wav)** - ***right-click, "Save link as ..."***
* **[Tone_1kHz_100ms_hanning_right.wav](../../meg/files/Tone_1kHz_100ms_hanning_right.wav)** - ***right-click, "Save link as ..."***

**<span style="color:blue">basicAudioVisualTask.m</span>**

```matlab
function basicAudioVisualTask()
% simple test of audio-visual setup on PTB
% using io64-module for parallel port triggers
% 
% Revision history:
% - created on 20 Jan 2018, cjb
%
% Copyright 2018 Christopher J. Bailey under the MIT License
%
% Permission is hereby granted, free of charge, to any person obtaining a
% copy of this software and associated documentation files (the
% "Software"), to deal in the Software without restriction, including
% without limitation the rights to use, copy, modify, merge, publish,
% distribute, sublicense, and/or sell copies of the Software, and to
% permit persons to whom the Software is furnished to do so, subject to
% the following conditions:
% 
% The above copyright notice and this permission notice shall be included
% in all copies or substantial portions of the Software.
% 
% THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
% OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
% MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
% IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
% CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
% TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
% SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
%
% Parts of this code are copied from the Psychtoolbox examples,
% Copyright Psychtoolbox developers under the MIT License, see
% https://github.com/Psychtoolbox-3/Psychtoolbox-3/blob/master/Psychtoolbox/License.txt


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Find out which device to use; ASIO is a must, but there may be several
% For Creative-cards, got to the Control Panel-app, and find the
% 'Wave Device' under 'Device Information'
% To list all devices seen by PortAudio,
% >> all_audio_devs = PsychPortAudio('GetDevices');
% >> disp({all_audio_devs(:).DeviceName})

ASIO_DEV_NAME = 'Xonar DS ASIO(64)';
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% For developing, use a non-ASIO device if you like
% ASIO_DEV_NAME = 'DisplayPort';
skipSyncTest = 0;  % 1==don't test sync quality (fails without proper card)
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Aarhus-specific volume limit: set to 1 if you want 
% scale_max_volume_to = 0.563;
scale_max_volume_to = 0.25;  % CAREFUL YOU DON'T BLOW OUT AN EARDRUM!! TEST LEVEL ON YOURSELF FIRST!!
% scale_max_volume_to = 1.0;  % full blast out of the soundcard--DANGERZONE
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Paradigm parameters
minISI = 0.5;
maxISI = 0.8;
nStim = 120;  % stimuli / type
nStimFrames = 6;  % frames on; 6 == 50 ms @ 120 Hz

nTargetFrames = 12;  % 100 ms @ 120 Hz
nTargets = 10;  % targets in total
fixC = [140, 0, 0];
targetC = [0, 140, 0];

% trig_codes.audL = 128;
trig_codes.audL = 3;
trig_codes.audR = 5;
trig_codes.sefL = 16;
trig_codes.sefR = 32;
trig_codes.visUR = 1;
trig_codes.visLR = 2;
trig_codes.visLL = 4;
trig_codes.visUL = 8;
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% For developing/testing, including latency
Debug=0;
useAudio = 1;
latencyTest = 0;  % set to 1 for untapered 1kHz sinusoid (100 ms)
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%% DO NOT MODIFY BELOW HERE

% Force GetSecs and WaitSecs into memory to avoid latency later on:
GetSecs;
WaitSecs(0.1);

if useAudio
    InitializePsychSound(1);  % 1 = reallyneedlowlatency

    if ~latencyTest
        leftWav = 'Tone_1kHz_100ms_hanning_left.wav';
        % leftWav = 'leftChan-1000Hz-50ms-48kHz.wav';
        rightWav = 'Tone_1kHz_100ms_hanning_right.wav';
        % rightWav = 'rightChan-1000Hz-50ms-48kHz.wav';

        % Read WAV files from filesystem:
        [yL, freqL] = psychwavread(leftWav);
        [yR, freqR] = psychwavread(rightWav);
        % See PTB sound demos for resampling to 48 kHz!

        assert(freqL == freqR, 'Left and right channel rates must be equal')
        freq = freqL;
        assert(size(yL, 2) == 2, 'All WAV files must be stereo (L is not)')
        assert(size(yR, 2) == 2, 'All WAV files must be stereo (R is not)')

        audL = yL' / (max(yL(:, 1)) / scale_max_volume_to);
        audR = yR' / (max(yR(:, 2)) / scale_max_volume_to);
    else
        % For latency testing:
        % Generate some beep sound 1000 Hz, 0.1 secs, 50% amplitude:
        freq = 48000;
        audL(1,:) = 0.5 * MakeBeep(1000, 0.1, freq);
        audL(2,:) = zeros(size(audL));
        audR(1,:) = audL(2,:);
        audR(2,:) = audL(1,:);
    end
    
    nrchannels = 2;  % fix to stereo
    
    % win_asio_devs = PsychPortAudio('GetDevices', 3);
    all_audio_devs = PsychPortAudio('GetDevices');
    DeviceIndex = -1;
    for ii = 1:length(all_audio_devs)
        if strcmp(all_audio_devs(ii).DeviceName, ASIO_DEV_NAME)
            DeviceIndex = all_audio_devs(ii).DeviceIndex;
            break
        end
    end
    assert(DeviceIndex  > 0, 'ASIO device %s not found', ASIO_DEV_NAME)
    
    % try
    % Try with the 'freq'uency we wanted:
    mode = 1;  % 1 == sound playback only;
    reqlatencyclass = 2; % 2 == take full control over audio device
    pahandle = PsychPortAudio('Open', DeviceIndex, mode,...
                              reqlatencyclass, freq, nrchannels);
    
    %%% FAIL if sound device isn't happy with frequency!
    % catch
    %    % Failed. Retry with default frequency as suggested by device:
    %    fprintf('\nCould not open device at wanted playback frequency of %i Hz. Will retry with device default frequency.\n', freq);
    %    fprintf('Sound may sound a bit out of tune, ...\n\n');

    %    psychlasterror('reset');
    %    pahandle = PsychPortAudio('Open', [], [], 0, [], nrchannels);
    % end

    % Perform one warmup trial, to get the sound hardware fully up and running,
    % performing whatever lazy initialization only happens at real first use.
    % This "useless" warmup will allow for lower latency for start of playback
    % during actual use of the audio driver in the real trials:
    % Fill buffer with silence:
    PsychPortAudio('FillBuffer', pahandle, zeros(2, 10000));
    PsychPortAudio('Start', pahandle, 1, 0, 1);
    PsychPortAudio('Stop', pahandle, 1);

end


%%% OPEN THE SCREEN
try

Screen('Preference','SkipsyncTests', skipSyncTest);
AssertOpenGL;
screenNumber = max(Screen('Screens'));

% Define black and white
white = WhiteIndex(screenNumber);
black = BlackIndex(screenNumber);
gray = white / 2;

ScrSize=get(0,'ScreenSize');
ScrSize=ScrSize(3:end);

if Debug
    ScrSize=floor(ScrSize.*0.5); %this is for debug; leaves a  tiny window open
    ScreenRect=[0 0 ScrSize];
else
    ScreenRect=[];
end

[window, winRect] = Screen('OpenWindow', screenNumber, black, ScreenRect);

[scrSizeX, scrSizeY] = Screen('WindowSize', window);% get size of open window
ifi = Screen('GetFlipInterval', window); % one refresh cycle. RR  1/ifi (60 Hz here)
fixX = floor(scrSizeX / 2);
fixY = floor(scrSizeY / 2);

% for getting the latency right
waitframes = 0;  % ceil((2 * suggestedLatencySecs) / ifi) + 1;

WaitSecs(1);

% start screen - not sure if/when this is executed
Screen('TextFont', window,'Arial');
Screen('TextSize',window,40);

Screen('Flip', window);

%% Make checkerboards in the 4 quadrants
[checkTexture, destRects] = makeCheckTexture(window, winRect);


%%% INITIALIZE TRIGGERS
% fake it if necessary
sendTrigger = intialiseParallelPort();

DrawFormattedText(window, ['Press key to prime triggers\nDo not record yet!'],'center', scrSizeY/2,[255 255 255],[],[],[],2)
drawFrameSync(window)
Screen('Flip', window);
KbStrokeWait;

for ii = 0:7
    sendTrigger(power(2, ii));
    WaitSecs(0.1);
end
sendTrigger(0);
Screen('Flip', window);

%%
    
    %****************************************************************************************************************************
    %%% START EXPERIMENT
    
    DrawFormattedText(window, ['Ready?\nRR = ' num2str(1/ifi) ' Hz'],'center',scrSizeY/2,[255 255 255],[],[],[],2)
    Screen('Flip', window); % show new screen
    HideCursor;
    KbStrokeWait;
   
    drawFixation(window, fixX, fixY, fixC);
    Screen('Flip', window);
    
    WaitSecs(2);
    
    if useAudio
        stimList(1) = struct('type', 1, 'stimulus', audL, 'location', 0, 'trigger', trig_codes.audL);
        stimList(2) = struct('type', 1, 'stimulus', audR, 'location', 0, 'trigger', trig_codes.audR);
    else
        stimList(1) = struct('type', 1, 'stimulus', 0, 'location', 0, 'trigger', trig_codes.audL);
        stimList(2) = struct('type', 1, 'stimulus', 0, 'location', 0, 'trigger', trig_codes.audR);
    end        
    
    vis_triglist = [trig_codes.visUR, trig_codes.visLR, trig_codes.visLL, trig_codes.visUL];
    for ii = 1:length(destRects)
        stimList(ii + 2) = struct('type', 0, 'stimulus', checkTexture,...
               'location', destRects{ii}, 'trigger', vis_triglist(ii));
%                'location', destRects{ii}, 'trigger', ii+2);
    end
    
    stimSequence = repmat(1:length(stimList), 1, nStim);

    % targets
    stimList(end + 1) = struct('type', -1, 'stimulus', -1, 'location', 0, 'trigger', 32);
    stimSequence = [stimSequence, length(stimList)*ones(1, nTargets)];
    stimSequence = stimSequence(randperm(length(stimSequence)));
        
    for iITI=1:length(stimSequence)
        
        curStim = stimList(stimSequence(iITI));
        
        % Screen('FillRect', window, [255 255 255] , ScreenRect);   % Fill the display with white

        % This flip clears the display to black and returns timestamp of black onset:
        % It also triggers start of audio recording by the DataPixx, if it is
        % used, so the DataPixx gets some lead-time before actual audio onset.
        drawFixation(window, fixX, fixY, fixC);
        [vbl1 visonset1]= Screen('Flip', window);

        holdScreen = 0;
        curC = fixC;
        tWhen = 0;  % relevant for sync'ing audio & visual only
        if (useAudio) && (curStim.type == 1)
            % Fill the audio playback buffer with the audio data 'wavedata':
            PsychPortAudio('FillBuffer', pahandle, curStim.stimulus);

            %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
            %%% These are relevant if the audio needs to be sync'ed with a
            %%% frame flip: have to pre-empt the flipping time, in which
            %%% case having waitframes > 0 might allow the sound card to
            %%% get its shit together. On an Audigy5/Rx this wasn't
            %%% relevant.
            
            %%% Compute tWhen onset time for wanted visual onset at >= tWhen:
            % tWhen = vbl1 + (waitframes - 0.5) * ifi;
            %%% Schedule start of audio at exactly the predicted visual stimulus
            %%% onset caused by the next flip command.
            % tPredictedVisualOnset = PredictVisualOnsetForTime(window, tWhen);
            % PsychPortAudio('Start', pahandle, 1, tPredictedVisualOnset, 0);
            %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
            
            %%% Send sound immediately, wait for it to actually start, then
            %%% fire off a trigger; latency should be < 2 ms & no jitter!
            % reps = 1, when = 0 (now), waitforstart = 1 (block until
            % really started)
            Screen('Flip', window);
            PsychPortAudio('Start', pahandle, 1, 0, 1);
            %%% SEND STIMULUS-SPECIFIC TRIGGERS
            sendTrigger(curStim.trigger);
        
        elseif (curStim.type < 1)
            if curStim.type == 0
                Screen('DrawTexture', window, curStim.stimulus, [], curStim.location);
                % draw frame sync spot
                drawFrameSync(window)
                holdScreen = nStimFrames;
            elseif curStim.type == -1
                curC = targetC;
                holdScreen = nTargetFrames;
            end
            % Ok, the next flip will do a black-white transition...
            drawFixation(window, fixX, fixY, curC);
            [vbl visual_onset t1] = Screen('Flip', window, tWhen);  

            %%% SEND STIMULUS-SPECIFIC TRIGGERS
            sendTrigger(curStim.trigger);
        end

        for hh = 1:holdScreen - 1
            drawFixation(window, fixX, fixY, curC);
            Screen('Flip', window);
        end
        drawFixation(window, fixX, fixY, fixC);
        Screen('Flip', window);
            
        % switch off TTL
        sendTrigger(0);

        if useAudio
            PsychPortAudio('Stop', pahandle, 1);
        end

        
        %%% ITI: count down and while waiting check for interrupting
        %key press.
        debrun=GetSecs;
        curISI = getISI(minISI, maxISI);
        while GetSecs-debrun < curISI
            [~, ~, keyCode] = KbCheck;
            if strcmp(KbName(keyCode),'q')==1
                %clean up and quit
                RestoreScreen('User hit quit')
                return  %this returns control to command window!
            end
        end
    end

    drawFixation(window, fixX, fixY, fixC);
    Screen('Flip', window);
    
    WaitSecs(2);
    
    DrawFormattedText(window, 'Run finished','center',scrSizeY/2,[255 255 255],[],[],[],2);
    Screen('Flip', window); %
    
    KbStrokeWait;
    RestoreScreen() % see below for what this function does
    
catch
    Screen('CloseAll');
    psychrethrow(psychlasterror);

end

end


%%
function RestoreScreen(varargin)
% restore normal display state (return to 120 Hz mode, exit PsychToolbox, etc.)
ShowCursor;
Screen('CloseAll');
PsychPortAudio('Close');

if nargin > 0
    fprintf(1, 'Exited with status: %s\n', varargin{1});
end

clear functions

end

%%
function [checkTexture, destRects] = makeCheckTexture(win, winRect)

    [width, height] = RectSize(winRect);
    % Get the centre coordinate of the window
    [xCenter, yCenter] = RectCenter(winRect);

    miniboard = eye(2,'uint8') .* 255;

    checkerboard = repmat(miniboard, ceil(0.5 .* 8))';
    checkerboard = imresize(checkerboard, 20,'box');
    
    checkTexture = Screen('MakeTexture', win, checkerboard);
    
    cbSize = size(checkerboard);
    cbSidelen = floor(cbSize(1) / 2) + 50;
    baseRect = [0 0 cbSize];
    centeredRect = CenterRectOnPointd(baseRect, xCenter, yCenter);

    destRects = cell(1, 4);
    for ii = 1:4
        if ii==1
            destRect = CenterRectOnPointd(baseRect, xCenter + cbSidelen, yCenter + cbSidelen);
        elseif ii == 2
            destRect = CenterRectOnPointd(baseRect, xCenter + cbSidelen, yCenter - cbSidelen);
        elseif ii == 3
            destRect = CenterRectOnPointd(baseRect, xCenter - cbSidelen, yCenter - cbSidelen);
        elseif ii == 4
            destRect = CenterRectOnPointd(baseRect, xCenter - cbSidelen, yCenter + cbSidelen);
        end
        destRects{ii} = destRect;
        %Screen('DrawTexture',win,checkTexture, [], destRect);
    end

end

function drawFixation(window, posX, posY, col)

    Screen('Drawtext',window, '+',posX,posY,col); %fixation cross
end

function drawFrameSync(window)
    
%     Screen('FillRect',window, [255 255 255], [1570, 830, 1900, 1060])
    Screen('FillRect',window, [255 255 255], [1870, 1030, 1900, 1060])
end

function curISI = getISI(minISI, maxISI)
    curISI = minISI + (maxISI - minISI)*rand;
end
```

**<span style="color:blue">With many thanks to Dr. Chris Bailey, Aarhus University</span>**