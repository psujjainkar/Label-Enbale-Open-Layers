<!DOCTYPE html>
<html>
  <head>
    <title>Vector Layer</title>
    <link rel="stylesheet" href="https://openlayers.org/en/v3.20.1/css/ol.css" type="text/css">
    <!-- The line below is only needed for old environments like Internet Explorer and Android 4.x -->
    <script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=requestAnimationFrame,Element.prototype.classList,URL"></script>
    <script src="https://openlayers.org/en/v3.20.1/build/ol.js"></script>
  </head>
  <body>
    <div id="map" class="map"></div>
    <div id="info">&nbsp;</div>
    <script>
      var style = new ol.style.Style({
        fill: new ol.style.Fill({
          color: 'rgba(255, 255, 255, 0.6)'
        }),
        stroke: new ol.style.Stroke({
          color: '#319FD3',
          width: 1
        }),
        text: new ol.style.Text({
          font: '12px Calibri,sans-serif',
          fill: new ol.style.Fill({
            color: 'white'
          }),
          stroke: new ol.style.Stroke({
            color: 'blue',
            width: 3
          })
        })
      });

   

      var vectorLayer = new ol.layer.Vector({
        source: new ol.source.Vector({
          url: 'JSON URL',
          format: new ol.format.GeoJSON()
        }),
        style: function(feature, resolution) {
          style.getText().setText(resolution < 50 ? feature.get('name') : '');
          return style;
        }
      });

      var map = new ol.Map({
        layers: [
          new ol.layer.Tile({
            source: new ol.source.OSM()
          }),
          vectorLayer
        ],
        target: 'map',
        view: new ol.View({
          center: [0, 0],
          zoom: 5
        })
      });

      

    </script>
  </body>
</html>
