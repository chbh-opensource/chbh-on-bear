# Setting up your code to collect good ET data

## calling eye-tracker and sending messages

For eye-tracking timing is of the essence!
Even if you do not care about exact stimulus timing, you really should care about logging the time relevant events happen as accurately as possible!


=== "Example Code Matlab"

    Here's some example code for how to define and send messages in Matlab. 
    
    !!! note
        Matlab example contributed by [Romy Froemer](https://github.com/froemero).

    ``` matlab
        %% setting ET via console prompt at the start of the task
        novalidinput =1;
        while novalidinput == 1
        p.SessionInfo.isET = (input('Do eye-tracking? y or n: ','s'));

        if isstrprop(p.SessionInfo.isET,'upper')
           p.SessionInfo.isET = lower(p.SessionInfo.isET); 
        end

        if strcmp(p.SessionInfo.isET, 'y')
            p.SessionInfo.isET = 1;
            novalidinput =0;
        elseif strcmp(p.SessionInfo.isET, 'n')
            p.SessionInfo.isET=0;
            novalidinput =0;
        end
        end

        %% initializing file and eye-tracker
        % set file name
        p.TaskParams.ET.edfFile =  strcat('MPRD',p.SubID); % define filename for edf file
        %here, initialize a structure corresponding to the parameters of the
        %display where stimuli are being created, for use in calculating the
        %DVA of eye position location. The argument to pass is the screen
        %number that corresponds to where the already opened window pointer is. (see function below)
        p = initializeEyetrackingParams(p.screenParams.screenNum,p);

        %% example for sending messages:
        if (p.SessionInfo.isET && ~p.SessionInfo.isPractice)
            Eyelink('Message', 'DotsOn');
        end

        %% cali instructions %%%%
            showETInstruction(p, p.SessionInfo.Instructions.CaliInstruction, 'to start the calibration. While doing so, please look at the + above.')
            p = EyelinkSetup(1,p);
            save(fullfile(p.SessionInfo.filePath,['MPRDM_v', p.Version, '_',p.SubID,'_',p.SessionInfo.date,'.mat']),'p');
            Eyelink('IsConnected');
            if p.TaskParams.ET.recordContinuous ==1
                Eyelink('Command', 'set_idle_mode');
                WaitSecs(0.05);
                Eyelink('StartRecording');
                % record a few samples before we actually start displaying
                % otherwise you may lose a few msec of data
                WaitSecs(0.1);
            end

        %% shut down eyeLink
        if p.SessionInfo.isET
           % End of Experiment;
           %% when adding EEG add start trigger here
           %% add end message:
           Eyelink('Message', 'ExpEnd');
           % close the file firsts
           % close graphics window, close data file and shut down tracker
           Eyelink('Command', 'set_idle_mode');
           WaitSecs(0.5);
           Eyelink('CloseFile');
           EyelinkSetup(0,p) % receiving (any) files and shutting down eyelink
        end

        %% function to start/stop eye-tracking which saves and pulls file
        function [p] = EyelinkSetup(startOrStop, p)

        %Local function to set up defaults for each Eyelink and start recording.
        %Designed to be called before starting each block. Requires previous call
        %to EyelinkInitDefaults to work appropriately

        %startOrStop is a binary variable, where 1 = 'start up the Eyelink and
        %initialize', and 0 = 'turn off Eyelink'

        if startOrStop==1 %starting up the Eyelink
    
            p.TaskParams.ET.el=EyelinkInitDefaults(p.screenParams.wPtr); %initialize the Eyelink default settings
    
            % Initialize Eyelink connection (real or dummy). The flag '1' requests
            % use of callback function and eye camera image display:
            if ~EyelinkInit([], 1)
                fprintf('Eyelink Init aborted.\n');
                cleanup;
               return;
            end
    
            if p.TaskParams.ET.save_edf
                i = Eyelink('Openfile', p.TaskParams.ET.edfFile);
                if i~=0
                    fprintf('Cannot create EDF file ''%s'' ', p.TaskParams.ET.edfFile);
                    Eyelink( 'Shutdown');
                    Screen('CloseAll');
                    return;
                end
                Eyelink('command', 'add_file_preamble_text ''Recorded by EyelinkToolbox MPRDM experiment''');
            end
            
            if ~isfield(p.TaskParams.ET,'eye_used')
                p.TaskParams.ET.eye_used=0;
            end
    
    
            % Send any additional setup commands to the tracker
            Eyelink('Command','calibration_type = HV5'); % calibration type changed 12/01/2023 from HV9 due to issues with corners
            Eyelink('Command','recording_parse_type = GAZE');
    
            if p.TaskParams.ET.save_edf
                % set EDF file contents using the file_sample_data and
                % file-event_filter commands
                % set link data thtough link_sample_data and link_event_filter
                Eyelink('command', 'file_event_filter = LEFT,RIGHT,FIXATION,SACCADE,BLINK,MESSAGE,BUTTON,INPUT');
                Eyelink('command', 'link_event_filter = LEFT,RIGHT,FIXATION,SACCADE,BLINK,MESSAGE,BUTTON,INPUT');
            else
                Eyelink('Command','link_event_filter = LEFT,RIGHT,FIXATION,SACCADE,BLINK');
            end
    
            %perform calls to the Eyelink host to get the correct queued eye data
            Eyelink('command','link_sample_data = LEFT,RIGHT,GAZE,AREA,GAZERES,HREF,PUPIL,STATUS,INPUT,HMARKER');
    
            % HH Settings
            Eyelink('command', 'file_sample_data  = LEFT,RIGHT,GAZE,HREF,AREA,GAZERES,STATUS,INPUT');
            %   Eyelink('command', 'link_sample_data  = LEFT,RIGHT,GAZE,GAZERES,AREA,STATUS,INPUT');
    
            Eyelink('command','inputword_is_window = ON');
    
            Eyelink('Command','sample_rate = 1000');
    
            % changed 01/2022: we read in the coordinates from display params (like HH)
            Eyelink('command','screen_pixel_coords = %ld %ld %ld %ld', 0, 0, p.TaskParams.ET.dp.w_width-1, p.TaskParams.ET.dp.w_height-1);
            Eyelink('message', 'DISPLAY_COORDS %ld %ld %ld %ld', 0, 0, p.TaskParams.ET.dp.w_width-1, p.TaskParams.ET.dp.w_height-1);
    
            %Eyelink('Command','screen_pixel_coords = 0 0 1024 768');
            %Eyelink('Command','screen_pixel_coords = 0 0 1151 863'); %need to fix the resolution input thing here
            Eyelink('Command','draw_line = x1, y1, x2, y2, 0');
            Eyelink('Command','file_event_data = GAZE,VELOCITY');
            Eyelink('Command','link_event_data = GAZE,VELOCITY');
            Eyelink('Command','saccade_velocity_threshold = 200');
            Eyelink('Command','saccade_motion_threshold = 0.15');
    
            % what is that and what does it do?
            %result = Eyelink('StartSetup',1);
            result = EyelinkDoTrackerSetup(p.TaskParams.ET.el); % do calibration
    
            %Eyelink('StartRecording');
    
            disp('Eyelink up and running!');
    
        elseif startOrStop==0 %done with Eyelink for now, shut it down
    
            if p.TaskParams.ET.save_edf
                try
                    fprintf('Receiving data file ''%s''\n', p.TaskParams.ET.edfFile );
                    status=Eyelink('ReceiveFile');
                    if status > 0
                        fprintf('ReceiveFile status %d\n', status);
                    end
                    if 2==exist([p.TaskParams.ET.edfFile, '.edf'], 'file')
                        fprintf('Data file ''%s'' can be found in ''%s''\n', p.TaskParams.ET.edfFile, pwd);
                        movefile([p.TaskParams.ET.edfFile, '.edf'], 'data/ET_Results')
                    end
                catch
                    fprintf('Problem receiving data file ''%s''\n', p.TaskParams.ET.edfFile );
                end
            end
            %reset sampling rate for other experimenter's use and shutdown the Eyelink
            if p.TaskParams.ET.resetParams
                Eyelink('Command','sample_rate = 250');
                Eyelink('Command','calibration_type = HV9');
            end
            disp('....now clearing eyelink! :)');
            Eyelink('Shutdown');
            p.TaskParams.ET.el=-1;
    
        end

    ```

=== "Example Code Python"

<!--     Here's some example code for how to send triggers in python. 
    All following Python code snippets are from Python code elements run by Opensesame.

    1)	Import the labjackU3 module at the beginning of the experiment:  
        ```python
            import labjackU3

        ```
    
    2)	Insert a Python code element in the trial sequence at exactly the moment you want to sent the trigger and sent the trigger you want from that code element. In this example the trigger “99” is sent everytime the Python code element is executed within the trial sequence:
        ```python
            labjackU3.trigger(99) 

        ```
    The triggers can be either hard-coded as in the example above or soft-coded and defined somewhere else, as in the following example. Here the trigger with information about the memory array is defined somewhere else in the experiment (e.g. the run file) in a variable named “trigger_ma_info”:
        ```python
            labjackU3.trigger(trigger_ma_info)

        ```
    Example of a trial sequence in opensesame, to illustrate the placement of the python code snippets.
    
    ![Python Triggers](images/EEG/Python_triggers.png)

    Caveat: LabJack has a sleep time implemented this will influence the timing of your task, as the python code sending the trigger is paused after sending it, this could become relevant for experiments that need highly precise timing. The pause duration of LabJack can be changed with a line of code that is inserted after importing the LabJack module. In this example the pause time is reduced to 2.5ms.
        ```python
            labjackU3.DURATION = 0.025
        ```
    When triggers are sent closely after the LabJack pause might not be sufficient to prevent trigger overlap, so you can either increase the labjackU3.DURATION or you use the opensesesame module “time” to pause the experiment. To do that you need to import “time” at the beginning of the experiment and set it to sleep after sending a trigger. In this example, time is paused for 5ms.
        ```python
            import time

             time.sleep(0.05) 
        ``` -->
    
    
    
    
