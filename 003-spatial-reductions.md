var srtm = ee.Image("USGS/SRTMGL1_003"),
    geometry = /* color: #ffc82d */ee.Geometry.Polygon(
        [[[-112.17864990234375, 36.12345548205636],
          [-112.2747802734375, 36.02466804934359],
          [-112.14019775390625, 36.00911716117325],
          [-111.99736151664732, 36.10624062602223]]]),
    forest = ee.Image("UMD/hansen/global_forest_change_2016_v1_4");

var slope = ee.Terrain.slope(srtm);
Map.addLayer(slope, {min: 0, max: 60}, 'slope');

// Compute mean slope in a hand-drawn polygon.
var slopeDict = slope.reduceRegion({
  reducer: ee.Reducer.mean(),
  geometry: geometry,
  scale: 30 // meters!
});
print(slopeDict);

/*
// Compute forest loss area.
var lossDict = forest.select('loss')
    .multiply(ee.Image.pixelArea()) // Square meters!
    .reduceRegion({
      reducer: ee.Reducer.sum(),
      geometry: geometry,
      scale: 30 // meters!
    });
print(lossDict.get('loss')); // Square meters!
*/
