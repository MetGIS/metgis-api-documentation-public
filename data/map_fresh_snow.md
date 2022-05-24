# Fresh Snow Map (hr_sn)

This map shows the forecast amount of fresh snow (cm), accumulated in 3-hour intervals.

Multiple forecast time steps are available (e.g. forecast for 3 hours, 6 hours, 9 hours, ..) and there is one independent map per time step.

The data is provided as raster tiles.

Two maps are available. One covers the entire world and has a spatial resolution of ~1.5km. The other covers the Alps area and has a spatial resolution of ~100m.

## Time Steps

### Time Steps World

The available time steps can be found using the [meta.json](../metgis_maps_API_reference.md#metajson) document: 
https://tiles.metgis.com/meta-world/0.8/meta.json

### Time Steps Alps

The available time steps can be found using the [meta.json](../metgis_maps_API_reference.md#metajson) document: 
https://tiles.metgis.com/meta-world/0.8/meta.json

<details>
  <summary>Get Array of Available Time Steps</summary>

  ```js
  fetch('https://tiles.metgis.com/meta/0.8/meta.json')
    .then(res => res.json())
    .then(data => {
      const startDate = new Date(data.forecastIssued)
      const step = data.timeStep
      const timeStepCount = data.timeStepNumber
      const arr = []

      for (let i = 0; i < timeStepCount; i++) {
        const hours = i * step
        const date = new Date(startDate.getTime())
        date.setHours(date.getHours() + hours)

        arr.push({ timestep: i + 1, date: date.toISOString() })
      }

      return Promise.resolve(arr)
    })
    .then(arr => { console.log(arr) })
  ```

  outputs for example:

  ```js
  [
    { timestep: 1, date: "2021-05-31T18:00:00.000Z" },
    { timestep: 2, date: "2021-05-31T21:00:00.000Z" },
    { timestep: 3, date: "2021-06-01T00:00:00.000Z" },
    { timestep: 4, date: "2021-06-01T03:00:00.000Z" },
    { timestep: 5, date: "2021-06-01T06:00:00.000Z" },
    { timestep: 6, date: "2021-06-01T09:00:00.000Z" },
    { timestep: 7, date: "2021-06-01T12:00:00.000Z" },
    { timestep: 8, date: "2021-06-01T15:00:00.000Z" },
    { timestep: 9, date: "2021-06-01T18:00:00.000Z" },
    { timestep: 10, date: "2021-06-01T21:00:00.000Z" },
    { timestep: 11, date: "2021-06-02T00:00:00.000Z" },
    { timestep: 12, date: "2021-06-02T03:00:00.000Z" },
    { timestep: 13, date: "2021-06-02T06:00:00.000Z" },
    { timestep: 14, date: "2021-06-02T09:00:00.000Z" },
    { timestep: 15, date: "2021-06-02T12:00:00.000Z" },
    { timestep: 16, date: "2021-06-02T15:00:00.000Z" },
    { timestep: 17, date: "2021-06-02T18:00:00.000Z" },
    { timestep: 18, date: "2021-06-02T21:00:00.000Z" },
    { timestep: 19, date: "2021-06-03T00:00:00.000Z" },
    { timestep: 20, date: "2021-06-03T03:00:00.000Z" },
    { timestep: 21, date: "2021-06-03T06:00:00.000Z" },
    { timestep: 22, date: "2021-06-03T09:00:00.000Z" },
    { timestep: 23, date: "2021-06-03T12:00:00.000Z" },
    { timestep: 24, date: "2021-06-03T15:00:00.000Z" },
    { timestep: 25, date: "2021-06-03T18:00:00.000Z" }
  ]
  ```

</details>

## Map Data (Tiles)

### Fresh Snow Map World

Tiles can be fetched with following urls: 

```
https://t1.metgis.com/hr_sn-world_{t}/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_{t}/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_{t}/{z}/{x}/{y}.png?key=<my-key>
```

(change `{t}` to a number of an available time step)

### Fresh Snow Map Alps

Tiles can be fetched with following urls: 

```
https://t1.metgis.com/hr_sn_{t}/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_{t}/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_{t}/{z}/{x}/{y}.png?key=<my-key>
```

(change `{t}` to a number of an available time step)

### Embed In Website

This map is served as png tiles. The easiest way to embed this map into a website, is to use [maplibre-gl-js](https://maplibre.org/maplibre-gl-js-docs/api/).

<details>
  <summary><b>Basic Code Example</b> - Visualizing a MetGIS weather map on an OpenStreetMap background map</summary>

  ```html
  <!DOCTYPE html>
  <html>

  <head>
    <link rel="stylesheet" href="https://cdn.skypack.dev/maplibre-gl@^1.14.0/dist/maplibre-gl.css" />
    <style>
      * { margin: 0; padding: 0; }
      #map { position: absolute; top: 0; bottom: 0; width: 100%; } 
    </style>
  </head>

  <body>
    <div id="map"></div>

    <script type="module">
      import { Map } from 'https://cdn.skypack.dev/maplibre-gl@^1.14.0'

      const map = new Map({
        // See the explanation of the fields at https://maplibre.org/maplibre-gl-js-docs/api/map/
        container: 'map',
        style: {
          // See https://maplibre.org/maplibre-gl-js-docs/style-spec/root
          version: 8,
          sources: {
            // See https://maplibre.org/maplibre-gl-js-docs/style-spec/sources/
            openstreetmap: {
              type: 'raster',
              tiles: [
                'https://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
                'https://b.tile.openstreetmap.org/{z}/{x}/{y}.png',
                'https://c.tile.openstreetmap.org/{z}/{x}/{y}.png'
              ]
            },
            freshSnow: {
              type: 'raster',
              // Using the 7th time step (the numbering starts from 1)
              tiles: [
                'https://t1.metgis.com/hr_sn_7/{z}/{x}/{y}.png?key=<my-key>',
                'https://t2.metgis.com/hr_sn_7/{z}/{x}/{y}.png?key=<my-key>',
                'https://t3.metgis.com/hr_sn_7/{z}/{x}/{y}.png?key=<my-key>'
              ],
              tileSize: 256
            }
          },
          layers: [
            // See https://maplibre.org/maplibre-gl-js-docs/style-spec/layers/
            {
              id: 'basemap',
              type: 'raster',
              source: 'openstreetmap',
              minzoom: 0,
              maxzoom: 22
            },
            {
              id: 'freshSnow',
              type: 'raster',
              source: 'freshSnow',
              paint: {
                'raster-opacity': 0.9
              }
            }
          ]
        },
        center: [13.320730, 47.018263],
        zoom: 6
      })
    </script>
  </body>

  </html>
  ```

</details>
