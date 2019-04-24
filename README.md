# freesurferQCing
scripts to do manual quality checks of cortical and subcortical surfaces and volumes

## Autorecon-all ##

Note: this can only be done once the subject directory has been moved to Sherlock Oak

Log onto the Sherlock server in terminal: ```ssh SUNet@login.sherlock.stanford.edu```
Then, ```cd $OAK```
Then, ```cd TIGER_data/TIGER_FreeSurfer/TIGER_FS_bin```
Run either TIGER_sherlock.sh or TIGER2_sherlock.sh depending on the timepoint (XX = ID):
```
sbatch -t 2-00 -p iang ./TIGER_sherlock.sh XX
```
This will run FreeSurfer recon-all for that subject, which takes ~7 hours. Note you can submit multiple jobs at once, one after the other if you have several subjects to be run (meaning, you don’t need to wait for one to finish before starting the next)

Check to see if FreeSurfer is done running by going here to look for the subject: ```TIGER_data/TIGER_FreeSurfer/TIGER_FS_subjDir/```

Additionally, you can check to see the status of your jobs on Sherlock using this command:
```squeue -u SUNet```

## QCing subcortical autosegmentation ##

```cd /Volumes/group/proc/TIGERanalysis/TIGER_FreeSurfer/TIGER_FS_bin/```

(XX=ID, TX= timepoint; e.g. 14-T1): ```./tiger_checkAseg.sh XX-TX```

If you are interested in viewing 3D surface subcortical volumes, visit this link: https://surfer.nmr.mgh.harvard.edu/fswiki/FreeviewGuide/FreeviewWorkingWithData/FreeviewAnatomicalVolumes

## QCing cortical autosegmentation ##

```cd /Volumes/group/proc/TIGERanalysis/TIGER_FreeSurfer/TIGER_FS_bin/```

```./tiger_checkDesikanSeg XX-TX```

## QCing cortical surface autosegmentation ##

```cd /Volumes/group/proc/TIGERanalysis/TIGER_FreeSurfer/TIGER_FS_bin/```

```./tiger_checkDesikanSurf XX-TX```


