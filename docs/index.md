# SeisFlows Development Log: New Functions to SeisFlows

SeisFlows is an open source FWI package developed by Ryan Modrak.  
For more information, please refer to [Introduction](https://seisflows.readthedocs.io/en/latest/)

## What I have done:
1. `seisflows/plugins/adjoint.py`       
    -Avoid dividing zero when mute near-offset data in envelope inversion.    
    
2. `seisflows/tools/signal.py` `seisflows/preprocess/base.py`      
    -Apply tapered mask to shot gather, muting body waves and later waves to preserve surface wave only.   
    
3. `seisflows/workflow/migration.py` `seisflows/solver/base.py`      
    -Fix some bugs in RTM. The original code failed to get correct adjoint source.  
    
4. `seisflows/solver/base.py`       
    -Allow to use different STATION file for different SOURCE. The naming rule must be the same. The station name must be STATIONS_(shot_index). Add a new parameter 'PAR.USER_DEFINE_STATION' to control this feature. Remember to set use_existing_STATIONS=.true. when you use this option. You can ignore 'PAR.USER_DEFINE_STATION' if you use a fixed receiver array in synthetic test. This fixed receiver array can be defined either by STATIONS file under specfem2d-master/DATA or parameters in Par_file.     
    
5. Add script to create mask model and plot misfit curves   
    
6. Add matlab scripts to convert SEGY data to SU format for SeisFlows. And Output geometry files     
    
7. Add scripts to generate simple specfem2d binary model    
    
8. We can use the latest SPECFEM2D instead of the specified version `d745c542`   
    
9. `seisflows/preprocess/base_mbpf.py`      
   -Apply a moving bandpass filter strategy to obtain adjoint source   

10. Use GPU version SPECFEM2D in SeisFlows, but I found that only kappa and mu kernel are non-zero. Thus, kernel parameters are kappa and mu, model parameters are vp and vs.    

After steps 4&6, SeisFlows can be used for real data.

## Unsolved problems:

1. Tikhonov regularization  
    
## Future work:
1. Test double difference adjoint tomography (DONE)    
    
2. Convert 3D seismic data to 2D. [code](https://github.com/Jiangwb/2DNoise_Adjoint_tomography_backup/tree/master/seiscode/3D_2D)    

3. Submit the job to cluster

## SeisFlows examples
The example links are not available now. You may find SeisFlows examples in my GitHub repositories:      
[SeisFlows Examples](https://github.com/Jiangwb/SeisFlows-examples)       
`Two layer model` - Kernel tests      
`Foothill model`  - Body/surface wave FWI tests        
`Marmousi model`  - Body/surface wave FWI tests        
I will upload more examples in the future.

## How to generate 2D model for SeisFlows
step 1: convert mdl model to SEP model      
step 2: run SEM forward modeling to generate ascii model        
step 3: convert ascii model to gll model by using a fortran script       

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
