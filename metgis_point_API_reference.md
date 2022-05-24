# MetGIS Point API

The MetGIS Point API is an application programming interface that can be used to access current and forecast weather data in JSON format. This document provides a detailed description of its usage. Information about obtaining access rights to it can be found [here](https://weatherapi.metgis.com/) (English) or [here](https://wetterapi.metgis.com/overview/) (German).

## Quick Start

The API is accessed via HTTP-GET using an URL of the following form:
```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&alt={altitude}&lang={language}&v={package-version}
```

The geographic location for which the data is requested for can also be transmitted by specifying a postcode and country in the request, omitting the parameters lat, lon and alt:
```
https://api.metgis.com/forecast?key={your-key}&zip={postcode}&country={country}&v={package-version}
```
**Important**: Forecasts for postcodes can only be requested for points in Switzerland, Austria and Germany!

The parameters that have to be set are in in curly brackets and listed in the following table:


Parameter | Description | Comments 
------- | :------: | ---------
key | Key needed to access MetGIS point API | Paying customers have received their API Key after ordering. Information about the collection of free test keys can be found [here](https://weatherapi.metgis.com/get-free-developer-key/). Mandadory parameter.
lat | Latitude of point the weather data is requested for in degrees [°] | Latitude of points south of the equator is negative, use point (.) as decimal separator. Mandatory parameter if no postcode and country is specified.
lon | Longitude of point the weather data is requested for in degrees [°] | Longitude west of 0° meridian can be given as negative values or in the range from 180° to 360°, use point (.) as decimal separator. Mandatory parameter if no postcode and country is specified.
alt | Altitude of point the weather data is requested for in meters above sea level  | Optional parameter. If no altitude is given, our computations will use height data from [ASTER data, Version 3 (30m horizontal resolution)](https://earthdata.nasa.gov/learn/articles/new-aster-gdem)
zip | Postcode of point the weather data is requested for. | Service can only be used for points in Switzerland, Austria and Germany. Mandatory parameter if no latitude and longitude is specified. 
country | Country of point the weather data is requested for. Can either be `ch`, `at` or `de` | Service can only be used for points in Switzerland, Austria and Germany. Mandatory parameter if no latitude and longitude is specified.  
v | Name of requested weather data package | Key must have access rights to requested package, for available package versions check the table in section [package versions](#package-versions). Mandatory parameter.
lang | Language select key | Optional parameter. Can be used to change the language in text forecasts for certain packages. Can be either `de` for German (default), `en` for English or `es` for Spanish. 
fctime | Parameter to specify date and time for the package version `fctisl`. | Format of this parameter is `yyyymmddHHMM`, e. g. `202204172230` for the 17th of April 2022 at half past ten in the evening (UTC time!). Mandatory parameter for the package `fctisl`.

A valid request will be responded with a file in JSON format that contains the weather data. The files are mostly self explaining, but a detailed description of the available packages is given [in the next section](#package-versions). Please remember that data elements of JSON files generally do not contain any particular order. Thus the file can look a bit messed up at first. The units for all the parameters are specified in the file.


The next section will explain the different available weather data packages, while the section [common errors](#common-errors) will try to provide help in case anything goes wrong.

## Package Versions

### Overview

The following table presents an overview of weather data packages available from the MetGIS Point API.

The packages differ in terms of:
* Forecast range: This stands for the time period a forecast covers. MetGIS weather forecasts currently reach out up to 10 days in the future.
* Time resolution: This stands for the available interval of forecast time steps (1, 3, 6 or 24 hours). 
* Forecast parameters: A wide range of forecast parameters are available via the MetGIS Point API. Check this [compilation](data/variable_list_point_api.md) for more details.

| Package Version | Description | Optional Parameters |
| ---- | :----: | ----- |
| [current](#package-current) | Weather data for the current moment at location of interest | alt |
| [starter](#package-starter) | Forecast weather data for the location of interest. Forecasts in 3-hourly and daily resolution included | alt |
| [smart](#package-smart) | Current and forecast weather data  for the location of interest. Forecasts in 3-hourly and daily resolution included | alt |
| [premium](#package-premium) | Current and extended weather forecast data for the location of interest. Forecasts in hourly, 3-, 6-hourly and daily resolution | alt, lang |
| [winter](#package-winter) | Current and extended weather forecast data for the location of interest. Forecasts in hourly, 3-, 6-hourly and daily resolution. This forecast incorporates special "winter" parameters like fresh snow density and the height of the 0°C isotherm | alt | 
| [fctisl](#package-fctisl) | Weather forecast data for a specific time, very compact. | alt |

The following sections describe the available packages:

### Package current

The response JSON describes the current state of the weather at the point of interest. It can be retrieved by calling the API like this:
```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&v=current
```
This table gives an overview of what is included in this package:
| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:| :-----: |
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_local_time), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - | - |
| Current | [Temperature](data/variable_list_point_api.md#temperature), [PrecipitationTotal_Intensity](data/variable_list_point_api.md#precipitationtotal_intensity),  [PrecipitationSnow_Intensity](data/variable_list_point_api.md#precipitationsnow_intensity), [PrecipitationRain_Intensity](data/variable_list_point_api.md#precipitationrain_intensity), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindDirection](data/variable_list_point_api.md#winddirection), [WindStrength](data/variable_list_point_api.md#windstrength), [SunSet](data/variable_list_point_api.md#sunset), [SunRise](data/variable_list_point_api.md#sunrise), [MoonSet](data/variable_list_point_api.md#moonset), [MoonRise](data/variable_list_point_api.md#moonrise), [MoonPhase](data/variable_list_point_api.md#moonphase), [Icon](data/variable_list_point_api.md#icon) | Valid for time of request | - |

This [example file](data/current.json) shows what a response JSON looks like. It consists of the objects `Info` that contains the geographic coordinates of the point of interest and the time the forecast is valid for, and `Current`, which holds the actual weather parameters and their descriptions. The current weather data is obtained from surrounding observations and numerical weather prediction model data for the time at which the request is happening.




### Package starter

Requesting this data package yields a JSON format answer, with forecast weather data for any point of interest. It can be requested like this:
```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&v=starter
``` 
This table gives an overview of the information included in this package:




| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:|:-----:|
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_local_time), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - | -|
| Forecast_3hourly | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon),  [PrecipitationTotal_3hourlySum](data/variable_list_point_api.md#precipitationtotal_3hourlysum), [Temperature](data/variable_list_point_api.md#temperature), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WeatherDescription](data/variable_list_point_api.md#weatherdescription) | 1 day | 3 hours |
| Forecast_daily | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationTotal_dailySum](data/variable_list_point_api.md#precipitationtotal_dailysum]), [TemperatureMaximum](data/variable_list_point_api.md#TemperatureMaximum), [TemperatureMinimum](data/variable_list_point_api.md#TemperatureMinimum), [WindDirection](data/variable_list_point_api.md#), [WindSpeed](data/variable_list_point_api.md#), [WeatherDescription](data/variable_list_point_api.md#weatherdescription) | 3 days | 1 day |

What the response JSON looks like is shown in this [example file](data/starter.json). It consists of the objects `Info`, `Forecast_3hourly` and `Forecast_daily`. 

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated. A full description of the contents can be found [here](data/info_block_1.md).

`Forecast_3hourly` contains arrays of weather forecast data for the next 24 hours, in 3-hourly resolution, and an array with the times and dates the predictions are valid for.

The object `Forecast_daily` contains weather parameters describing the weather over periods of 24 hours for the next three days. Included are sums, minimum and maximum values of certain parameters and a weather icon code describing the weather character on given day.

### Package smart

Requesting this data package yields a JSON format answer, with forecast and current weather data for any point of interest. It can be requested like this:
```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&v=smart
``` 
This table gives an overview of the information included in this package:




| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:|:-----:|
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_local_time), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - | -|
| Current | [Temperature](data/variable_list_point_api.md#temperature), [PrecipitationTotal_Intensity](data/variable_list_point_api.md#precipitationtotal_intensity),  [PrecipitationSnow_Intensity](data/variable_list_point_api.md#precipitationsnow_intensity), [PrecipitationRain_Intensity](data/variable_list_point_api.md#precipitationrain_intensity), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindDirection](data/variable_list_point_api.md#winddirection), [WindStrength](data/variable_list_point_api.md#windstrength), [SunSet](data/variable_list_point_api.md#sunset), [SunRise](data/variable_list_point_api.md#sunrise), [MoonSet](data/variable_list_point_api.md#moonset), [MoonRise](data/variable_list_point_api.md#moonrise), [MoonPhase](data/variable_list_point_api.md#moonphase), [Icon](data/variable_list_point_api.md#icon) | Valid for time of request | - |
| Forecast_3hourly | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [PrecipitationRain_3hourlySum](data/variable_list_point_api.md#precipitationrain_3hourlysum), [PrecipitationSnow_3hourlySum](data/variable_list_point_api.md#precipitationsnow_3hourlysum), [PrecipitationTotal_3hourlySum](data/variable_list_point_api.md#precipitationtotal_3hourlysum), [Temperature](data/variable_list_point_api.md#temperature), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindStrength](data/variable_list_point_api.md#windstrength) | 3 days | 3 hours |
| Forecast_daily | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [PrecipitationRain_dailySum](data/variable_list_point_api.md#precipitationrain_dailysum), [PrecipitationSnow_dailySum](data/variable_list_point_api.md#precipitationsnow_dailysum), [PrecipitationTotal_dailySum](data/variable_list_point_api.md#precipitationtotal_dailysum]), [SunRise](data/variable_list_point_api.md#sunrise), [SunSet](data/variable_list_point_api.md#sunset), [TemperatureMaximum](data/variable_list_point_api.md#TemperatureMaximum), [TemperatureMinimum](data/variable_list_point_api.md#TemperatureMinimum), [ThunderstormProbability](data/variable_list_point_api.md#), [WindDirection](data/variable_list_point_api.md#), [WindSpeed](data/variable_list_point_api.md#), [WindStrength](data/variable_list_point_api.md#), [WeatherDescription](data/variable_list_point_api.md#weatherdescription)  | 8 days | 1 day |



What the response JSON looks like is shown in this [example file](data/smart.json). It consists of the objects `Info`, `Current`, `Forecast_3hourly` and `Forecast_daily`. 

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated. A full description of the contents can be found [here](data/info_block_1.md).

The Object `Current` provides information about the current weather conditions at the specified location at the time of the data request. It is obtained from surrounding observations and numerical weather prediction model data. A description of its contents can be found [here](data/current_block_1.md).

`Forecast_3hourly` contains arrays of weather forecast data for the next 3 days, in 3-hourly resolution, and an array with the times and dates the predictions are valid for. A complete description of the included weather parameters can be found [here](data/forecast3hourly_block_1.md).

The object `Forecast_daily` contains weather parameters describing the weather over periods of 24 hours for the next eight days. Included are sums, minimum and maximum values of certain parameters and a weather icon code describing the weather character on given day. A complete listing of the included fields can be found [here](data/forecastdaily_block_1.md).



### Package premium

This package contains detailed weather forecast data in different temporal resolutions. It can be requested with a URL of the following form:

```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&v=premium&lang={en|de|es}
```
Like in the other packages, the query parameter `lang` can be used to request the weather forecasts text in English language if set to `en` or in Spanish if set to `es`. The default value is `de` for German. As with all other packages the `alt` parameter can be used if very accurate geographic data is available, otherwise the height above sea level will be interpolated from [ASTER data, Version 3 (30m horizontal resolution)](https://earthdata.nasa.gov/learn/articles/new-aster-gdem).

The following table provides an overview of the information contained in this package:
| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | -----| ---------|
| Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_local_time), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude](data/variable_list_point_api.md#altitude) | - |
| Current | [Temperature](data/variable_list_point_api.md#temperature), [PrecipitationTotal_Intensity](data/variable_list_point_api.md#precipitationtotal_intensity),  [PrecipitationSnow_Intensity](data/variable_list_point_api.md#precipitationsnow_intensity), [PrecipitationRain_Intensity](data/variable_list_point_api.md#precipitationrain_intensity), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindDirection](data/variable_list_point_api.md#winddirection), [WindStrength](data/variable_list_point_api.md#windstrength), [SunSet](data/variable_list_point_api.md#sunset), [SunRise](data/variable_list_point_api.md#sunrise), [MoonSet](data/variable_list_point_api.md#moonset), [MoonRise](data/variable_list_point_api.md#moonrise), [MoonPhase](data/variable_list_point_api.md#moonphase), [Icon](data/variable_list_point_api.md#icon) | Valid for time of request | - |
| Forecast_hourly | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationRain_hourlySum](data/variable_list_point_api.md#precipitationrain_hourlysum), [PrecipitationSnow_hourlySum](data/variable_list_point_api.md#precipitationsnow_hourlysum), [PrecipitationTotal_hourlySum](data/variable_list_point_api.md#precipitationtotal_hourlysum), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [Temperature](data/variable_list_point_api.md#temperature), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindStrength](data/variable_list_point_api.md#windstrength) | 4 days | 1 hour |
| Forecast_3hourly | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [PrecipitationRain_3hourlySum](data/variable_list_point_api.md#precipitationrain_3hourlysum), [PrecipitationSnow_3hourlySum](data/variable_list_point_api.md#precipitationsnow_3hourlysum), [PrecipitationTotal_3hourlySum](data/variable_list_point_api.md#precipitationtotal_3hourlysum), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [Temperature](data/variable_list_point_api.md#temperature), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindStrength](data/variable_list_point_api.md#windstrength) | 9.5 days | 3 hours | 
| Forecast_6hourly | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [PrecipitationRain_6hourlySum](data/variable_list_point_api.md#precipitationrain_6hourlysum), [PrecipitationSnow_6hourlySum](data/variable_list_point_api.md#precipitationsnow_6hourlysum), [PrecipitationTotal_6hourlySum](data/variable_list_point_api.md#precipitationtotal_6hourlysum), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [Temperature](data/variable_list_point_api.md#temperature), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindStrength](data/variable_list_point_api.md#windstrength) | 9.5 days | 6 hours |
| Forecast_daily | [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [Icon](data/variable_list_point_api.md#icon), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [PrecipitationRain_dailySum](data/variable_list_point_api.md#precipitationrain_dailysum), [PrecipitationSnow_dailySum](data/variable_list_point_api.md#precipitationsnow_dailysum), [PrecipitationTotal_dailySum](data/variable_list_point_api.md#precipitationtotal_dailysum), [RelativeHumidityMean](data/variable_list_point_api.md#relativehumiditymean), [SunRise](data/variable_list_point_api.md#sunrise), [SunSet](data/variable_list_point_api.md#sunset), [TemperatureMaximum](data/variable_list_point_api.md#temperaturemaximum), [TemperatureMinimum](data/variable_list_point_api.md#temperatureminimum), [TextForecast](data/variable_list_point_api.md#textforecast), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [TotalCloudCoverMean](data/variable_list_point_api.md#totalcloudcovermean), [WindDirection](data/variable_list_point_api.md#winddirection), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindSpeedMaximum](data/variable_list_point_api.md#windspeedmaximum), [WindStrength](data/variable_list_point_api.md#windstrength), [WeatherDescription](data/variable_list_point_api.md#weatherdescription)  | 10 days | 1 day |

 
What a response JSON looks like is shown in this [example](data/premium.json). It contains the JSON Objects listed in column Item in the table above.

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated. A full description of the contents can be found [here](data/info_block_1.md).

The Object `Current` provides information about the current weather conditions at the specified location at the time of the data request. It is obtained from surrounding observations and numerical weather prediction model data. A description of its contents can be found [here](data/current_block_premium.md).

`Forecast_3hourly` contains arrays of weather forecast data for the next 3 days, in 3-hourly resolution, and an array with the times and dates the predictions are valid for. A complete description of the included weather parameters can be found [here](data/forecast3hourly_block_premium.md)

`Forecast_6hourly` covers the same needs as `Forecast_3hourly` but with a temporal resolution of 6 hours. All available fields in this object can be found [here](data/forecast6hourly_block_premium.md)

The object `Forecast_daily` contains weather parameters describing the weather over periods of 24 hours for the next eight days. Included are sums, minimum and maximum values of certain parameters and a weather icon code describing the weather character on the given days. A complete listing of the included fields can be found [here](data/forecastdaily_block_premium.md).


### Package winter

Requesting this data package yields a JSON format answer, with forecast and current weather data for any point of interest. On top of an extended variety of conventional forecast data, special parameters that are important in cold and snowy conditions are included. It can be requested like this:
```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&v=winter
``` 
This table gives an overview of the information included in this package:




| Item | Included Parameters | Forecast Range | Time Resolution |
| --- | ------ | :-----:|:-----:|
Info | [Description](data/variable_list_point_api.md#description), [Forecast_Calculated_LocalTime](data/variable_list_point_api.md#forecast_calculated_localtime), [Forecast_Calculated_UTC](data/variable_list_point_api.md#forecast_calculated_utc), [Latitude](data/variable_list_point_api.md#latitude), [Longitude](data/variable_list_point_api.md#longitude), [Altitude_[m]](data/variable_list_point_api.md#altitude_[m])  | - |  - |
| Current | [Temperature](data/variable_list_point_api.md#temperature), [MoonPhase](data/variable_list_point_api.md#moonphase), [FreshSnowDensity](data/variable_list_point_api.md#freshsnowdensity), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [TotalCloudCover](data/variable_list_point_api.md#totalcloudcover), [WindSpeed](data/variable_list_point_api.md#windspeed), [ZeroDegreeIsothermHeight](data/variable_list_point_api.md#zerodegreeisothermheight), [PrecipitationType](data/variable_list_point_api.md#precipitationtype), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [FeltTemperature](data/variable_list_point_api.md#felttemperature), [PrecipitationSnow_Intensity](data/variable_list_point_api.md#precipitationsnow_intensity), [LowerCloudLimit](data/variable_list_point_api.md#lowercloudlimit), [WindDirection](data/variable_list_point_api.md#winddirection), [WindStrength](data/variable_list_point_api.md#windstrength), [PrecipitationTotal_Intensity](data/variable_list_point_api.md#precipitationtotal_intensity), [MoonRise](data/variable_list_point_api.md#moonrise), [SnowfallLine](data/variable_list_point_api.md#snowfallline), [Sunset](data/variable_list_point_api.md#sunset), [UpperCloudLimit](data/variable_list_point_api.md#uppercloudlimit), [WetBulbTemperature](data/variable_list_point_api.md#wetbulbtemperature), [MoonSet](data/variable_list_point_api.md#moonset), [Sunrise](data/variable_list_point_api.md#sunrise), [Icon](data/variable_list_point_api.md#icon), [PrecipitationRain_Intensity](data/variable_list_point_api.md#precipitationrain_intensity) | -  | - |
| Forecast_hourly | [Temperature](data/variable_list_point_api.md#temperature), [FreshSnowDensity](data/variable_list_point_api.md#freshsnowdensity), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [PrecipitationRain_hourlySum](data/variable_list_point_api.md#precipitationrain_hourlysum), [TotalCloudCover](data/variable_list_point_api.md#totalcloudcover), [WindSpeed](data/variable_list_point_api.md#windspeed), [PrecipitationTotal_hourlySum](data/variable_list_point_api.md#precipitationtotal_hourlysum), [ZeroDegreeIsothermHeight](data/variable_list_point_api.md#zerodegreeisothermheight), [WindStrength_usedValues](data/variable_list_point_api.md#windstrength_usedvalues), [PrecipitationSnow_hourlySum](data/variable_list_point_api.md#precipitationsnow_hourlysum), [PrecipitationType](data/variable_list_point_api.md#precipitationtype), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [FeltTemperature](data/variable_list_point_api.md#felttemperature), [WindDirection_usedValues](data/variable_list_point_api.md#winddirection_usedvalues), [WindDirection](data/variable_list_point_api.md#winddirection), [LowerCloudLimit](data/variable_list_point_api.md#lowercloudlimit), [WindStrength](data/variable_list_point_api.md#windstrength), [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [SunshineDuration_hourlySum](data/variable_list_point_api.md#sunshineduration_hourlysum), [SnowfallLine](data/variable_list_point_api.md#snowfallline), [PrecipitationSnow_Sum](data/variable_list_point_api.md#precipitationsnow_sum), [UpperCloudLimit](data/variable_list_point_api.md#uppercloudlimit), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [WetBulbTemperature](data/variable_list_point_api.md#wetbulbtemperature), [Icon](data/variable_list_point_api.md#icon), [ThunderstormProbabilities_usedValues](data/variable_list_point_api.md#thunderstormprobabilities_usedvalues) |  4 days | 1 hour |
Forecast_3hourly | [MinimumWetBulbTemperature](data/variable_list_point_api.md#minimumwetbulbtemperature), [FreshSnowDensity](data/variable_list_point_api.md#freshsnowdensity), [MinimumFeltTemperature](data/variable_list_point_api.md#minimumfelttemperature), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindString_usedValues](data/variable_list_point_api.md#windstring_usedvalues), [RelativeHumidity](data/variable_list_point_api.md#relativehumidity), [PrecipitationSnow_3hourlySum](data/variable_list_point_api.md#precipitationsnow_3hourlysum), [FeltTemperature](data/variable_list_point_api.md#felttemperature), [WindStrength](data/variable_list_point_api.md#windstrength), [PrecipitationRain_3hourlySum](data/variable_list_point_api.md#precipitationrain_3hourlysum), [UpperCloudLimit](data/variable_list_point_api.md#uppercloudlimit), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [MinimumRelativeHumidity](data/variable_list_point_api.md#minimumrelativehumidity), [Icon](data/variable_list_point_api.md#icon), [Temperature](data/variable_list_point_api.md#temperature), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [ZeroDegreeIsothermHeight](data/variable_list_point_api.md#zerodegreeisothermheight), [SunshineDuration_3hourlySum](data/variable_list_point_api.md#sunshineduration_3hourlysum), [PrecipitationType](data/variable_list_point_api.md#precipitationtype), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [WindDirection_usedValues](data/variable_list_point_api.md#winddirection_usedvalues), [WindDirection](data/variable_list_point_api.md#winddirection), [LowerCloudLimit](data/variable_list_point_api.md#lowercloudlimit), [MaximumWetBulbTemperature](data/variable_list_point_api.md#maximumwetbulbtemperature), [MaximumRelativeHumidity](data/variable_list_point_api.md#maximumrelativehumidity), [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [MinimumTemperature](data/variable_list_point_api.md#minimumtemperature), [SnowfallLine](data/variable_list_point_api.md#snowfallline), [MaximumFeltTemperature](data/variable_list_point_api.md#maximumfelttemperature), [MaximumTemperature](data/variable_list_point_api.md#maximumtemperature), [WetBulbTemperature](data/variable_list_point_api.md#wetbulbtemperature), [PrecipitationTotal_3hourlySum](data/variable_list_point_api.md#precipitationtotal_3hourlysum), [ThunderstormProbabilities_usedValues](data/variable_list_point_api.md#thunderstormprobabilities_usedvalues) | 9.5 days| 3 hours |
Forecast_6hourly | [Temperature](data/variable_list_point_api.md#temperature), [MinimumWetBulbTemperature](data/variable_list_point_api.md#minimumwetbulbtemperature), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [MinimumFeltTemperature](data/variable_list_point_api.md#minimumfelttemperature), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindString_usedValues](data/variable_list_point_api.md#windstring_usedvalues), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [SunshineDuration](data/variable_list_point_api.md#sunshineduration), [FeltTemperature](data/variable_list_point_api.md#felttemperature), [WindDirection_usedValues](data/variable_list_point_api.md#winddirection_usedvalues), [WindDirection](data/variable_list_point_api.md#winddirection), [MaximumWetBulbTemperature](data/variable_list_point_api.md#maximumwetbulbtemperature), [MaximumRelativeHumidity](data/variable_list_point_api.md#maximumrelativehumidity), [WindStrength](data/variable_list_point_api.md#windstrength), [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [MinimumTemperature](data/variable_list_point_api.md#minimumtemperature), [SnowfallLine](data/variable_list_point_api.md#snowfallline), [MaximumFeltTemperature](data/variable_list_point_api.md#maximumfelttemperature), [PrecipitationSnow_6hourlySum](data/variable_list_point_api.md#precipitationsnow_6hourlysum), [PrecipitationRain_6hourlySum](data/variable_list_point_api.md#precipitationrain_6hourlysum), [MaximumTemperature](data/variable_list_point_api.md#maximumtemperature), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [PrecipitationTotal_6hourlySum](data/variable_list_point_api.md#precipitationtotal_6hourlysum), [MinimumRelativeHumidity](data/variable_list_point_api.md#minimumrelativehumidity), [Icon](data/variable_list_point_api.md#icon), [ThunderstormProbabilities_usedValues](data/variable_list_point_api.md#thunderstormprobabilities_usedvalues) | 9.5 days | 6 hours |    
Forecast_daily | [MoonPhase](data/variable_list_point_api.md#moonphase), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [MinimumFeltTemperature](data/variable_list_point_api.md#minimumfelttemperature), [WindSpeed](data/variable_list_point_api.md#windspeed), [WindString_usedValues](data/variable_list_point_api.md#windstring_usedvalues), [SunSet](data/variable_list_point_api.md#sunset), [PrecipitationProbability](data/variable_list_point_api.md#precipitationprobability), [SunshineDuration](data/variable_list_point_api.md#sunshineduration), [SunRise](data/variable_list_point_api.md#sunrise), [WindDirection_usedValues](data/variable_list_point_api.md#winddirection_usedvalues), [MaximumSnowfallLine](data/variable_list_point_api.md#maximumsnowfallline), [WindDirection](data/variable_list_point_api.md#winddirection), [WindStrength](data/variable_list_point_api.md#windstrength), [ForecastTimes_LocalTime](data/variable_list_point_api.md#forecasttimes_localtime), [PrecipitationTotal_dailySum](data/variable_list_point_api.md#precipitationtotal_dailysum), [MinimumTemperature](data/variable_list_point_api.md#minimumtemperature), [MoonRise](data/variable_list_point_api.md#moonrise), [PrecipitationSnow_dailySum](data/variable_list_point_api.md#precipitationsnow_dailysum), [MaximumFeltTemperature](data/variable_list_point_api.md#maximumfelttemperature), [MaximumTemperature](data/variable_list_point_api.md#maximumtemperature), [MinimumSnowfallLine](data/variable_list_point_api.md#minimumsnowfallline), [ThunderstormProbability](data/variable_list_point_api.md#thunderstormprobability), [MoonSet](data/variable_list_point_api.md#moonset), [Icon](data/variable_list_point_api.md#icon), [PrecipitationRain_dailySum](data/variable_list_point_api.md#precipitationrain_dailysum), [ThunderstormProbabilities_usedValues](data/variable_list_point_api.md#thunderstormprobabilities_usedvalues) | 10 days | 1 day|

What a response JSON looks like is shown in this [example](data/winter.json). It contains the JSON Objects listed in column Item in the table above.

`Info` contains a general description of the data, geographic information of the point of interest and the date and time when the forecast was calculated.

The Object `Current` provides information about the current weather conditions at the specified location at the time of the data request. It is obtained from surrounding observations and numerical weather prediction model data. 

`Forecast_3hourly` contains arrays of weather forecast data for the next 3 days, in 3-hourly resolution, and an array with the times and dates the predictions are valid for. 

`Forecast_6hourly` covers the same needs as `Forecast_3hourly` but with a temporal resolution of 6 hours.

The object `Forecast_daily` contains weather parameters describing the weather over periods of 24 hours for the next eight days. Included are sums, minimum and maximum values of certain parameters and a weather icon code describing the weather character on the given days.


### Package fctisl


This package includes weather forecast data for a single point in time, and can therefore be used to keep the web traffic low if only a limited amount of data is needed. To request it the additional parameter `fctime` has to be provided, specifying the time and date for which the forecast data is needed:

```
https://api.metgis.com/forecast?key={your-key}&lat={latitude}&lon={longitude}&alt={altitude}&v=fctisl&fctime={yyyymmddHHMM}
```
The format of this parameter is `yyyymmddHHMM`, e. g. `202204172230` for the 17th of April 2022 at half past ten in the evening (UTC time!). Please note that weather data can only be requested in within the range of the next ten days.

This table gives an overview of the information included in this package:




| Item | Included Parameters | 
| --- | ------ |
| forecasts | [date](data/variable_list_point_api.md#date), [Temperature](data/variable_list_point_api.md#temperature), [PrecipitationTotal_Intensity](data/variable_list_point_api.md#precipitationtotal_intensity), [PrecipitationSnow_Intensity](data/variable_list_point_api.md#precipitationsnow_intensity), [WeatherDescription](data/variable_list_point_api.md#weatherdescription), [alt](data/variable_list_point_api.md#alt), [lon](data/variable_list_point_api.md#lon), [WindSpeed](data/variable_list_point_api.md#windspeed), [Icon](data/variable_list_point_api.md#icon), [WindDirection](data/variable_list_point_api.md#winddirection), [lat](data/variable_list_point_api.md#lat) |

What a response JSON looks like is shown in this [example](data/fctisl.json). The forecasts structure contains the weather data for the requested time and date at the specified location. Also included in the JSON file are fields that describe the units used for the forecast data.

## Common Errors

The API will respond with different error messages that will be explained below:

- `Failure: 400 Bad Request: malformed geographic information (could not process lat,lon,alt)`: This response means that there is probably a syntax error in the geographic part of the request, e. g. using a comma instead of a point as decimal marker.
- `{"description":"You don't have access to the queried version with the supplied API key","error":"noaccesstoversion"}`: This could either mean that the supplied key is not allowed to request this specific data package, or that there is a typo in the package version (e. g. `premim` instead of `premium`). This message is also delivered if the data package version is not present in the request.
- `{"error":"invalidkey","description":"The supplied API key is not valid"}`: The supplied key is not found in the user database or got revoked.

## FAQs

**How to pick the right value from a JSON forecast file?**

All weather data in the JSON file is structured in various sections (“objects”) based on temporal resolution, e.g.:

Section (“objects”) | Description
--- | ---
Forecast_3hourly | Contains forecasts with values on a 3-hour basis. Where applicable, the parameter names in this section contain the extension “_3hourlySum”. The same logic applies to "Forecast_6hourly" or Forecast_hourly".
Forecast_daily | Contains forecasts with values on a daily basis. Where applicable, the parameter names in this section contain the extension “_dailySum”.

After choosing the right section (“object”), take a look at the array called `ForecastTimes_LocalTime`. This array contains the exact individual dates all weather data in the object refer to. To finally retrieve a specific weather-related value for a specific date, pick the value at the respective position. E.g. to get the value for the 3rd date (“`ForecastTimes_LocalTime`), you have to use the 3rd value of a given weather parameter array.

Temporal Resolution | Example of “ForecastTimes_LocalTime” array
--- | ---
3 hours | e.g. “2017-07-26T15:00+02:00”, “2017-07-26T18:00+02:00”, “2017-07-26T21:00+02:00”, “2017-07-27T00:00+02:00”… Important: For parameters that relate to sums (e.g. precipitation, sunshine duration) the time refers to the past period, i.e. “…T15:00” covers the 3-hours period between 12:00 and 15:00.
1 day | e.g. “2017-07-28”, “2017-07-29”, “2017-07-30”, “2017-07-31”, “2017-08-01”, “2017-08-02”…

Example: How much will it rain tonight between 18:00 and 21:00 hours?

In the object “Forecast_3hourly” you will find the “ForcastTimes_LocalTime” array with these values:
“2017-07-26T15:00+02:00”, “2017-07-26T18:00+02:00”, “2017-07-26T21:00+02:00”.

For parameters like precipitation, the time always refers to the past period. So the 3rd value (“2017-07-26T21:00+02:00”) contains the period in question.

Now have a look at “PrecipitationRain_3hourlySum” which e.g. shows: 0, 5, 18. Since you need the 3rd value, you will retrieve “18” as the correct amount. Use the “PrecipitationRain_3hourlySum_Unit” element to find out the parameter unit: mm/3h.

**Can you tell me more about the usage of time parameters, local time and daylight savings time?**

All time/date specifications are based on the international ISO 8601 norm to avoid misinterpretations and improve automatic data processing. They are displayed in local time of the coordinate in question (Format: YYYY-MM-DDTHH:MM+time difference to UTC). Daylight savings time is incorporated.
(So just to make 100% sure: “SunSet: ["2018-02-12T18:50+05:00"]” would mean that on February 12th the sun sets at 6.50 pm local time at the coordinate in question. You do NOT need to do any calculations. The “+05:00” just shows the time difference compared to UTC, but this is just for your information as it is already incorporated)


**What about the integration of weather icons? Do you provide any?**

To help you display weather icons on your website or in your app, we include the parameter “Icon” that contains a descriptive file name (26 possible values, e.g.“sunny.png”). This value summarizes as far as possible cloud cover, precipitation quantity (snow/rain) and thunderstorm probability for the period in question and enables you to integrate your individual weather icons.
For our API customers we provide basic icon sets in different styles for free (.ai and .png-format). Please get in touch with us and we'll happily send them to you. These sets may only be used within your purchased application and may not be redistributed.
If you've already got an icon set which you want to use, this overview might help you to assign them correctly to the corresponding values of the "Icon" parameter:
![](img/all_weather_icons.png)

**Do you provide a tool to check my number of API calls?**

The MetGIS API Monitoring Tool (AMT) allows you at any time to get a review of the API calls processed with your API Key(s). You can check the number of API calls you have made in the past, up to the present date. This includes daily or monthly time resolutions and simple diagrams. 

Access to the AMT is via the page https://www.metgis.com/api-monitoring-tool/. To log in, please use your personal username and password.
