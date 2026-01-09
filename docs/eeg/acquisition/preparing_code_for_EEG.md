# Setting up your code to collect good EEG data

## sending triggers

For EEG timing is of the essence!
Even if you do not care about exact stimulus timing, you really should care about logging the time relevant events happen as accurately as possible!

[Documentation and code for how to send triggers with labjack](https://github.com/damiancruse/chbh_eeg_labjack)



     

        



=== "Example Code Matlab"

    Here's some example code for how to define and send triggers in Matlab. 
    For this to work, make sure you have downloaded the code for labjack to your task code folder and added the path (see example).
    !!! note
        Matlab example contributed by [Romy Froemer](https://github.com/froemero).

    ``` matlab
        %% setting EEG via console prompt at the start of the task
        novalidinput = 1;
        while  novalidinput==1
            expParams.isEEGsession = (input('Do EEG? y or n: ','s'));

            if isstrprop(p.isET, 'upper')
                expParams.isEEGsession = lower(expParams.isEEGsession);
            end

            if strcmp(expParams.isEEGsession, 'y')
                expParams.isEEGsession = 1;
                novalidinput = 0;
            elseif strcmp(expParams.isEEGsession, 'n')
                expParams.isEEGsession=0;
                novalidinput = 0;
            end
        end

        %% setting up the EEG
        if expParams.isEEGsession
            addpath('taskCode/EEG_code/'); % in this example, the labjack code lives in a folder called EEG_code within a folder called taskCode

            if expParams.isEEGsession

                try
                    L = lab_init_sa;
                    expParams.EEGpars.ext.L = L;
                    disp('EEG SUCCESSFULLY CONFUFURED!');
                    % here also define event codes
                    % 1x = stimulus onset, 2x = response onset; Confidence = trig +20
                    % x = phase: FAM = 1, RATE = 2, CHOICE = 0

                    % FAM triggers
                    expParams.EEGpars.trigs.FamStimCode = 11; % a task relevant stimulus comes on - Choice
                    expParams.EEGpars.trigs.FamRespCode = 21; % a response is given

                    % RATE Triggers
                    expParams.EEGpars.trigs.RateStimCode = 12;
                    expParams.EEGpars.trigs.RateRespCode = 22; % -  RATE
                    expParams.EEGpars.trigs.ConfPromptCode = 32;
                    expParams.EEGpars.trigs.ConfRespCode = 42;

                    % CHOICE Triggers
                    expParams.EEGpars.trigs.trialCode = 1;      % a trial begins (first item)
                    expParams.EEGpars.trigs.stimCode = 10;      % a task relevant stimulus comes on - Choice (all items after first)
                    expParams.EEGpars.trigs.respCode = 20;      % a response is given
                    expParams.EEGpars.trigs.fbCode = 30;        % show chosen
                    expParams.EEGpars.trigs.erCode = 40;        % error response code
                    expParams.EEGpars.trigs.NOrespCode = 99;    % trial ended without a response


                    expParams.EEGpars.trigs.runStartCode = 50;
                    expParams.EEGpars.trigs.runEndCode = 60;
                catch
                    disp('FAILED EEG CONFIGURATION!  :-(');
                end


                try
                    % Turn off all pins in the parallel port
                    lab_put_code_sa(expParams.EEGpars.ext.L,0); 
                    disp('EEG TRIGGER SUCCESSFUL!');
                catch
                    disp('FAILED EEG TRIGGER!  :-(');
                end


            end
        end

        %% Sending an actual trigger (example)


            % here's where stimuli are actually shown
            Screen(p.wPtr, 'Flip',0,1);  % don't clear!

            if expParams.isEEGsession && ~expParams.CHOICE.isPracticeNow
                lab_put_code_sa(expParams.EEGpars.ext.L,expParams.EEGpars.trigs.trialCode);
            end
    ```

=== "Example Code Python"

    Here's some example code for how to define and send triggers in python. 
    For this to work,...

    ```python


    ```



## stimulus timing
