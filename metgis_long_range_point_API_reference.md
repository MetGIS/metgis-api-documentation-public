
# MetGIS long-range Point API

The MetGIS long-range Point API is an application programming interface that can be used to access long-range weather forecast data in JSON format. This document provides a detailed description of its usage.

The API is accessed via HTTP-GET using a URL of the following form:
```
https://api.metgis.com/{endpoint}?key={your-key}&lat={latitude}&lon={longitude}&alt={altitude}&lang={language}&v={package-version}
```

The parameters that have to be set are in in curly brackets and listed in the following table:

Parameter | Description | Comments 
------- | :------: | ---------
endpoint | HTTP endpoint for choosing the forecast model | For the monthly forecast: `forecat-lr-monthly`, for the daily: `forecat-lr-daily`.
key | Key needed to access MetGIS point API | Paying customers have received their API Key after ordering. Information about the collection of free test keys can be found [here](https://weatherapi.metgis.com/get-free-developer-key/). Mandadory parameter.
lat | Latitude of point the weather data is requested for in degrees [°] | Latitude of points south of the equator is negative, use point (.) as decimal separator. Mandatory parameter if no postcode and country is specified.
lon | Longitude of point the weather data is requested for in degrees [°] | Longitude west of 0° meridian can be given as negative values or in the range from 180° to 360°, use point (.) as decimal separator. Mandatory parameter.
alt | Altitude of point the weather data is requested for in meters above sea level  | Optional parameter. If no altitude is given, our computations will use height data from [ASTER data, Version 3 (30m horizontal resolution)](https://earthdata.nasa.gov/learn/articles/new-aster-gdem)
v | Name of requested weather data package | Key must have access rights to requested package, for available package versions check the next sections. Mandatory parameter.

A valid request will be responded with a file in JSON format that contains the weather data. The files are mostly self explaining, but a detailed description of the available packages is given in the next sections. Please remember that data elements of JSON files generally do not contain any particular order. Thus the file can look a bit messed up at first. The units for all the parameters are specified in the file. In case anything goes wrong, the section [common errors](#common-errors) will try to provide help. 

## Monthly Forecast

The API is accessed via HTTP-GET using an URL of the following form, at the `forecat-lr-monthly` endpoint:
```
https://api.metgis.com/forecast-lr-monthly?key={your-key}&lat={latitude}&lon={longitude}&alt={altitude}&v=fclrmonthly
```
Currently, only the `fclrmonthly` package is available for the monthly forecast.

The following forecast fields are available:

| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:|:-----:|
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_localtime), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - | -|
| Forecast_monthly |  [ForecastDates_Utc](data/variable_list_lr_point_api.md#ForecastDates_Utc), [Temperature5thPercentile](data/variable_list_lr_point_api.md#Temperature5thPercentile), [Temperature25thPercentile](data/variable_list_lr_point_api.md#Temperature25thPercentile), [TemperatureMean](data/variable_list_lr_point_api.md#TemperatureMean), [Temperature75thPercentile](data/variable_list_lr_point_api.md#Temperature75thPercentile), [Temperature95thPercentile](data/variable_list_lr_point_api.md#Temperature95thPercentile), [TemperatureMeanAnomaly](data/variable_list_lr_point_api.md#TemperatureMeanAnomaly), [PrecipitationRate5thPercentile](data/variable_list_lr_point_api.md#PrecipitationRate5thPercentile), [PrecipitationRate25thPercentile](data/variable_list_lr_point_api.md#PrecipitationRate25thPercentile), [PrecipitationRateMean](data/variable_list_lr_point_api.md#PrecipitationRateMean), [PrecipitationRate75thPercentile](data/variable_list_lr_point_api.md#PrecipitationRate75thPercentile), [PrecipitationRate95thPercentile](data/variable_list_lr_point_api.md#PrecipitationRate95thPercentile), [PrecipitationRateMeanAnomaly](data/variable_list_lr_point_api.md#PrecipitationRateMeanAnomaly) | 5 to 7 months | 1 month |

What the response JSON looks like is shown in this [example file](data/fclrmonthly.json). It consists of the objects `Info`, and `Forecast_monthly`. 

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated. A full description of the contents can be found [here](data/info_block_1.md).

`Forecast_monthly` contains arrays of weather forecast data for the next months, in monthly resolution, and an array with the months the predictions are valid for.

## Daily Forecast

The API is accessed via HTTP-GET using an URL of the following form, at the `forecat-lr-daily` endpoint:
```
https://api.metgis.com/forecast-lr-daily?key={your-key}&lat={latitude}&lon={longitude}&alt={altitude}&v=fclrdaily
```

Currently, only the `fclrdaily` package is available for the daily forecast.

The following forecast fields are available:

| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:|:-----:|
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_localtime), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - | -|
| Forecast_daily | [ForecastDates_Utc](data/variable_list_lr_point_api.md#ForecastDates_Utc), [TemperatureMin](data/variable_list_lr_point_api.md#TemperatureMin), [TemperatureMean](data/variable_list_lr_point_api.md#TemperatureMean), [TemperatureMax](data/variable_list_lr_point_api.md#TemperatureMax), [PrecipitationTotal_dailySum](data/variable_list_lr_point_api.md#PrecipitationTotal_dailySum), [DownwardShortWaveRadiation](data/variable_list_lr_point_api.md#DownwardShortWaveRadiation) | 5 to 7 months | 1 month |

What the response JSON looks like is shown in this [example file](data/fclrdaily.json). It consists of the objects `Info`, and `Forecast_daily`. 

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated. A full description of the contents can be found [here](data/info_block_1.md).

`Forecast_daily` contains forecast data of up to 40 ensemble models, from `Ensemble_1` to `Ensemble_40`. There can be fewer, depending on data availability. 
Ensemble forecasts are created by perturbing the initial conditions of the main forecast model (i. e. by applying small random changes on it). Their purpose is to assess the certainty of the forecast. If more ensemble models predict a given weather condition, the certainty that this weather condition will occur is higher.
Each ensemble model is an object that contains the parameters listed above. 
The parameters are available for the next 5 to 7 months (depending on data availability), with a daily resolution, for each model in the ensemble. 

## Common errors
The API will respond with different error messages that will be explained below:
- `{"error": "bad_request", "description": "User input validation problem: Longitude -200° is outside of the allowed -180°..180° range"}`  
  Please check if your input parameters are correct.
- `{"error": "noaccesstoversion", "description": "You don't have access to the queried version with the supplied API key"}`  
  This could either mean that the supplied key is not allowed to request this specific data package, or that there is a typo in the package version
  (e. g. `premim` instead of `premium`). This message is also delivered if the data package version is not present in the request.
- `{"error": "invalidkey", "description": "The supplied API key is not valid"}`  
  The supplied key is not found in the user database or got revoked.
- Internal errors: `{"error": "internal_server_error", "description": ""}`, `site can't be reached` or `metgis.com unexpectedly closed the connection`  
  Please contact us and specify the full URL used for the request and the time when the request was made.
