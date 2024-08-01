# MetGIS Maps API
The MetGis Topo-API offers tiled-topographic data as pngs.

To access the data you need an API-KEY with access to the topo data.
With an valid API-KEY you can access the data via:

```
https://topo-api.metgis.com/{datapath}/{z}/{x}/{y}.png?apikey={key}
```
 
| Tileset  	|  datapath 	
|---	|---	
| background  	| /background  
|  overlay 	| /overlay  	
|  dem 	|  /dem 
|  worlddem 	|  /worlddem/tiles/

A valid request for example would look like that.
```
https://topo-api.metgis.com/overlay/8/139/89.png?apikey=rkkmEckq34cfk2FCkaadfr3
```

## Tileset description

### Background

Background map tiles with geographic information like lakes and mountains (hillshaded).

### Overlay

Overlay map tiles with geographic information like streets, places, and points of interest.

### Dem

RGB encoded elevation data (as png) to display 3D elevation in serveral map libaries such as maplibre-gl.
This set covers Europe wherby the area of Austria has a reultion up to 5m.

### Worlddem

RGB encoded elevation data (as png) to display 3D elevation in serveral map libaries such as maplibre-gl.
This set covers the whole world with a resulution up to 30m.
