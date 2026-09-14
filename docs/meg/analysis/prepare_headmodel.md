# Prepare Headmodel

**<span style="color:maroon">A MATLAB function called *Prepare_Headmodel.m*</span>**

The code can be **used to prepare a headmodel for source localization**. The code **assumes a BIDS like format in the RAW data folder**.

!!! note "It will need adpation to suit required needs; don't expect it to work ***right off the bat***"

**Prepare_headmodel.m**

```matlab
function [] = Prepare_Headmodel(sub)
%
% This is to prepare a headmodel for source localization
% It is best to add some breakpoint where some manual labour is involved
% The script assumes a BIDS like format in the RAW data folder

%set paths

%data folder
raw_folder = '[DATA FOLDER WHERE RAW DATA FIF FILE IS LOCATED]';
proc_folder= '[DATA OUTPUT FOLDER]';


%Subject selection
if nargin<1
    choice_made=0;
    sub_folders=dir([raw_folder filesep 'S*']);
    has_t1=zeros(1,length(sub_folders));
    has_hm=zeros(1,length(sub_folders));
    for s=1:length(sub_folders)
        sub=sub_folders(s).name;
        if exist([proc_folder sub filesep 'headmodel.mat'])
            has_hm(s)=1;
        end
        sub_folder=[raw_folder sub filesep];
        subfolders=dir(sub_folder);
        for i=1:length(subfolders)
            if length(subfolders(i).name)>2
                ses_dir_files=dir([sub_folder subfolders(i).name]);
                for n=1:length(ses_dir_files)
                    if ~isempty(strfind('MRI',ses_dir_files(n).name))
                        has_t1(s)=1;
                    end
                end
            end
        end
    end
    
    fprintf('Subjects with unprocessed T1: \n')
    cnt=1;
    for s=1:size(sub_folders,1)
        if has_t1(s) && ~has_hm(s)
            fprintf(['[' int2str(cnt) '] ' sub_folders(s).name '\n'])
            choice_sub{cnt}=sub_folders(s).name;
            cnt=cnt+1;
        end
    end
    fprintf('Subjects with processed T1: \n')
    for s=1:size(sub_folders,1)
        if has_t1(s)
            fprintf(['[' int2str(cnt) '] ' sub_folders(s).name '\n'])
            choice_sub{cnt}=sub_folders(s).name;
            cnt=cnt+1;
        end
    end
    while ~choice_made
        choice=input('Enter number: ');
        if choice>size(sub_folders,1) || choice<1
            disp('Invalid choice, please try again');
        else
            sub=choice_sub{choice};
            disp(['Subject ' sub ' selected'])
            choice_made=1;
        end
    end
end

%identify session containing raw MEG data
sub_folder=[raw_folder sub filesep];
subfolders=dir(sub_folder);
for i=1:length(subfolders)
    if length(subfolders(i).name)>2
        ses_dir_files=dir([sub_folder subfolders(i).name]);
        for n=1:length(ses_dir_files)
            if ~isempty(strfind('MEG',ses_dir_files(n).name))
                meg_data=[sub_folder subfolders(i).name filesep ses_dir_files(n).name filesep];
            end
            if ~isempty(strfind('MRI',ses_dir_files(n).name))
                mri_data=[sub_folder subfolders(i).name filesep ses_dir_files(n).name filesep];
            end
        end
    end
end

try
    MEG_files=dir([meg_data '*.fif']);
    MRI_files=dir([mri_data '*.nii']);
catch
    error('Incomplete dataset (MRI probably missing')
end

%% Get data

%MRI file
if size(MRI_files,1)==1
    MRI_file=[mri_data MRI_files(1).name];
    disp(['MRI file: ' MRI_file ' selected'])
else
    disp('Available files:')
    for i=1:size(MRI_files,1)
        fprintf(['[' int2str(i) '] ' MRI_files(i).name '\n'])
    end
    choice_made=0;
    while ~choice_made
        choice=input('Please choose anatomical file to use: ');
        
        if choice>size(MRI_files,1) || choice<1
            disp('Invalid choice, please try again');
        else
            MRI_file=[MRI_files.folder filesep MRI_files(choice).name];
            disp(['MRI file: ' MRI_file ' selected'])
            choice_made=1;
        end
    end
end

mri = ft_read_mri(MRI_file);
hs = ft_read_headshape([meg_data filesep MEG_files(1).name]);

%% Segment MRI to extract brain

%before changing anything, create a segmented brain
%This seems to work better, as the MRI is still in 'normal' orientation
cfg = [];
cfg.output = {'brain'};
mri_segmented = ft_volumesegment(cfg, mri);

%% Align MRI and polhemus

cfg=[];
cfg.method         = 'headshape';
cfg.headshape.headshape      = hs;
cfg.coordsys = 'neuromag';
cfg.headshape.interactive    = 'yes';
cfg.viewresult     = 'yes';
cfg.headshape.icp= 'yes';
mri_aligned = ft_volumerealign(cfg, mri);

%To view the final results(set breakpoint here)
cfg.headshape.icp= 'no';
ft_volumerealign(cfg, mri_aligned)

%% Create the headmodel

%apply the alignment to the segmented brain
mri_segmented.transform = mri_aligned.transform;

%Actually prepare the headmodel
cfg = [];
cfg.method='singleshell';
vol = ft_prepare_headmodel(cfg, mri_segmented);

%% check
%check aligment between headmodel and anatomical scan
%we have to load the sensor definition
%lets pick the first one
sens=ft_read_sens([meg_data filesep MEG_files(1).name]);

%both sensors and the headmodel should be in cm
vol = ft_convert_units(vol,'cm');
mri_aligned = ft_convert_units(mri_aligned,'cm');

figure;
ft_plot_mesh(vol.bnd(1), 'facecolor', 'r');
hold on;
ft_plot_ortho(mri_aligned.anatomy,'transform',mri_aligned.transform,'style','intersect')

hold on;
ft_plot_sens(sens, 'style', '*b', 'facecolor' , 'y', 'facealpha' , 0.5);
view(25, 10)
set(gcf, 'color', 'w')

%% Save results

if ~exist([proc_folder sub])
    mkdir([proc_folder sub]);
end
disp(['Saving headmodel for subject ' sub]);
save([proc_folder sub filesep 'headmodel.mat'],'vol','mri_aligned','mri_segmented','sens');
disp('Done.')


end
```

**<span style="color:blue">Many thanks to Dr. Tjerk Gutteling for the code</span>**