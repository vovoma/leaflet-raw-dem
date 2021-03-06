Leaflet-raw-DEM
===============

A first attempt at reading and visualizing raw elevation data with Leaflet using Canvas.

Supports reading zipped DEM (Digital Elevation Model) files in the [ESRI BIL](http://resources.arcgis.com/en/help/main/10.1/index.html#//009t00000010000000) (Band interleaved by line) raster format (single band only), e.g. as provided by [USGS EarthExplorer](http://earthexplorer.usgs.gov/) for SRTM 1 Arc-Second Global.

Renders the data as raster grid, similar (yet very basic) to what desktop GIS like QGIS and uDig do, but in the Browser. With elevation labels on high zooms.

File viewer:
* [index.html](http://nrenner.github.io/leaflet-raw-dem/)  
Open local zipped BIL files (*_bil.zip) using the file dialog or drag&drop

Examples:
* [example/mallorca.html](http://nrenner.github.io/leaflet-raw-dem/example/mallorca.html) - [detail](http://nrenner.github.io/leaflet-raw-dem/example/mallorca.html#zoom=18&lat=39.828352&lon=3.115423) (building)  
Two SRTM 1-arc v3 files (1.9 MB and 2.5 MB) as example, loading may takes a few seconds
* [example/clip.html](http://nrenner.github.io/leaflet-raw-dem/example/clip.html)  
Minimal example using a 6*3 grid sample file, no extra dependencies, for development

## Status

Work in progress, known issues, needs validation and testing. Provided as is, not sure if continued or maintained (low priority).

## Limitations

* only single band BIL files supported
* assuming 16-bit signed integers and Little-endian (Intel) byte-order
* Spherical Mercator (EPSG 3857) only (?)
* only linear color scale supported right now
* ...

### Known issues

* border artefacts
* viewport not always fully covered at last row/column
* ...

## Usage

Convert other formats to BIL using ``gdal_translate`` with the [GDAL EHdr](http://www.gdal.org/frmt_various.html#EHdr) format, e.g.:

    mkdir tmp
    gdal_translate -of EHdr srtm_37_05/srtm_37_05.tif tmp/srtm_37_05.bil
    zip -j srtm_37_05_bil.zip tmp/*
    rm -r tmp

## Build

Requires [Node and npm](http://nodejs.org/) (or [io.js](https://iojs.org)), [Bower](http://bower.io/) and [Gulp](http://gulpjs.com/):

    npm install -g bower
    npm install -g gulp

Install:

    npm install
    bower install

Build:

    gulp

Develop:

    gulp watch


## To-do

* hgt format (basically the same with the header derived from the file name)
* Web Worker
* autoScale/stats across multiple layers
* ...

## Ideas / see also

* [buddebej/ol3-dem](https://github.com/buddebej/ol3-dem) - WebGL, eu-dem, png Data-Tiles
* [Dynamic hill shading in the browser](https://www.mapbox.com/blog/dynamic-hill-shading/)
* [xlhomme/GeotiffParser.js](https://github.com/xlhomme/GeotiffParser.js)
* [Terrain building with three.js](http://blog.thematicmapping.org/2013/10/terrain-building-with-threejs.html)
* [WCS i threejs](http://labs.kartverket.no/wcs-i-threejs/) - WCS, tiff-js, three.js (FOSS4G 2014 talk)
* [Weather-gridGL](http://briegn1.github.io/weather-gridGL/)
* [Turfjs/turf-isobands](https://github.com/Turfjs/turf-isobands)
* [Animated heatmaps and grids with Turf ](https://www.mapbox.com/blog/heatmaps-and-grids-with-turf/)

## License

Copyright (c) 2015 Norbert Renner, licensed under the [MIT License (MIT)](LICENSE)
