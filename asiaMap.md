---
layout: page
permalink: /photos/asia/index.html
title: "Travel Map: Asia"
tags: [photos, Asia, map]
chart: true
comments: true
share: true
category: Photography
---


<div id="listdiv" style="width:200px; overflow:auto; height:500px; float:right;"></div>
<div id="mapdiv" style="height: 500px;"></div>            











<script type="text/javascript">
    var map;
    var descriptionBurgundy = 'test';
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
                    descriptionWindowY: 0,
                    descriptionWindowX: 800,
                    descriptionWindowWidth: 350,
                    descriptionWindowHeight: 450
                };

        map.zoomControl.buttonFillColor = "#0088cc";
        map.zoomControl.buttonRollOverColor= "#ffcc00";

        var dataProvider = {
            mapVar: AmCharts.maps.worldLow,
            zoomLevel: 4,
            zoomLongitude: 110.262958, 
            zoomLatitude:32.527056,
            images: [
                        {
                            svgPath:icon,
                            latitude: 13.7500,
                            longitude: 100.4667,
                            width: 24,
                            height: 24,
                            title: "Chiang Mai, Phuket, & Bangkok",
                            url: "https://www.flickr.com/photos/jtvanlew/collections/72157649188613270/"
                        },
                        {
                            svgPath:icon,
                            latitude: 39.9139,
                            longitude: 116.3917,
                            width: 24,
                            height: 24,
                            title: "Beijing",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157628701218815/"
                        },
                        {
                            svgPath:icon,
                            latitude: 32.05,
                            longitude: 118.7667,
                            width: 24,
                            height: 24,
                            title: "Nanjing",
                            url: "http://www.flickr.com/photos/jtvanlew/collections/72157637897569516/"
                        },
                        {
                            svgPath:icon,
                            latitude: 29.65,
                            longitude: 91.1,
                            width: 24,
                            height: 24,
                            title: "Tibet",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624393012924/"
                        },
                        {
                            svgPath:icon,
                            latitude: 31.2,
                            longitude: 121.5,
                            width: 24,
                            height: 24,
                            title: "Shanghai",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157628733053801/"
                        },
                        {
                            svgPath:icon,
                            latitude: 31.3,
                            longitude: 120.6,
                            width: 24,
                            height: 24,
                            title: "Suzhou",
                            url: "http://www.flickr.com/photos/jtvanlew/collections/72157637898268663/"
                        },
                        {
                            svgPath:icon,
                            latitude: 32.9,
                            longitude: 119.8,
                            width: 24,
                            height: 24,
                            title: "Towns in the Jiangsu Province",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157628731953493/"
                        },
                        {
                            svgPath:icon,
                            latitude: 34.2667,
                            longitude: 108.9,
                            width: 24,
                            height: 24,
                            title: "Xi'an",
                            url: "http://www.flickr.com/photos/jtvanlew/collections/72157637898085464/"
                        },
                        {
                            svgPath:icon,
                            latitude: 34.4833,
                            longitude: 110.0833,
                            width: 24,
                            height: 24,
                            title: "Huashan Mountain",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624392985964/"
                        },
                        {
                            svgPath:icon,
                            latitude: 35.2667,
                            longitude: 108.8,
                            width: 24,
                            height: 24,
                            title: "Baolong Ravine",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624267569893/"
                        },
                        {
                            svgPath:icon,
                            latitude: 25.0667,
                            longitude: 102.6833,
                            width: 24,
                            height: 24,
                            title: "Kunming, Dali, Lijiang, and Baoshang Village",
                            url: "http://www.flickr.com/photos/jtvanlew/collections/72157637896841195/"
                        },
                        {
                            svgPath:icon,
                            latitude: 35.0117,
                            longitude: 135.7683,
                            width: 24,
                            height: 24,
                            title: "Kyoto",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157627504638174/"
                        },
                        {
                            svgPath:icon,
                            latitude: 34.6939,
                            longitude: 135.5022,
                            width: 24,
                            height: 24,
                            title: "Osaka",
                            url: "https://www.flickr.com/photos/jtvanlew/sets/72157627504638174/"
                        },
                        {
                            svgPath:icon,
                            latitude: 25.0333,
                            longitude: 121.6333,
                            width: 24,
                            height: 24,
                            title: "Taipei",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624184180487/"
                        },
                        {
                            svgPath:icon,
                            latitude: 22.6333,
                            longitude: 120.2667,
                            width: 24,
                            height: 24,
                            title: "Kaosiung",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624179652395/"
                        },
                        {
                            svgPath:icon,
                            latitude: 22.9833,
                            longitude: 120.1833,
                            width: 24,
                            height: 24,
                            title: "Tainan",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624184150727/"
                        },
                        {
                            svgPath:icon,
                            latitude: 23.9830,
                            longitude: 120.7326,
                            width: 24,
                            height: 24,
                            title: "Caotun",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624179280179/"
                        },
                        {
                            svgPath:icon,
                            latitude: 21.9800,
                            longitude: 120.7970,
                            width: 24,
                            height: 24,
                            title: "Kenting",
                            url: "http://www.flickr.com/photos/jtvanlew/sets/72157624304338448/"
                        },],
            areas:[
                {id:"CN", description: descriptionBurgundy, zoomLevel: 5, },
                {id:"JP", zoomLevel: 10, },
                {id:"TW", },
                {id:"TH", }, ],

                            };
        map.dataProvider = dataProvider;

        map.objectList = new AmCharts.ObjectList("listdiv");
        map.showImagesInList = false;
        map.showAreasInList = true;
        map.write("mapdiv");

    });
</script>
