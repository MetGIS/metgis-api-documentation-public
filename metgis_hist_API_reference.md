# MetGIS HIST API

The MetGIS HIST API is an application programming interface that can be used to access historical weather data in JSON format. It follows REST API constraints. This document provides a detailed description of it's usage. Information about obtaining access rights to it can be found [here](https://weatherapi.metgis.com/histapi), or [contact us](https://contact.metgis.com/de/).

The historical data is reconstructed on the basis of global model analyzes (includes data from weather stations, ground radar, satellites, weather balloons, weather buoys, measured values from aircraft, etc.), regional weather simulation models and the MetGIS downscaling algorithm, applied on a 1 km grid. This data is enriched with a network of additional, certified stations for even more reliable results.

## Quick Start

The API can be accessed via http using an URL of the following form:

```
https://api.hist.metgis.com/histapiserverRest/histdata?lon={longitude}&lat={latitude}&time={timestamp}&v={package-version}&key={your-key}
```

The parameters that have to be set are in curly brackets and listed in the following table:

| Parameter |                             Description                             | Comments                                                                                                                                                                                                                                                                                                   |
| --------- | :-----------------------------------------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key       |                Key needed to access MetGIS HIST API                 | Paying customers have received their API Key after ordering. Sometimes keys for testing may be available. Mandadory parameter.                                                                                                                                                                             |
| lat       | Latitude of point the weather data is requested for in degrees [°]  | Latitude of points south of the equator is negative, use point (.) as decimal separator, ranges can be given with an underscore (e. g. `47.16_48.25` for all values between 47.15° and 48.25° north). Mandatory parameter.                                                                                 |
| lon       | Longitude of point the weather data is requested for in degrees [°] | Longitude west of 0° meridian can be given as negative values or in the range from 180° to 360°, use point (.) as decimal separator, ranges can be given with an underscore (e. g. `12.14_13.45` for all values between 12.14° and 13.45° east). Mandatory parameter.                                      |
| v         |               Name of requested weather data package                | Key must have access rights to requested package. For available package versions check the table in section [package versions](#package-versions). Mandatory parameter.                                                                                                                                    |
| time      |    The timestamp for which the meteorological data is requested     | The timestamp is given in the format `yyyymmddHHMM`, e. g. `201603021100` for data for the 2nd of March 2016 at 11 o'clock (UTC). Time ranges can be given with underscores (`starttimestamp_endtimestamp`), to retrieve all data between two points in time. All times refer to UTC. Mandatory parameter. |

A valid request will be responded with a file in JSON format that contains the specified historical weather data. The files are mostly self explaining, but a detailed description of the available packages is given in the section ["Package versions"](#package-versions).

Data access limits: There are limits to how much data can be retrieved in one request. For hourly data packages the limit is 40.000 individual data points, which means either an hourly time series containing 40.000 values, or a spatial area containing 40.000 points for one point in time. If you specify a spatial and temporal range, the numbers will be multiplied. For daily data packages the limit is 100.000 points. If your request exceeds the limit, you will be notified, and you have to divide your request in smaller chunks to retrieve the data.

## Weather Parameters

The MetGIS Hist API provides access to the following weather parameters:

| Weather Parameter | Unit            | Details                                                                                                                                                                                                        |
| ----------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Temperature       | °C              | Air temperature two meters above the ground                                                                                                                                                                    |
| Precipitation     | mm              | Amount of accumulated rainfall and/or snow. In the case of snow, the liquid water equivalent is used (resulting water if fallen snow would have been melted).                                                  |
| Fresh Snow        | cm              | Amount of accumulated fresh snow.                                                                                                                                                                              |
| Wind Speed        | m/s             | Ten-minute average of wind speed 10 meters above the ground.                                                                                                                                                   |
| Wind Direction    | deg             | Ten-minute average of wind direction 10 meters above the ground (in degrees clockwise from north, -9999 means rotating).                                                                                       |
| Relative Humidity | %               | Relative humidity of the air two meters above the ground                                                                                                                                                       |
| Sunshine Duration | h               | Accumulated duration of sunshine                                                                                                                                                                               |
| Cloudiness        | %               | Degree of cloudiness, meaning what percentage of the sky is covered by clouds at a given time                                                                                                                  |
| Global Radiation  | Wm<sup>-2</sup> | Total short-wave radiation from the sky falling onto a horizontal surface on the ground. It includes both the direct solar radiation and the diffuse radiation resulting from reflected or scattered sunlight. |

## Package Versions

| Package Version |                                                                                                                                           Description                                                                                                                                            |
| --------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| hitemp          |                                                                                                                   Historical temperature data available in hourly resolution.                                                                                                                    |
| hirh            |                                                                                                                Historical relative humidity data available in hourly resolution.                                                                                                                 |
| hihrp           |                                                                                                                  Historical precipitation data available in hourly resolution.                                                                                                                   |
| hihrsn          |                                                                                                                    Historical fresh snow data available in hourly resolution                                                                                                                     |
| hiwind          |                                                                                                                       Historical wind data available in hourly resolution.                                                                                                                       |
| hicld           |                                                                                                                   Historical cloud cover data available in hourly resolution.                                                                                                                    |
| hidswr          |                                                                                                                 Historical global radiation data available in hourly resolution.                                                                                                                 |
| hidsum          | Summary of the meteorological conditions for the day of the given timestamp. This package includes daily minimum, maximum and mean values of the parameters temperature, cloud cover, relative humidity and wind as well as the daily sum of the parameters precipitation and sunshine duration. |
| hidsmall        |                                            Summary of the meteorological conditions for the day of the given timestamp. This package includes daily minimum, maximum and mean values of the parameter temperature and the daily sum of precipitation.                                            |

A correct API request to retrieve the data package `hidsum` for the first to the third of April 2017 for specific coordinates would look like this:

```
https://api.hist.metgis.com/histapiserverRest/histdata?lon=14.207701&lat=47.989155&time=201704010000_201704030000&v=hidsum&key={key}
```

And it would yield a JSON file like this:

```

{

    "Info": "Historical Weather Data Daily Summary",
    "data": [
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170401",
            "tmp_mean": 14.9,
            "tmp_max": 21.8,
            "tmp_min": 7.9,
            "prec_sum": 0.0,
            "wind_dir_weighted": 99.0,
            "wind_dir_max": 191.0,
            "wind_speed_mean": 1.6,
            "wind_speed_max": 5.1,
            "wind_speed_min": 0.0,
            "cloud_cover_mean": 5.0,
            "cloud_cover_max": 28.0,
            "cloud_cover_min": 0.0,
            "sun_dur": 11.89,
            "rel_hum_mean": 53.0,
            "rel_hum_max": 64.0,
            "rel_hum_min": 39.0
        },
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170402",
            "tmp_mean": 13.9,
            "tmp_max": 20.6,
            "tmp_min": 7.6,
            "prec_sum": 0.1,
            "wind_dir_weighted": 268.0,
            "wind_dir_max": 259.0,
            "wind_speed_mean": 2.5,
            "wind_speed_max": 5.1,
            "wind_speed_min": 1.0,
            "cloud_cover_mean": 10.0,
            "cloud_cover_max": 30.0,
            "cloud_cover_min": 0.0,
            "sun_dur": 12.16,
            "rel_hum_mean": 64.0,
            "rel_hum_max": 86.0,
            "rel_hum_min": 42.0
        },
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170403",
            "tmp_mean": 11.9,
            "tmp_max": 16.8,
            "tmp_min": 7.2,
            "prec_sum": 13.6,
            "wind_dir_weighted": 319.0,
            "wind_dir_max": 284.0,
            "wind_speed_mean": 2.1,
            "wind_speed_max": 4.1,
            "wind_speed_min": 1.0,
            "cloud_cover_mean": 44.0,
            "cloud_cover_max": 100.0,
            "cloud_cover_min": 0.0,
            "sun_dur": 7.8,
            "rel_hum_mean": 81.0,
            "rel_hum_max": 98.0,
            "rel_hum_min": 67.0
        }
    ],
    "Info_tmp_mean": "mean temperature of the day (in °C)",
    "Info_tmp_min": "minimum temperature of the day (in °C)",
    "Info_tmp_max": "maximum temperature of the day (in °C)",
    "Info_prec_sum": "total precipitation accumulated during the day (in mm)",
    "Info_wind_dir_max": "wind direction of maximum wind (in degrees clockwise from north)",
    "Info_wind_dir_weighted": "prevailing wind direction during day (in degrees clockwise from north, -9999 means rotating)",
    "Info_wind_speed_mean": "mean wind speed (in m/s)",
    "Info_wind_speed_max": "maximum wind speed (in m/s)",
    "Info_wind_speed_min": "minimum wind speed (in m/s)",
    "Info_cloud_cover_mean": "mean cloud cover (in %)",
    "Info_cloud_cover_max": "maximum cloud cover (in %)",
    "Info_sun_dur": "accumulated sunshine duration (in h)",
    "Info_rel_hum_mean": "mean relative humidity (in %)",
    "Info_rel_hum_max": "maximum relative humidity (in %)",
    "Info_rel_hum_min": "minimum relative humidity (in %)",
    "Info_lat": "latitude of the data point (in degrees)",
    "Info_lon": "longitude of the data point (in degrees)",
    "Info_alt": "altitude of the data point (in m above mean sea level)",
    "Info_cloud_cover_min": "minimum cloud cover (in %)"

}
```

To retrieve hourly temperature data for the range from 9 to 12 o'clock on the first of April 2017, the request would look like this:

```
https://api.hist.metgis.com/histapiserverRest/histdata?lon=14.207701&lat=47.989155&time=201704010900_201704011200&v=hitemp&key={key}
```

This request would yield the following JSON file:

```
{

    "Info": "Historical Temperature Data",
    "data": [
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170401 09:00",
            "tmp": 14.9
        },
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170401 10:00",
            "tmp": 16.9
        },
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170401 11:00",
            "tmp": 18.7
        },
        {
            "lon": 14.2,
            "lat": 47.992,
            "alt": 427,
            "date": "20170401 12:00",
            "tmp": 20.2
        }
    ],
    "Info_lat": "latitude of the data point (in degrees)",
    "Info_lon": "longitude of the data point (in degrees)",
    "Info_alt": "altitude of the data point (in m above mean sea level)",
    "Info_tmp": "Temperature (in °C)"

}
```

Please note that in the hourly-resolution data packages hihrp and hihrsn, the numbers given for precipitation and fresh snow refer to one-hour time intervals ending at the given timestamp (reference time).

<!--- TODO: add package sunshine duration if operational -->

## Common Errors

The API responds with specific messages for certain errors. They are presented here:

- `Please check request parameters`: One of the query parameters could not be parsed. Check the format of `lat`, `lon`, `package-version` and `timestamp`.
- `Please check key or allowed service version`: There is either a typo in the key, or the key does not have permission to retrieve the requested package.
- `Too many results! Please limit search radius or time parameters`: Your query is trying to retrieve too much data at once. Please divide the request in smaller temporal or spatial chunks.
