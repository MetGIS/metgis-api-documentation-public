# MetGIS Weather Warnings GeoJSON Info

MetGIS compiles and edits all weather warnings issued by 38 European National Meteorological and Hydrological Services (NMHSs) in a continuous process, using the MeteoAlarm website to retrieve the basic warning information. The results are collected and can be downloaded from the MetGIS API. Information about obtaining access rights to it can be found [here](https://weatherapi.metgis.com/).

## Obtaining the Data 

The JSON data can be downloaded from the MetGIS API by requesting it via https:
```
https://data.metgis.com/weather-warnings/?key={your-key}&country={3-letter-country-code}
```
The list of countries that are available, and their code can be viewed in the [last section](#available-countries) of this document. It is possible to request warnings for a list countries by separating the codes with the pipe symbol. The following example request shows how to download all warnings for Austria and Belgium:
```
https://data.metgis.com/weather-warnings/?key={your-key}&country=AUT|BEL
```
If you want to obtain warnings for all countries in europe set the URL parameter country to 'europe' instead of using an extended list of country codes. 

The interfaces to the national weather services providing the original warning messages are checked at least once per 5 minutes, therefore the data is always up-to-date. It will contain warnings for weather events that could be severe or harmful, but it will not contain warnings for small scale features related to larger scale weather patterns. An example: If the weather conditions are favorable for thunderstorms, a warning will be issued for the area in which they are expected, a couple of hours in advance. But there will be no short term warnings regarding individual thunderstorms. 

## Structure and Contents of the Weather Warnings

The data is provided in JSON format, with a GeoJSON conform object for each country that is included in the file.
The structure for a response that contains warnings for Slovakia and Slovenia would look like this:
```
{
  "SVK": {
    "type": "FeatureCollection",
    "features": [
      [
        {
          "type": "Feature",
          "geometry": {
            "coordinates": [
              [
                [
                  22.167207464797563,
                  48.57777005582136
                ],
                ...
              ]
            ]
        }
    },
  "SVN": {
    "type": "FeatureCollection",
    "features": [
      [
        {
          "type": "Feature",
          "geometry": {
            "coordinates": [
              [
                [
                  14.566,
                  46.373
                ],
                ...
              ]
            ]
        }
    }
}
```
         

The objects provided for each country are regular [GeoJSON](https://geojson.org/) objects that follow the conventions and specifications of standard [RFC 7946](https://datatracker.ietf.org/doc/html/rfc7946). Therefore they can easily be used for further processing with software packages focusing on geographic tasks, e. g. WMS tile server and GIS systems.

### Awareness Levels
- Yellow (Moderate): The weather is potentially dangerous. The weather phenomena that have been forecast are not unusual, but be attentive if you intend to practice activities exposed to meteorological risks. Keep informed about the expected meteorological conditions and do not take any avoidable risks.

- Orange (Severe): The weather is dangerous. Unusual meteorological phenomena have been forecast. Damage and casualties are likely to happen. Be very vigilant and keep regularly informed about the detailed expected meteorological conditions. Be aware of the risks that might be unavoidable. Follow any advice given by your authorities.

- Red (Extreme): The weather is very dangerous. Exceptionally intense meteorological phenomena have been forecast. Major damage and accidents are likely, in many cases with a threat to life and limb, over a wide area. Keep frequently informed about detailed expected meteorological conditions and risks. Follow orders and any advice given by your authorities under all circumstances. Be prepared for extraordinary measures.


### Awareness Types

Most of the warnings issued are linked to one or more of the following awareness types:
- wind
- snow/ice
- thunderstorm
- fog
- high temperature
- low temperature
- coastal event
- forest fire
- avalanches
- rain
- flooding
- rain/flood

There may also be warnings that are not directly linked to any of the awareness types listed above, e. g volcanic activity. The weather phenomena warned about may vary slightly from country to country. Each weather warning refers o an area precisely defined by the issuing weather service.

### Metadata included in the file

The weather warnings geojson file contains a section called metadata, where additional information regarding the information is given. This section also includes the field "last_update" which refers to the last time at which the geojson file was created.




Since the MetGIS Weather Warnings GeoJSON file is based on the MeteoAlarm Website, companies using this GeoJSON must also follow the Terms and Conditions of Meteoalarm.
Here is an excerpt of the most important items:
- The (awareness) information being redistributed must not be modified in any way.
- The source of the Information must always be displayed as "EUMETNET – MeteoAlarm".
- For all Information being redistributed through internet applications, a link must be provided to the following URL: www.meteoalarm.org.
- The time of issue of the Information being redistributed, … must be included in any redistribution.
- Any operational redistribution of Information must always be made available to users in real-time, with the delay between the publication on the MeteoAlarm Website and the redistributor's website being on average less than 5 minutes and never longer than 10 minutes.
- All redistributors must publish the following disclaimer: "Time delays between this website and the www.meteoalarm.org website are possible. For the most up-to-date awareness information as published by the participating National Meteorological and Hydrological Services, please refer to www.meteoalarm.org."


## Available Countries

The countries for which warnings can be downloaded are shown in the table below.

| Country | Code |
| ------ | ----|  
| Albania | ALB |
| Andorra | AND |
| Armenia | ARM |
| Austria | AUT |
| Belarus | BLR |
| Belgium | BEL |
| Bosnia and Herzegovina | BIH |
| Bulgaria | BGR |
| Croatia | HRV |
| Cyprus | CYP |
| Czech Republic | CZE |
| Denmark | DNK |
| Estonia | EST |
| Faroe Islands | FRO |
| Finland | FIN |
| France | FRA |
| Georgia | GEO |
| Germany | DEU |
| Gibraltar | GIB |
| Greece | GRC |
| Hungary | HUN |
| Iceland | ISL |
| Ireland | IRL |
| Isle of Man | IMN |
| Israel | ISR |
| Italy | ITA |
| Kosovo | XKX |
| Latvia | LVA |
| Liechtenstein | LIE |
| Lithuania | LTU |
| Luxembourg | LUX |
| Macedonia | MKD |
| Malta | MLT |
| Moldova | MDA |
| Monaco | MCO |
| Montenegro | MNE |
| Netherlands | NLD |
| Norway | NOR |
| Poland | POL |
| Portugal | PRT |
| Romania | ROU |
| Russian Federation | RUS |
| San Marino | SMR |
| Serbia | SRB |
| Slovakia | SVK |
| Slovenia | SVN |
| Spain | ESP |
| Sweden | SWE |
| Switzerland | CHE |
| Turkey | TUR |
| Ukraine | UKR |
| United Kingdom | GBR |
| Vatican City State | VAT |