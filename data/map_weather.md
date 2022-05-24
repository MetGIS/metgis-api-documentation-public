# Weather Map

Clouds, rain and snow are visualized in one single map.

Multiple time steps are available and there is one independent map per time step.

The map is available in two versions. One version covers the entire world, the other version covers only the Alps region with a resolution more than ten times higher.

### Embed In Website

All the following maps are served in vector format as protobuf files. The easiest way to embed a map into a website, is to use [maplibre-gl-js](https://github.com/maplibre/maplibre-gl-js).

<details>
  <summary><b>Basic Code Example</b></summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <link
      rel="stylesheet"
      href="https://cdn.skypack.dev/maplibre-gl@^1.14.0/dist/maplibre-gl.css"
    />
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
    </style>
  </head>

  <body>
    <div id="map"></div>

    <script type="module">
      import { Map } from "https://cdn.skypack.dev/maplibre-gl@^1.14.0";

      const map = new Map({
        container: "map",
        style: {
          version: 8,
          sources: {
            openstreetmap: {
              type: "raster",
              tiles: [
                "https://a.tile.openstreetmap.org/{z}/{x}/{y}.png",
                "https://b.tile.openstreetmap.org/{z}/{x}/{y}.png",
                "https://c.tile.openstreetmap.org/{z}/{x}/{y}.png"
              ]
            },
            weathermap: {
              type: "vector",
              tiles: [
                "https://t1.metgis.com/weathermap-world_t45/{z}/{x}/{y}.pbf?key=<my-key>",
                "https://t2.metgis.com/weathermap-world_t45/{z}/{x}/{y}.pbf?key=<my-key>",
                "https://t3.metgis.com/weathermap-world_t45/{z}/{x}/{y}.pbf?key=<my-key>"
              ]
            }
          },
          layers: [
            {
              id: "basemap",
              type: "raster",
              source: "openstreetmap",
              minzoom: 0,
              maxzoom: 22
            },
            {
              id: "clouds-2",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-2"]],
              paint: {
                "fill-color": "#cccccc"
              }
            },
            {
              id: "clouds-3",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-3"]],
              paint: {
                "fill-color": "#b2b2b2"
              }
            },
            {
              id: "clouds-4",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-4"]],
              paint: {
                "fill-color": "#999999"
              }
            },
            {
              id: "clouds-5",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-5"]],
              paint: {
                "fill-color": "#7f7f7f"
              }
            },
            {
              id: "clouds-6",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-6"]],
              paint: {
                "fill-color": "#666666"
              }
            },
            {
              id: "clouds-7",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "clouds-7"]],
              paint: {
                "fill-color": "#4c4c4c"
              }
            },
            {
              id: "rain-2",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-2"]],
              paint: {
                "fill-color": "#ADBAFA"
              }
            },
            {
              id: "rain-3",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-3"]],
              paint: {
                "fill-color": "#9DACF5"
              }
            },
            {
              id: "rain-4",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-4"]],
              paint: {
                "fill-color": "#8D9FF1"
              }
            },
            {
              id: "rain-5",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-5"]],
              paint: {
                "fill-color": "#7E91EC"
              }
            },
            {
              id: "rain-6",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-6"]],
              paint: {
                "fill-color": "#6E84E7"
              }
            },
            {
              id: "rain-7",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-7"]],
              paint: {
                "fill-color": "#5E76E3"
              }
            },
            {
              id: "rain-8",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-8"]],
              paint: {
                "fill-color": "#4E68DE"
              }
            },
            {
              id: "rain-9",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-9"]],
              paint: {
                "fill-color": "#3F5BD9"
              }
            },
            {
              id: "rain-10",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-10"]],
              paint: {
                "fill-color": "#2F4DD5"
              }
            },
            {
              id: "rain-11",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-11"]],
              paint: {
                "fill-color": "#1F40D0"
              }
            },
            {
              id: "rain-12",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-12"]],
              paint: {
                "fill-color": "#0F32CB"
              }
            },
            {
              id: "rain-13",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "rain-13"]],
              paint: {
                "fill-color": "#0025C7"
              }
            },
            {
              id: "snow-2",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-2"]],
              paint: {
                "fill-color": "#F7C2F0"
              }
            },
            {
              id: "snow-3",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-3"]],
              paint: {
                "fill-color": "#EFB3E7"
              }
            },
            {
              id: "snow-4",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-4"]],
              paint: {
                "fill-color": "#E7A4DD"
              }
            },
            {
              id: "snow-5",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-5"]],
              paint: {
                "fill-color": "#DF95D4"
              }
            },
            {
              id: "snow-6",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-6"]],
              paint: {
                "fill-color": "#D786CA"
              }
            },
            {
              id: "snow-7",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-7"]],
              paint: {
                "fill-color": "#CF77C1"
              }
            },
            {
              id: "snow-8",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-8"]],
              paint: {
                "fill-color": "#C768B7"
              }
            },
            {
              id: "snow-9",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-9"]],
              paint: {
                "fill-color": "#BF59AE"
              }
            },
            {
              id: "snow-10",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-10"]],
              paint: {
                "fill-color": "#B74AA4"
              }
            },
            {
              id: "snow-11",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-11"]],
              paint: {
                "fill-color": "#AF3B9B"
              }
            },
            {
              id: "snow-12",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-12"]],
              paint: {
                "fill-color": "#A72C91"
              }
            },
            {
              id: "snow-13",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-13"]],
              paint: {
                "fill-color": "#9F1D88"
              }
            },
            {
              id: "snow-14",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-14"]],
              paint: {
                "fill-color": "#970E7E"
              }
            },
            {
              id: "snow-15",
              type: "fill",
              source: "weathermap",
              "source-layer": "weathermap",
              filter: ["all", ["==", "layer", "snow-15"]],
              paint: {
                "fill-color": "#8F0075"
              }
            }
          ]
        },
        center: [11.33982, 46.49067],
        zoom: 6
      });
    </script>
  </body>
</html>
```

</details>

For styling you can use our predefined style provided in the style.json file or your own style.

## Weather Map World

_Worldwide weather map, which shows clouds, rain and snow in one map._

This meta.json: https://api.metgis.com/meta-weathermap-world provides all access urls.
The array “layers” contains an entry per available time step. Every entry provides access URLs for vector-tiles (in .pbf format), tile.json and style.json. To use these URLs, you have to append your access key as a query parameter: `?key=<my-key>`

## Weather Map Alps

_Weather map covering the Alps region, showing clouds, rain and snow in one map._

<details>
  <summary>Bbox: minLon: 5, minLat: 43, maxLon: 23, maxLat: 51.2</summary>

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [5, 43],
            [5, 51.2],
            [23, 51.2],
            [23, 43],
            [5, 43]
          ]
        ]
      },
      "properties": {}
    }
  ]
}
```

</details>

This meta.json: https://api.metgis.com/meta-weathermap-alps provides all access urls.
The array ”layers” contains an entry per available time step. Every entry provides access URLs for vector-tiles (in .pbf format), tile.json and style.json. To use these URLs, you have to append your access key as a query parameter: `?key=<my-key>`
