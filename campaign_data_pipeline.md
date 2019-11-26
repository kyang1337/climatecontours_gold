## Front-end to Back-end Data Pipeline for Labeling Campaigns:

  

###  During campaign:

-  .jpg images are fetched from a directory in Cori: /global/project/projectdirs/ClimateNet/Images_test/*
    

	-  Those images are created from .nc files at /ClimateNet/data/*
    
	-   Data to be displayed are sampled by calling the script /ClimateNet/image_scripts/newFileNames.ipynb
    

	-   Samples without replacement
    
-   Script creates .txt files in /global/project/projectdirs/ClimateNet/SetOfFileNames with the filenames of sampled .jpg
    

-   The images for different channels are pre-generated by a script: /ClimateNet/image_scripts/all_chey.py
    

-   xml files are generated and stored at path: [http://labelmegold.services.nersc.gov/climatecontours_gold/submittedAnnotations/tmq/](http://labelmegold.services.nersc.gov/climatecontours_gold/submittedAnnotations/tmq/)
    

	-   The xml files are then saved to Cori for processing using script: project/projectdirs/ClimateNet/grabAnnotations.py
    

	-   htar bundle xmls together & hsi to transfer
    

	-   Backed up to HPSS at /nersc/projects/ClimateNet/labels
    

  

###   After campaign cleaning:
    

-   Convert non-deleted XML polygons to numpy arrays of same dimensions as h5 data
    
-   Create one field with all TC masks, another with all AR masks
    
-   Flip the masks vertically and shift image if necessary to match h5 data layout
    
-   Copy the h5 files from wherever the source is
    
-   Append the masks as new fields on the copied h5s (NOT the originals)
    
-   Finally put the .netcdf files at path: /project/projectdirs/ClimateNet/h5_data_processed/[campaign_name]