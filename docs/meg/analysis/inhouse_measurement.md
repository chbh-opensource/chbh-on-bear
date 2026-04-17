# "InHouse" Measurement

**An in-house measure** of the **mean power noise level**, and a **note of the noisiest sensor**, for the **Magnetometers and Gradiometers**, 
at **two different highpass frequencies, 0.1Hz and 0.03Hz**.

The **60<sup>o</sup> gantry position** is normally used, **IAS is off**, and **~2min of data is usually acquired**.

This "**empty room**" measurement is **taken on a daily basis (where possible)** and ideally should be **taken as part of a standard acquisition 
session** when acquiring data with a participant.

**<span style="color:maroon">Usage ...</span>**

```matlab
>> analyseTriux('191205\empty_room_60_2min_003Hz_IAS_off.fif')
```

!!! NOTE "The *FieldTrip toolbox* will be needed to be installed in MATLAB, download from ... <br /> - **[https://www.fieldtriptoolbox.org/](https://www.fieldtriptoolbox.org/)**"

**analyseTriux.m**

```matlab
function analyseTriux(fiffname)

D = calculatePSD(fiffname); 
figure(1)
analyseGradiometers(D,fiffname); 
figure(2)
analyseMagnetometers(D,fiffname); 
```

**calculatePSD.m**

```matlab
function data_Pow = calculatePSD(fiffname)

cfg = [];
cfg.dataset = fiffname; 
data_org        = ft_preprocessing(cfg);


% data_org = fx_applySSP(data_org,fiffname);

cfg = [];
cfg.length               = 5; % lenght of time window = 5 s => 0.2 Hz resolution
data_ref                 = ft_redefinetrial(cfg, data_org);

cfg              = [];
cfg.output       = 'pow';
cfg.channel      = 'MEG';
cfg.method       = 'mtmfft';
cfg.taper        = 'hanning';
cfg.keeptrials   = 'no'; 

data_Pow = ft_freqanalysis(cfg, data_ref);
```

**analyseGradiometers.m**

```matlab
function analyseGradiometers(D,fiffname)

mag = 1:3:306;
grad1 = 2:3:306; 
grad2 = 3:3:306; 
grad = sort([grad1 grad2]) ;
freqrange = [0 100];

for k = 1:length(grad)
    Slabel{k} = D.label{grad(k)};
end

Pgrad = 1e26*D.powspctrm(grad,:);  % (fT/cm)^2
Pmag  = 1e30*D.powspctrm(mag,:);   %  fT^2 

fidx = find(D.freq > freqrange(1) & D.freq <freqrange(2));

% ======================================
% Plot spectra

clf
subplot(221)

PgradL = log10(Pgrad);
m = 0; 
for k=1:size(PgradL,1)
    if isfinite(PgradL(k,1))
        m = m + 1; 
        PgradLC(m,:) = PgradL(k,:); 
    end
end
    
plot(D.freq,mean(PgradLC,1));
xlim(freqrange)
ylim([0 4])
title('Gradiometers mean')
xlabel('Frequency (Hz)')
ylabel('Power (fT/m)^2/Hz ')

subplot(222)
plot(D.freq,  PgradLC);
xlim(freqrange)
ylim([0 4])
title('Gradiometers mean')
xlabel('Frequency (Hz)')
ylabel('Power (fT/m)^2/Hz ')

%
%============================================

subplot(413) 
PgradTotal = mean(PgradLC(:,fidx),2);
[Psort,Pidx] = sort(PgradTotal,'descend');

bar(1:length(Psort), Psort')
title(strcat('Noise level:',{' '}, num2str(freqrange(1)), ' Hz to ',{' '} ,num2str(freqrange(2)), ' Hz'))
xlabel('sensors sorted by power')
ylabel('Power (fT/m)^2/Hz ')
ylim([0 4])

subplot(427)

xlim([0 100])
ylim([0 100]) 
text(0,100,sprintf('Mean power (all gradimeters) = %2.2f',mean(PgradTotal)))

for k=1:10
    text(0,100-k*10,sprintf('Sensor %s Power = %2.2f',Slabel{Pidx(k)},Psort(k)))    
end
axis off 

annotation('textbox', [0 0.9 1 0.1], ...
    'String', strcat(pwd,'\',fiffname), ...
    'EdgeColor', 'none', ...
    'HorizontalAlignment', 'left','Interpreter','none')

annotation('textbox', [0 0.9 1 0.1], ...
    'String', strcat('Analysed: ',date), ...
    'EdgeColor', 'none', ...
    'HorizontalAlignment', 'right','Interpreter','none')

pname = strcat(fiffname(1:end-4),'QTgrad_v2.pdf');

h=gcf;
set(h,'Position',[50 50 1200 800]);
set(h,'PaperOrientation','landscape');
print(gcf, '-dpdf','-bestfit', pname)
```

**analyseMagnetometers.m**

```matlab
function analyseSensors(D,fiffname)

mag = 1:3:306;
grad1 = 2:3:306; 
grad2 = 3:3:306; 
grad = sort([grad1 grad2]) ;
freqrange = [0 100];

for k = 1:length(grad)
    Slabel{k} = D.label{grad(k)};
end

Pgrad = 1e26*D.powspctrm(grad,:);  % (fT/cm)^2
Pmag  = 1e30*D.powspctrm(mag,:);   %  fT^2 

fidx = find(D.freq > freqrange(1) & D.freq <freqrange(2));

% ======================================
% Plot spectra

clf
subplot(221)

PmagL = log10(Pmag);
m = 0; 
for k=1:size(PmagL,1)
    if isfinite(PmagL(k,1))
        m = m + 1; 
        PmagLC(m,:) = PmagL(k,:); 
    end
end

plot(D.freq,mean(PmagLC,1));
xlim(freqrange)
ylim([0 8])
title('Magnetometers mean')
xlabel('Frequency (Hz)')
ylabel('Power fT^2/Hz ')

subplot(222)
plot(D.freq,  PmagLC);
xlim(freqrange)
ylim([0 8])
title('Magentometersmeters mean')
xlabel('Frequency (Hz)')
ylabel('Power fT^2/Hz ')

%============================================

subplot(413) 
PmagTotal = mean(PmagLC(:,fidx),2);
[Psort,Pidx] = sort(PmagTotal,'descend');

bar(1:length(Psort), Psort')
title(strcat('Noise level:',{' '}, num2str(freqrange(1)), ' Hz to ',{' '} ,num2str(freqrange(2)), ' Hz'))
xlabel('sensors sorted by power')
ylabel('Power (fT^2/Hz) ')
ylim([0 8])

subplot(427)

xlim([0 100])
ylim([0 100]) 
text(0,100,sprintf('Mean power (all magnetometers) = %2.2f',mean(PmagTotal)))

for k=1:10

    text(0,100-k*10,sprintf('Sensor %s Power = %2.2f',Slabel{Pidx(k)},Psort(k)))
    
end
axis off 

annotation('textbox', [0 0.9 1 0.1], ...
    'String', strcat(pwd,'\',fiffname), ...
    'EdgeColor', 'none', ...
    'HorizontalAlignment', 'left','Interpreter','none')

annotation('textbox', [0 0.9 1 0.1], ...
    'String', strcat('Analysed: ',date), ...
    'EdgeColor', 'none', ...
    'HorizontalAlignment', 'right','Interpreter','none')

%axis off

pname = strcat(fiffname(1:end-4),'QTmag-v2.pdf');

h=gcf;
set(h,'Position',[50 50 1200 800]);
set(h,'PaperOrientation','landscape');
print(gcf, '-dpdf','-bestfit', pname)
```

**<span style="color:blue">Many thanks to Prof. Ole Jensen for the code.</span>**
