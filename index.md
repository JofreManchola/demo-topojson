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

Para completar esta demostración se deben instalar dos plugins en QGIS, la intalación de estos plug

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```


### Contacto

Si tiene algún comentario no dude en contactarme @jofremanchola.
