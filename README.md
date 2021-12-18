<!DOCTYPE HTML>
<html lang="en-US">
<head>
  <meta charset="UTF-8">
  <title></title>
  <style type="text/css">
  #map_canvas {
    height: 300px;
    width: 300px;
  }
  </style>
</head>
<body>
<div id="map_canvas" width="300" height="300"></div>
<input type="text" id="query" value=""/>
<input type="submit" id="search" value="search"/>
<script src="http://maps.googleapis.com/maps/api/js?sensor=false" src="//maps.google.com/maps/api/js?sensor=false"></script>
<script type="text/javascript">
var geo = {};
window.onload = function() {
  var latlng = new google.maps.LatLng(39.102431, -94.583698),
      options  = {
        zoom               : 4,
        mapTypeId          : google.maps.MapTypeId.TERRAIN,
        center             : latlng,
        streetViewControl  : true,
        scaleControl       : true,
        scrollwheel        : true,
        mapTypeControl     : true,
        overviewMapControl : true,
        panControlOptions  : {
          position         : google.maps.ControlPosition.TOP_LEFT
        },
        zoomControlOptions : {
          position         : google.maps.ControlPosition.TOP_LEFT
        }
      };
      map    = new google.maps.Map(document.getElementById('map_canvas'), options),
      marker = new google.maps.Marker({
                     position  : latlng,
                     map       : map,
                     draggable : false
                   }),
      geocoder = new google.maps.Geocoder(),
      search = document.getElementById('search'), 
      query = document.getElementById('query');

  function codeAddress() {
    var address = query.value;
    geocoder.geocode( { 'address': address}, function(results, status) {
      console.log(results);
      if (status == google.maps.GeocoderStatus.OK) {
        map.setCenter(results[0].geometry.location);
        var marker = new google.maps.Marker({
            map: map,
            position: results[0].geometry.location
        });
      } else {
        alert("Geocode was not successful for the following reason: " + status);
      }
    });
  };

  search.onclick = function() {
   codeAddress(); 
  };
};
</script>
</body>
</html>
