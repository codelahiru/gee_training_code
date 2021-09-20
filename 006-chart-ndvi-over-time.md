var roi = /* color: #00ff00 */ee.Geometry.Point([-122.10067749023438, 37.43615762405059]),
    l8 = ee.ImageCollection("LANDSAT/LC08/C01/T1_TOA");

// Define a function that will add an NDVI band to a Landsat 8 image.
var addNDVI = function(image) {
  var ndvi = image.normalizedDifference(['B5', 'B4']).rename('NDVI');
  return image.addBands(ndvi);
};

// Filter and map the function over the collection.
var withNDVI = l8.filterDate('2017-01-01', '2017-12-31')
    .map(addNDVI); // <-- map() the function over the collection.

// Make a chart.
var chart = ui.Chart.image.series({
  imageCollection: withNDVI.select('NDVI'),
  region: roi,
  reducer: ee.Reducer.first(),
  scale: 30
});

// Define custom options for the chart. See:
// https://developers.google.com/chart/interactive/docs/reference
var options = {
  title: 'NDVI over time',
  hAxis: { title: 'time' },
  vAxis: { title: 'NDVI' },
  series: {
    0: { color: 'green' }
  }
};

// Set the options of the chart and print it.
chart = chart.setOptions(options);
print(chart);    
