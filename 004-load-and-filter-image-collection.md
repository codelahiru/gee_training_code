var l8 = ee.ImageCollection("LANDSAT/LC08/C01/T1_TOA");

// Filter the image collection to a date range.
var filtered = l8.filterDate('2017-07-01', '2017-07-31');

// Add to the map as a most-recent pixel mosaic.
Map.addLayer(filtered, {}, 'filtered');
