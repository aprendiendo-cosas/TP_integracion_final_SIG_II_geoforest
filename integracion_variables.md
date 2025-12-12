# Técnicas de agregación de variables ambientales basadas en la teoría de la decisión

> + **_Tipo de material_**: <span style="display: inline-block; font-size: 12px; color: white; background-color: #029BF9; border-radius: 5px; padding: 5px; font-weight: bold;"> Teoría</span>  <span style="display: inline-block; font-size: 12px; color: white; background-color: #4caf50; border-radius: 5px; padding: 5px; font-weight: bold;"> Prácticas</span> 
> + **_Versión_**: 2025-2026
> + **_Asignatura_** : SIG II (Máster GEOFOREST). 
> + **_Autor_**: Curro Bonet-García (fjbonet@uco.es)
> + **_Duración_**: 4 horas.



## Objetivos

Esta actividad tiene los siguientes objetivos de aprendizaje:

+ Entender que hay otras técnicas diferentes a la estadística correlacional para entender (y modelar) la naturaleza. 
+ Aprender que estas otras técnicas (evaluación multicriterio, integración booleana de variables, etc.) tienen, como todo, ventajas e inconvenientes.
+ Aprender técnicas de integración de datos relacionados con la asistencia a la toma de decisiones. 



## Hilo argumental

Esta sesión se organiza en torno al siguiente hilo argumental:
+ Enumeración de los factores ecológicos y socioeconómicos que nos permiten responder a la pregunta inicialmente planteada en esta asignatura. Esta fase es clave porque en ella realizamos un proceso de abstracción o de modelización de la realidad: es necesario entender bien el problema de gestión o científico que queremos resolver para identificar adecuadamente las variables involucradas en el mismo. 
+ Identificación del tipo de problema que estamos tratando de resolver y evaluació de la disponibilidad de datos (y de herramientas analíticas) para su abordaje. Algunas preguntas o problemas pueden ser resueltos con técnicas correlacionales (establecer relaciones entre variables dependientes e independientes), mientras que otras requieren una aproximación más mecanicista (simular los procesos socioecológicos implicados). En otras ocasiones no disponemos de tiempo o de datos para hacer nada de lo anterior. En esos casos debemos de recurrir a técnicas en las que el conocimiento experto tiene más importancia. De forma algo más detallada, disponemos de los siguientes grandes grupos de técnicas analíticas:
  + Métodos estadísticos: se trata de encontrar una función matemática que explique correctamente cómo cambia la variable dependiente (regeneración de encina bajo el pinar) en función de las múltiples variables independientes. Esta aproximación es la tradicional.
  + Álgebra de mapas: Se trata de un conjunto de técnicas que permiten combinar mapas procedentes de formatos diversos para resolver un problema de ubicación en el espacio de una actividad dada (en nuestro caso ubicación de las zonas con más regeneración).
  + Métodos basados en procesos: Consisten en simular el funcionamiento íntimo de los procesos elementales implicados en la pregunta en cuestión. 

El siguiente esquema muestra las técnicas anteriores de manera más gráfica.



![tipos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/tipos_metodos.png)



En nuestro caso no podemos hacer experimentos porque no tenemos recursos económicos ni tiempo. Tampoco podemos realizar modelos basados en procesos porque no disponemos del conocimiento necesario ni del tiempo para adquirirlo (tampoco es el objetivo de esta asignatura). Así que, trataremos de responder a la pregunta inicial que nos hacemos en la asignatuar usando técnicas empíricas que tienen en cuenta el conocimiento experto y otras aproximaciones más "difusas" que las otras mostradas en el esquema. Más específicamente usaremos las siguientes técnicas:

- Técnicas de superposición y combinación de variables: Estos métodos consisten en "unir" las distintas variables implicadas en un proceso o problema concreto usando justificaciones o razonamientos relacionados con el conocimiento experto. Se trata, por tanto, de "proyectar" en un procedimiento matemático el conocimiento que una o varias personas tienen sobre un problema o proceso concreto. Estas técnicas son muy fáciles de implementar, ya que implican operaciones matemáticas sencillas. Su principal desventaja es que son muy dependientes del conocimiento experto. De modo que si este está sesgado o es incorrecto, también lo serán los resultados obtenidos. Para reducir esta fuente de error se suelen aplicar usando colectivos de personas con distintas "versiones" del conocimiento experto. En esta asignatura utilizaremos estas dos técnicas:

  - Evaluación multicriterio: Agregación de variables mediante pesos.
  - Operadores lógicos: Agregación de variables mediante operadores.
- Técnicas de agrupación de variables: En estos métodos no hay un proceso real de integración, sino que se realiza una clasificación del territorio en función de los valores que tiene cada punto para cada una de las variables seleccionadas. Como cada variable puede tener valores continuos, los algoritmos que usamos aquí definen rangos para clasificar las variables y crear grupos (o cluster) de lugares (píxeles, polígonos) que tienen características similares. La siguiente imagen ejemplifica bien esta forma de proceder. Imaginemos que en un territorio determinado hay solo dos variables que consideramos importantes. 


En las siguientes secciones se describen con más detalle los métodos anteriores.



## Técnicas de superposición y combinación de variables

El siguiente esquema muestra de manera resumida las distintas fases que hemos de cumplir para aplicar estas técnicas que permiten la superposición de variables y que están muy relacionadas con la teoría de la decisión.

![pasos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/esquema_metodo.png)



Aunque los tres primeros pasos de esta metodología ya han sido trabajados parcialmente en sesiones anteriores, dedicaremos un rato a generar de manera colaborativa un modelo conceptual relacionado con nuestro problema inicial. A continuación, describimos en la siguiente sección la transformación de las variables en criterios.

### Construcción de un modelo conceptual
Iniciamos un proceso colaborativo para construir un mapa conceptual que nos ayude a entender mejor el problema que estamos abordando. Se trata de un proceso iterativo. Es decir, iniciamos el procedimiento y vamos repitiéndolo o mejorándolo añadiendo o modificando variables, conceptos e ideas. Damos los siguientes pasos:
+ En primer lugar enumeramos las variables que nos resultan interesantes y tratamos de justificarlas. 
+ En algunos casos estas variables no generan debate. Pero en otras ocasiones se establecen conversaciones relevantes porque hay dudas razonables sobre la idoneidad de alguna de las propuestas realizadas. En este sentido, debatimos sobre lo siguiente:
  + La relación entre la macroescala y la microescala se pone de manifiesto al hablar del clima. Consideramos relevante incorporar la temperatura y la precipitación como variables que describen el macroclima. Sin embargo, la radiación solar incidente se incorpora como variable relevante a escala microclimática. 
  + También aplicamos un razonamiento parecido al hablar del suelo. El tipo de suelo nos da información del mismo a escala macro y la profundidad potencial (calculada como el Wetness index) a escala micro.


El proceso de creación de un modelo conceptual se extiende a las siguientes fases. Vamos incorporando a dicho modelo elementos que nos ayudan a describir la transformación de la variable en criterio y la integración de dichos criterios mediante pesos u operadores booleanos. 

El siguiente esquema muestra las tres versiones del modelo conceptual que hemos generado en clase. También se puede descargar [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/presentacion/modelo_conceptual_SIG_II.drawio.zip) en formato visible por [diagrams](https://app.diagrams.net/). :
















### Transformación de variable a criterio

A lo largo de la asignatura hemos trabajado en la generación de mapas que muestran la distribución espacial de algunas variables biofísicas relevantes para nuestro caso de estudio: severidad del incendio, diversidad (índice de Shannon), producción primaria, etc. Estas capas expresan la variable en cuestión usando unidades propias de la variable considerada (ej. árboles/hectárea). Además se pueden usar para multitud de situaciones diferentes. Es decir, un mapa de profundidad del suelo, por ejemplo, se puede usar para nuestro caso de estudio y para cualquier otro en el que el suelo sea relevante.

Pero cuando aplicamos a la variable un cierto criterio decisional debemos de transformar el mapa que representa la distribución espacial de dicha variable. Es decir, si queremos tener un mapa que muestre la distribución espacial de un criterio concreto, es necesario transformar la variable de la que partimos. Por ejemplo, imaginemos que queremos ubicar en el territorio un área recreativa. Y resulta que la densidad del bosque es determinante para esto: las zonas más densas no son adecuadas porque en ellas no caben las mesas del área recreativa. Así, en este caso, **al aumentar la densidad del bosque, se reduce la idoneidad para albergar áreas recreativas**. Sin embargo, en el ejemplo que nos ocupa ocurre lo contrario: **al aumentar la densidad aumenta la idoneidad** porque debemos de reducir la competencia intraespecífica en aquellos lugares en los que ésta es más intensa (más densidad). En el proceso de transformación de la *variable* a *criterio*, aplicamos una función de transformación. Esta función cumple dos objetivos:

+ Estandariza los valores de todos los mapas para usar un rango de 0 a 1 (o a veces de 0 a 255)
+ Transforma los valores de la variable (producción primaria, profundidad del suelo, etc.) a valores de idoneidad cualitativos.

La función de transformación puede tener formas diferentes. En la siguiente figura se muestran algunos ejemplos:

![tipos_funciones](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/estandarizacion.jpg)



En nuestro caso asumiremos que la relación entre cada variable y su criterio es lineal. Así que tendremos dos situaciones representadas por los dos dibujos que hay a continuación: Función de preferencia (de transferencia o transformación) directa e inversa. 



![pertenencia](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/funcion_pertenencia_lineal.png)

En los dibujos anteriores también puedes ver cómo calcular los parámetros de las funciones. Dado que una recta está definida por dos puntos, es fácil despejar los parámetros de la ecuación de la recta (pendiente y ordenada en el origen) a partir de los valores extremos (que toman valores 0 y 1 en el mapa de idoneidad).

Para aplicar la función resultante en cada variable a la capa correspondiente, usamos la calculadora raster. Para ello necesitamos saber los valores máximos y mínimos de cada una de las capas. En la pestaña de propiedades de cada capa de QGIS podemos ver fácilmente los valores máximos y mínimos. Luego, pondremos en la calculadora ráster la ecuación correspondiente. A continuación va un ejemplo:

+ Mínimo: 0.008539155125618
+ Máximo: 6.4734792709351
+ Por tanto, la ecuación sería así:

```python  
  (1/(6.4734792709351-0.008539155125618))*"shannon@1" - (0.008539155125618/(6.4734792709351-0.008539155125618))
```

### Métodos de integración de variables.
Estudiaremos los tres siguientes métodos

#### Evaluación multicriterio

El análisis multicriterio es una técnica muy sencilla que permite conciliar en un mismo mapa criterios diferentes. Es una forma de espacializar criterios decisionales basados en conocimiento experto. Es decir, gracias a esta técnica podemos obtener mapas que recojan los criterios de un centro decisor concreto con relación a un aspecto determinado.  En nuestro ejemplo tenemos varios criterios y se trata de unificarlos en un único mapa que asigne un valor de aptitud global a cada punto afectado por el incendio. Por ejemplo:
+ Criterio de intensidad del incendio: a más intensidad más aptitud.
+ Criterio de profundidad del suelo: a más profundidad más aptitud.
+ Criterio de distancia a manchas donadoras de semillas: A más distancia menos aptitud.

Para agregar los criterios empezaremos asignando un peso a cada uno de ellos. La suma de los pesos ha de ser 1. El criterio que tenga más peso contribuirá en mayor medida al mapa final. Procedemos en dos pasos:

El proceso de integración se hace fácilmente con la calculadora de mapas de QGIS u operando con las capas raster en el caso de que trabajemos con R o con Python. El resultado final es la suma del producto de cada criterio (capa _apt_) por su peso. Introducimos la siguiente ecuación en la calculadora raster:

```python  
  ("apt_densidad@1"*0.6)+("apt_cti@1"*0.1)+("apt_distancia@1"*0.3)
 
```
La siguiente imagen muestra el método con otro ejemplo diferente:

![pesos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/pesos_ponderados.png)

Uno de los problemas del análisis multicriterio es que ocurre una compensación de criterios. Si una variable tiene un valor muy alto en un lugar determinado, puede que el resultado final en ese punto sea alto aunque el valor de un criterio importante en ese punto sea bajo. Esto puede hacer que lugares no adecuados sean etiquetados como sí adecuados. Un ejemplo que ilustra esta situación: imaginemos que queremos montar un equipo de baloncesto. Un buen jugador de baloncesto ha de tener las siguientes características:
+ Altura.
+ Fortaleza en los brazos.
+ Tobillos resistentes.

Si le damos distintos pesos a esas variables y con eso "puntuamos" la idoneidad de una lista de personas para entrar en nuestro equipo, puede darse la situación de que una persona tenga alta puntuación final aún teniendo los tobillos débiles. Eso implica tomar una decisión equivocada puesto que estaríamos incluyendo en el equipo a una persona que no rendiría bien. Esta situación denota que hay criterios que no solo tienen más peso que otros, sino que además deben satisfacerse **necesariamente** para tomar una decisión acertada. Y esto nos lleva a la segunda técnica de análisis de la decisión:

#### Operadores lógicos

En esta segunda técnica no se asignan pesos a los criterios que combinamos sino que se establecen condiciones que deben cumplir los lugares de nuestra zona de estudio para ser idoneos según el objetivo del proceso decisiona en cuestión. Volviendo al ejemplo del jugador de baloncesto ideal, diríamos algo así: debe de tener los tobillos fuertes **y** **o bien** ser fuerte **o bien** ser alto. De alguna forma estamos diciendo que hay una condición **necesaria** para ser buen jugador, pero no suficiente. Necesita tener los tobillos resistentes y luego una de las otras dos condiciones. Esta forma de combinar criterios decisionales recibe el nombre de integración mediante operadores booleanos porque implican el uso de las conjunciones **o** e **y**. 

En el ejemplo que nos ocupa, usaremos operadores lógicos para integrar las tres capas. Consideraremos que un lugar es adecuado para satisfaer nuestros objetivos si cumple un criterio específico y una combinación de los otros dos. Es decir, pondremos como criterio fundamental que los lugares adecuados tengan una **alta severidad**. Si no se cumple este criterio, nunca se podrá obtener un valor alto al final del proceso de integración de las variables. Los otros dos criterios serán optativos entre sí. Es decir, seleccionaremos como lugares adecuados aquellos que **o bien están cerca de una mancha de vegetación natural, o bien tienen suelos potencialmente húmedos**. Es decir, en conjunto aplicaremos los siguientes criterios concatenados: Un lugar es considerado como adecuado si:

+ Tiene una alta densidad de pinos **Y**:
+ Está cerca de una mancha de vegetación natural **O** tiene suelos potencialmente húmedos. 

Para implementar esta operación en un SIG, usamos dos operadores matemáticos muy sencillos:

+ Valor **máximo** entre dos capas: es el equivalente al operador **O**. Si en un píxel hay valores altos de aptitud en una capa y bajos en otra, el resultado será alto, puesto que estamos eligiendo el máximo de ambos. Si la aptitud es alta en los dos casos, también seleccionaremos un valor alto. Es decir, se trata de un operador poco restrictivo.
+ Valor **mínimo** entre dos capas: es el equivalente al operador **Y**. Si en un píxel hay valores altos de aptitud en una capa y bajos en otra, el resultado será bajo, puesto que estamos eligiendo el mínimo de ambos. Solo si la aptitud es alta en los dos casos, seleccionaremos un valor alto. Es decir, se trata de un operador poco restrictivo.

La siguiente figura muestra el funcionamiento de estos operadores:

![booleanos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/operadores_booleanos.png)

Para aplicar estos operadores a nuestras capas, puedes la calculadora de mapas de QGIS (funciones MIN y MAX). 

Los operadores anteriores son un poco "rígidos" dado que solo seleccionan los valores extremos (mínimo o máximo). Para suavizar el resultado se pueden usar otros operadores como los mostrados en la siguiente figura:

![difusos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/operadores_difusos.png)



#### Reclasificación de los resultados obtenidos

Tras aplicar cualquiera de las técnicas anteriores obtendremos un mapa con valores de aptitud que van de 0 a 1. Este mapa puede ser muy útil para comprender mejor el proceso socioecológico en el que estamos trabajando. Pero normalmente cuando se toman decisiones es necesario seleccionar una serie de zonas concretas en las que se va a realizar una actuación determinada. Por eso es útil simplificar el mapa resultante para elegir solo los lugares (=píxeles) que resulten más idoneos para nuestro objetivo. El resto los descartaremos porque no reunen los requisitos que hemos impuesto. Para hacer esta selección aplicaremos una operación muy común en análisis raster: [reclasificación](https://docs.qgis.org/3.4/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html#qgisreclassifybytable). Consiste en reducir la diversidad de valores de un raster asigando nuevos en función de un rango. Por ejemplo, asignaremos el valor de 1 a todos los píxeles que tengan una aptitud igual o mayor de 0.8. Para hacer esto, construimos una tabla de reclasificación.

Para reclasificar una capa rastser en QGIS, buscamos el algoritmo "reclassify by table" en el buscador de procesos de QGIS. Añadimos los siguientes parámetros:
- _raster layer_: _apt\_final.tif_
- _reclassification table_: Abrimos la tabla y añadimos las siguientes filas:


| Desde (Mínimo) | hasta (Máximo)| Valor nuevo|
|----------------:|------------:|---------:|
|0|0.9| 0|
| 0.9 | 1|1|
 - _reclassified raster_ (capa de salida): _apt\_final\_re.tif_



#### Técnicas de agrupación de variables

Este conjunto de técnicas consiste en una serie de algoritmos que permiten clasificar una serie de variables y crear grupos de elementos que tienen características parecidas. El término "clasificación" es el más comunmente utilizado en estos casos. 

Se trata de crear grupos de elementos que tienen características parecidas en virtud de una serie de variables. En nuestro caso, la idea es seleccionar lugares (píxeles o polígonos) que son parecidos desde el punto de vista de las variables ambientales estudiadas. Las técnicas de clasificación hacen estos grupos teniendo en cuenta las similitudes entre los elementos a agrupar. Para ello es necesario definir un umbral de similitud. Es decir, se trata de agrupar elementos en función de cómo de similares son entre sí con respecto a una serie de variables.

En nuestro caso la agrupación de las variables tiene consecuencias espaciales porque cada uno de los puntos del territorio (píxeles o polígonos) están espacialmente referenciados. Por tanto, el resultado de la agrupación será un mapa.

El siguiente esquema muestra gráficamente la filosofía de esta técnica. No obstante, hay mucha información disponible en internet. Basta con buscar *K-means* (que es una de las técnicas más comunes) o clasificación supervisada.

![tipos](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/2024-2025/imagenes/clustering.png)

A la izquierda se representan dos variables espacializadas (abajo) y el valor de una serie de puntos (numerados del 1 al 10) en función de las dos variables (gráfica superior izquierda). La clasificación consiste en construir grupos de puntos que tienen unas caracteríticas parecidas desde el punto de vista de las dos variables consideradas. Esta clasificación implica establecer similitudes entre los puntos (gráfica de arriba a la derecha). Además, esa clasificación se traduce en un mapa que muestra la distribución de las zonas homogéneas. Para cada conjunto de puntos se pueden definir un número ilimitado de agrupaciones diferentes. Las técnicas utilizadas para hacer la agrupación permiten seleccionar la más adecuada usando criterios estadísticos.

Para hacer clasificaciones como las descritas anteriormente se pueden usar muchas herramientas diferentes. Es posible hacerlas en QGIS y también en R, donde hay multitud de paquetes específicamente diseñados para ello. A la hora de elegir una herramienta para hacer este procedimiento, es importante que utilice de manera explícita la componente espacial. Es decir, que la herramienta pueda hacer un agrupamiento geográfico. O dicho de otra forma, que proyecte el agrupamiento al territorio. Y aquí lo dejamos. Si queréis experimentar con estas herramientas, tenéis muchas a vuestro alcance. Para encontrarlas basta con usar las palabras clave *clustering* o *k-means*.



## Ejemplo sencillo

Partimos de una pregunta que no se puede resolver fácilmente con técnicas más "duras" (correlacional o modelización)

> ¿Qué variables podemos utilizar para declarar una zona como espacio protegido?

Responder a esta pregunta desde la lógica correlacional a la que estamos acostumbrados (variable dependiente y variables independientes que se relacionan) es imposible por varios motivos:

+ Hay demasiadas variables en la susceptiblidad de un territorio para ser útil desde el punto de vista de la protección de la naturaleza. No podemos contemplarlas todas.
+ Aunque consiguiéramos fijar algunas variables, no disponemos de la capacidad experimental necesaria para establecer relaciones entre las variables. Tendríamos que plantear un experimento en el que las distintas variables potencialmente explicativas (diversidad, distancia a núcleos urbanos, etc.) se manifestaran de manera similar en dos territorios: uno protegido y otro sin proteger. Esto es imposible.

Así que para decidir qué lugares son más adecuados para albergar un espacio protegido debemos de buscar otros métodos de generar conocimiento. Estas aproximaciones, más difusas y flexibles que las que conocemos, nos permiten abordar problemas como el que nos ocupa. Podemos englobar estas técnicas bajo la denominación de "álgebra de mapas". Estos métodos consisten en "unir" las distintas variables implicadas en un proceso o problema concreto usando justificaciones o razonamientos relacionados con el conocimiento experto. Se trata, por tanto, de "proyectar" en un procedimiento matemático el conocimiento que una o varias personas tienen sobre un problema o proceso concreto. Estas técnicas son muy fáciles de implementar, ya que implican operaciones matemáticas sencillas. Su principal desventaja es que son muy dependientes del conocimiento experto. De modo que si este está sesgado o es incorrecto, también lo serán los resultados obtenidos. Para reducir esta fuente de error se suelen aplicar usando colectivos de personas con distintas "versiones" del conocimiento experto. 

En la sesión anterior se identificaron una serie de variables potencialmente útiles para responder a la pregunta que nos ocupa. Estas variables se identificaron basándose en el criterio experto de los estudiantes y de la profesora Cristina:

+ Diversidad. La diversidad biológica es importante para considerar una zona como potencialmente protegible. Se supone que es esa diversidad la que queremos proteger. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/shannon.tif) puedes descargar el mapa de diversidad de Andalucía. 
+ Distancia a zonas urbanas. La distancia entre la zona protegida y los núcleos urbanos también es importante porque esto puede condicionar los posibles impactos al espacio protegido o el uso que se hace de este. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/dist_zona_urbana.tif) puedes descargar el mapa de distancias de cada punto de Andalucía a la zona urbana más cercana. 
+ Distancia a vías de comunicación. Igualmente, lo bien o mal comunicado que esté un espacio protegido condiciona tanto los impactos potenciales de la actividad humana como su posible uso por parte de la sociedad. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/dist_red_viaria.tif) puedes descargar el mapa de distancias de cada punto de Andalucía a la carretera más cercana. 
+ Efecto del cambio climático. Sabemos que el clima está cambiando. Quizás es importante tener en cuenta esta variable para diseñar nuestra red de espacios protegidos. Usaremos una capa que muestra la estimación de la desviación de temperatura media anual (en décimas de grado) para la década de 2090 a 2100. Esta capa se ha obtenido a partir de la [REDIAM](https://www.juntadeandalucia.es/medioambiente/portal/acceso-rediam) y puedes descargla [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/temp_futuro.tif). 

Ahora debemos de transformar las variables en criterios:

#### Mapa de diversidad -> Aptitud con relación a la biodiversidad.
Asumiremos una relación directa entre variable y aptitud. Es decir, a más diversidad mejor para nuestros objetivos (identificar sitios potencialmente protegibles). Sabemos que los valores máximos y mínimos del mapa de diversidad son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0.008539155125618
+ Máximo: 6.4734792709351
+ Por tanto, la ecuación sería así:

```python  
  (1/(6.4734792709351-0.072917148470879))*"shannon@1" - (0.072917148470879/(6.4734792709351-0.072917148470879))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_shannon.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/refs/heads/2024-2025/geoinfo/apt_shannon.tif) puedes descargarlo. 

#### Distancia a zonas urbanas -> Aptitud con relación a la distancia a zonas urbanas.
Asumiremos una relación directa entre variable y aptitud. Es decir, a más distancia mejor para nuestros objetivos (identificar sitios potencialmente protegibles). Justificamos esta afirmación diciendo que las zonas urbanas generan impactos importantes en los espacios protegidos y por tanto es mejor que estén lejos de ellas. Sabemos que los valores máximos y mínimos del mapa de distancias a zonas urbanas son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0
+ Máximo: 22983.689453125
+ Por tanto, la ecuación sería así:

```python  
  (1/(22983.689453125-0))*"dist_zona_urbana@1" - (0/(22983.689453125-0))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_dist_zona_urbana.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/apt_dist_zona_urbana.tif) puedes descargarlo. 

#### Distancia a la red viaria -> Aptitud con relación a la distancia a la red viaria.
Asumiremos una relación inversa entre variable y aptitud. Es decir, a más distancia peor para nuestros objetivos (identificar sitios potencialmente protegibles). Justificamos esta afirmación diciendo que los espacios protegidos necesitan gestión y que para ello es importante que estén cerca de carreteras y caminos. Esto es muy cuestionable en realidad, pero lo hacemos así por fines docentes. Sabemos que los valores máximos y mínimos del mapa de distancias a carreteras son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0
+ Máximo: 17755.28125
+ Por tanto, la ecuación sería así:

```python  
 (1/(0-17755.28125))*"dist_red_viaria@1" - (17755.28125/(0-17755.28125))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_dist_red_viaria.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/apt_dist_red_viaria.tif) puedes descargarlo. 



#### Aumento previsto de temperatura -> Aptitud con relación al impacto del cambio climático

Asumiremos una relación inversa entre variable y aptitud. Es decir, a más aumento de temperatura respecto a la media de la serie histórica, menos aptitud para nuestro objetivo. Justificamos esta decisión porque nos interesa que los espacios protegidos estén en lugares poco afectados por el cambio climático.  Sabemos que los valores máximos y mínimos del mapa de distancias a carreteras son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 1.6337893009186
+ Máximo: 17755.28125
+ Por tanto, la ecuación sería así:

```python  
 (1/(1.7122367620468-4.7942304611206))*"temp_futuro@1" - (4.7942304611206/(1.7122367620468-4.7942304611206))
```

Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_temp_futuro.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/apt_temp_futuro.tif) puedes descargarlo. 

Una vez que tenemos todos los criterios espacializados, podemos aplicar dos métodos para integrar las variables: evaluación multicriterio y operadores booleanos:

### Evaluación multicriterio
El proceso de integración se hace fácilmente con la calculadora de mapas de QGIS u operando con las capas raster en el caso de que trabajemos con R o con Python. El resultado final es la suma del producto de cada criterio (capa _apt_) por su peso. El valor relativo de cada peso nos da una idea del escenario decisional en el que nos encontramos. Por ejemplo, la siguiente combinación de pesos da mucha importancia a la diversidad y al escenario de cambio climático. Llamaremos al resultado de esta operación [*escenario_1.tif*](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/escenario_1.tif)

```python  
("apt_shannon@1" * 0.4)+("apt_temp_futuro@1"*0.4)+ ( "apt_dist_red_viaria@1"*0.1)+("apt_dist_zona_urbana@1"*0.1)
 
```
También podemos crear otro escenario quitando importancia al efecto del cambio climático. Llamaremos [*escenario_2.tif*](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/escenario_2.tif) a este resultado:

```python  
("apt_shannon@1" * 0.5)+("apt_temp_futuro@1"*0.1)+ ( "apt_dist_red_viaria@1"*0.2)+("apt_dist_zona_urbana@1"*0.2)
 
```

Uno de los problemas del análisis multicriterio es que ocurre una compensación de criterios. Si una variable tiene un valor muy alto en un lugar determinado, puede que el resultado final en ese punto sea alto aunque el valor de un criterio importante en ese punto sea bajo. Esto puede hacer que lugares no adecuados sean etiquetados como sí adecuados. Un ejemplo que ilustra esta situación: imaginemos que queremos montar un equipo de baloncesto. Un buen jugador de baloncesto ha de tener las siguientes características:
+ Altura.
+ Fortaleza en los brazos.
+ Tobillos resistentes.

Si le damos distintos pesos a esas variables y con eso "puntuamos" la idoneidad de una lista de personas para entrar en nuestro equipo, puede darse la situación de que una persona tenga alta puntuación final aún teniendo los tobillos débiles. Eso implica tomar una decisión equivocada puesto que estaríamos incluyendo en el equipo a una persona que no rendiría bien. Esta situación denota que hay criterios que no solo tienen más peso que otros, sino que además deben satisfacerse **necesariamente** para tomar una decisión acertada. Y esto nos lleva a la segunda técnica de análisis de la decisión:

### Operadores lógicos (o booleanos)
Para aplicar estos operadores a nuestras capas, usamos la calculadora de mapas de QGIS en tres pasos anidados:

Primero combinamos con el operador **o** la aptitud con relación a la diversidad y la vulnerabilidad al cambio climático:

```py
MAX ( "apt_shannon@1","apt_temp_futuro@1")
```

Al resultado le llamamos [*apt_shannon_o_apt_temp_futuro.tif*](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/apt_shannon_o_apt_temp_futuro.tif)

Luego combinamos con el operador **o** la aptitud con relación a la distancia a núcleos urbanos y a vías de comunicación:

```py
MAX ("apt_dist_red_viaria@1","apt_dist_zona_urbana@1")
```

Al resultado le llamamos [*apt_dist_vias_o_apt_dist_nucleos.tif*](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/apt_dist_vias_o_apt_dist_nucleos.tif)

Por último, combinamos los dos resultados parciales obtenidos anteriormente con el operador **y**:

```py
MIN("apt_dist_vias_o_apt_dist_nucleos@1","apt_shannon_o_apt_temp_futuro@1")
```

Al resultado le llamamos *[escenario_3.tif](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/geoinfo/escenario_3.tif)*



## Lecturas complementarias

Además de lo visto anteriormente, os paso la siguiente información que puede resultar de utilidad:

+ [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/modelos_ecologicos.pdf) que describe distintos tipos de modelos ecológicos. Incide en alguno de los conceptos descritos en la sesión final de nuestra asignatura. 
+ [Resumen](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/herramientas_apoyo_decisiones.pdf) de mi tesis (año 2003, no os riais de los esquemas, por favor. En esa época no existía R ni siquiera QGIS). En el texto se describen los conceptos generales sobre integración de información ambiental usando técnicas de operadores booleanos. He recortado solo la parte interesante. Eso hace que el texto no sea muy fluido porque faltan secciones.
+ Varios textos sobre análisis multicriterio:
  + [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/multicriterio_seleccion_zonas_plantas_electricas.pdf) sobre el uso del análisis multicriterio para localizar plantas de producción fotovoltaica. 
  + [Interesante](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/MCE_review.pdf) revisión del uso de las técnicas multicriterio en cuestiones de conservación de la naturaleza. Muy recomendable este trabajo.
  + [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/ecological_corridors_multicriteria.pdf) que describe cómo la conectividad ecológica del paisaje usando evaluación multicriterio.
  + [Informe](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2024-2025/biblio/Memoria_Apicola_2004.pdf) de la REDIAM que describe cómo se hizo el mapa de aprovechamientos apícolas de Andalucía usando la técnica de la evaluación multicriterio. 
+ [Manual](https://geodacenter.github.io/workbook/9a_spatial1/lab9a.html) interesante sobre el uso de la clasificación espacialmente explícita.


## Vídeo de la sesión

<iframe width="560" height="515" src="https://www.youtube.com/embed/4KgzEq73a6Y?si=uUgwBiKiuqgMc119" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>





****

[Aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/archive/refs/tags/2024-2025.zip) puedes descargar un archivo .zip que contiene este guión en formato html y todo el material que incluye.

****
Haz click [aquí](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/releases) para ver cómo ha cambiado este guión en los distintos cursos académicos.

****
 <p xmlns:cc="http://creativecommons.org/ns#" >El contenido de este repositorio se puede utilizar bajo la siguiente licencia:  <a  href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1"  target="_blank" rel="license noopener noreferrer"  style="display:inline-block;">CC BY-NC-SA 4.0<img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"  alt=""></a></p> 

<p>Esta licencia no aplica a enlaces a artículos, libros o imágenes no originales. Estos productos tienen su licencia correspondiente.</p>

