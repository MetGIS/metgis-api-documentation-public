# List of Variables and Fields Used by the MetGIS Point API

## Altitude\_[m]

Altitude of point the forecast was calculated for in meters above mean sea level.

## Description

Short description of the package version.

## FeltTemperature

Parameter that describes the air temperature as felt by a human being. For cold temperatures this is equivalent to wind chill temperatures while for warm temperatures the influence of humidity on the felt temperature is incorporated.

## Forecast_Calculated_LocalTime

Time when the forecast was calculated, related to the local time zone of the point of interest (ISO 8601 date format).

## Forecast_Calculated_UTC

Time when the forecast was calculated in UTC (ISO 8601 date format).

## ForecastTimes_LocalTime

Array of times and dates at which the forecasts in the same object are valid. The time zone is set according to the coordinates of the location and the format is compliant with ISO 8601.

## FreshSnowDensity_Unit

Unit of [FreshSnowDensity](#freshsnowdensity)

## FreshSnowDensity

Forecast of the density the fresh snow will have at the point of interest.

## Icon

File name of weather icon that describes the weather conditions at the point of interest for a given time. The file names are descriptive so it’s easy to use your individual icons. Possible values are described here:

<details>
<summary>MetGIS Point API icons</summary>

| Icon                                   | Description                                        | Image                                                                                    |
| -------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| cloud_bright_rain_drizzle.png          | light showers                                      | ![cloud_bright_rain_drizzle.png](../img/cloud_bright_rain_drizzle.png)                   |
| cloud_bright_rain_easy.png             | wet                                                | ![cloud_bright_rain_easy.png](../img/cloud_bright_rain_easy.png)                         |
| cloud_bright_rain_hard.png             | heavy rain                                         | ![cloud_bright_rain_hard.png](../img/cloud_bright_rain_hard.png)                         |
| cloud_bright_rain_snow_easy.png        | changeable, light showers of rain or snow possible | ![cloud_bright_rain_snow_easy.png](../img/cloud_bright_rain_snow_easy.png)               |
| cloud_bright_rain_snow_hard.png        | heavy snowfall and rain                            | ![cloud_bright_rain_snow_hard.png](../img/cloud_bright_rain_snow_hard.png)               |
| cloud_bright_snow_drizzle.png          | light snow showers                                 | ![cloud_bright_snow_drizzle.png ](../img/cloud_bright_snow_drizzle.png)                  |
| cloud_bright_snow_easy.png             | some snowfall                                      | ![cloud_bright_snow_easy.png ](../img/cloud_bright_snow_easy.png)                        |
| cloud_bright_snow_hard.png             | heavy snowfall                                     | ![cloud_bright_snow_hard.png](../img/cloud_bright_snow_hard.png)                         |
| cloud_thunder_rain.png                 | overcast with thunderstorms                        | ![cloud_thunder_rain.png](../img/cloud_thunder_rain.png)                                 |
| cloud_thunder_rain_snow.png            | thunderstorms with rain or snow                    | ![cloud_thunder_rain_snow.png](../img/cloud_thunder_rain_snow.png)                       |
| cloud_thunder_snow.png                 | thunderstorms with snow                            | ![cloud_thunder_snow.png](../img/cloud_thunder_snow.png)                                 |
| cloudy_bright.png                      | overcast                                           | ![cloudy_bright.png](../img/cloudy_bright.png)                                           |
| sun_bright_cloud.png                   | sunny                                              | ![sun_bright_cloud.png](../img/sun_bright_cloud.png)                                     |
| sun_cloud_bright_rain_drizzle.png      | changeable, light showers possible                 | ![sun_cloud_bright_rain_drizzle.png](../img/sun_cloud_bright_rain_drizzle.png)           |
| sun_cloud_bright_rain_easy.png         | changeable, showers possible                       | ![sun_cloud_bright_rain_easy.png](../img/sun_cloud_bright_rain_easy.png)                 |
| sun_cloud_bright_rain_hard.png         | wet, sunny spells possible                         | ![sun_cloud_bright_rain_hard.png](../img/sun_cloud_bright_rain_hard.png)                 |
| sun_cloud_bright_rain_snow_easy.png    | changeable, light showers of rain or snow possible | ![sun_cloud_bright_rain_snow_easy.png](../img/sun_cloud_bright_rain_snow_easy.png)       |
| sun_cloud_bright_rain_snow.png         | snowfall or rain, sunny spells possible            | ![sun_cloud_bright_rain_snow.png](../img/sun_cloud_bright_rain_snow.png)                 |
| sun_cloud_bright_rain_snow_thunder.png | thundery showers of rain or snow possible          | ![sun_cloud_bright_rain_snow_thunder.png](../img/sun_cloud_bright_rain_snow_thunder.png) |
| sun_cloud_bright_rain_thunder.png      | thundery showers possible                          | ![sun_cloud_bright_rain_thunder.png](../img/sun_cloud_bright_rain_thunder.png)           |
| sun_cloud_bright_snow_drizzle.png      | changeable, light snow showers possible            | ![sun_cloud_bright_snow_drizzle.png](../img/sun_cloud_bright_snow_drizzle.png)           |
| sun_cloud_bright_snow_easy.png         | changeable, snow showers possible                  | ![sun_cloud_bright_snow_easy.png](../img/sun_cloud_bright_snow_easy.png)                 |
| sun_cloud_bright_snow_hard.png         | snowfall, sunny spells possible                    | ![sun_cloud_bright_snow_hard.png](../img/sun_cloud_bright_snow_hard.png)                 |
| sun_cloud_bright_snow_thunder.png      | thundery snow showers possible                     | ![sun_cloud_bright_snow_thunder.png](../img/sun_cloud_bright_snow_thunder.png)           |
| sun_cloudy_bright.png                  | partly cloudy                                      | ![sun_cloudy_bright.png](../img/sun_cloudy_bright.png)                                   |
| sunny.png                              | cloudless                                          | ![sunny.png](../img/sunny.png)                                                           |

</details>

## Latitude

Latitude of point the forecast was calculated for (in decimal degrees). Negative values refer to latitudes south of the equator.

## Longitude

Longitude of point the forecast was calculated for (in decimal degrees). Negative values refer to longitudes west of the zero meridian.

## LowerCloudLimit

Forecast of the cloud base height above sea level.

## LowerCloudLimit_Unit

Unit of [LowerCloudLimit](#lowercloudlimit)

## MaximumFeltTemperature

Maximum [felt temperature](#felttemperature) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MaximumFeltTemperature_Unit

Unit of [MaximumFeltTemperature](#maximumfelttemperature)

## MaximumRelativeHumidity

Maximum [relative humidity](#relativehumidity) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MaximumRelativeHumidity_Unit

Unit of [MaximumRelativeHumidity](#maximumrelativehumidity)

## MaximumSnowfallLine

Highest altitude above sea level, till which, within a given forcast time interval, precipitation can fall in form of rain. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MaximumSnowfallLine_Unit

Unit of [MaximumSnowfallLine](#maximumsnowfallline).

## MaximumTemperature

Maximum temperature 2 meters above ground within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MaximumTemperature_Unit

Unit of [MaximumTemperature](#maximumtemperature)

## MaximumWetBulbTemperature

Maximum [wet bulb temperature](#wetbulbtemperature) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MaximumWetBulbTemperature_Unit

Unit of [MaximumWetBulbTemperature](#maximumwetbulbtemperature)

## MinimumFeltTemperature

Minimum [felt temperature](#felttemperature) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MinimumFeltTemperature_Unit

Unit of [MinimumFeltTemperature](#minimumfelttemperature)

## MinimumRelativeHumidity

Minimum [relative humidity](#relativehumidity) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MinimumRelativeHumidity_Unit

Unit of [MinimumRelativeHumidity](#minimumrelativehumidity)

## MinimumSnowfallLine

Lowest altitude above sea level to which, within a given forcast time interval, precipitation is supposed to fall in form of snow. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MinimumSnowfallLine_Unit

Unit of [MinimumSnowfallLine](#minimumsnowfallline).

## MinimumTemperature

Minimum temperature 2 meters above ground within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MinimumTemperature_Unit

Unit of [MinimumTemperature](#minimumtemperature).

## MinimumWetBulbTemperature

Minimum [wet bulb temperature](#wetbulbtemperature) within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## MinimumWetBulbTemperature_Unit

Unit of [MinimumWetBulbTemperature](#minimumwetbulbtemperature)

## MoonRise

Time of moonrise at point of interest in local time zone (ISO 8601 date format).

## MoonSet

Time of moonset at point of interest in local time zone (ISO 8601 date format).

## MoonPhase

Moon phase at point of interest. Possible Values are:

| English         | German          |
| --------------- | --------------- |
| New Moon        | Neumond         |
| Waxing Crescent | Erstes Viertel  |
| Waxing Gibbous  | Zweites Viertel |
| Full Moon       | Vollmond        |
| Waning Gibbous  | Drittes Viertel |
| Waning Crescent | Viertes Viertel |

## PrecipitationProbability

Probability of precipitation greater than 0.2 mm/m² in the interval leading up to the corresponding forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationProbability_Unit

Unit of [PrecipitationProbability](#PrecipitationProbability)

## PrecipitationRain_3hourlySum

Forecast three-hour rain sum at the point of interest. The interval length of the summation is 3 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationRain_3hourlySum_Unit

Unit of [PrecipitationRain_3hourlySum](#PrecipitationRain_3hourlySum).

## PrecipitationRain_6hourlySum

Forecast six-hour rain sum at the point of interest. The interval length of the summation is 6 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationRain_6hourlySum_Unit

Unit of [PrecipitationRain_6hourlySum](#PrecipitationRain_6hourlySum).

## PrecipitationRain_dailySum

Forecast daily rain sum at the point of interest. The interval length of the summation is 24 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationRain_dailySum_Unit

Unit of [PrecipitationRain_dailySum](#PrecipitationRain_dailySum).

## PrecipitationRain_hourlySum

Forecast hourly rain sum at the point of interest. The interval length of the summation is one hour and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationRain_hourlySum_Unit

Unit of [PrecipitationRain_hourlySum](#PrecipitationRain_hourlySum).

## PrecipitationRain_Intensity

Intensity of rainfall at point of interest for a given time.

## PrecipitationRain_Intensity_Unit

Unit of [PrecipitationRain_Intensity](#PrecipitationRain_Intensity).

## PrecipitationSnow_3hourlySum

Forecast three-hour fresh snow amount at the point of interest. The interval length of the summation is 3 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationSnow_3hourlySum_Unit

Unit of [PrecipitationSnow_3hourlySum](#PrecipitationSnow_3hourlySum)

## PrecipitationSnow_6hourlySum

Forecast six-hour snow sum at the point of interest. The interval length of the summation is 6 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationSnow_6hourlySum_Unit

Unit of [PrecipitationSnow_6hourlySum](#PrecipitationSnow_6hourlySum).

## PrecipitationSnow_dailySum

Forecast daily fresh snow amount at the point of interest. The interval length of the summation is 24 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationSnow_dailySum_Unit

Unit of [PrecipitationSnow_dailySum](#PrecipitationSnow_dailySum)

## PrecipitationSnow_hourlySum

Forecast hourly fresh snow sum at the point of interest. The interval length of the summation is one hour and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationSnow_hourlySum_Unit

Unit of [PrecipitationSnow_hourlySum](#PrecipitationSnow_hourlySum).

## PrecipitationSnow_Intensity

Intensity of snowfall at point of interest for a given time.

## PrecipitationSnow_Intensity_Unit

Unit of [PrecipitationSnow_intensity](#precipitationsnow_intensity).

## PrecipitationTotal_3hourlySum

Forecast three-hour sum of total precipitation (rain and/or water equivalent of snow). The interval length of the summation is 3 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationTotal_3hourlySum_Unit

Unit of [PrecipitationTotal_3hourlySum](#PrecipitationTotal_3hourlySum.md).

## PrecipitationTotal_6hourlySum

Forecast six-hour total precipitation (rain and/or water equivalent of snow) sum at the point of interest. The interval length of the summaation is 6 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationTotal_6hourlySum_Unit

Unit of [PrecipitationTotal_6hourlySum](#PrecipitationTotal_6hourlySum).

## PrecipitationTotal_dailySum

Forecast daily total precipitation amount (rain and/or water equivalent of snow) at the point of interest. The interval length of the summation is 24 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationTotal_dailySum_Unit

Unit of [PrecipitationTotal_dailySum](#PrecipitationTotal_dailySum)

## PrecipitationTotal_hourlySum

Forecast hourly total precipitation (rain and/or water equivalent of snow) sum at the point of interest. The interval length of the summation is one hour and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## PrecipitationTotal_hourlySum_Unit

Unit of [PrecipitationTotal_hourlySum](#PrecipitationTotal_hourlySum).

## PrecipitationTotal_Intensity

Intensity of total precipitation (rain and/or water equivalent of snow) at the point of interest for a given time.

## PrecipitationTotal_Intensity_Unit

Unit of [PrecipitationTotal_Intensity](#PrecipitationTotal_Intensity).

## PrecipitationType

String expressing the kind of precipitation that is forecast. Possible values are `rain`, `snow` and `sleet`.

## RelativeHumidity

Relative humidity at point of interest, 2 meters above ground.

## RelativeHumidity_Unit

Unit of [RelativeHumidity](#relativehumidity)

## SnowfallLine

Altitude above mean sea level to which precipitation falls in form of snow.

## SnowfallLine_Unit

Unit of [SnowfallLine](#snowfallline)

## SunshineDuration

Duration of sunshine occurring at the point of interest during a given forecast time interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## SunshineDuration_Unit

Unit of [SunshineDuration](#sunshineduration).

## SunRise

Time of sunrise at point of interest in local time zone (ISO 8601 date format).

## SunSet

Time of sunset at point of interest in local time zone (ISO 8601 date format).

## Temperature

Air temperature at point of interest for a given time, 2 meters above ground.

## Temperature_Unit

Unit of [Temperature](#Temperature)

## TemperatureMaximum

Maximum air temperature within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## TemperatureMaximum_Unit

Unit of [TemperatureMaximum](#TemperatureMaximum).

## TemperatureMinimum

Minimum air temperature within a forecast interval. The forecast interval length is determined by the time resolution of the forecast, and the interval ends with the respective forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## TemperatureMinimum_Unit

Unit of [TemperatureMinimum](#TemperatureMinimum).

## ThunderstormProbability

General description of thunderstorm risk for the interval leading up to the corresponding forecast time at the point of interest. Possible values are `low`, `moderate`, `high` and `extreme`. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## ThunderstormProbabilities_usedValues

This Variable contains the values that [ThunderstormProbability](#thunderstormprobability) can possibly be.

## TotalCloudCover

Forecast of the total cloud cover at the point of interest.

## TotalCloudCover_Unit

Unit of [TotalCloudCover](#totalcloudcover)

## UpperCloudLimit

Forecast of the maximum height of the clouds at the point of interest.

## UpperCloudLimit_Unit

Unit of [UpperCloudLimit](#uppercloudlimit)

## WeatherDescription

Short verbal description of forecasted weather.

## WetBulbTemperature

Wet bulb temperature at point of interest for a given time, 2 meters above ground. The wet bulb temperature is the temperature of adiabatic saturation. This is the temperature indicated by a moistened thermometer bulb exposed to the air flow.

## WetBulbTemperature_Unit

Unit of [WetBulbTemperature](#wetbulbtemperature).

## WindDirection

Main direction the wind blows from, e.g. north wind blows from the north. The wind direction is taken from an eight part compass rose. Possible values are `N`, `NE`, `E`, `SE`, `S`, `SW`, `W` and `NW`. In the occurrence of calm conditions and/or circulating wind, the value `XX` is used.

## WindDirection_usedValues

This Variable contains the values that [WindDirection](#winddirection) can possibly be.

## WindSpeed

Ten-minute average of wind speed 10 meters above ground. Attention: gusts may reach more than twice that speed.

## WindSpeed_Unit

Unit of [WindSpeed](#windspeed_unit).

## WindStrength

Verbal description of occurring wind speed, based on the internationally renowned Beaufort scale. Values: `low`, `moderate`, `high` and `extreme`.

## WindString_usedValues

This variable contains the values that [WindStrength](#windstrength) can possibly bear.

## ZeroDegreeIsothermHeight

Forecast of the height above sea level at which the 0°C isotherm will be at the point of interest.

## ZeroDegreeIsothermHeight_Unit

Unit of [ZeroDegreeIsothermHeight](#zerodegreeisothermheight)
