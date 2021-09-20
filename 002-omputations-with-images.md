var srtm = ee.Image("USGS/SRTMGL1_003"), forest = ee.Image("UMD/hansen/global_forest_change_2016_v1_4");

// Compute slope from the SRTM image.
var slope = ee.Terrain.slope(srtm);

var slopevis = {min: 0, max: 30, palette: ['green','yellow','red']};

Map.addLayer(srtm, {min: 0, max: 3000}, 'DEM');
Map.addLayer(slope, slopevis, 'slope');
/*

// Compute forest loss after 2010.
var lossAfter2010 = forest.select(['lossyear']).gt(10);
var visParams = {min: 0, max: 1, palette: ['black', 'red']};
//Map.addLayer(lossAfter2010, visParams, 'lossAfter2010');
*/
    
