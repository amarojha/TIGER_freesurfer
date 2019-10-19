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

NOTE: you may get a message saying ```freeview command not found```

This denotes that your terminal is not pointing to the FreeSurferSetup script. You can enter the following manually to dix for this:

```export FREESURFER_HOME=/Applications/freesurfer```

```source $FREESURFER_HOME=/SetUpFreeSurfer.sh```

If this does not work then you can try running the SetUpFreeSurfer script by hand in terminal:

```
if [ -z $FREESURFER_HOME ]; then
    echo " ERROR: Environment variable FREESURFER_HOME must be defined prior to sourcing Freesurfer." 
    return
fi
```

```
if [ -z $SUBJECTS_DIR ]; then
    export SUBJECTS_DIR=$FREESURFER_HOME/subjects
fi
```

```
if [ -z $FUNCTIONALS_DIR ]; then
    export FUNCTIONALS_DIR=$FREESURFER_HOME/sessions
fi
```

```
source $FREESURFER_HOME/FreeSurferEnv.sh
```

### Notes about subcortical QCing ###

**NOTE:** right/left are flipped when viewing structures in FSLeyes

- lateral ventricles: these are always good unless they have a 5th ventricle, in which case you should exclude the person

- cerebellum: look for WM coverage - if that's bad, both GM/WM are not usable; make sure it's fully covered

- thalamus: large green structure in center; usually messy but ok

- lat. DC: reddish-pink structure immersed in thalamus; almost always good

- caudate: blue0gray above the lat. DC

- putamen: pink, shouldn't touch gray matter too much; should be roundish; shouldn't be concave/"C" shaped

- pallidum: more medial (blue) adjacent putamen

- NAcc: gold, little more anterior

- hippocampus: greenish-yellow, use axial view; check that left hippo doesn't overextend

- amygdala: almost always fine; make sure it doesn't go into hippo's space (blue), anterior to hippo, fairly ventral

**GENERAL NOTES:** spend most time in sagittal view; the left side usually has more issues; regions may be funky when they come in or fade out but that's ok.

Once you are done with QCing in Excel, use the "pull FS volumes" script, changing the paths to reflect TIGER

You'll need Matlab 2015a for ebst results; try to do them in smaller batches


## QCing cortical autosegmentation ##

```cd /Volumes/group/proc/TIGERanalysis/TIGER_FreeSurfer/TIGER_FS_bin/```

```./tiger_checkDesikanSeg XX-TX```

## QCing cortical surface autosegmentation ##

```cd /Volumes/group/proc/TIGERanalysis/TIGER_FreeSurfer/TIGER_FS_bin/```

```./tiger_checkDesikanSurf XX-TX```


