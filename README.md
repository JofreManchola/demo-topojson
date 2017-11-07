## TopoJSON y GeoJSON en d3.js

El objetivo de esta demostración es mostrar algunas fuentes de datos geográficos, su descarga en shapefile, la conversión a GeoJSON y TopoJSON y finalmente su uso en una visualización utilizando [d3.js](https://d3js.org/).

### Características TopoJSON
Es deseable conocer a fondo el formato GeoJSON y TopoJSON, para mayor detalle puede consultar el sitio oficial de la [OGC](http://www.opengeospatial.org/) o el documento de Antonio Sierra [ http://www.idee.es/resources/presentaciones/JIIDE13/miercoles/5_GeoJSON_y_TopoJSON.pdf ](http://www.idee.es/resources/presentaciones/JIIDE13/miercoles/5_GeoJSON_y_TopoJSON.pdf) que expuso en el evento _IV jornadas Ibéricas de infraestructuras de datos espaciales (2013)_. Para el alcance de esta demostración basta con saber que:
- El TopoJSON es una extensión del GeoJSON.
- Su característica principal es la eliminación de arcos redundantes.
- Por lo anterior logra una disminución del tamaño del archivo en comparación con un GeoJSON.
- Debido a las características del TopoJSON, hay una inclusión de error en el proceso de simplificación.

### Requerimientos
En esta demostración se va a utilizar [QGIS](https://www.qgis.org/) que es un software GIS de escritorio _free and open source_.

### Acceso a la explicación completa
Para acceder a la página haga clic [aquí](https://jofremanchola.github.io/demo-topojson/).