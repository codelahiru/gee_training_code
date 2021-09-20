var l8raw = ee.ImageCollection("LANDSAT/LC08/C01/T1");

// Make a cloud-free composite and display it.
var composite = ee.Algorithms.Landsat.simpleComposite({
  collection: l8raw.filterDate('2017-01-01', '2017-12-31'),
  asFloat: true
});
var trueColorVis = {min: 0, max: 0.3, bands: ['B4','B3','B2']};
Map.addLayer(composite, trueColorVis, 'composite');


// Compute NDVI.
var ndvi = composite.normalizedDifference(['B5', 'B4']).rename('NDVI');

// Display NDVI.
Map.addLayer(ndvi, {min: 0, max: 1, palette: ['white', 'green']}, 'ndvi');
