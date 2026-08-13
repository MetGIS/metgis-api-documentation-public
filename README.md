# User Manuals to MetGIS Weather APIs

The documents in this git repository describe how to use the various MetGIS APIs that allow to retrieve different types of weather data. 
The following APIs are documented:

## MetGIS Point API
This API can be used to fetch weather forecasts and information about the current weather in JSON format.

**Important note: from August 2026, a new version of the Point API is available. The old version is expected to be shut down soon, according to agreement with our existing users.**

- [New Point API documentation](metgis_point_API_reference.md)
- [Transition guide from the old Point API to the new one](data_metgis_point_API_reference/metgis_point_API_change_list.md)
- [Old Point API documentation](metgis_point_API_reference_old.md)

## MetGIS Maps API

High-resolution weather forecast and snow cover layers for easy integration. See the [documentation](metgis_maps_API_reference.md).

## MetGIS Regional HIST API

Weather data for Central Europe from the past in hourly resolution on a 1km grid, perfectly suitable for AI training. See the [documentation](metgis_hist_API_reference.md). 

## MetGIS Global HIST API

Weather data from all over the planet in hourly resolution. The data is interpolated "on the fly" to the target coordinates using global reanalysis model data as input for the MetGIS downscaling algorithm. See the [documentation](metgis_global_hist_API_reference.md).

## MetGIS Climate API 

API to request climate data from any place on the planet. The data is calculated "on the fly" for the target coordinates using global reanalysis model data as input. [See the documentation](metgis_climate_API_reference.md)

## MetGIS Long Range API

Weather trends and probabilities for the next 7 months. See the [documentation](metgis_long_range_point_API_reference.md). 

## MetGIS Weather Warnings

Easy access to all official weather warnings for Europe. See the [documentation](metgis_weather_warnings_API_reference.md). 


