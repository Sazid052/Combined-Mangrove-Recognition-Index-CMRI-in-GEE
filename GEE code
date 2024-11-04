var BD = geometry;
var India = geometry2;

// Set the map center
Map.setCenter(89.1071, 21.912, 8);
// Define the years for which you want to calculate CMRI
var years = ee.List.sequence(2001, 2023);

// Iterate through the years
years.getInfo().forEach(function(year) {
  var prevYear = year - 1; // Get the previous year
  var startDate = ee.Date(prevYear + '-12-01'); // Start from December of the previous year
  var endDate = ee.Date(year + '-02-28'); // End in February of the current year

  // Filter the NDVI and NDWI datasets for the current year
  var ndviDataset = ee.ImageCollection('MODIS/MOD09GA_006_NDVI')
    .filter(ee.Filter.date(startDate, endDate));

  var ndwiDataset = ee.ImageCollection('MODIS/MOD09GA_006_NDWI')
    .filter(ee.Filter.date(startDate, endDate));

  var ndvi = ndviDataset.select('NDVI');
  var ndwi = ndwiDataset.select('NDWI');
  
  
  // Bangladesh
  // Clip the NDVI and NDWI datasets to BD (Bangladesh)
  var clippedNDVI_BD = ndvi.mean().clip(BD);
  var clippedNDWI_BD = ndwi.mean().clip(BD);

  // Calculate CMRI for BD: CMRI = NDVI - NDWI
  var cmri_BD = clippedNDVI_BD.subtract(clippedNDWI_BD);

  // Calculate the mean value of CMRI for Bangladesh
  var meanCMRI_BD = cmri_BD.reduceRegion({
    reducer: ee.Reducer.mean(),
    geometry: BD,
    scale: 463.313
  });

  // Print the mean values to the console for each year
  print('Mean CMRI for Bangladesh in', year, meanCMRI_BD.get('NDVI'));
  
  
  // India
  // Clip the NDVI and NDWI datasets to India
  var clippedNDVI_India = ndvi.mean().clip(India);
  var clippedNDWI_India = ndwi.mean().clip(India);

  // Calculate CMRI for India: CMRI = NDVI - NDWI
  var cmri_India = clippedNDVI_India.subtract(clippedNDWI_India);

  // Calculate the mean value of CMRI for India
  var meanCMRI_India = cmri_India.reduceRegion({
    reducer: ee.Reducer.mean(),
    geometry: India,
    scale: 463.313
  });

  // Print the mean values to the console for each year
  print('Mean CMRI for India in', year,  meanCMRI_India.get('NDVI'));
  
  
  
  // // Export the CMRI image as an Asset or to your Drive with the year included in the description.
  // Export.image.toDrive({
  //   image: cmri_BD,
  //   description: 'CMRI_BD_' + year, // Include the year in the description
  //   folder: 'CMRI', // Change to your desired folder
  //   fileNamePrefix: 'CMRI_BD_' + year,
  //   scale: 463.313, // Change to your desired scale
  //   region: BD
  // });
  
  // Export.image.toDrive({
  //   image: cmri_India,
  //   description: 'CMRI_India_' + year, // Include the year in the description
  //   folder: 'CMRI', // Change to your desired folder
  //   fileNamePrefix: 'CMRI_India_' + year,
  //   scale: 463.313, // Change to your desired scale
  //   region: India
  // });
  
  
  // // Display the CMRI layer on the map
  // Map.addLayer(cmri_BD, {min: -1, max: 1, palette: ['FF0000', '00FF00']}, year + ' CMRI for Bangladesh');
  // Map.addLayer(cmri_India, {min: -1, max: 1, palette: ['FF0000', '00FF00']}, year + ' CMRI for India');
  
  
  
  //////////////////////////////////////////////////////////////////////////////////////////////////
  // Area Calculation
  //////////////////////////////////////////////////////////////////////////////////////////////////
  
  // Define the threshold for cmri_BD
  var threshold = 0.35;
  var pixelSizeSqKm = 454.1582149 * 454.1582149 / 1e6;
  
  // Create a binary image where cmri_BD > threshold
  var cmri_BD_GT_Threshold = cmri_BD.gt(threshold);
  
  // Calculate the number of pixels where cmri_BD > threshold
  var pixelCount_BD = cmri_BD_GT_Threshold.reduceRegion({
    reducer: ee.Reducer.sum(),
    geometry: BD,
    scale: 454.1582149
  });
  
  // Get the pixel count
  var count_BD = ee.Number(pixelCount_BD.get('NDVI'));
  
  // Calculate the area in square kilometers
  var areaSqKm_BD = count_BD.multiply(pixelSizeSqKm);
  
  // Print the area
  print('Bangladesh area (sq km) in ' + year, areaSqKm_BD);
  
  
  // Create a binary image where cmri_India > threshold
  var cmri_India_GT_Threshold = cmri_India.gt(threshold);
  
  // Calculate the number of pixels where cmri_India > threshold
  var pixelCount_India = cmri_India_GT_Threshold.reduceRegion({
    reducer: ee.Reducer.sum(),
    geometry: India,
    scale: 454.1582149
  });
  
  // Get the pixel count
  var count_India = ee.Number(pixelCount_India.get('NDVI'));
  
  // Calculate the area in square kilometers
  var areaSqKm_India = count_India.multiply(pixelSizeSqKm);
  
  // Print the area
  print('India area (sq km) in ' + year, areaSqKm_India);

});
