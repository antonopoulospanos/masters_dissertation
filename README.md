
# Using Satellite Multispectral Data to Monitor Vegetation Trends as a Result of Climate Change

Author: Panos Antonopoulos (University of Cambridge)

## Description

This project is submitted as part of the course requirements of the MPhil in Data Intensive Science at the University of Cambridge. 

The primary objective of this research project is to reproduce the findings presented in [https://www.mdpi.com/2072-4292/15/14/3628](https://www.mdpi.com/2072-4292/15/14/3628), namely the observation of a statistically significant continuous greening strip along the Pacific slope of Peru and northern Chile over a time period of 24 years. Additionally, this project extends the original work by (i) developing an open source fully contained pipeline in Python, using the Google Earth Engine API to pre-process, post-process, and carry out statistical analysis on the data, (ii) examining another region (California, USA) to demonstrate scalability and generality of the pipeline, and (iii) proposing future work which may build on that presented here.


## Table of Contents
- [Data Availability](#data-availability)
- [Usage](#usage)
- [Notes](#notes)

## Data Availability

The raw data used for this project is found here: 
[Raw Pixel Data](https://drive.google.com/drive/folders/1L7Zzio2DFTQEQrPdJe5F_KVH2erBIgnu?usp=share_link). 

- This includes `.csv` files for each tile, where each row corresponds to a pixel within the tile. The columns alternate between Enhanced Vegetation Index (EVI) values and Quality Assessment (QA) categories for each image date covering the Region of Interest (ROI). The final column contains the geographic location of each pixel in GeoJSON format.

The processed data obtained from this is found here: 
[Processed EVI Data](https://drive.google.com/drive/folders/1TLv86JKJ2GnFhgdbdUxCk9qyMyefkq5U?usp=share_link). 

- This includes `.json` files for each tile, where the geographic location of the pixel is stored together with its change in EVI over the 24 year period as computed from the statistical analysis presented in the key paper linked to above.

The data used for correlation calculations can be found here: [Correlations Data](https://drive.google.com/drive/folders/1zb0g7kIrjP7cZxK22nt2B4e-aa4hXDJi?usp=share_link). 

- This includes `.csv` files containing the precipitation and spatially averaged EVI time series for the Greening Strip (GS), the intersections between the GS and the Köppen-Geiger climate zones, as well as the Köppen-Geiger climate zones within the original ROI. Additionally, alongside the Land Cover
Classification System data used to mask unwanted areas, the Sea Surface Temperature (SST) and CO$_{2}$ time series are also included. 

Please make sure to include the [Raw Pixel Data](https://drive.google.com/drive/folders/1L7Zzio2DFTQEQrPdJe5F_KVH2erBIgnu?usp=share_link) into the `pa517` directory and modify the `raw_pixel_evi_data` variable in the `notebook_setup.txt` file accordingly if you want to run the post processing pipeline from scratch. 
Similarly, Please make sure to include the [Processed EVI Data](https://drive.google.com/drive/folders/1TLv86JKJ2GnFhgdbdUxCk9qyMyefkq5U?usp=share_link) into the `pa517` directory and modify the `processed_pixel_evi_data` variable in the `notebook_setup.txt` file accordingly if you want to just reproduce the final results. 

## Usage

Due to the essential role of Google Earth Engine in this project, the pipeline was developed using Google Colab and Google Drive because of their compatibility and seamless integration with the platform. The code is presented in Jupyter Notebooks to clearly outline the steps followed so that future researchers can easily follow the procedure and amend/extend the analysis. 

The Jupyter Notebooks are to be run using the standard Colab Python envirnoment, where additional packages are installed and imported at the beginning of each notebook. Additionally, the notebooks are configured using the `notebook_setup.txt` file within the `./src` folder. This file contains all necessary information such that the study ROI, start date, and end date can be changed just once for the whole pipeline.

### Earth Engine Assets

The Earth Engine assets used in this project are contained within the `./earth_engine_assets` directory. These can be imported into a Google Earth Engine project for easy use with this pipeline. 


### Notebook Contents

The repository contains the following Jupyter Notebooks in the `./src/notebooks` directory.

- #### data_acquisition.ipynb

This notebook contains the code to acquire the data. Specifically, it tiles the ROI that is specified in the `notebook_setup.txt` file and exports each tile's pixel time series data.

- #### data_processing.ipynb

This notebook contains the code to process the data. Specifically, it implements the analysis pipeline described in [the key paper](https://www.mdpi.com/2072-4292/15/14/3628) and plots the resulting $\Delta _{EVI}$ heatmap.

- #### calculating_correlations.ipynb

This notebook contains the code to obtain the spatially averaged EVI time series for each region, along with the corresponding climate driver time series. It also includes the code to calculate the correlations between these time series.

### Demonstration gifs

For guidance on how to import/export layers to/from QGIS, together with how to trace regions, please see the demonstration gifs contained in the `./demos` directory.