# Reset VPixx PROPixx Projector

If **fast-flicker code has been running**, and **MATLAB is not exited gracefully/Projector reset**, then the **displayed projected image may show black and white "ghosting"/double images** when the **next MEG Operator "wakes" the Projector**.<br /> 
The **original fix** was to **power down the projector completely and then restart**.<br />

The **following MATLAB code is now used** (as a Function) to **reset the PROPixx Projector back to its default settings** after usage at 1440 Hz.

A file called **"RESET_VPIXX.m"** can be **found on the Stim PC Desktop. Load into MATLAB and Run**.

**<span style="color:blue">Many thanks to Dr. Alex Zhigalov for the code</span>**


```matlab
%-------------------------------------------------------------------------------
% Function RESET_VPIXX
%-------------------------------------------------------------------------------
function RESET_VPIXX()

tag_setup_projector('open');
tag_setup_projector('reset');
tag_setup_projector('close');

end % end

%-------------------------------------------------------------------------------
% Function
%-------------------------------------------------------------------------------
function tag_setup_projector(command)

if strcmp(command, 'open')
  Datapixx('Open');
elseif strcmp(command, 'set')
  Datapixx('SetPropixxDlpSequenceProgram', 5); % 1440 Hz
  Datapixx('RegWrRd');
elseif strcmp(command, 'reset')
  Datapixx('SetPropixxDlpSequenceProgram', 0); % default
  Datapixx('RegWrRd');
elseif strcmp(command, 'close')
  Datapixx('Close');
else
  fprintf(1, 'Propixx command ''%s'' is not defined.\n', command);
  return
end
  
end % end

%-------------------------------------------------------------------------------
```

