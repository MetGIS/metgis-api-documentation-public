# List of Variables and Fields Used by the MetGIS long-range Point API

The forecast interval of the variables is determined by [ForecastDates_Utc](#ForecastDates_Utc).

The naming of the fields that contain the physical unit of a given variable follows the `<variable-name>_Unit` pattern.

## ForecastDates_Utc
In the monthly forecast, the date represents the time interval of the entire month, e. g. 2023-08-01 represents Aug 2023.

In the daily forecast, the date represents the time interval from 0 to 24 hours UTC on that day.

## TemperatureMin
Minimum air temperature 2 meters above ground, in the given time interval, for one specific ensemble run considered in the CFS downscaling process.

## Temperature5thPercentile
5th percentile of the air temperature 2 meters above ground at the specified time, derived from all ensamble runs considered in the CFS downscaling process.

## Temperature25thPercentile
25th percentile of the air temperature 2 meters above ground at the specified time, derived from all ensamble runs considered in the CFS downscaling process.

## TemperatureMean
Mean air temperature 2 meters above ground, in the given time interval, for one specific ensemble run considered in the CFS downscaling process.

## Temperature75thPercentile
75th percentile of the air temperature 2 meters above ground at the specified time, derived from all ensamble runs considered in the CFS downscaling process.

## Temperature95thPercentile
95th percentile of the air temperature 2 meters above ground at the specified time, derived from all ensamble runs considered in the CFS downscaling process.

## TemperatureMax
Maximum air temperature 2 meters above ground, in the given time interval, for one specific ensemble run considered in the CFS downscaling process.

## TemperatureMeanAnomaly
Departure of the air temperature 2 meters above ground from the 30-year average, in the given time interval.

## PrecipitationRate5thPercentile
5th percentile of the precipitation rate at ground surface in the respective interval, derived from all ensamble runs considered in the CFS downscaling process.

## PrecipitationRate25thPercentile
25th percentile of the precipitation rate at ground surface in the respective interval, derived from all ensamble runs considered in the CFS downscaling process.

## PrecipitationRateMean
Mean precipitation rate, in the given time interval, for one specific ensemble run considered in the CFS downscaling process.

## PrecipitationRate75thPercentile
75th percentile of the precipitation rate at ground surface in the respective interval, derived from all ensamble runs considered in the CFS downscaling process.

## PrecipitationRate95thPercentile
95th percentile of the precipitation rate at ground surface in the respective interval, derived from all ensamble runs considered in the CFS downscaling process.

## PrecipitationRateMeanAnomaly
Departure of the precipitation rate from the 30-year average, in the given time interval.

## PrecipitationTotal_dailySum
Forecast daily total precipitation amount (rain and/or water equivalent of snow) at the point of interest. The interval length of the summation is 24 hours and ends with the correspondent forecast time. Go [here](forecast3hourly_example_1.md) for an explicit example of forecast times and parameters for intervals.

## DownwardShortWaveRadiation
Mean downward short wave radiation, in the given time interval, for one specific ensemble run considered in the CFS downscaling process.

