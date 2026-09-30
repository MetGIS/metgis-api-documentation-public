# MetGIS Precipitation Radar API

> **Availability:** This API is available on request. Please contact MetGIS for access.

The MetGIS Precipitation Radar API delivers raster map tiles showing precipitation measured by radar, updated every 5 minutes.

## Endpoint

```
GET https://tiles-radar.metgis.com/data/metgis-radar-map-{timestep}/{z}/{x}/{y}.png
```

### Path parameters

| Parameter  | Description                                                              | Example               |
|------------|--------------------------------------------------------------------------|-----------------------|
| `timestep` | Timestamp of the radar image in UTC, format `YYYY-MM-DDTHHMMSS`          | `2026-09-30T042000`   |
| `z`        | Zoom level                                                               | `6`                   |
| `x`        | Tile column (XYZ scheme)                                                 | `34`                  |
| `y`        | Tile row (XYZ scheme)                                                    | `22`                  |

Available timesteps are listed in the metadata JSON (see below).

## Available timesteps

The metadata JSON lists all currently available radar images, newest first, in 5-minute steps:

```
GET https://radar-tiles.metgis.com/meta-radar/radar-meta.json
```

Example response (shortened):

```json
{
  "description": "MetGIS Tile Server",
  "layers": [
    {
      "raster": "https://tiles-radar.metgis.com/data/metgis-radar-map-2026-09-30T042000/{z}/{x}/{y}.png",
      "timestamp": "2026-09-30T04:20:00Z"
    },
    {
      "raster": "https://tiles-radar.metgis.com/data/metgis-radar-map-2026-09-30T041500/{z}/{x}/{y}.png",
      "timestamp": "2026-09-30T04:15:00Z"
    },
    ...
  ],
  "parameters": {
    "radarmap": {
      "parameterName": "5 min rain sum measured by radar in mm"
    }
  }
}
```

| Field                | Description                                                       |
|----------------------|-------------------------------------------------------------------|
| `layers[].raster`    | Tile URL template for this timestep (use it directly as a source) |
| `layers[].timestamp` | Time of the radar image (ISO 8601, UTC)                           |
| `parameters`         | Description of the data parameter                                 |

> **Tip:** Don't hard-code timesteps. Always read the metadata JSON to get the latest available images.

## Response

- **Format:** PNG raster tile
- **Tile size:** 256 × 256 pixels
- **Temporal resolution:** 5 minutes
- **Time zone:** UTC
- **Unit:** `mm/5min` (rain sum over 5 minutes, measured by radar)

### Legend

| From (mm/5min) | Color     | Hex       |
|----------------|-----------|-----------|
| 0.03           | Light cyan| `#abfeff` |
| 0.1            | Cyan      | `#53d2ff` |
| 0.3            | Light blue| `#2babff` |
| 1              | Blue      | `#1b7eda` |
| 3              | Purple    | `#9a329a` |
| 10             | Magenta   | `#e619e5` |

## Contact

To request access, contact MetGIS at **TODO: email/URL**.# MetGIS Precipitation Radar API

> **Availability:** This API is available on request. Please contact MetGIS for access.

The MetGIS Precipitation Radar API delivers raster map tiles showing precipitation measured by radar, updated every 5 minutes.

## Endpoint

```
GET https://tiles-radar.metgis.com/data/metgis-radar-map-{timestep}/{z}/{x}/{y}.png
```

### Path parameters

| Parameter  | Description                                                              | Example               |
|------------|--------------------------------------------------------------------------|-----------------------|
| `timestep` | Timestamp of the radar image in UTC, format `YYYY-MM-DDTHHMMSS`          | `2026-09-30T042000`   |
| `z`        | Zoom level                                                               | `6`                   |
| `x`        | Tile column (XYZ scheme)                                                 | `34`                  |
| `y`        | Tile row (XYZ scheme)                                                    | `22`                  |

Available timesteps are listed in the metadata JSON (see below).

## Available timesteps

The metadata JSON lists all currently available radar images, newest first, in 5-minute steps:

```
GET https://radar-tiles.metgis.com/meta-radar/radar-meta.json
```

Example response (shortened):

```json
{
  "description": "MetGIS Tile Server",
  "layers": [
    {
      "raster": "https://tiles-radar.metgis.com/data/metgis-radar-map-2026-09-30T042000/{z}/{x}/{y}.png",
      "timestamp": "2026-09-30T04:20:00Z"
    },
    {
      "raster": "https://tiles-radar.metgis.com/data/metgis-radar-map-2026-09-30T041500/{z}/{x}/{y}.png",
      "timestamp": "2026-09-30T04:15:00Z"
    },
    ...
  ],
  "parameters": {
    "radarmap": {
      "parameterName": "5 min rain sum measured by radar in mm"
    }
  }
}
```

| Field                | Description                                                       |
|----------------------|-------------------------------------------------------------------|
| `layers[].raster`    | Tile URL template for this timestep (use it directly as a source) |
| `layers[].timestamp` | Time of the radar image (ISO 8601, UTC)                           |
| `parameters`         | Description of the data parameter                                 |

> **Tip:** Don't hard-code timesteps. Always read the metadata JSON to get the latest available images.

## Response

- **Format:** PNG raster tile
- **Tile size:** 256 × 256 pixels
- **Temporal resolution:** 5 minutes
- **Time zone:** UTC
- **Unit:** `mm/5min` (rain sum over 5 minutes, measured by radar)

### Legend

| From (mm/5min) | Color     | Hex       |
|----------------|-----------|-----------|
| 0.03           | Light cyan| `#abfeff` |
| 0.1            | Cyan      | `#53d2ff` |
| 0.3            | Light blue| `#2babff` |
| 1              | Blue      | `#1b7eda` |
| 3              | Purple    | `#9a329a` |
| 10             | Magenta   | `#e619e5` |

## Contact

To request access, contact MetGIS at **office@metgis.com**.
