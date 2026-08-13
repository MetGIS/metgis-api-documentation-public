# MetGIS Global HIST API

The MetGIS Global HIST API is an application programming interface that can be used to access historical weather data in JSON format. It follows REST API constraints. This document provides a detailed description of its usage. Information about obtaining access rights can be found [here](https://weatherapi.metgis.com/histapi), or [contact us](https://metgis.com/en/contact-us/).

The historical data is reconstructed on the basis of global model analyses (including data from weather stations, ground radar, satellites, weather balloons, weather buoys, and measured values from aircraft, etc.), global weather simulation models, and the MetGIS downscaling algorithm, applied on a 0.1 degree grid over land and a 0.25 degree grid over the sea. This data is enriched with a network of additional, certified stations for even more reliable results.

Data is available from 2005 through one week prior to the current date. It is updated daily and undergoes rigorous quality testing to ensure a consistently high-quality product. If you need data from before 2005 please [contact us](https://metgis.com/en/contact-us/).

## Quick Start

The API can be accessed via HTTP using a URL of the following form:

```
https://api.hist-global.metgis.com/forecast?lon={longitude}&lat={latitude}&start_date={timestamp_startdate}&end_date={timestamp_enddate}&v={package-version}&key={your-key}
```

The parameters that have to be set are in curly brackets and listed in the following table:

| Parameter |                             Description                             | Comments                                                                                                                                                                                                                                                                                                   |
| --------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key       |                Key needed to access MetGIS Global HIST API                 | Paying customers have received their API Key after ordering. Sometimes keys for testing may be available. Mandatory parameter.                                                                                                                                                                             |
| lat       | Latitude of point the weather data is requested for in degrees ° | Latitude of points south of the equator is negative, use point (.) as decimal separator. Mandatory parameter.                                                                                 |
| lon       | Longitude of point the weather data is requested for in degrees ° | Longitude west of 0° meridian can be given as negative values or in the range from 180° to 360°, use point (.) as decimal separator. Mandatory parameter.                                      |
| v         |               Name of requested weather data package                | Key must have access rights to requested package. For available package versions check the table in section [package versions](#package-versions). Mandatory parameter.                                                                                                                                    |
| start_date      |    The start date for which the meteorological data is requested     | The timestamp is given in the format `YYYYMMDD`, e. g. `20160302` for data for the 2nd of March 2016. Mandatory parameter. |
| end_date      |    The end date for which the meteorological data is requested     | The timestamp is given in the format `YYYYMMDD`, e. g. `20160302` for data for the 2nd of March 2016. Mandatory parameter. |

A valid request will be answered with a file in JSON format that contains the specified historical weather data. The files are mostly self-explanatory, but a detailed description of the available packages is given in the section ["Package versions"](#package-versions).

Data access limits: There are limits to how much data can be retrieved in one request. For hourly data packages the limit is 40,000 individual data points, meaning either an hourly time series containing 40,000 values, or a spatial area containing 40,000 points for one point in time. If you specify a spatial and temporal range, the numbers will be multiplied. For daily data packages the limit is 100,000 points. If your request exceeds the limit, you will be notified and will need to divide your request into smaller chunks to retrieve the data.

## Weather Parameters

The MetGIS Global HIST API provides access to the following weather parameters:

| Weather Parameter | Unit            | Details                                                                                                                                                                                                        |
| ----------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Temperature       | °C              | Air temperature two meters above the ground                                                                                                                                                                    |
| Total Precipitation     | mm              | Amount of accumulated rainfall and/or snow. In the case of snow, the liquid water equivalent is used (resulting water if fallen snow would have been melted).                                                  |
| Liquid Precipitation    | mm              | Amount of accumulated rainfall                        |
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
| hisumsn        |  Sum of new snow during the specified period.  |
| hidegreeday        |  Sum of heating degree days during the specified period.  |
| hiagrismall        |  Summary of the meteorological conditions during the given period. Useful for agricultural purposes. This package includes sum of the parameters growing degree days, heavy, liquid (rain) and total precipitation, as well as the mean wind speed during the requested period. |
| hiagrilarge        |  Summary of the meteorological conditions during the given period. Useful for agricultural purposes. This package includes sum of the parameters growing degree days, global radiation, evapotranspiration, heavy, liquid (rain) and total precipitation, as well as the mean wind speed and the climatic water balance and deficit during the requested period. |

A correct API request to retrieve the data package `hidsum` from the first to the third of April 2017 for specific coordinates would look like this:

```
https://api.hist-global.metgis.com/forecast?lon=16.35639&lat=48.24861&start_date=20170401&end_date=20170403&v=hidsum&lang=en
&key={key}
```

And it would yield a JSON file like this:

```

{
    "data": [
        {
            "Data_daily": {
                "Dates_UTC": [
                    "2017-04-01T00:00+00:00",
                    "2017-04-02T00:00+00:00",
                    "2017-04-03T00:00+00:00"
                ],
                "DownwardShortWaveRadiation_dailySum": [
                    5454,
                    5537,
                    5105
                ],
                "DownwardShortWaveRadiation_dailySum_unit": "Wh/m²",
                "MaximumRelativeHumidity": [
                    74,
                    85,
                    95
                ],
                "MaximumRelativeHumidity_unit": "%",
                "MaximumTemperature": [
                    21.4,
                    22.6,
                    19.6
                ],
                "MaximumTemperature_unit": "°C",
                "MaximumTotalCloudCover": [
                    0,
                    0,
                    0
                ],
                "MaximumTotalCloudCover_unit": "%",
                "MaximumWindSpeed": [
                    32.5,
                    19.9,
                    16.7
                ],
                "MaximumWindSpeed_unit": "km/h",
                "MeanRelativeHumidity": [
                    57,
                    58,
                    70
                ],
                "MeanRelativeHumidity_unit": "%",
                "MeanTemperature": [
                    14.9,
                    16.1,
                    13.8
                ],
                "MeanTemperature_unit": "°C",
                "MeanTotalCloudCover": [
                    0,
                    0,
                    1
                ],
                "MeanTotalCloudCover_unit": "%",
                "MeanWindSpeed": [
                    26.4,
                    12.4,
                    11.4
                ],
                "MeanWindSpeed_unit": "km/h",
                "MinimumRelativeHumidity": [
                    43,
                    37,
                    52
                ],
                "MinimumRelativeHumidity_unit": "%",
                "MinimumTemperature": [
                    9.2,
                    10.2,
                    7.5
                ],
                "MinimumTemperature_unit": "°C",
                "MinimumTotalCloudCover": [
                    0,
                    1,
                    4
                ],
                "MinimumTotalCloudCover_unit": "%",
                "MinimumWindSpeed": [
                    21.8,
                    4.4,
                    2.1
                ],
                "MinimumWindSpeed_unit": "km/h",
                "PrecipitationRain_dailySum": [
                    0.0,
                    0.0,
                    0.0
                ],
                "PrecipitationRain_dailySum_unit": "mm",
                "PrecipitationSnow_dailySum": [
                    0.0,
                    0.0,
                    0.0
                ],
                "PrecipitationSnow_dailySum_unit": "cm",
                "PrecipitationTotal_dailySum": [
                    0.0,
                    0.0,
                    0.0
                ],
                "PrecipitationTotal_dailySum_unit": "mm"
            },
            "Info": {
                "Altitude_[m]": 201.0,
                "Description": "Summary of the meteorological conditions for the day of the given timestamp. This package includes daily minimum, maximum and mean values of the parameters temperature, cloud cover, relative humidity and wind as well as the daily sum of the parameters precipitation and sunshine duration.",
                "Latitude": 48.24861,
                "Longitude": 16.35639,
                "Start_date": "2017-04-01",
                "End_date": "2017-04-03"
            }
        }
    ],
    "count": 1
}
```

To retrieve hourly temperature data for the first of April 2017, the request would look like this:

```
https://api.hist-global.metgis.com/forecast?lon=16.35639&lat=48.24861&start_date=20170401&end_date=20170401&v=hitemp&lang=en
&key={key}
```

This request would yield the following JSON file:

```
{
    "data": [
        {
            "Data_hourly": {
                "Temperature": [
                    11.1,
                    10.7,
                    10.3,
                    9.8,
                    9.5,
                    9.2,
                    9.8,
                    11.5,
                    14.2,
                    16.1,
                    17.9,
                    19.1,
                    20.1,
                    20.9,
                    21.4,
                    21.1,
                    19.9,
                    18.1,
                    16.4,
                    15.2,
                    14.4,
                    13.7,
                    13.7,
                    13.2
                ],
                "Temperature_unit": "°C",
                "Times_UTC": [
                    "2017-04-01T00:00+00:00",
                    "2017-04-01T01:00+00:00",
                    "2017-04-01T02:00+00:00",
                    "2017-04-01T03:00+00:00",
                    "2017-04-01T04:00+00:00",
                    "2017-04-01T05:00+00:00",
                    "2017-04-01T06:00+00:00",
                    "2017-04-01T07:00+00:00",
                    "2017-04-01T08:00+00:00",
                    "2017-04-01T09:00+00:00",
                    "2017-04-01T10:00+00:00",
                    "2017-04-01T11:00+00:00",
                    "2017-04-01T12:00+00:00",
                    "2017-04-01T13:00+00:00",
                    "2017-04-01T14:00+00:00",
                    "2017-04-01T15:00+00:00",
                    "2017-04-01T16:00+00:00",
                    "2017-04-01T17:00+00:00",
                    "2017-04-01T18:00+00:00",
                    "2017-04-01T19:00+00:00",
                    "2017-04-01T20:00+00:00",
                    "2017-04-01T21:00+00:00",
                    "2017-04-01T22:00+00:00",
                    "2017-04-01T23:00+00:00"
                ]
            },
            "Info": {
                "Altitude_[m]": 201.0,
                "Description": "Historical temperature data available in hourly resolution.",
                "Latitude": 48.24861,
                "Longitude": 16.35639,
                "Start_date": "2017-04-01",
                "End_date": "2017-04-01"
            }
        }
    ],
    "count": 1
}
```

Please note that in the hourly-resolution data packages hihrp and hihrsn, the numbers given for precipitation and fresh snow refer to one-hour time intervals ending at the given timestamp (reference time).

## Common Errors

The API responds with specific messages for certain errors. They are presented here:

- `Please check request parameters`: One of the query parameters could not be parsed. Check the format of `lat`, `lon`, `start_date`, `end_date` and `package-version`.
- `Please check key or allowed service version`: There is either a typo in the key, or the key does not have permission to retrieve the requested package.
- `Too many results! Please limit search radius or time parameters`: Your query is trying to retrieve too much data at once. Please divide the request in smaller temporal chunks.
