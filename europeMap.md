---
layout: page
permalink: /photos/europe/index.html
title: "Travel Map: Europe"
tags: [photos, Europe, map]
chart: true
comments: true
share: true
category: Photography
---




<div id="listdiv" style="width:200px; overflow:auto; height:600px; float:right;"></div>
<div id="mapdiv" style="height: 600px;"></div>            





<script type="text/javascript">
    var map;

    // svg path for Flag icon
    var icon = "M9.5,3v10c8,0,8,4,16,4V7C17.5,7,17.5,3,9.5,3z M6.5,29h2V3h-2V29z";

    AmCharts.ready(function() {
        map = new AmCharts.AmMap();
        map.pathToImages = "http://www.ammap.com/lib/3/images/";
        //map.panEventsEnabled = true; // this line enables pinch-zooming and dragging on touch devices
        map.imagesSettings = {
            color:"#000000",
        };
        map.allowClickOnSelectedObject = true
        map.backgroundZoomsToTop = true
        map.areasSettings = {
                    autoZoom: true,
                    color: "#0088cc",
                    selectedColor: "#ffcc00",
                    rollOverColor: "#CC0000",
                };


        map.zoomControl.buttonFillColor = "#0088cc";
        map.zoomControl.buttonRollOverColor= "#ffcc00";

        var dataProvider = {
            mapVar: AmCharts.maps.worldLow,
            zoomLevel: 5,
            zoomLongitude: 11.699611, 
            zoomLatitude: 46.652606,
            images: [
                        {
                            svgPath:icon,
                            latitude: 32.0833,
                            longitude: 34.8,
                            width: 24,
                            height: 24,
                            title: "Tel Aviv, Jerusalem, & others",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157628748155661/"
                        },
                        {
                            svgPath:icon,
                            latitude: 41.0136,
                            longitude: 28.955,
                            width: 24,
                            height: 24,
                            title: "Istanbul",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624268458721/"
                        },
                        {
                            svgPath:icon,
                            latitude: 47.4719,
                            longitude: 19.0503,
                            width: 24,
                            height: 24,
                            title: "Budapest & nearby",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393259156/"
                        },
                        {
                            svgPath:icon,
                            latitude: 48.2092,
                            longitude: 16.3728,
                            width: 24,
                            height: 24,
                            title: "Vienna",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393286162/"
                        },
                        {
                            svgPath:icon,
                            latitude: 50.0833,
                            longitude: 14.4167,
                            width: 24,
                            height: 24,
                            title: "Prague",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393278580/"
                        },
                        {
                            svgPath:icon,
                            latitude: 52.5167,
                            longitude: 13.3833,
                            width: 24,
                            height: 24,
                            title: "Berlin",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624268412885/"
                        },
                        {
                            svgPath:icon,
                            latitude: 51.2333,
                            longitude: 6.7833,
                            width: 24,
                            height: 24,
                            title: "Hamburg, Düsseldorf, and Koln",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393248364/"
                        },
                        {
                            svgPath:icon,
                            latitude: 46.9500,
                            longitude: 7.4500,
                            width: 24,
                            height: 24,
                            title: "Bern (and nearby)",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157636528671866/"
                        },
                        {
                            svgPath:icon,
                            latitude: 51.2167,
                            longitude: 3.2333,
                            width: 24,
                            height: 24,
                            title: "Bruges",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393222014/"
                        },
                        {
                            svgPath:icon,
                            latitude: 53.20,
                            longitude: 5.8,
                            width: 24,
                            height: 24,
                            title: "Friesland",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624268434665/"
                        },
                        {
                            svgPath:icon,
                            latitude: 52.3731,
                            longitude: 4.8922,
                            width: 24,
                            height: 24,
                            title: "Amsterdam & nearby",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624393252748/"
                        },
                        {
                            svgPath:icon,
                            latitude: 41.3833,
                            longitude: 2.1833,
                            width: 24,
                            height: 24,
                            title: "Barcelona",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157642932794635/"
                        },
                        {
                            svgPath:icon,
                            latitude: 51.5072,
                            longitude: 0.1275,
                            width: 24,
                            height: 24,
                            title: "Nottingham, Hebden Bridge, & London",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624268421549/"
                        },],
            areas:[
                {id:"IL", 
                    
                    zoomLevel: 10,
                    
                },
                {id:"TR",
                    zoomLevel: 10,
                },
                {id:"HU", 
                    zoomLevel: 10,
                },
                {id:"AT", 
                    zoomLevel: 10,
                },
                {id:"CZ", 
                    zoomLevel: 10,
                },
                {id:"DE", 
                    zoomLevel: 10,
                },
                {id:"CH", 
                    zoomLevel: 10,
                },
                {id:"BE", 
                    zoomLevel: 10,
                },
                {id:"NL", 
                    zoomLevel: 10,
                },
                {id:"ES", 
                    zoomLevel: 10,
                },
                {id:"GB",
                },      
                ],

        };
        map.dataProvider = dataProvider;

        map.objectList = new AmCharts.ObjectList("listdiv");
        map.showImagesInList = false;

        map.write("mapdiv");

});
</script>