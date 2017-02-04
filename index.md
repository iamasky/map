<!DOCTYPE html>
<html>
  <head>
    <title>Geolocation</title>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no">
    <meta charset="utf-8">
    <style>
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
      #map {
        height: 100%;
      }
    </style>
  </head>
  <body>
  	<h2>Fun! 高雄旅遊趣</h2>
    <button onClick="go();">GO School</button>
    <button onClick="goPosition();">GO Position</button>
    <div id="map"></div>
    <script>
// Note: This example requires that you consent to location sharing when
// prompted by your browser. If you see the error "The Geolocation service
// failed.", it means you probably did not give permission for the browser to
// locate you.


var map;
var marker;

function go() {
	var myLatLng = {lat:22.6750049, lng:120.2829533};
	map.setCenter( myLatLng );
	marker.setPosition( myLatLng );
	}

function goPosition() {
	  navigator.geolocation.getCurrentPosition(function(position) {
      var pos = {
        lat: position.coords.latitude,
        lng: position.coords.longitude
      };
	  map.setCenter(pos);
	  marker.setPosition(pos);
	  });
}


function initMap() {
  map = new google.maps.Map(document.getElementById('map'), {
    scaleControl: true,
	center: {lat: -34.397, lng: 150.644},
    zoom: 15
  });
  
  var infowindow = new google.maps.InfoWindow;
  infowindow.setContent('<b>目前所定位的位置</b>');
  
  // Try HTML5 geolocation.
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function(position) {
      var pos = {
        lat: position.coords.latitude,
        lng: position.coords.longitude
      };


      //infoWindow.setPosition(pos);
      //infoWindow.setContent('目前位置');
	  
	  //顯示目前位置
      map.setCenter(pos);
	  
	  marker = new google.maps.Marker({
	  map: map, 
	  position:{lat: position.coords.latitude, lng: position.coords.longitude},
	  title: "目前位置"
  	  });
	  
	  marker.addListener('click', function() {
      infowindow.open(map, marker);
      });
  
  	  var contentString = '<b>目前所定位的位置</b>';
  	  var infowindow = new google.maps.InfoWindow({
		content:contentString
  	  });
	  
	  var marker2 = new google.maps.Marker({
	  map: map, 
	  position:{lat: position.coords.latitude+0.003, lng: position.coords.longitude+0.003},
	  title: "第二位置"
  	  });
	  
	  var contentString = '<h1>第二位置<p><img src=http://icons.iconarchive.com/icons/martz90/circle/64/android-icon.png></h2>';
  	  var infowindow2 = new google.maps.InfoWindow({
		content:contentString,
		maxWidth: 300
  	  });
	  
	  marker2.addListener('mouseover', function() {
      infowindow2.open(map, marker2);
      });
  
      marker2.addListener('mouseout', function() {
      infowindow2.close();
      });
	  
    }, function() {
      handleLocationError(true, infoWindow, map.getCenter());
    });
  } else {
    // Browser doesn't support Geolocation
    handleLocationError(false, infoWindow, map.getCenter());
  }
}

function handleLocationError(browserHasGeolocation, infoWindow, pos) {
  infoWindow.setPosition(pos);
  infoWindow.setContent(browserHasGeolocation ?
                        'Error: The Geolocation service failed.' :
                        'Error: Your browser doesn\'t support geolocation.');
}



    </script>
    <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyAmkeppbrJJZvDeowFQISwWyH4lmMUHViQ&callback=initMap"
        async defer></script>
  </body>
</html>
