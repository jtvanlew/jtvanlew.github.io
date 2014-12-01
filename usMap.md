---
layout: page
permalink: /photos/usa/index.html
title: "Travel Map: United States"
tags: [photos, USA, United States, map]
chart: true
comments: true
share: true
category: Photography
---






<div id="mapdiv" style="height: 500px;"></div>            





<script type="text/javascript">
    var map;
    // svg path for Flag icon
    //var icon = "M9.5,3v10c8,0,8,4,16,4V7C17.5,7,17.5,3,9.5,3z M6.5,29h2V3h-2V29z";
    var icon = "M9,0C4.029,0,0,4.029,0,9s4.029,9,9,9s9-4.029,9-9S13.971,0,9,0z M9,15.93 c-3.83,0-6.93-3.1-6.93-6.93S5.17,2.07,9,2.07s6.93,3.1,6.93,6.93S12.83,15.93,9,15.93 M12.5,9c0,1.933-1.567,3.5-3.5,3.5S5.5,10.933,5.5,9S7.067,5.5,9,5.5 S12.5,7.067,12.5,9z";
    AmCharts.ready(function() {
        map = new AmCharts.AmMap();
        map.pathToImages = "http://www.ammap.com/lib/3/images/";
        //map.panEventsEnabled = true; // this line enables pinch-zooming and dragging on touch devices
        //map.imagesSettings = {
        //    color:"#000000",
        //};
        map.imagesSettings = {
                color: "#000000",
                rollOverColor: "#cc4400",
                rollOverScale: 2,
                selectedScale: 2,
                selectedColor: "#cc4400"
            };
        map.allowClickOnSelectedObject = true
        map.backgroundZoomsToTop = true
        map.areasSettings = {
                    autoZoom: true,
                    color: "#0088cc",
                    selectedColor: "#ffcc00",
                    rollOverColor: "#CC0000",
                    descriptionWindowY: 0,
                    descriptionWindowX: 800,
                    descriptionWindowWidth: 350,
                    descriptionWindowHeight: 450
                };

        map.zoomControl.buttonFillColor = "#0088cc";
        map.zoomControl.buttonRollOverColor= "#ffcc00";

        var dataProvider = {
            mapVar: AmCharts.maps.usaLow,
            //zoomLevel: 4,
            //zoomLongitude: 110.262958, 
            //zoomLatitude:32.527056,
            images: [
                        {
                            svgPath:icon,
                            latitude:-36.983064, longitude:-80.512686,
                            width: 24,
                            height: 24,
                            title: "Tucson",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-17.173892, longitude:-84.532376,
                            width: 24,
                            height: 24,
                            title: "Phoenix",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-7.451896, longitude:-79.005303,
                            width: 24,
                            height: 24,
                            title: "Forest Lakes",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-14.779314, longitude:-119.704658,
                            width: 24,
                            height: 24,
                            title: "San Diego",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:8.685042, longitude:-123.221887,
                            width: 24,
                            height: 24,
                            title: "Los Angeles",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-80.40832, longitude:-128.246499,
                            width: 24,
                            height: 24,
                            title: "Coldfoot",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:88.975517, longitude:-121.714503,
                            width: 24,
                            height: 24,
                            title: "Seattle",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:63.205383, longitude:-127.744037,
                            width: 24,
                            height: 24,
                            title: "Yosemite National Park",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:15.980185, longitude:-134.778494,
                            width: 24,
                            height: 24,
                            title: "Santa Cruz Island National Park",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:47.121191, longitude:-114.680047,
                            width: 24,
                            height: 24,
                            title: "Death Valley National Park",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:8.685042, longitude:-114.177585,
                            width: 24,
                            height: 24,
                            title: "Joshua Tree National Park",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:28.621505, longitude:-135.783416,
                            width: 24,
                            height: 24,
                            title: "El Capitan State Beach",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:79.984235, longitude:151.121917,
                            width: 24,
                            height: 24,
                            title: "New York City",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:83.363601, longitude:59.171521,
                            width: 24,
                            height: 24,
                            title: "Madison",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:60.870708, longitude:-43.330559,
                            width: 24,
                            height: 24,
                            title: "Breckenridge",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-1.245401, longitude:-50.867477,
                            width: 24,
                            height: 24,
                            title: "Albuquerque",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:77.56943, longitude:-76.492997,
                            width: 24,
                            height: 24,
                            title: "Ogden",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:48.789236, longitude:53.644448,
                            width: 24,
                            height: 24,
                            title: "St. Louis",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:58.999372, longitude:-142.817873,
                            width: 24,
                            height: 24,
                            title: "Pacific Coast Highway",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:38.946723, longitude:-54.887166,
                            width: 24,
                            height: 24,
                            title: "Durango",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        {
                            svgPath:icon,
                            latitude:-89.417824, longitude:-75.488075,
                            width: 24,
                            height: 24,
                            title: "Ketchican",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157624369084323/"
                        },
                        ],
            areas:[
                {id: "US-AZ",},
                {id: "US-CA",},
                {id: "US-WA",},
                {id: "US-NM",},
                {id: "US-AK",},
                //{id: "US-NV",},
                {id: "US-NY",},
                {id: "US-WI",},
                {id: "US-CO",},
                {id: "US-MO",},
                {id: "US-UT",},],
                            };
        map.dataProvider = dataProvider;

        map.objectList = new AmCharts.ObjectList("listdiv");
        map.showImagesInList = false;
        map.showAreasInList = true;
        map.write("mapdiv");

    });
</script>