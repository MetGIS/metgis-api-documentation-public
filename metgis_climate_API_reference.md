# MetGIS CLIMATE API

The MetGIS CLIMATE API is an application programming interface that can be used to access climate data in JSON format. It follows REST API constraints. This document provides a detailed description of its usage. Information about obtaining access rights can be found [here](https://weatherapi.metgis.com/histapi), or [contact us](https://metgis.com/en/contact-us/).

The historical data used to calculate climate indices is reconstructed on the basis of global model analyses (includes data from weather stations, ground radar, satellites, weather balloons, weather buoys, measured values from aircraft, etc.), global weather simulation models and the MetGIS downscaling algorithm, applied on a 0.1 degree grid over land and 0.25 degree grid over the sea. This data is enriched with a network of additional, certified stations for even more reliable results.

The data is available for a specific month or day of a month. Data is available from 1985 through the end of the previous month. It is updated approximately one week after the end of each month and undergoes rigorous quality testing to ensure a consistently high-quality product. If you need data from before 1985 please [contact us](https://metgis.com/en/contact-us/).

## Quick Start

The API can be accessed via HTTP using a URL. To request climate data for a specific month use the following form:

```
https://api.climate.metgis.com/forecast?lon={longitude}&lat={latitude}&start_date={timestamp_startdate}&end_date={timestamp_enddate}&month={month}&v=hiclimmonth&key={your-key}
```
To request climate data for a specific day use the following form:

```
https://api.climate.metgis.com/forecast?lon={longitude}&lat={latitude}&start_date={timestamp_startdate}&end_date={timestamp_enddate}&month={month}&day={day}&v=hiclimday&key={your-key}
```

The parameters that have to be set are in curly brackets and listed in the following table:

| Parameter |                             Description                             | Comments                                                                                                                                                                                                                                                                                                   |
| --------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key       |                Key needed to access MetGIS CLIMATE API                 | Paying customers have received their API Key after ordering. Sometimes keys for testing may be available. Mandatory parameter.                                                                                                                                                                             |
| lat       | Latitude of point the weather data is requested for in degrees °  | Latitude of points south of the equator is negative, use point (.) as decimal separator. Mandatory parameter.                                                                                 |
| lon       | Longitude of point the weather data is requested for in degrees ° | Longitude west of 0° meridian can be given as negative values or in the range from 180° to 360°, use point (.) as decimal separator. Mandatory parameter.                                      |
| v         |               Name of requested weather data package                | Key must have access rights to requested package. For available package versions check the table in section [package versions](#package-versions). Mandatory parameter.                                                                                                                                    |
| start_date      |    The start date for which the meteorological data is requested     | The timestamp is given in the format `YYYYMMDD`, e. g. `20160302` for data for the 2nd of March 2016. Mandatory parameter. |
| end_date      |    The end date for which the meteorological data is requested     | The timestamp is given in the format `YYYYMMDD`, e. g. `20160302` for data for the 2nd of March 2016. Mandatory parameter. |
| month      |    The month for which the meteorological data is requested, or the month containing the requested day     | The timestamp is given in the format `MM`, e. g. `03` for data for March. Mandatory parameter. |
| day      |    The day for which the meteorological data is requested   | The timestamp is given in the format `DD`, e. g. `02` for data for the 2nd of your chosen month. Mandatory parameter for package `hiclimday`. |

A valid request will be responded with a file in JSON format that contains the specified historical weather data. The files are mostly self-explanatory, but a detailed description of the available packages is given in the section ["Package versions"](#package-versions).

Data access limits: #TODO!

## Weather Parameters

The MetGIS CLIMATE API provides access to the following weather parameters:

| Weather Parameter | Unit            | Details                                                                                                                                                                                                        |
| ----------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mean Temperature       | °C              | Mean air temperature two meters above the ground for the requested day/month during the specified timeframe        |
| Absolute Minimum Temperature       | °C              | Minimum air temperature two meters above the ground for the requested day/month during the specified timeframe         |
| Mean Minimum Temperature       | °C              | Mean daily minimum air temperature two meters above the ground for the requested day/month during the specified timeframe         |
| Absolute Maximum Temperature       | °C              | Maximum air temperature two meters above the ground for the requested day/month during the specified timeframe        |
| Mean Maximum Temperature       | °C              | Mean daily maximum air temperature two meters above the ground for the requested day/month during the specified timeframe        |
| Mean Relative Humidity | %               | Mean relative humidity of the air two meters above the ground for the requested day/month during the specified timeframe                                                                                                                                                       |
| Mean Precipitation     | mm              | Mean amount of accumulated rainfall and/or snow for the requested day/month during the specified timeframe. In the case of snow, the liquid water equivalent is used (resulting water if fallen snow would have been melted).                                                  |
| Mean Fresh Snow        | cm              | Mean amount of accumulated fresh snow for the requested day/month during the specified timeframe    |
| Rainy Day Probability   | %            | Probability of rain above 0.2mm/1mm/5mm for the requested day/month during the specified timeframe    |
| Snowy Day Probability   | %            | Probability of snow above 0.2mm/1mm/5mm for the requested day/month during the specified timeframe. For the amount of snow, the liquid water equivalent is used (resulting water if fallen snow would have been melted)    |
| Sunny Day Probability   | %            | Probability of cloud cover under 20% for the requested day/month during the specified timeframe    |

## Package Versions

| Package Version |                                                                                                                                           Description                                                                                                                                            |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hiclimday        | Climate statistics for one day of a specified month  |
| hiclimmonth      | Climate statistics for one whole month  |


A correct API request to retrieve the data package `hiclimday` for the first to the third of April for specific coordinates would look like this:

```
https://api.climate.metgis.com/forecast?lat=48.0&lon=16.2&start_date=19860101&end_date=20251231&month=4&day=03&v=hiclimday&key={key}
```

And it would yield a JSON file like this:

```

{
    "Climate_statistics": {
        "AbsoluteMaximumTemperature": 22.0,
        "AbsoluteMaximumTemperature_unit": "°C",
        "AbsoluteMinimumTemperature": -0.9,
        "AbsoluteMinimumTemperature_unit": "°C",
        "MeanFreshSnow_SWE": 0.5,
        "MeanFreshSnow_SWE_unit": "mm",
        "MeanMaximumTemperature": 13.8,
        "MeanMaximumTemperature_unit": "°C",
        "MeanMinimumTemperature": 3.9,
        "MeanMinimumTemperature_unit": "°C",
        "MeanPrecipitation": 0.9,
        "MeanPrecipitation_unit": "mm",
        "MeanRelativeHumidity": 64,
        "MeanRelativeHumidity_unit": "%",
        "MeanTemperature": 8.9,
        "MeanTemperature_unit": "°C",
        "RainyDayProbability_0.2mm": 35,
        "RainyDayProbability_0.2mm_unit": "%",
        "RainyDayProbability_1mm": 15,
        "RainyDayProbability_1mm_unit": "%",
        "RainyDayProbability_5mm": 0,
        "RainyDayProbability_5mm_unit": "%",
        "SnowyDayProbability_0.2mm_SWE": 15,
        "SnowyDayProbability_0.2mm_SWE_unit": "%",
        "SnowyDayProbability_1mm_SWE": 5,
        "SnowyDayProbability_1mm_SWE_unit": "%",
        "SnowyDayProbability_5mm_SWE": 5,
        "SnowyDayProbability_5mm_SWE_unit": "%",
        "SunnyDayProbability": 13,
        "SunnyDayProbability_unit": "%"
    },
    "Info": {
        "Altitude_[m]": 325.0,
        "Description": "Package "hiclimday"",
        "Latitude": 48.0,
        "Longitude": 16.2,
        "Start_date": "1986-01-01",
        "End_date": "2025-12-31",
        "Statistical_day": 3.0,
        "Statistical_month": 4.0
    }
}
```

A correct API request to retrieve the data package `hiclimmonth` for the month of June for specific coordinates would look like this:

```
https://api.climate.metgis.com/forecast?lat=48.0&lon=16.2&start_date=19860101&end_date=20251231&month=6&v=hiclimmonth&key={key}
```

This request would yield the following JSON file:

```
{
    "Climate_statistics": {
        "AbsoluteMaximumTemperature": 34.2,
        "AbsoluteMaximumTemperature_unit": "°C",
        "AbsoluteMinimumTemperature": 2.9,
        "AbsoluteMinimumTemperature_unit": "°C",
        "MeanFreshSnow_SWE": 0.0,
        "MeanFreshSnow_SWE_unit": "mm",
        "MeanMaximumTemperature": 22.7,
        "MeanMaximumTemperature_unit": "°C",
        "MeanMinimumTemperature": 13.3,
        "MeanMinimumTemperature_unit": "°C",
        "MeanPrecipitation": 97.3,
        "MeanPrecipitation_unit": "mm",
        "MeanRelativeHumidity": 69,
        "MeanRelativeHumidity_unit": "%",
        "MeanTemperature": 18.1,
        "MeanTemperature_unit": "°C",
        "RainyDayProbability_0.2mm": 69,
        "RainyDayProbability_0.2mm_unit": "%",
        "RainyDayProbability_1mm": 48,
        "RainyDayProbability_1mm_unit": "%",
        "RainyDayProbability_5mm": 21,
        "RainyDayProbability_5mm_unit": "%",
        "SnowyDayProbability_0.2mm_SWE": 0,
        "SnowyDayProbability_0.2mm_SWE_unit": "%",
        "SnowyDayProbability_1mm_SWE": 0,
        "SnowyDayProbability_1mm_SWE_unit": "%",
        "SnowyDayProbability_5mm_SWE": 0,
        "SnowyDayProbability_5mm_SWE_unit": "%",
        "SunnyDayProbability": 10,
        "SunnyDayProbability_unit": "%"
    },
    "Info": {
        "Altitude_[m]": 325.0,
        "Description": "Package "hiclimmonth"",
        "Latitude": 48.0,
        "Longitude": 16.2,
        "Start_date": "1986-01-01",
        "End_date": "2025-12-31",
        "Statistical_month": 6.0
    }
}
```

## Climate Trends

Trend analysis and forecasting based on the historical climate data are available upon request. Please [contact us](https://metgis.com/en/contact-us/) to discuss your requirements.

## Common Errors

The API responds with specific messages for certain errors. They are presented here:

- `Please check request parameters`: One of the query parameters could not be parsed. Check the format of `lat`, `lon`, `start_date`, `end_date`, `month`, `day`, and `v`.
- `Please check key or allowed service version`: There is either a typo in the key, or the key does not have permission to retrieve the requested package.
- `Too many results! Please limit search radius or time parameters`: Your query is trying to retrieve too much data at once. Please divide the request in smaller temporal chunks.
