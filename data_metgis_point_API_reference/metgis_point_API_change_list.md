# Transition guide from the old Point API to the new one

- The new Point API endpoint is `https://point-api.metgis.com/forecast` instead of `https://api.metgis.com/forecast`.
- Your existing API key is valid for the new Point API, too.
- The `winter` package was renamed to `coldweather`.

## `starter` package
- The momentary wind values in `Forecast_daily` were replaced by aggregated or derived values:
  - `WindDirection` -> `WindDirectionAtMaxSpeed`
  - `WindStrength` -> `MaximumWindStrength`
- Changes in the names only:
    - `TemperatureMaximum` -> `MaximumTemperature`
    - `TemperatureMinimum` -> `MinimumTemperature`
    - `WindSpeedMaximum` -> `MaximumWindSpeed`
    - `WeatherDescription` -> `ShortText`
- `WindDirection` and `WindDirectionAtMaxSpeed` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.

## `smart` package
- The momentary wind values in `Forecast_daily` were replaced by aggregated or derived values:
  - `WindDirection` -> `WindDirectionAtMaxSpeed`
  - `WindStrength` -> `MaximumWindStrength`
- Changes in the names only:
    - `SunRise`, `SunSet`, `MoonRise`, and `Moonset` were renamed to `Sunrise`, `Sunset`, `Moonrise`, and `Moonset` respectively.
    - SunshineDuration was renamed to represent the aggregation period, for example `SunshineDuration_dailySum`
        or `SunshineDuration_6hourlySum`.
    - `TemperatureMaximum` -> `MaximumTemperature`
    - `TemperatureMinimum` -> `MinimumTemperature`
    - `WindSpeedMaximum` -> `MaximumWindSpeed`
    - `TotalCloudCoverMinimum` -> `MinimumTotalCloudCover`
    - `TotalCloudCoverMean` -> `MeanTotalCloudCover`
    - `TotalCloudCoverMaximum` -> `MaximumTotalCloudCover`
    - `WeatherDescription` -> `ShortText`
- `WindDirection`, `WindStrength`, `MoonPhase` and `WindDirectionAtMaxSpeed` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.
- The special values of `Moonrise`, `Moonset`, `Sunrise` and `Sunset` (e.g. "does not rise" or "does not set", relevant for arctic regions) are now translated as well; see `<ParameterName>_usedValues` in the JSON response for the possible values.

## `premium` package
- The momentary wind values in `Forecast_daily` were replaced by aggregated or derived values:
  - `WindDirection` -> `WindDirectionAtMaxSpeed`
  - `WindStrength` -> `MaximumWindStrength`
- `MaximumWindGust` was added to `Forecast_daily`.
- Changes in the names only:
    - `SunRise`, `SunSet`, `MoonRise`, and `Moonset` were renamed to `Sunrise`, `Sunset`, `Moonrise`, and `Moonset` respectively.
    - SunshineDuration was renamed to represent the aggregation period, for example `SunshineDuration_dailySum`
        or `SunshineDuration_6hourlySum`.
    - `TemperatureMaximum` -> `MaximumTemperature`
    - `TemperatureMinimum` -> `MinimumTemperature`
    - `FeltTemperatureMinimum` -> `MinimumFeltTemperature`
    - `FeltTemperatureMaximum` -> `MaximumFeltTemperature`
    - `RelativeHumidityMean` -> `MeanRelativeHumidity`
    - `WindSpeedMaximum` -> `MaximumWindSpeed`
    - `TotalCloudCoverMinimum` -> `MinimumTotalCloudCover`
    - `TotalCloudCoverMean` -> `MeanTotalCloudCover`
    - `TotalCloudCoverMaximum` -> `MaximumTotalCloudCover`
    - `WeatherDescription` -> `ShortText`
    - `TextForecast` -> `LongText`
- `WindDirection`, `WindStrength`, `MoonPhase` and `WindDirectionAtMaxSpeed` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.
- The special values of `Moonrise`, `Moonset`, `Sunrise` and `Sunset` (e.g. "does not rise" or "does not set", relevant for arctic regions) are now translated as well; see `<ParameterName>_usedValues` in the JSON response for the possible values.

## `coldweather` package - renamed from `winter` package (!)
- The momentary wind values in `Forecast_daily` were replaced by aggregated or derived values:
  - `WindDirection` -> `WindDirectionAtMaxSpeed`
  - `WindStrength` -> `MaximumWindStrength`
- `MaximumWindGust` was added to `Forecast_daily`.
- Changes in the names only:
    - `SunRise`, `SunSet`, `MoonRise`, and `Moonset` were renamed to `Sunrise`, `Sunset`, `Moonrise`, and `Moonset` respectively.
    - SunshineDuration was renamed to represent the aggregation period, for example `SunshineDuration_dailySum`
        or `SunshineDuration_6hourlySum`.
    - `TemperatureMaximum` -> `MaximumTemperature`
    - `TemperatureMinimum` -> `MinimumTemperature`
    - `FeltTemperatureMinimum` -> `MinimumFeltTemperature`
    - `FeltTemperatureMaximum` -> `MaximumFeltTemperature`
    - `RelativeHumidityMean` -> `MeanRelativeHumidity`
    - `WindSpeedMaximum` -> `MaximumWindSpeed`
    - `WeatherDescription` -> `ShortText`
    - `TextForecast` -> `LongText`
- New variables in `Forecast_daily` block:
    - `TextForecast`
    - `MaximumWetBulbTemperature`
    - `MinimumWetBulbTemperature`
    - `MinimumTotalCloudCover`
    - `MeanTotalCloudCover`
    - `MaximumTotalCloudCover`
- New variables in `Forecast_hourly` block:
    - `DownwardShortWaveRadiation`
    - `DewPointTemperature`
- `WindDirection`, `WindStrength`, `MoonPhase` and `WindDirectionAtMaxSpeed` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.
- The special values of `Moonrise`, `Moonset`, `Sunrise` and `Sunset` (e.g. "does not rise" or "does not set", relevant for arctic regions) are now translated as well; see `<ParameterName>_usedValues` in the JSON response for the possible values.

## `a2` package
- Typo correction in `Current` block: `TotoalCloudCover` -> `TotalCloudCover`
- The momentary wind values in `Forecast_daily` were replaced by aggregated or derived values:
  - `WindDirection` -> `WindDirectionAtMaxSpeed`
  - `WindStrength` -> `MaximumWindStrength`
- `MaximumWindGust` was added to `Forecast_daily`.
- Changes in the names only:
    - `SunRise`, `SunSet`, `MoonRise`, and `Moonset` were renamed to `Sunrise`, `Sunset`, `Moonrise`, and `Moonset` respectively.
    - SunshineDuration was renamed to represent the aggregation period, for example `SunshineDuration_dailySum`
        or `SunshineDuration_6hourlySum`.
    - `TemperatureMaximum` -> `MaximumTemperature`
    - `TemperatureMinimum` -> `MinimumTemperature`
    - `FeltTemperatureMinimum` -> `MinimumFeltTemperature`
    - `FeltTemperatureMaximum` -> `MaximumFeltTemperature`
    - `RelativeHumidityMean` -> `MeanRelativeHumidity`
    - `WindSpeedMaximum` -> `MaximumWindSpeed`
    - `WeatherDescription` -> `ShortText`

## `solar24` package
- Forecast block name changed: `Forecast_24h_hourly` -> `Forecast_hourly`

## `solarD9` package
- Forecast block name changed: `Forecast_3_hourly` -> `Forecast_3hourly`
- `Forecast_3hourly` now contains data from the current time on, for the next 9 days. 

## `stdaily` package
- Forecast block name changed: `forecast` -> `Forecast_daily`
- `ForecastDate` -> `ForecastTimes_LocalTime`
- `SurfaceTemperature` was changed to `MeanSeaSurfaceTemperature`.
  *It is only available on water and near shorelines.*

## `current` package
- Changes in the names only:
    - `SunRise`, `SunSet`, `MoonRise`, and `Moonset` were renamed to `Sunrise`, `Sunset`, `Moonrise`, and `Moonset` respectively.
    - `WeatherDescription` -> `ShortText`
- `WindDirection`, `WindStrength` and `MoonPhase` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.
- The special values of `Moonrise`, `Moonset`, `Sunrise` and `Sunset` (e.g. "does not rise" or "does not set", relevant for arctic regions) are now translated as well; see `<ParameterName>_usedValues` in the JSON response for the possible values.

## `fctisl` package
- `forecasts` block was renamed to `Forecast`.
- Location and time information were moved to `Info`, and the variable names were changed:
  - `lat` -> `Latitude`
  - `lon` -> `Longitude`
  - `alt` -> `Altitude_[m]`
  - `date` -> `Forecast_Calculated_UTC` and `Forecast_Calculated_LocalTime`
- `WindStrength` was added.
- `WindDirection`, `WindStrength` and `MoonPhase` are now translated into the language given by the `lang` parameter, or German by default; see `<ParameterName>_usedValues` in the JSON response for the possible values.
- The special values of `Moonrise`, `Moonset`, `Sunrise` and `Sunset` (e.g. "does not rise" or "does not set", relevant for arctic regions) are now translated as well; see `<ParameterName>_usedValues` in the JSON response for the possible values.

