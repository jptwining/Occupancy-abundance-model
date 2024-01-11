# Summary
These are MCMC samplers and processing and run scripts for a occupancy-abundance model for abundance-mediated species interactions. This model framework models detection/non-detection data to estimated occupancy, abundance, and interactions between the species of interest. This model enables the user to use detection/non-detection data collected over repeat surveys to model interactions as a function of abundance. These samplers are presented in Twining et al. submitted, and are based on adaptations of the [Waddle et al. (2010)](https://www.jstor.org/stable/25680391) formulation for modelling species interactions within an occupancy model, but instead of modelling the state model of a subordinate species a function of the occupancy states, it is modelled as a function of abundance (N). We provide a range of MCMC samplers for different ecological scenarios between two or more species including disease- and predator- mediated competition, mesopredator release, and tri-trophic cascades.

# The working directory

Below you fill find descriptions of each folder in this repository and files contained within them.

# The data folder (./data)

This folder has X files.

**1. alNY_2013-2021_6kmbuffer_allsitecovs.csv**

This file contains all of the summarized spatial covariate data at a 6km scale used in the analysis. Each row is a different 6km 2 pixel in New York State, each column is a covariate, and each cell is a value.

The covariates used in the analysis.

| **Covariate**    | **Description**                                                                              | **Source**                                                                                                                                       |
|------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Deciduous        | Proportion of a 6 km2 buffer around the detector made up of deciduous forest                 | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Coniferous       | Proportion of a 6 km2 buffer around the detector made up of coniferous forest                | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Mixed            | Proportion of a 6 km2 buffer around the detector made up of mixed forest                     | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Pasture          | Proportion of a 6 km2 buffer around the detector made up of pasture                          | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Cultivated.Crops | Proportion of a 6 km2 buffer around the detector made up of cultivated crops                 | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| road_density     | Mean number of km of road per km2 in each 6 km2 buffer                                       | calculated from primary and secondary roads raster provided by the NYSDEC, hosted on the githu                                                   |
| snow_depth       | Mean daily snow depth(m) of the 6 km2 buffer around each detector across the sampling period | National Operational Hydrologic Remote Sensing Centre, 2004. Snow data assimilation system (SNODAS) products (https://doi.org/10.7265/N5TB14TC). |
| forest_edge      | Edge density of combined class of all forest in each 6 km2 buffer around detectors           | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| GPP              | The amount of carbon captured by plants (kg C MJ-1) in at the detectors                      | MODIS Land Satellite, 2017 (https://lpdaac.usgs.gov/products/mod17a2hv006/)                                                                      |
| Camera           | The camera trap model used at each site (Bushnell, Recoynx, Browning)                        | Fieldwork datasheets                                                                                                                             |

**2.allNY__2013-2021_15kmbuffer_allsitecovs.csv**

This file contains all of the summarized spatial covariate data at a 15km scale used in the analysis. Each row is a different 15km 2 pixel in New York State, each column is a covariate, and each cell is a value.

The covariates used in the analysis.

| **Covariate**    | **Description**                                                                               | **Source**                                                                                                                                       |
|------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Deciduous        | Proportion of a 15 km2 buffer around the detector made up of deciduous forest                 | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Coniferous       | Proportion of a 15 km2 buffer around the detector made up of coniferous forest                | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Mixed            | Proportion of a 15 km2 buffer around the detector made up of mixed forest                     | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Pasture          | Proportion of a 15 km2 buffer around the detector made up of pasture                          | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| Cultivated.Crops | Proportion of a 15 km2 buffer around the detector made up of cultivated crops                 | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| road_density     | Mean number of km of road per km2 in each 15 km2 buffer                                       | calculated from primary and secondary roads raster provided by the NYSDEC, hosted on the githu                                                   |
| snow_depth       | Mean daily snow depth(m) of the 15 km2 buffer around each detector across the sampling period | National Operational Hydrologic Remote Sensing Centre, 2004. Snow data assimilation system (SNODAS) products (https://doi.org/10.7265/N5TB14TC). |
| forest_edge      | Edge density of combined class of all forest in each 15 km2 buffer around detectors           | NLCD, 2019 (https://www.mrlc.gov/data/nlcd-2019-land-cover-conus)                                                                                |
| GPP              | The amount of carbon captured by plants (kg C MJ-1) in at the detectors                       | MODIS Land Satellite, 2017 (https://lpdaac.usgs.gov/products/mod17a2hv006/)                                                                      |
| Deer             | The probability of occupancy (ψ) of white-tailed deer in a 15 km2 buffer around each detector | Calculated from detection/non-detection data and covariate hosted in the repository (see below)                                                  |
| Camera           | The camera trap model used at each site (Bushnell, Recoynx, Browning)                         | Fieldwork datasheets                                                                                                                             |

**3. allNY_2016_2018_bearPOrecord_pixelID_10kmgrid_noweeklydups_final.csv**

This file contains all the presence-only data used in this analysis for black bears  (maximum 1 per 10 km2 pixel per week) between the years 2016-2018 both from public online repositories and iSeeMammals, a citizen science bear monitoring project run by Cornell University

**4. NY_blackbears_ordinaldates.csv**

This file contains the sampling dates (in ordinal format) for each sampling occasion from the summer surveys from 2016-2018. Each row is a site, each column is an occasion.

**5. allNY_2013-2021_coyotePArecords_pixelID_10kmgrid.csv**

This file contains all the detection/non-detection data for coyotes collected during winter surveys from 2013-2021 in the southern tier of New York State. Each row is a site, each column is an occasion, each cell is a detection/non-detection record.

**6. allNY_2013_2021_coyotePOrecord_pixelID_10kmgrid_noweeklydups.csv**

This file contains all the presence-only data used in this analysis for coyotes (maximum 1 per 10 km2 pixel per week) between the years 2013-2021 both from public online repositories

**7. 'juliandays_allNY_2013-2021.csv'**

This file contains the sampling dates (in ordinal format) for each sampling occasion for the winter surveys from 2013-2021. Each row is a site, each column is an occasion.

**8. allNY_2013-2021_bobcatPArecords_pixelID_10kmgrid.csv**

This file contains all the detection/non-detection data for bobcats collected during winter surveys from 2013-2021 in the southern tier of New York State. Each row is a site, each column is an occasion, each cell is a detection/non-detection record.

**9. allNY_2013_2021_bobcatPOrecord_pixelID_10kmgrid_noweeklydups.csv**

This file contains all the presence-only data used in this analysis for bobcats (maximum 1 per 10 km2 pixel per week) between the years 2013-2021 both from public online repositories

**10. Allcompiled_POdata_NYMS_noduplicates.csv**

This file contains all the mammal species presence-only detections compiled from New York Mammal Survey which draws records from GBIF, iNaturalist, and emammal (https://www.nynhp.org/projects/statewide-mammal-survey/)

# The model folder (./models)

The models are coded up via the nimble package version 0.13.1 (de Valpine et al. 2022).

**1. nimble_ppp_integrated_model_bear_10km_yearindexed_randomeffects_centrered.R**

This is the nimble IPPP model that is fit to the black bear data files above. The code is commented out to describe each part of the model.

**2. nimble_ppp_integrated_model_coyote_10km_yearindexed_randomeffects_centered**

This is the nimble IPPP model that is fit to the coyote data files above. The code is commented out to describe each part of the model.

**3. nimble_ppp_integrated_model__bobcat_10km_indexingoveryear_randomeffects_centered**

This is the nimble IPPP model that is fit to the bobcat data files above. The code is commented out to describe each part of the model.


# The scripts folder (./scripts)

**1. bear_PO_PA_model_10km_nimble_formattingandrunscript_indexoveryear**

This is the formatting and run script for the bear data and model above. This code is commented throughout.

**2. coyote_PO_PA_model_10km_nimble_formattingandrunscript_indexoveryear**

This is the formatting and run script for the coyote data and model above. This code is commented throughout.

