# Combined-Mangrove-Recognition-Index-CMRI-in-GEE

## Overview
The Combined Mangrove Recognition Index (CMRI) integrates NDVI and NDWI to identify mangrove forests more accurately. NDVI highlights dense vegetation, crucial for detecting healthy mangroves, with values close to 1. NDWI emphasizes water features, with mangroves typically showing moderate values due to their intertidal location. By combining high NDVI and NDWI, CMRI effectively differentiates mangroves from both open water and vegetation, making it useful for mapping mangroves in complex coastal environments.

This project calculates the  Combined Mangrove Recognition Index (CMRI) using MODIS NDVI and NDWI datasets in Google Earth Engine (GEE). The script computes CMRI values over specified regions from 2001 to 2023, estimates the area where CMRI exceeds a given threshold, and offers options for data export and visualization.

## Key Features
- Calculation of CMRI using MODIS datasets over a specified time range.
- Mean CMRI values computed for specified regions.
- Area estimation for regions where CMRI exceeds a defined threshold.
- Options to export CMRI images to Google Drive.
- Visualization of CMRI data on the GEE map interface.

## Requirements
- Google Earth Engine account.
- Basic knowledge of JavaScript and familiarity with the GEE Code Editor.

## Usage Instructions
1. **Setup**: Load the code in the Google Earth Engine Code Editor.
2. **Define Regions**: Replace `geometry` and `geometry2` with your own regions of interest.
   ```javascript
   var BD = geometry; // Replace with your geometry for Bangladesh
   var India = geometry2; // Replace with your geometry for India
3. **Run the Script**: Execute the script in GEE to compute and display the results.
4. **Export Data**: Uncomment the Export.image.toDrive lines to save CMRI images to Google Drive.
5. **Visualization**: Uncomment the Map.addLayer lines to view the CMRI images on the map.

## Outputs
**Console Outputs**:
- Mean CMRI values for each year for both regions.
- Area estimates (in square kilometers) where CMRI exceeds the threshold.

**Exported Data**:
- CMRI images exportable to Google Drive for further analysis or visualization.

**Map Layers**:
- CMRI images for visual inspection within GEE.

## Notes
- **Regions of Interest**: Ensure to define and replace the regions (geometry and geometry2) with your specific areas of interest.
- **Threshold Value**: Modify the threshold variable as necessary for your analysis.
- **Adjustable Parameters**: The script allows for modifications to time range, threshold values, and export settings.

## Resources
- [MODIS NDVI Data](https://developers.google.com/earth-engine/datasets/catalog/MODIS_MOD09GA_006_NDVI)
- [MODIS NDWI Data](https://developers.google.com/earth-engine/datasets/catalog/MODIS_MOD09GA_006_NDWI)
