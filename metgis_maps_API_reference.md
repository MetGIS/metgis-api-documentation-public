# MetGIS Maps API

The MetGIS Maps API offers weather information as a Tile Map Service (TMS). This standardized format enables you to integrate our weather predictions into any dynamic map on your website or within your app. The data is delivered as tile maps. Check our [demo page](http://tiles.metgis.com/tiles-demo/) to see an example of weather data layers integrated into zoomable maps.

Tiled maps provide the map data in form of rectangular tiles. Tiles are accessed in a Z/X/Y notation, where Z is the zoom level and X,Y are the indices of the tiles. The 0th zoom level contains 1 tile (0/0/0) and would cover the whole earth. Each higher zoom level divides the tiles of the previous zoom level into 4 new tiles. So the 1st zoom level contains 4 tiles (1/0/0, 1/1/0, 1/0/1, 1/1/1). The n-th zoom level contains [2^(2n)](https://www.wolframalpha.com/input/?i=Table%5B2%5E%282n%29%2C%7Bn%2C0%2C22%2C1%7D%5D) tiles in total.

The tiles can be fetched from URLs similar to the ones below. There are multiple subdomains `t1`, `t2` and `t3` pointing to the same tiles in order to make the downloading of the tiles from the browser faster by increasing the allowed number of parallel connections.

```
https://t1.metgis.com/tmp2m-world_1/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/tmp2m-world_1/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/tmp2m-world_1/{z}/{x}/{y}.png?key=<my-key>
```

Fortunately, in practice, we don't have to worry about loading the individual tiles because we can use a library. For embedding a map into a website, you can use [maplibre-gl-js](https://maplibre.org/maplibre-gl-js-docs/api/).

## Overview of Available Weather and Snow Maps

| Weather Parameter                                              | Map Coverage | Unit      | Map Format  | Time Resolution | Forecast Range | Daily Updates |
| -------------------------------------------------------------- | ------------ | --------- | ----------- | --------------- | -------------- | ------------- |
| [Temperature](data/map_temperature.md)                         | World, Alps  | °C        | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Precipitation](data/map_precipitation.md)                     | World, Alps  | mm        | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Fresh Snow](data/map_fresh_snow.md)                           | World, Alps  | cm        | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Fresh Snow Daily](data/map_fresh_snow_daily.md)               | World, Alps  | cm        | Raster, UTF | 24/48/72 hrs    | 72 hrs         | 2             |
| [Sunshine Duration](data/map_sunshine_duration.md)             | World, Alps  | h         | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Cloudiness](data/map_cloudiness.md)                           | World, Alps  | %         | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Wind](data/map_wind.md)                                       | Alps         | km/h      | Raster, UTF | 3 hrs           | 72 hrs         | 2             |
| [Combined Weather Map (Clouds/Rain/Snow)](data/map_weather.md) | World, Alps  | %, mm, cm | Vector      | 3 hrs           | 72 hrs         | 2             |
| [Snow Cover](data/map_snow_alps.md)                            | Alps         | yes/no    | Vector      | -               | No forecast    | 1             |

Click on your parameter of interest to get more detailed map information!

## Difference Between Raster And Vector Maps

For raster maps, already rendered tiles (PNGs) are loaded. With vector maps, binary tiles are loaded and rendered on the client side. This gives vector maps the advantage that custom styles can be applied.

For vector maps a style must be defined _(we provide a default style for each map in the associated style.json file)_, for raster maps no style can be defined, they look like they come.

## Raster Maps

### [Temperature](data/map_temperature.md)

### [Precipitation](data/map_precipitation.md)

### [Fresh Snow](data/map_fresh_snow.md)

### [Fresh Snow Daily](data/map_fresh_snow_daily.md)

### [Sunshine Duration](data/map_sunshine_duration.md)

### [Cloudiness](data/map_cloudiness.md)

### [Wind](data/map_wind.md)

## Vector Maps

### [Snow Cover](data/map_snow_alps.md)

### [Combined Weather Map (Clouds, Rain, Snow)](data/map_weather.md)

## Time Step

Weather forecasts are issued for 3 hour intervals. They start at the time specified as `forecastIssued` in the [meta.json](#metajson). The parameters temperature, cloudiness and wind are valid for the exact time (e.g. 12:00 UTC), whereas the parameters precipitation, sunshine and fresh snow are valid for the whole interval of the past three hours (e.g. 9:00 UTC - 12:00 UTC) - this also means that there are no forecasts for these parameters for time step = 1.

To simplify the access to the tiles we introduced time steps which represent the 3 hour intervals. Starting at 1 - which reflects the weather forecasts for the time `forecastIssued` - it counts up to 25 where every single step counts as 3 hours. Please see the following table related to the example `"forecastIssued": "2015-01-03T18:00Z"` for clarification:

| **`timestep`** | **forecast valid for temperature, cloudiness + wind** | **forecast valid for precipitation + fresh snow** |
| -------------- | ----------------------------------------------------- | ------------------------------------------------- |
| 1              | 2015-01-03 18:00 UTC                                  | not available                                     |
| 2              | 2015-01-03 21:00 UTC                                  | 2015-01-03 18:00 - 21:00 UTC                      |
| 5              | 2015-01-04 6:00 UTC                                   | 2015-01-04 3:00 - 6:00 UTC                        |
| ...            | ...                                                   | ...                                               |
| 25             | 2015-01-06 12:00 UTC                                  | 2015-01-06 9:00 - 12:00 UTC                       |

## meta.json

For every forecast run a file with meta-information is produced. It contains the start time of the forecast run and other useful information. This `meta.json` is located at `http://tiles.metgis.com/meta/{V}/meta.json` where `{V}` stands for the version number. Please check the current version in [the changelog](http://tiles.metgis.com/meta/).

```endpoint
GET http://tiles.metgis.com/meta/{V}/meta.json
```

**Properties:**

| **Property**            | **Description**                                                                                                                                                                                                                                                                                                 |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `description`           | a brief description of the service                                                                                                                                                                                                                                                                              |
| `productInfo`           | information on the product                                                                                                                                                                                                                                                                                      |
| `forecastIssued`        | start time of the calculations of the meteorological forecast model as ISO-Datestring (UTC). This is also the time of the latest measurements that exercise an influence on the forecast.                                                                                                                       |
| `forecastCompleted`     | end time of the calculation of the tiles as ISO-Datestring (UTC)                                                                                                                                                                                                                                                |
| `projection`            | EPSG-Code of the coordinate reference system used for the tiles                                                                                                                                                                                                                                                 |
| `bbox`                  | the bounding box of the currently available tiles (latitude/longitude of the lower left and upper right box limit)                                                                                                                                                                                              |
| `timeStep`              | length of period of time between two forecast times, typically 3 hours                                                                                                                                                                                                                                          |
| `timeStepUnit`          | the unit of `timeStep` and `parameterPeriod`, `h` stands for hour                                                                                                                                                                                                                                               |
| `timeStepNumber`        | number of `timeSteps` for this forecast                                                                                                                                                                                                                                                                         |
| `attribution`           | attribution that has to be shown in conjunction with the forecasts, see the [demo page](http://tiles.metgis.com/tiles-demo/)                                                                                                                                                                                    |
| `parameters`            | list of available weather parameters                                                                                                                                                                                                                                                                            |
| `parameterUnit`         | unit of the given parameter                                                                                                                                                                                                                                                                                     |
| `parameterPeriod`       | time period which a single prediction refers to in hours. For most parameters (e.g. temperature) this is a point in time, for some others (e.g. `precipitation`) it is a period (typically as long as the `timeStep`). `0` indicates a point in time, any other number describes the length of the time period. |
| `parameterPeriodOffset` | **only for cumulated parameters,** defines the offset of the start time from `forecastIssued`                                                                                                                                                                                                                   |
| `parameterName`         | Language dependent name of the given parameter, indetified by ISO 639-1 Codes. Currently available languages: English, German, Spanish, French, Italian, Slovenian.                                                                                                                                             |

### Example Response

```json
{
  "description": "MetGIS Tile Server",
  "productInfo": "MetGIS Weather Forecast based on GFS Data",
  "forecastIssued": "2015-01-03T18:00Z",
  "forecastCompleted": "2015-01-04T03:44Z",
  "projection": "EPSG:3857",
  "bbox": "43.0,5.0,50.0,18.0",
  "timeStep": 3,
  "timeStepUnit": "h",
  "timeStepNumber": 25,
  "attribution": "Weather Forecast &copy; <a title='MetGIS Professional Weather Service' href='http://www.metgis.com/' target='_blank'>MetGIS</a>",
  "parameters": {
    "wind": {
      "parameterUnit": "km/h",
      "parameterPeriod": 0,
      "parameterName": {
        "sl": "Veter",
        "de": "Wind",
        "it": "Vento",
        "fr": "Vent",
        "en": "Wind",
        "es": "Viento"
      }
    },
    "tmp2m": {
      "parameterUnit": "°C",
      "parameterPeriod": 0,
      "parameterName": {
        "sl": "Temperatura",
        "de": "Temperatur",
        "it": "Temperatura",
        "fr": "Température",
        "en": "Temperature",
        "es": "Temperatura"
      }
    },
    "tcdcprs": {
      "parameterUnit": "%",
      "parameterPeriod": 0,
      "parameterName": {
        "sl": "Oblačnost",
        "de": "Bewölkung",
        "it": "Nuvolosità",
        "fr": "Nébulosité",
        "en": "Cloudiness",
        "es": "Nubosidad"
      }
    },
    "hr_p": {
      "parameterUnit": "mm",
      "parameterPeriod": 3,
      "parameterName": {
        "sl": "Padavine",
        "de": "Niederschlag",
        "it": "Precipitazione",
        "fr": "Précipitations",
        "en": "Precipitation",
        "es": "Precipitación"
      }
    },
    "hr_sn": {
      "parameterUnit": "cm",
      "parameterPeriod": 3,
      "parameterName": {
        "sl": "Novozapadli sneg",
        "de": "Neuschnee",
        "it": "Neve fresca",
        "fr": "Neige fraiche",
        "en": "Fresh Snow",
        "es": "Nieve fresca"
      }
    },
    "hr_sn_0-24": {
      "parameterUnit": "cm",
      "parameterPeriod": 24,
      "parameterPeriodOffset": 0,
      "parameterName": {
        "sl": "Novozapadli sneg 0-24h",
        "de": "Neuschnee 0-24h",
        "it": "Neve fresca 0-24h",
        "fr": "Neige fraiche 0-24h",
        "en": "Fresh Snow 0-24h",
        "es": "Nieve fresca 0-24h"
      }
    },
    "hr_sn_24-72": {
      "parameterUnit": "cm",
      "parameterPeriod": 48,
      "parameterPeriodOffset": 24,
      "parameterName": {
        "sl": "Novozapadli sneg 24-72h",
        "de": "Neuschnee 24-72h",
        "it": "Neve fresca 24-72h",
        "fr": "Neige fraiche 24-72h",
        "en": "Fresh Snow 24-72h",
        "es": "Nieve fresca 24-72h"
      }
    }
  }
}
```

## UTF Grids

### UTFGrid Tiles

Our [UTFGrids](https://github.com/mapbox/utfgrid-spec) provide numerical information related to our tiles. Like in our [demo page](https://tiles.metgis.com/tiles-demo/) you can use the UTFGrid Layers with a "mouseover" or "on tap" on mobile devices. Thus numerical forecast values can be displayed at specified geographic locations.

#### UTFGrid URL

```http
http://{t1-t3}.metgis.com/{parameter}_{timestep}_grid/{z}/{x}/{y}.json?callback={cb}&key={YOUR-API-KEY}
```

**Parameters:**

| **URL Parameter**   | **Description**                                                                                                                                                                              |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `{t1-t3}`           | subdomains to get around browser limitations on the number of simultaneous HTTP connections to each host, available are `t1`, `t2` and `t3`                                                  |
| `{parameter}`       | the code of the desired weather parameter as described in `meta.json`                                                                                                                        |
| `{timestep}`        | value of the desired time step, starting at 1 - which reflects the weather forecasts for the time `forecastIssued`, for clarification see [Time Step](#time-step) and [meta.json](#metajson) |
| `{x}`, `{y}`, `{z}` | x,y coordinates and zoom level of a tile                                                                                                                                                     |
| `{YOUR-API-KEY}`    | your unique API-Key, [more information](#api-key)                                                                                                                                            |

Please check our [sample code](#examples) to see how to use the UTFGrids in your application.

### Tiles Displaying Numerical Values for Selected Locations

To show values for a variety of significant locations (cities, towns, peaks, ...) as additional overlay on your map, you can integrate our Point-Layers. They are available for all of our [weather parameters](#weather-parameters).

#### Sample call

```http
http://{t1-t3}.metgis.com/{parameter}_{timestep}_point/{z}/{x}/{y}.png?key={YOUR-API-KEY}
```

### Color values

The color values related to the parameters are as follows:

**Temperature**

| **Value [°C]** | **Color** |
| -------------- | --------- |
| <-30           | `#737373` |
| -30            | `#969696` |
| -28            | `#bdbdbd` |
| -26            | `#efedf5` |
| -24            | `#dadaeb` |
| -22            | `#bcbddc` |
| -20            | `#9e9ac8` |
| -18            | `#807dba` |
| -16            | `#6a51a3` |
| -14            | `#544082` |
| -12            | `#06407c` |
| -10            | `#08519c` |
| -8             | `#2171b5` |
| -6             | `#4292c6` |
| -4             | `#6baed6` |
| -2             | `#9ecae1` |
| 0              | `#238443` |
| 2              | `#41ab5d` |
| 4              | `#78c679` |
| 6              | `#addd8e` |
| 8              | `#d9f0a3` |
| 10             | `#f7fcb9` |
| 12             | `#ffffcc` |
| 14             | `#ffeda0` |
| 16             | `#fed976` |
| 18             | `#feb24c` |
| 20             | `#fd8d3c` |
| 22             | `#fdbb84` |
| 24             | `#fc8d59` |
| 26             | `#ef6548` |
| 28             | `#d7301f` |
| 30             | `#bd0026` |
| 32             | `#b30000` |
| 34             | `#800026` |
| 36             | `#7f0000` |
| 38             | `#4c0016` |
| >40            | `#35000f` |

**Precipitation**

| **Value [mm]** | **Color** |
| -------------- | --------- |
| 0.1 <= x < 0.2 | `#deebf7` |
| 0.2 <= x < 0.5 | `#c6dbef` |
| 0.5 <= x < 1   | `#9ecae1` |
| 1 <= x < 1.5   | `#6baed6` |
| 1.5 <= x < 2   | `#4292c6` |
| 2 <= x < 3     | `#2171b5` |
| 3 <= x < 4     | `#08519c` |
| 4 <= x < 6     | `#08306b` |
| 6 <= x < 8     | `#fde0ef` |
| 8 <= x < 12    | `#f1b6da` |
| 12 <= x < 16   | `#de77ae` |
| 16 <= x        | `#c51b7d` |

**Fresh Snow**

| **Value [cm]** | **Color** |
| -------------- | --------- |
| 0.1 <= x < 0.3 | `#ffffff` |
| 0.3 <= x < 1   | `#c6ecf9` |
| 1 <= x < 2     | `#a0e0f6` |
| 2 <= x < 4     | `#59ccf2` |
| 4 <= x < 6     | `#19bbf1` |
| 6 <= x < 8     | `#019ccf` |
| 8 <= x < 12    | `#f79df3` |
| 12 <= x < 16   | `#f353ec` |
| 16 <= x < 20   | `#f311e8` |
| 20 <= x < 30   | `#fbc607` |
| 30 <= x < 50   | `#fba204` |
| 50 <= x < 80   | `#f7760f` |
| 80 <= x < 120  | `#e03603` |
| 120 <= x       | `#a11a04` |

**Cloudiness**

| **Value [%]**    | **Color** |
| ---------------- | --------- |
| 25 <= x < 37.5   | `#cccccc` |
| 37.5 <= x < 50   | `#b2b2b2` |
| 50 <= x < 62.5   | `#999999` |
| 62.5 <= x < 75   | `#7f7f7f` |
| 75 <= x < 87.5   | `#666666` |
| 87.5 <= x <= 100 | `#4c4c4c` |

**Sunshine Duration**

| **Value [h]** | **Color** |
| ------------- | --------- |
| 0.5           | `#f8eed1` |
| 1.5           | `#ebcd76` |
| 2.5           | `#dfad1b` |

**Wind**

| **Value [km/h]** | **Image**        |
| ---------------- | ---------------- |
| 0 <= x < 2       | wind-0-270.png   |
| 2 <= x < 5       | wind-2-270.png   |
| 5 <= x < 10      | wind-5-270.png   |
| 10 <= x < 20     | wind-10-270.png  |
| 20 <= x < 30     | wind-20-270.png  |
| 30 <= x < 40     | wind-30-270.png  |
| 40 <= x < 50     | wind-40-270.png  |
| 50 <= x < 75     | wind-50-270.png  |
| 75 <= x < 100    | wind-75-270.png  |
| 100 <= x         | wind-100-270.png |

#### JavaScript Objects for generating legends

```javascript
{
    "tmp2m": [[">40","#35000f"],["38","#4c0016"],["36","#7f0000"],["34","#800026"],["32","#b30000"],["30","#bd0026"],["28","#d7301f"],["26","#ef6548"],["24","#fc8d59"],["22","#fdbb84"],["20","#fd8d3c"],["18","#feb24c"],["16","#fed976"],["14","#ffeda0"],["12","#ffffcc"],["10","#f7fcb9"],["8","#d9f0a3"],["6","#addd8e"],["4","#78c679"],["2","#41ab5d"],["0","#238443"],["-2","#9ecae1"],["-4","#6baed6"],["-6","#4292c6"],["-8","#2171b5"],["-10","#08519c"],["-12","#06407c"],["-14","#544082"],["-16","#6a51a3"],["-18","#807dba"],["-20","#9e9ac8"],["-22","#bcbddc"],["-24","#dadaeb"],["-26","#efedf5"],["-28","#bdbdbd"],["-30","#969696"],["<-30","#737373"]],

    "hr_p": [["16","#c51b7d"],["12","#de77ae"],["8","#f1b6da"],["6","#fde0ef"],["4","#08306b"],["3","#08519c"],["2","#2171b5"],["1.5","#4292c6"],["1","#6baed6"],["0.5","#9ecae1"],["0.2","#c6dbef"],["0.1","#deebf7"]],

	"hr_sn_cumulated": [["120","#a11a04"],["80","#e03603"],["50","#f7760f"],["30","#fba204"],["20","#fbc607"],["16","#f311e8"],["12","#f353ec"],["8","#f79df3"],["6","#019ccf"],["4","#19bbf1"],["2","#59ccf2"],["1","#a0e0f6"],["0.3","#c6ecf9"],["0.1","#ffffff"]],

    "hr_sn": [["16","#f311e8"],["12","#f353ec"],["8","#f79df3"],["6","#019ccf"],["4","#19bbf1"],["2","#59ccf2"],["1","#a0e0f6"],["0.3","#c6ecf9"],["0.1","#ffffff"]],

    "tcdcprs": [["87.5","#4c4c4c"],["75","#666666"],["62.5","#7f7f7f"],["50","#999999"],["37.5","#b2b2b2"],["25","#cccccc"]],

    "snsd_3h": [["2.5","#dfad1b"],["1.5","#ebcd76"],["0.5","#f8eed1"]],

    "wind": [["100","#ffffff url('img/270n/wind-100-270.png') no-repeat center; width: 59px; height: 33px;"],["75","#ffffff url('img/270n/wind-75-270.png') no-repeat center; width: 54px; height: 30px;"],["50","#ffffff url('img/270n/wind-50-270.png') no-repeat center; width: 48px; height: 28px;"],["40","#ffffff url('img/270n/wind-40-270.png') no-repeat center; width: 43px; height: 24px;"],["30","#ffffff url('img/270n/wind-30-270.png') no-repeat center; width: 36px; height: 20px;"],["20","#ffffff url('img/270n/wind-20-270.png') no-repeat center; width: 29px; height: 16px;"],["10","#ffffff url('img/270n/wind-10-270.png') no-repeat center; width: 23px; height: 13px;"],["5","#ffffff url('img/270n/wind-5-270.png') no-repeat center; width: 18px; height: 10px;"],["2","#ffffff url('img/270n/wind-2-270.png') no-repeat center; width: 13px; height: 8px;"],["0","#ffffff url('img/270n/wind-0-270.png') no-repeat center; width: 8px; height: 8px;"]]
  }
```

## Examples

Our weather maps may be integrated into your website or app, using different software frameworks. Some of them are:

**Web**

- [Leaflet](http://leafletjs.com/)
- [OpenLayers](http://openlayers.org/)
- [Google Maps API](https://developers.google.com/maps/)

**Apps**

- [Google Maps Android API](https://developers.google.com/maps/documentation/android/)
- [Google Maps SDK for iOS](https://developers.google.com/maps/documentation/ios/)
- Apple's [Maps for Developers](https://developer.apple.com/maps/)
- [Mapbox SDK](https://www.mapbox.com/mobile/)

#### Example of integration with Leaflet

```javascript
var temperatureLayer = L.tileLayer(
  "http://t1.metgis.com/tmp2m_5/{z}/{x}/{y}.png?key=YOUR_API_KEY"
);
```

The following examples show possible implementations with different frameworks.

### Leaflet

This exapmle shows how to implement a weather map using [Leaflet](http://leafletjs.com/).

#### Example of temperature integration:

```javascript
var tmp2mUrl = "http://{s}.metgis.com/tmp2m_";
var urlSuffix = "/{z}/{x}/{y}.png?key=YOUR-API-KEY";
var timestep = 1; // a value between 1 and 25

var layertmp2m = L.tileLayer(tmp2mUrl + timestep + urlSuffix, {
  maxZoom: 15,
  attribution:
    "Weather Forecast &copy; <a title='MetGIS Professional Weather Service' href='http://www.metgis.com/' target='_blank'>MetGIS</a>",
  opacity: 0.7,
  subdomains: ["t1", "t2", "t3"]
});
```

#### Add UTFGrids

```javascript
// To integrate UTFGrids with Leaflet you have to use the Leaflet.utfgrid plugin.
// https://github.com/danzel/Leaflet.utfgrid

var tmp2mGridUrl = "http://{s}.metgis.com/tmp2m_";
var gridUrlSuffix = "_grid/{z}/{x}/{y}.json?callback={cb}";
var timestep = 1; // a value between 1 and 25

var layertmp2mGrid = new L.UtfGrid(tmp2mGridUrl + timestep + gridUrlSuffix, {
  resolution: 4,
  pointerCursor: false,
  maxRequests: 8,
  subdomains: ["t1", "t2", "t3"]
});
layertmp2mGrid.on("mouseover", function(e) {
  console.log(e.data);
});
```

Please refer to our [demo page](http://tiles.metgis.com/tiles-demo/) to view a fully functional example.

### OpenLayers 3

This exapmle shows how to implement a weather map using [OpenLayers](http://openlayers.org/).

#### Simple example of temperature:

```javascript
var map = new ol.Map({
  target: "map",
  layers: [
    new ol.layer.Tile({
      source: new ol.source.MapQuest({ layer: "sat" })
    }),
    new ol.layer.Tile({
      source: new ol.source.XYZ({
        url: "http://t{1-3}.metgis.com/tmp2m_7/{z}/{x}/{y}.png",
        maxZoom: 15,
        attributions: [
          new ol.Attribution({
            html:
              "Weather Forecast &copy; <a title='MetGIS Professional Weather Service' href='http://www.metgis.com/' target='_blank'>MetGIS</a>"
          })
        ]
      }),
      opacity: 0.7
    })
  ],
  view: new ol.View({
    center: ol.proj.transform([12.41, 47.82], "EPSG:4326", "EPSG:3857"),
    zoom: 5
  })
});
```

#### With UTFGrids:

```javascript
var view = new ol.View({
  center: ol.proj.transform([12.41, 47.82], "EPSG:4326", "EPSG:3857"),
  zoom: 5
});
var gridSource = new ol.source.TileUTFGrid({
  url:
    "http://tiles.metgis.com/meta/0.6/metgis_tilejsonwrapper.php?parameter=hr_p&timestep=7&key=YOUR-API-KEY"
});
var gridLayer = new ol.layer.Tile({ source: gridSource });

var map = new ol.Map({
  target: "map",
  layers: [
    new ol.layer.Tile({
      source: new ol.source.MapQuest({ layer: "sat" })
    }),
    new ol.layer.Tile({
      source: new ol.source.XYZ({
        url: "http://t{1-3}.metgis.com/hr_p_7/{z}/{x}/{y}.png",
        maxZoom: 15,
        attributions: [
          new ol.Attribution({
            html:
              "Weather Forecast &copy; <a title='MetGIS Professional Weather Service' href='http://www.metgis.com/' target='_blank'>MetGIS</a>"
          })
        ]
      }),
      opacity: 0.7
    }),
    gridLayer
  ],
  view: view
});

var displayCountryInfo = function(coordinate) {
  var viewResolution = /** @type {number} */ (view.getResolution());
  gridSource.forDataAtCoordinateAndResolution(
    coordinate,
    viewResolution,
    function(data) {
      console.log(data);
    }
  );
};

map.on("pointermove", function(evt) {
  if (evt.dragging) {
    return;
  }
  var coordinate = map.getEventCoordinate(evt.originalEvent);
  displayCountryInfo(coordinate);
});
```

**Note:** the `ol.source.TileUTFGrid` expects a [TileJSON](https://github.com/mapbox/tilejson-spec) file. We provide a PHP script that returns the appropriate data. Please submit the required fields to the query string to get the correct version.

`http://tiles.metgis.com/meta/0.6/metgis_tilejsonwrapper.php?parameter={parameter}&timestep={timestep}&key={YOUR-API-KEY}&callback={cb}`

Please refer to the official OpenLayers [TileUTFGrid Example](http://openlayers.org/en/v3.6.0/examples/tileutfgrid.html) for more information regarding the `ol.source.TileUTFGrid`.

## Common Errors
Will be added shortly.

