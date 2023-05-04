# SPM12

More coming soon! please email andrew or raise a PR on github if you'd like to contribute to this page

## Running first-level analyses with parfor

!!! info
    Example contributed by Arkady Konovalov

Simple parallelisation of a for-loop can be performed using [parfor](https://www.mathworks.com/help/matlab/ref/parfor.html). This functionality is provided by MatLab and enables faster processing of `for` loops simply by changing the syntax at the start to say `parfor` rather than `for`.

Here is an example function which makes use of `parfor` whilst computing GLMs using SPM.

``` matlab
function glm_level1(model)
% This function takes a model structure as input and performs first-level
% estimations in a General Linear Model (GLM) analysis for a set of subjects.

subjects = model.Subj;

% FIRST LEVEL (individual) estimations
% Get the number of subjects to be processed.
N = size(subjects,2);

% Iterate over each subject in "subjects" using parallel processing
parfor i = 1:N

        % Get the current subject ID from "subjects"
        id = subjects(i);

        % Get the corresponding BIDS (Brain Imaging Data Structure) ID and
        % session information for the current subject.
        BIDS_id = model.ids{id};
        BIDS_sess = model.sess{id};

        % Construct the path to the GLM folder for the current subject.
        path = [model.glmfolder BIDS_id];

        % Construct the path to the SPM.mat file for the current subject.
        modelfile = [path '/SPM.mat'];

        % Delete the existing SPM.mat file for the current subject (clean
        % up previously done models)
        delete(modelfile);

        % Create a job structure for the current subject.
        job = analysis_job_func(BIDS_id, BIDS_sess, model);

        % Create an empty cell array to be used as inputs for the "spm_jobman" function.
        inputs = cell(0,1);

        % Set the SPM defaults to 'FMRI'.
        spm('defaults', 'FMRI');

        % Run the current job using the "spm_jobman" function.
        spm_jobman('run', job, inputs{:});

end

end
```

!!! note

    Make sure you specify the appropriate number of cores when starting the MatLab GUI App, you may not notice a substantial speed-up if you run MatLab using the default of 4 cores. Do try to avoid asking for substantially more than you might need however - BlueBEAR is a shared resource.
