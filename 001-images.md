var srtm = ee.Image("USGS/SRTMGL1_003"),
    forest = ee.Image("UMD/hansen/global_forest_change_2016_v1_4");

// Display
Map.addLayer(srtm, {min: 0, max: 3000}, 'srtm');
Map.addLayer(forest, {bands: 'loss', max: 1}, 'loss');

/*
// Extract a band
var loss = forest.select('loss');

// Mask the band with itself to remove zeros
Map.addLayer(loss.updateMask(loss), {palette: 'red'}, 'masked loss');
*/
