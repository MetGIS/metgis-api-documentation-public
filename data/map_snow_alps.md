# Snow Cover Map Alps

This map visualizes snow cover (snow/no snow). It is a snapshot of snow cover compiled from multiple data sources. Current data for the entire map area are not always available, and in certain weather conditions data ages of 1-2 weeks may occur. This is for two reasons: At first the main sources of data are satellites that rely on cloudless visibility, and secondly, there may be a delay of a few days between satellite recordings and their data availability. 

The [main map](#snow-cover) shows the snow cover, which combines all data sources.

Further maps are provided that show: 
- the snow cover observed by the [Sentinel](https://sentinel.esa.int/web/sentinel/missions/sentinel-2) satellites only, 
- the snow cover observed by the [MODIS](https://modis.gsfc.nasa.gov/about/) satellites only, 
- the age of the data of the combined snow cover map (latest update in all map locations), and 
- the information sources used in all locations of the combined snow cover map.

The most useful map for end users is probably the combined snow cover map. But the [map of data age](#snow-information-age) and the [map of information source](#snow-information-source) are surely interesting for certain groups.

### Embed In Website

All the following maps are served in vector format as protobuf files. The easiest way to embed a map into a website, is to use [maplibre-gl-js](https://github.com/maplibre/maplibre-gl-js).

<details>
  <summary><b>Basic Code Example</b></summary>

  ```html
  <!DOCTYPE html>
  <html>

  <head>
    <link rel="stylesheet" href="https://cdn.skypack.dev/maplibre-gl@^1.14.0/dist/maplibre-gl.css" />
    <style>
      * { margin: 0; padding: 0; }
      #map {position: absolute; top: 0; bottom: 0; width: 100%; }
    </style>
  </head>

  <body>
    <div id="map"></div>

    <script type="module">
      import { Map } from 'https://cdn.skypack.dev/maplibre-gl@^1.14.0'

      const map = new Map({
        container: "map",
        style: {
          version: 8,
          sources: {
            openstreetmap: {
              type: 'raster',
              tiles: [
                'https://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
                'https://b.tile.openstreetmap.org/{z}/{x}/{y}.png',
                'https://c.tile.openstreetmap.org/{z}/{x}/{y}.png'
              ]
            },
            snowmap: {
              type: 'vector',
              tiles: [
                'https://t1.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my-key>',
                'https://t2.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my-key>',
                'https://t3.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my-key>'
              ]
            }
          },
          layers: [
            {
              id: 'basemap',
              type: 'raster',
              source: 'openstreetmap',
              minzoom: 0,
              maxzoom: 22
            },
            { 
              id: 'snow_cover', 
              type: 'fill', 
              source: 'snowmap', 
              'source-layer': 'snow', 
              paint: { 
                'fill-color': '#0099FF', 
                'fill-opacity': 0.8, 
                'fill-outline-color': 'rgba(0, 0, 0, 1)' 
              } 
            }
          ]
        },
        center: [11.33982, 46.49067],
        zoom: 6
      })
    </script>
  </body>
  </html>
  ```

</details>

For styling you can use our predefined style provided in the style.json file (see below) or your own style.


**Main Map**
* [**Snow Cover** (snow cover map combined from multiple sources)](#snow-cover)

**Meta Maps**
* [**Snow Cover Sentinel** (snow cover map, only from Sentinel source)](#snow-cover-sentinel)
* [**Snow Cover MODIS** (snow cover map, only from MODIS source)](#snow-cover-modis)
* [**Data Age** (age of snow cover information)](#snow-information-age)
* [**Snow Information Source** (which area of the map stems from which source)](#snow-information-source)

**Point Data**
* [**Point Access API** (exact coordinates can be queried)](#point-information)

## Snow Cover
_Snow cover information, combined from Sentinel satellite information, MODIS satellite information and MetGIS snowfall forecast information._

* Protobuf Files
  ```
  https://t1.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my key>
  https://t2.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my key>
  https://t3.metgis.com/snow-cover/{z}/{x}/{y}.pbf?key=<my key>
  ```

* Style JSON
  ```
  https://t1.metgis.com/snow-cover/style.json?key=<my key>
  https://t2.metgis.com/snow-cover/style.json?key=<my key>
  https://t3.metgis.com/snow-cover/style.json?key=<my key>
  ```

* Tile JSON
  ```
  https://t1.metgis.com/snow-cover.json?key=<my key>
  https://t2.metgis.com/snow-cover.json?key=<my key>
  https://t3.metgis.com/snow-cover.json?key=<my key>
  ```

## Snow Cover Sentinel
_Snow cover information from Sentinel satellite information._

* Protobuf Files
  ```
  https://t1.metgis.com/snow-cover-sentinel/{z}/{x}/{y}.pbf?key=<my key>
  https://t2.metgis.com/snow-cover-sentinel/{z}/{x}/{y}.pbf?key=<my key>
  https://t3.metgis.com/snow-cover-sentinel/{z}/{x}/{y}.pbf?key=<my key>
  ```

* Style JSON
  ```
  https://t1.metgis.com/snow-cover-sentinel/style.json?key=<my key>
  https://t2.metgis.com/snow-cover-sentinel/style.json?key=<my key>
  https://t3.metgis.com/snow-cover-sentinel/style.json?key=<my key>
  ```

* Tile JSON
  ```
  https://t1.metgis.com/snow-cover-sentinel.json?key=<my key>
  https://t2.metgis.com/snow-cover-sentinel.json?key=<my key>
  https://t3.metgis.com/snow-cover-sentinel.json?key=<my key>
  ```

## Snow Cover MODIS
_Snow cover information from MODIS satellite information._

* Protobuf Files
  ```
  https://t1.metgis.com/snow-cover-modis/{z}/{x}/{y}.pbf?key=<my key>
  https://t2.metgis.com/snow-cover-modis/{z}/{x}/{y}.pbf?key=<my key>
  https://t3.metgis.com/snow-cover-modis/{z}/{x}/{y}.pbf?key=<my key>
  ```

* Style JSON
  ```
  https://t1.metgis.com/snow-cover-modis/style.json?key=<my key>
  https://t2.metgis.com/snow-cover-modis/style.json?key=<my key>
  https://t3.metgis.com/snow-cover-modis/style.json?key=<my key>
  ```

* Tile JSON
  ```
  https://t1.metgis.com/snow-cover-modis.json?key=<my key>
  https://t2.metgis.com/snow-cover-modis.json?key=<my key>
  https://t3.metgis.com/snow-cover-modis.json?key=<my key>
  ```

## Snow Information Age
_Represents the age of the data visually. Light green is newer, red is older._

**Notice**: _For a textual description of each layer, check the style.json attributes: "age-label"._

* Protobuf Files
  ```
  https://t1.metgis.com/snow-information-age/{z}/{x}/{y}.pbf?key=<my key>
  https://t2.metgis.com/snow-information-age/{z}/{x}/{y}.pbf?key=<my key>
  https://t3.metgis.com/snow-information-age/{z}/{x}/{y}.pbf?key=<my key>
  ```

* Style JSON
  ```
  https://t1.metgis.com/snow-information-age/style.json?key=<my key>
  https://t2.metgis.com/snow-information-age/style.json?key=<my key>
  https://t3.metgis.com/snow-information-age/style.json?key=<my key>
  ```

* Tile JSON
  ```
  https://t1.metgis.com/snow-information-age.json?key=<my key>
  https://t2.metgis.com/snow-information-age.json?key=<my key>
  https://t3.metgis.com/snow-information-age.json?key=<my key>
  ```


## Snow Information Source
_Shows which part of the [snow cover information map](#snow-cover) refers to which data source._

**Notice**: _For the source=>color mapping check the style.json and compare the fill-color attribute with the id attribute._

* Protobuf Files
  ```
  https://t1.metgis.com/snow-information-source/{z}/{x}/{y}.pbf?key=<my key>
  https://t2.metgis.com/snow-information-source/{z}/{x}/{y}.pbf?key=<my key>
  https://t3.metgis.com/snow-information-source/{z}/{x}/{y}.pbf?key=<my key>
  ```

* Style JSON
  ```
  https://t1.metgis.com/snow-information-source/style.json?key=<my key>
  https://t2.metgis.com/snow-information-source/style.json?key=<my key>
  https://t3.metgis.com/snow-information-source/style.json?key=<my key>
  ```

* Tile JSON
  ```
  https://t1.metgis.com/snow-information-source.json?key=<my key>
  https://t2.metgis.com/snow-information-source.json?key=<my key>
  https://t3.metgis.com/snow-information-source.json?key=<my key>
  ```

## Snow Cover Point Information

### Point Information
Returns for individual points information about the existence (or absence) of a snow cover, based on the combined snow cover source. Information can be queried by longitude-latitude coordinates.

```
https://api.metgis.com/snow-cover?key=<my key>&lonlat=lon1,lat1|lon2,lat2 ...
```

returns a response which is a valid geojson (can be visualized for example in: [geojson.io](https://geojson.io)) and looks like this:
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "snow": 0,
        "sensingTime": "2020-11-11T10:04:10.000Z",
        "source": "Sentinel",
        "marker-color": "#000"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          13.567,
          46.123
        ]
      }
    }
  ]
}
```
  * **snow**: 1 => snow, 0 => no snow
  * **sensingTime**: when the observation took place
  * **source**: data source for this point
  * **coordinates**: lon,lat

### Bounds of Data Area
Information about the extent of the snow cover map is provided.

```
https://api.metgis.com/snow-cover/bounds?key=<my key>
```

returns something like:

```json
{
  "upperLeftLon": 5,
  "upperLeftLat": 51.6,
  "lowerLeftLon": 5,
  "lowerLeftLat": 43,
  "lowerRightLon": 23,
  "lowerRightLat": 43,
  "upperRightLon": 23,
  "upperRightLat": 51.6
}
```
