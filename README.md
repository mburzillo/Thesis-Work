# Thesis

New home for R thesis work

## File Descriptions: Rmds should be run in the order presented to produce final data for analysis


**Calculating_1930_City_Population.RMD** contains all calculations/data reshaping to take IPUMS files and find city populations for 1930. Final dataset includes city code, name, state, and population for all cities and all cities with Richmond HOLC maps (city_pop_name_1930_in_richmond). 

**combining_missing_and_all_holc_files.RMD:** this takes the shapefiles that were found to be missing from the fullshpfile file from Richmond (which was supposed to contain them all) and creates a master shapefile containing these files and the fullshpfile file called master_holc_shape_files.shp. This file is then imported into QGIS for intersection with the 1960s Census tracts to produce the file master_overlay.csv. 

**all_holc_files_cleaning.RMD:** this takes in the master_overlay.csv from QGIS, groups HOLC-Census tract intersection areas by Census tract, and then calculates proportion of census tract area covered by any HOLC areas and proportion graded D/Red. This file also joins this geographic data with city populations from 1930 from the data generated by Calculating_1930_City_Population.RMD. The final dataset produced is all_richmond_with_pop, which contains data for all 1960 census tracts with HOLC area coverage, the proportion area covered, and the proportion area graded D/Red in addition to the city population from the 1930 census.

**demo_tract_merge.RMD** takes in the all_richmond_with_pop dataset created by the all_holc_files_cleaning.RMD and joins it with the demographic data at the tract level from 1960 for analysis. Produces the data_for_analysis.csv file which will be the final dataset to export to Stata for regression analysis for predicting grades model.


## To Generate Data for Initial Model Explaining Tract Grades

1) Calculate 1930s population by city with *Calculating_1930_City_Population.RMD*
2) In QGIS, upload fullshpfile from the University of Richmond database and 1960 Census tracts
3) Perform intersection with 1960 Census tract boundaries in QGIS
4) Calculate relevant areas for intersection in QGIS
5) Save as csv/export from QGIS to re-import to r as *"master_overlay.csv"*
6) Run *all_holc_files_cleaning.RMD* to produce the dataset of tracts with proportion HOLC-area covered, and the proportion area graded D/Red in addition to the city population from the 1930 census.
7) Run *demo_tract_merge.RMD* to join the HOLC graded tract data with the demographic tract level data from IPUMS to create the final dataset for analysis


## Outdated Files: to be updated
**combining_holc_files.RMD:** creates on shapefile containing all of the relevant HOLC city files for the treatment group (40-50k pop) by combining all the files in the "Shapefiles/Richmond HOLC Files" folder. Adds in variables for city name, state, and map year based on the the HOLC fodler names for each city downloaded from the Richmond Mapping Inequality website.

**overlay_calcs.RMD** takes in the area overlay file from ArcGIS and assigns HOLC grades to each Census tract. Also creates an indicator for any tracts that are less than 50% covered by HOLC areas and any tract that receives a grade that represents less than 50% of the graded area in that tract. Creates the "all_cities_tract_grades" dataset which holds all the census tracts and assigned grades for analysis. 

**csv 1930 data** this was generated by taking the full 1930 Census sample from IPUMS. observations with cities with code 0 were first dropped, as these indicate "Not in identifiable city (or size group)." Then, the individual level observations were collapsed by year, city, and citypop and the perwts were summed. 

## Outdated Steps
2) Create master shapefile of all HOLC shapefiles using *combining_missing_and_all_holc_files.RMD*.  and 2) Upload resultant shape file *"master_holc_shape_files.shp"* to QGIS. We no longer need these because shapefile on Richmond website has been corrected. Instead used master shapefile downloaded from website, saved on Desktop, which contains the most comprehensive set of shapefiles from the HOLC maps.
