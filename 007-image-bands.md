var l8 = ee.ImageCollection("LANDSAT/LC08/C01/T1_TOA");

// Filter to all images in 2017.
var filtered = l8.filterDate('2017-01-01', '2017-12-31');

// Define a true color visualization for Landsat 8.
var trueColorVis = {min: 0, max: 0.3, bands: ['B4', 'B3', 'B2']};

// Display a most-recent pixel composite (and mosaic) as true-color.
Map.addLayer(filtered, trueColorVis, 'filtered (true-color)');

// Define a false-color (color IR) visualization for Landsat 8.
var colorIrVis = {min: 0, max: 0.3, bands: ['B5', 'B4', 'B3']};

// Display a most-recent pixel composite (and mosaic) as false-color.
Map.addLayer(filtered, colorIrVis, 'filtered (false-color)');
