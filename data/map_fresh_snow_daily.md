# Fresh Snow Daily Map

This maps show the forecasted amount of fresh snow (cm), accumulated in a specific timerange of 1-3 days.

The data is provided as raster tiles.

Two types of maps are available. One type covers the entire world and has a spatial resolution of ~1.5km. The other type covers the Alps area and has a spatial resolution of ~100m.

For each type, 6 maps are available:
* 00-24h (accumulated fresh snow of today)
* 00-48h (accumulated fresh snow of today + tomorrow)
* 00-72h (accumulated fresh snow of today + tomorrow + the day after tomorrow)
* 24-48h (accumulated fresh snow of tomorrow)
* 24-72h (accumulated fresh snow of tomorrow + the day after tomorrow)
* 48-72h (accumulated fresh snow for the day after tomorrow)

## Time Ranges

### Time Ranges World

The available time ranges can be found using the [meta.json](../metgis_maps_API_reference.md#metajson) document: 
https://tiles.metgis.com/meta-world/0.8/meta.json.
The time offset is relative to the property: `forecastIssued`.

### Time Ranges Alps

The available time ranges can be found using the [meta.json](../metgis_maps_API_reference.md#metajson) document: 
https://tiles.metgis.com/meta/0.8/meta.json.
The time offset is relative to the property: `forecastIssued`.

<details>
  <summary>Get Time Ranges</summary>

  ```js
  async function getTimeRange(start, end) {
    const res = await fetch('https://tiles.metgis.com/meta/0.8/meta.json')
    const data = await res.json()
    const startDate = new Date(data.forecastIssued)
    const endDate = new Date(data.forecastIssued)

    startDate.setHours(startDate.getHours() + start)
    endDate.setHours(endDate.getHours() + end)

    return Promise.resolve({ startDate, endDate })
  }

  const RANGE_00_24 = await getTimeRange(0, 24)
  const RANGE_00_48 = await getTimeRange(0, 48)
  const RANGE_00_72 = await getTimeRange(0, 72)
  const RANGE_24_48 = await getTimeRange(24, 48)
  const RANGE_24_72 = await getTimeRange(24, 72)
  const RANGE_48_72 = await getTimeRange(48, 72)

  console.log(RANGE_00_24)
  console.log(RANGE_00_48)
  console.log(RANGE_00_72)
  console.log(RANGE_24_48)
  console.log(RANGE_24_72)
  console.log(RANGE_48_72)
  ```

  outputs for example:

  ```js
  { startDate: 2021-06-02T03:00:00.000Z, endDate: 2021-06-03T03:00:00.000Z }
  { startDate: 2021-06-02T03:00:00.000Z, endDate: 2021-06-04T03:00:00.000Z }
  { startDate: 2021-06-02T03:00:00.000Z, endDate: 2021-06-05T03:00:00.000Z }
  { startDate: 2021-06-03T03:00:00.000Z, endDate: 2021-06-04T03:00:00.000Z }
  { startDate: 2021-06-03T03:00:00.000Z, endDate: 2021-06-05T03:00:00.000Z }
  { startDate: 2021-06-04T03:00:00.000Z, endDate: 2021-06-05T03:00:00.000Z }
  ```

</details>

## Map Data (Tiles)

(change `{t}` to a number of an available time step)

### Fresh Snow Daily Map World

Tiles can be fetchted with following urls: 

#### 00-24h

```
https://t1.metgis.com/hr_sn-world_0-24/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_0-24/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_0-24/{z}/{x}/{y}.png?key=<my-key>
```

#### 00-48h

```
https://t1.metgis.com/hr_sn-world_0-48/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_0-48/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_0-48/{z}/{x}/{y}.png?key=<my-key>
```

#### 00-72h

```
https://t1.metgis.com/hr_sn-world_0-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_0-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_0-72/{z}/{x}/{y}.png?key=<my-key>
```

#### 24-48h

```
https://t1.metgis.com/hr_sn-world_24-48/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_24-48/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_24-48/{z}/{x}/{y}.png?key=<my-key>
```

#### 24-72h

```
https://t1.metgis.com/hr_sn-world_24-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_24-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_24-72/{z}/{x}/{y}.png?key=<my-key>
```

#### 48-72h

```
https://t1.metgis.com/hr_sn-world_48-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn-world_48-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn-world_48-72/{z}/{x}/{y}.png?key=<my-key>
```

### Fresh Snow Daily Map Alps

Tiles can be fetchted with following urls: 

#### 00-24h

```
https://t1.metgis.com/hr_sn_0-24/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_0-24/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_0-24/{z}/{x}/{y}.png?key=<my-key>
```

#### 00-48h

```
https://t1.metgis.com/hr_sn_0-48/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_0-48/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_0-48/{z}/{x}/{y}.png?key=<my-key>
```

#### 00-72h

```
https://t1.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>
```

#### 24-48h

```
https://t1.metgis.com/hr_sn_24-48/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_24-48/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_24-48/{z}/{x}/{y}.png?key=<my-key>
```

#### 24-72h

```
https://t1.metgis.com/hr_sn_24-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_24-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_24-72/{z}/{x}/{y}.png?key=<my-key>
```

#### 48-72h

```
https://t1.metgis.com/hr_sn_48-72/{z}/{x}/{y}.png?key=<my-key>
https://t2.metgis.com/hr_sn_48-72/{z}/{x}/{y}.png?key=<my-key>
https://t3.metgis.com/hr_sn_48-72/{z}/{x}/{y}.png?key=<my-key>
```

### Embed In Website

These maps are served as png tiles. The easiest way to embed a map into a website, is to use [maplibre-gl-js](https://maplibre.org/maplibre-gl-js-docs/api/).

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
            freshSnowDaily: {
              type: 'raster',
              // forecast fresh snow for next 3 days accumulated
              tiles: [
                'https://t1.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>',
                'https://t2.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>',
                'https://t3.metgis.com/hr_sn_0-72/{z}/{x}/{y}.png?key=<my-key>'
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
              id: 'freshSnowDaily',
              type: 'raster',
              source: 'freshSnowDaily',
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
