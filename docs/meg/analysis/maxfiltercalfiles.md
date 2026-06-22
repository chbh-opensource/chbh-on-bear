# MaxFilter Fine-Calibration Files

If using MaxFilter for any analysis ...

**<span style="color:maroon">(Right-click link, "Save link as...").</span>**

**<span style="color:green">Supine:</span>** **[sss_cal_3140_0_190213.dat](../../meg/files/sss_cal_3140_0_190213.dat)** 

- the default, **before 24th November 2021**, named as **[sss_cal_3140_190213.dat](../../meg/files/sss_cal_3140_190213.dat)**

**<span style="font-size:x-large;color:green">60 Degree: [sss_cal_3140_60_190213.dat](../../meg/files/sss_cal_3140_60_190213.dat)</span>** 

- <span style="color:red">now the **default "*sss_cal.dat*" file, as from 24th November 2021**.</span>

**<span style="color:green">68 Degree:</span>** **[sss_cal_3140_68_190213.dat](../../meg/files/sss_cal_3140_68_190213.dat)**

If required, the ctc file (*which hasn't changed*) ...

**[ct_sparse_triux2.fif](../../meg/files/ct_sparse_triux2.fif)** (dated 10/02/2018)


From a note re: duty-of-care overnight Acquired data backup ...

```
If we can't copy the symbolic links,
new ones will need to be made if we have to copy the files back ...

"sss_cal.dat"

Location: /neuro/databases/sss
Points to: sss_cal_3140_60_190213.dat (as from 24/11/2021)
User: neuromag
Group: neuro

symlink "/projects/meg-data/rds/neuro/databases/sss/sss_cal.dat" -> "sss_cal_3140_60_190213.dat"

(was originally pointng to "sss_cal_3140_190213.dat" - a copy of "sss_cal_3140_0_190213.dat")

_______________________________________

"ct_sparse.fif"

Location: /neuro/databases/ctc
Points to: ct_sparse_triux2.fif
User: neuromag
Group: neuro

symlink "/projects/meg-data/rds/neuro/databases/ctc/ct_sparse.fif" -> "ct_sparse_triux2.fif" 
```

*<span style="color:blue">"MaxFilter fine-calibration file does not affect the recorded raw data at all, they are completely independent. 
Thus, the 60-degrees calibration can be applied to all recordings in seated position, whenever they have been performed."</span>*<br />
- **24th November 2021:** *Jukka Nenonen, Method Development Manager*.

**[NM24764U Product bulletin (fine-calibration)]** <!---(../../meg/pdfs/NM24764U_Product_bulletin.pdf) ---!> *(SharePoint link to be added)*