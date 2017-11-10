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

### Descarga de información geográfica
Para descargar información geográfica hay diversas fuentes, una de las primeras que podría consultar son las Infraestructuras de Datos Espaciales (IDE), en Colombia puede referirse a la [ICDE](http://www.icde.org.co/) (Infraestructura Colombiana de Datos Espaciales) y a [IDECA](https://www.ideca.gov.co/) (La IDE de Bogotá). En esta demostración se descargan datos de barrio común desde el [Laboratorio Urbano de Bogotá](https://bogota-laburbano.opendatasoft.com). Como referencia a continuación hay tres enlaces para encontrar información geográfica.
- Mapa de referencia de Bogotá (IDECA): https://www.ideca.gov.co/es/servicios/mapa-de-referencia
- Geocontenidos web (ICDE): http://www.icde.org.co/servicios/geocontenidos-web
- Laboratorio urbano: https://bogota-laburbano.opendatasoft.com

![Descarga de barrios desde el Laboratorio Urbano de Bogotá](assets\img\labUrbano3.png)

Para este caso se descarga el dato en formato shapefile, esto es un comprimido en zip por lo que se debe descomprimir antes de importarla en QGIS.

![Descarga de barrios desde el Laboratorio Urbano de Bogotá](assets\img\labUrbano4.png)

### Visualización en QGIS
Para importar en QGIS la capa de barrios, una vez descargarda y descomprimida se realiza lo siguiente:
1. En QGIS se selecciona la herramienta `Añadir capa vectorial`.
![Añadir capa vectorial a QGIS](assets\img\import_qgis.png)
2. Se selecciona la ubicación de la capa (conjunto de datos). Hay múltiples opciones para conectar los datos, en este caso se utiliza un archivo como origen de datos.
![Añadir capa vectorial a QGIS](assets\img\import_qgis2.png)
3. Esto ya debe mostrar la capa, hasta el momento no se conoce el datalle del dato ni se ha asignado simbología.
![Añadir capa vectorial a QGIS](assets\img\import_qgis3.png)

#### Explorando la tabla de atributos
Una vez cargada la capa en QGIS, explorar su tabla de atributos es simple, solamente haga clic contrario sobre la capa y seleccione la opción `Abrir tabla de atributos`.
![Abrir tabla de atributos](assets\img\import_qgis4.png)
En la tabla de atributos aparece el campo `localidad` que se usará para asignar la simbología a la capa.
![Abrir tabla de atributos](assets\img\qgis_table_attributes.png)

#### Asignado simbología
La simbología se configura en las propiedades de la capa, para esto nuevamente se hace clic contrario sobre la capa y se selecciona la opción `propiedades`.
![Abrir tabla de atributos](assets\img\import_qgis5.png)
Allí en la opción `Estilo` se representa con el tono el atributo `localidad`, en este caso he dejado que QGIS asigne automáticamente los colores por lo que la expresividad no es la mejor, se aprecian colores muy similares en la escala.
![Abrir tabla de atributos](assets\img\import_qgis6.png)
Después de aplicar y aceptar los cambios, se debería ver un mapa de Bogotá con la división de barrios comunes donde el color representa las localidades, en este caso se aprecian fácilmente errores en el dato.
![Abrir tabla de atributos](assets\img\import_qgis7.png)
![Abrir tabla de atributos](assets\img\import_qgis8.png)

## Uso de la capa en D3
Ahora sí a lo que nos interesa...
El objetivo de explorar los datos y asignar la simbología es obtener la misma visualización en d3.js ya que la geometría solamente no sería tan interesante.

### Instalación de plugins en QGIS
La instalación de plugins en QGIS normalmente se realiza por medio del menú `complementos` que permite su administración e instalación, en este caso el complemento aún se encuentra en fase experimental por lo que se debe descargar del sitio web de QGIS.

El plugis a instalar es `d3 Map Render` desde [ https://plugins.qgis.org/plugins/d3MapRenderer/ ](https://plugins.qgis.org/plugins/d3MapRenderer/).
![Abrir tabla de atributos](assets\img\img1.png)
![Abrir tabla de atributos](assets\img\img2.png)

La descarga es el archivo `d3MapRenderer-0.10.3.zip` que se encuentra debe descomprimir en el directorio de plugins de QGIS, el directorio predeterminado es `C:\Users\<nombre-de-usuario>\.qgis2\python\plugins`.
![Abrir tabla de atributos](assets\img\d3MapRender.png)
![Abrir tabla de atributos](assets\img\d3MapRender2.png)

Una vez instalado, se debe habilitar, así que ahora en QGIS, en el menú `complementos` se abre la ventana de administración, se busca `d3 Map Render` y se habilita.
![Abrir tabla de atributos](assets\img\qgis_complementos2.png), 
![Abrir tabla de atributos](assets\img\qgis_complementos3.png),

### QGIS a d3
Una vez habilitado el complemento aparece en barra de herramientas para su uso, para utilizarlo solamente clic y a seguir el wizard.
![Abrir tabla de atributos](assets\img\qgis_d3MapRender2.png),

Dentro de las configuraciones en esta demostración se ha configurado:
- El título de la visualización
- El directorio de salida del proyecto en d3.
- La proyección geográfica (se mantuvo la predeterminada).
- Se habilitaron las opciones de `zoom`, `paneo`.
- La ubicación de la leyenda.
- Los configuraron los campos deseados en el `idenfity`.

**Nota:** En las opciones de formato de salida únicamente está disponible *GeoJSON*, para exportar a TopoJSON puede utilizar el [TopoJSON 2.0 API Reference](https://github.com/topojson/topojson/blob/master/README.md).

![Abrir tabla de atributos](assets\img\qgis_d3MapRender3.png),
![Abrir tabla de atributos](assets\img\qgis_d3MapRender4.png),
![Abrir tabla de atributos](assets\img\qgis_d3MapRender5.png),
![Abrir tabla de atributos](assets\img\qgis_d3MapRender6.png),

Finalmente se obtiene en el directorio seleccionado una aplicación web con lo siguiente:

![Abrir tabla de atributos](assets\img\exportD3.png)

Explorando en el directorio `json` se encuentra un archivo *.json que al explorarlo se evidencia que tiene formato GeoJSON.
![Abrir tabla de atributos](assets\img\GeoJSON_Final.png)

## Aplicación web
El resultado del D3 Map Render se encuentra disponible en [esta aplicación web](GeoJSON/).

Finalmente, con el fin de obtener el mismo dato en formato TopoJSON, se sigue el tutorial de [d3 MapRenderer](http://maprenderer.org/d3/) (sugiero que lo sigan para más detalle), en el que básicamente se debe:
1. Instalar [Node.js](https://nodejs.org).
2. Instalar el paquete topojson.
> npm install -g topojson
3. Instalar el servidor http para Node.js (opcional).
> npm install -g http-server
4. Convertir el dato de formato GeoJSON a TopoJSON.
> geo2topo states=barriosprueba.json > topo_barriosprueba.json
5. Para mayor información sobre las posibilidades de generación, simplificación y manipulación del TopoJSON se sugiere consultar el [TopoJSON 2.0 API Reference](https://github.com/topojson/topojson/blob/master/README.md).


Explorando en archivo generado, se encuentra un archivo *.json que contiene la capa de barrios en formato TopoJSON (sin simplificar).
![Abrir tabla de atributos](assets\img\TopoJSON_Final.png)


### Contacto

Si tiene algún comentario no dude en contactarme @jofremanchola.
