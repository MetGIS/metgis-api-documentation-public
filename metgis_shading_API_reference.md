
# MetGIS Shading API

> **Availability:** This API is available on request. Please contact MetGIS for access.

The MetGIS Shading API delivers raster map tiles showing shading (shadows) cast by terrain. The data is available worldwide, calculated from the sun position, and provides a resolution of one minute.


## Endpoint

```
GET https://shadow.metgis.com/shadow-tiles/{z}/{x}/{y}.png?y={year}&mo={month}&d={day}&h={hour}&mi={minute}&key={api_key}
```

## Authentication

Requests are authenticated with an API key, passed as the `key` query parameter. To get a key, see [Contact](#contact).

> **Note:** Keep your API key private. Don't commit it to public repositories or expose it in client-side code you don't control.

## Parameters

### Path parameters

| Parameter | Description                        |
|-----------|------------------------------------|
| `z`       | Zoom level (maximum: `12`)         |
| `x`       | Tile column (XYZ scheme)           |
| `y`       | Tile row (XYZ scheme)              |

### Query parameters

All times are in **UTC**.

| Parameter | Type    | Required | Description         | Example   |
|-----------|---------|----------|---------------------|-----------|
| `y`       | integer | yes      | Year                | `2026`    |
| `mo`      | integer | yes      | Month (1-12)        | `6`       |
| `d`       | integer | yes      | Day of month (1-31) | `21`      |
| `h`       | integer | yes      | Hour (0-23)         | `14`      |
| `mi`      | integer | yes      | Minute (0-59)       | `30`      |
| `key`     | string  | yes      | Your API key        | `abc123…` |

## Example request

```
https://shadow.metgis.com/shadow-tiles/10/545/355.png?y=2026&mo=6&d=21&h=14&mi=30&key=YOUR_API_KEY
```

## Response

- **Format:** PNG raster tile
- **Tile size:** 256 × 256 pixels
- **Coverage:** Worldwide
- **Zoom levels:** up to 12
- **Temporal resolution:** 1 minute
- **Time zone:** UTC

### Tile legend

| Color     | Meaning                              |
|-----------|--------------------------------------|
| Dark gray | Area in shadow (no direct sunlight)  |
| White     | Sunlit area (direct sunlight)        |

## Contact

To request access, contact MetGIS at **office@metgis.com**.
