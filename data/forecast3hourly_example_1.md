# Forecast Intervals and Parameters

Forecast parameters can either be valid at a certain forecast time, or for the time interval before the forecast time. This example tries to clarify what summation, averaging, minimum and maximum means for parameters that are forecast for a period of time.

Here is an example of the object `Forecast_3Hourly`:

<details>
<summary>Example JSON</summary>
```json
{
    "ForecastTimes_LocalTime": [
        "2021-04-07T18:00+02:00",
        "2021-04-07T21:00+02:00",
        "2021-04-08T00:00+02:00",
        "2021-04-08T03:00+02:00",
        "2021-04-08T06:00+02:00",
        "2021-04-08T09:00+02:00",
        "2021-04-08T12:00+02:00",
        "2021-04-08T15:00+02:00",
        "2021-04-08T18:00+02:00",
        "2021-04-08T21:00+02:00",
        "2021-04-09T00:00+02:00",
        "2021-04-09T03:00+02:00",
        "2021-04-09T06:00+02:00",
        "2021-04-09T09:00+02:00",
        "2021-04-09T12:00+02:00",
        "2021-04-09T15:00+02:00",
        "2021-04-09T18:00+02:00",
        "2021-04-09T21:00+02:00",
        "2021-04-10T00:00+02:00",
        "2021-04-10T03:00+02:00",
        "2021-04-10T06:00+02:00",
        "2021-04-10T09:00+02:00",
        "2021-04-10T12:00+02:00",
        "2021-04-10T15:00+02:00",
        "2021-04-10T18:00+02:00",
        "2021-04-10T21:00+02:00",
        "2021-04-11T00:00+02:00",
        "2021-04-11T03:00+02:00",
        "2021-04-11T06:00+02:00",
        "2021-04-11T09:00+02:00",
        "2021-04-11T12:00+02:00",
        "2021-04-11T15:00+02:00"
    ],
    "Temperature": [
        6,
        2,
        1.5,
        1.3,
        0.8,
        5.6,
        8.9,
        10.1,
        8.8,
        3.1,
        2.4,
        1.9,
        2.3,
        6.1,
        8.4,
        9.8,
        7.8,
        6.1,
        5.8,
        7,
        6.7,
        8.6,
        11.8,
        8.5,
        7.3,
        7.1,
        7.3,
        7.5,
        7.8,
        8.2,
        9.3,
        9.5
    ],
    "PrecipitationTotal_3hourlySum": [
        0.4,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0.1,
        0.1,
        0.1,
        0,
        0,
        0,
        0,
        0.1,
        1.1,
        2.8,
        1,
        0.7,
        0.4,
        0.5,
        1.9,
        1.8,
        0.8
    ]
}
```

</details>

For convenience the following table shows a selection of those values in readable format:

| Array Element Index | ForecastTime_LocalTime | Temperature | PrecipitationTotal_3hourlySum |
| :-----------------: | :--------------------: | :---------: | :---------------------------: |
|         22          | 2021-04-10T09:00+02:00 |     8.6     |               0               |
|         23          | 2021-04-10T12:00+02:00 |    11.8     |              0.1              |
|         24          | 2021-04-10T15:00+02:00 |     8.5     |              1.1              |
|         25          | 2021-04-10T18:00+02:00 |     7.3     |              2.8              |
|         26          | 2021-04-10T21:00+02:00 |     7.1     |               1               |
|         27          | 2021-04-11T00:00+02:00 |     7.3     |              0.7              |

The temperatures in this array are valid for the time specified in the same row in the column `ForecastTimes_LocalTime`. For example: At midnight on the 11th of April 2021 the forecast temperature is 7.3°C.

For summarized or averaged parameters, like precipitation, the situation is a little bit different. The values correspondent to a certain forecast time are valid for the interval leading up to this time. The length of the interval is determined by the temporal resolution of the forecast. In this example it is 3 hours, so the value 2.8 with array element index 25 means that between 3pm and 6pm on the 10th of April 2021 a precipitation amount of 2.8 mm/m² is forecast. So the forecast times of every interval are their respective end points.

This is true for all parameters that are either summarized (precipitation, fresh snow amount,...), averaged (solar radiation) or otherwise linked to an interval (precipitation probability).
