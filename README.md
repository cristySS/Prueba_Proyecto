# R-GIS
Este repositorio contiene la documentación del desarrollo de sistema de riego de jardín 

# R-GIS

#### (Remote-Garden Irrigation System)

Este proyecto plantea el desarrollo de un prototipo que permita realizar riegos del jardín vía remota, incluyendo sensores de humedad para aplicar la humedad requerida por las plantas, sensor de temperatura para el cálculo de evaporación y sensor de luminosidad para cálculo de la transpiración; estos dos últimos permitirán un cálculo correcto de la lamina de riego que se regulara a través del tiempo de riego.

La cantidad de agua que utilizan las plantas depende del clima, del contenido de agua en el suelo y la especie cultivada. La determinación y el monitoreo de la humedad del suelo es primordial para resolver problemas vinculados a las necesidades de riego de los cultivos.

La programación del riego debe responder a dos preguntas básicas: ¿Cuándo regar? y ¿Cuánto regar? La respuesta a la primera pregunta es el intervalo de riegos y tiene la finalidad de optimizar la producción, conservar el agua, minimizar impactos ambientales y ahorrar dinero. La segunda respuesta debe estar orientada a igualar los requerimientos de agua del cultivo y realizar los aportes en cantidades suficientes, considerando la evaporación, transpiración, radiación, precipitación y temperatura. (Ilustración 1 Esquema de variables.)

![img](https://github.com/cristySS/R-GIS/blob/main/imagenes/Imagen1.jpg)

​                                                           *Ilustración 1 Esquema de variables.*

La evaporación en las superficies vegetales se denomina transpiración, o evapotranspiración si se incluye también la perdida de agua por evaporación que se produce en la superficie subyacente del suelo.

Los factores que influyen en la transpiración son los mismos que los que influyen en la Evaporación. El factor más influyente es el poder evaporante de la atmósfera y, por tanto, el déficit de saturación de la atmósfera, la temperatura del aire, la insolación, la velocidad del viento y la presión atmosférica.

Los factores meteorológicos actúan indirectamente sobre la intensidad de la transpiración, debido a su influencia sobre la apertura de los estomas. 

La iluminación, la temperatura o la humedad del aire favorecen la transpiración. La humedad del suelo influye también sobre la intensidad de transpiración. Si la humedad del suelo no es suficiente para que la planta pueda extraer agua del suelo, la transpiración cesa y la planta se muere. Se define el punto de marchitez como el contenido de humedad del suelo por debajo del cual la raíz de la planta no puede extraer el agua. En este punto la transpiración de la planta cesa y si esta situación se prolonga, la planta se marchita. El punto de marchitez depende del tipo de suelo y de la planta. 

Por otro lado, para las mismas condiciones atmosféricas y para el mismo terreno, la Transpiración de una planta depende de la especie vegetal, de la edad, del desarrollo, tipo de follaje y de la profundidad radicular.

La evaporación del agua está dada según el sitio o lugar donde la midamos, y esta depende de muchos factores como: horas luz, temperatura, viento, humedad ambiente, altura, entre otros. Los datos de evaporación se pueden obtener de la estación meteorológica más cercana; ésta se determina midiendo la altura de agua perdida en un tanque de agua, en milímetros.

La ecuación de *Penman-Monteith* se utiliza para la estimación de ETo, es decir la **evapotranspiración** que ocurre a partir de una superficie hipotética de un cultivo de pastos, bien regada, la cual considera valores fijos de altura del cultivo, albedo y resistencia de la superficie.

De acuerdo con el enfoque del coeficiente del cultivo, la evapotranspiración del cultivo ETc se calcula como el producto de la evapotranspiración del cultivo de referencia, ETo y el coeficiente del cultivo Kc (ver Tabla 1):

​                                                           ETc = Kc* ETo                                                                  (Ecuación 1)  



Donde: 
ETc	 evapotranspiración del cultivo [mm/d] 
Kc	coeficiente del cultivo [adimensional] 
ETo	 evapotranspiración del cultivo de referencia [mm/d]



La ETo se puede estimar usando la ecuación de Hargreaves para estimar ETo donde: 

​                      ETo = 0.0023 * (Tmedia + 17.8) * (Tmax - Tmin) *0.5 * Ra    mm/día                    (Ecuación 2)



La temperatura media:

​                                                   Tmedia = (Tmax + Tmin) /2                                                     (Ecuación 3)

calculada por periodos de 24 horas, tres mediciones diarias son las que realiza una estación meteorológica.

​                                        *Tabla 1. Coeficientes estacionales de consumo para varios cultivos.*

![image-20220614223526270](C:\Users\csama\AppData\Roaming\Typora\typora-user-images\image-20220614223526270.png)



**Radiación extraterrestre (Ra)** 
La radiación solar puede ser medida con piranómetros, radiómetros o solarímetros. Cuando no se cuenta con piranómetros, la radiación solar puede ser generalmente estimada de la duración de la insolación. La duración real de la insolación (horas sol reales), n, se mide con un heliógrafo. Este instrumento registra períodos de sol brillante usando un globo de cristal que actúa como lente. Los rayos solares se concentran en un punto focal que quema una parte de una tarjeta especialmente calibrada para ello y colocada concéntricamente con la esfera. El movimiento del sol cambia el punto focal a lo largo del día y un rastro aparece en la tarjeta. Si se nubla, se interrumpe el rastro. Las horas de sol brillante son indicadas por la longitud de los segmentos del rastro. La cantidad de calor transmitida por el suelo, G, se puede medir con sistemas de placas de flujo de calor en el suelo y con termopares.

Procedimiento de cálculo:
La radiación que choca a una superficie perpendicular a los rayos del sol en el extremo superior de la atmósfera terrestre se llama constante solar, y tiene un valor aproximado de 0.082 (MJ/m)/min. La intensidad local de la radiación, sin embargo, está determinada por el ángulo entre la dirección de los rayos solares y la superficie de la atmósfera. Este ángulo cambia durante el día y es diferente en diversas latitudes y en diversas épocas del año. La radiación solar recibida en la parte superior de la atmósfera terrestre sobre una superficie horizontal se conoce como radiación (solar) extraterrestre, Ra. Si el sol se encuentra directamente encima de la cabeza, el ángulo de incidencia es cero y la radiación extraterrestre es 0.082 (MJ/m)/min. Así como las estaciones cambian, la posición del sol, la longitud del día y la radiación extraterrestre también cambian. La radiación extraterrestre es entonces una función de la latitud, la época del año y la hora del día. Los valores de Ra a lo largo del año para diversas latitudes se presentan en la Ilustración 2 Variación anual de la radiación extraterrestre (Ra) en el ecuador, a los 20° y 40° de latitud norte y sur.

![image-20220614223715996](C:\Users\csama\AppData\Roaming\Typora\typora-user-images\image-20220614223715996.png)

*Ilustración 2 Variación anual de la radiación extraterrestre (Ra) en el ecuador, a los 20° y 40° de latitud norte y sur.*



**Radiación extraterrestre para periodos diarios (Ra)**
La radiación estraterrestre, Ra, para cada día del año y para diversas latitudes se puede estimas a partir de la constante solar, la declinación solar y la época del año:
Ra = [(24 * 60)/ PI]  * Gsc * dr * [Ws * sin (Q) * sin(d) + cos(Q) * cos(d) * sin(W)]                           (Ecuación 4)

Donde:
Ra	  	radiación extraterrestre, [(MJ/m)/día]
Gsc		constante solar = 0.082 (MJ/m)/m
dr	   	distancia relativa inversa Tierra-Sol  (Ecuación 5)
Ws	 	ángulo de radiación a ala puesta del sol [rad] (Ecuación 7 u 8) 
Q 		  latitud [rad] (calcular)
 d		   declinación solar [rad] (Ecuación 6)



Ra se expresa en (MJ/m)/día en la Ecuación 4. La latitud  Q, se expresa en radianes es positiva ora el hemisferio norte y negativa para el hemisferio sur.

La distancia relativa inversa Tierra-Sol, dr;  y la declinación solar, d, estan dadas por:

​                                 dr = 1 + 0.033 * cos [((2 * PI) / 365) * J]                                                       (Ecuación 5)



​                                  d = 0.409 * sen [((2* PI) / 365) * J - 1.39]                                                    (Ecuación 6)

donde J es el número del día en el año entre el 1 (1 de enero) y 365 (31 de diciembre). Los valores de J para todos los días del año y una ecuación para estimar su valor se presentan en  el Anexo 1, Cuadro 1.

El ángulo de radiacion a la hora de la puesta del sol, Ws, se da por:

​                                Ws = arccos [- tan (Q) * tan(d)]                                                                       (Ecuación 7)

Como la función de los arccos no están disponible en todos los lenguajes de programación, el ángulo de radiación a la hora de la puesta del sol se puede también calcular usando la función arctan:

​                                Ws  = (PI / 2) - arctan[(-tan(Q) * tan(d)) / (X ^ 0.5) ]                                      (Ecuación 8)

donde:
                                      X = 1- [tan (Q)]^2*[tan(d)]^2
                                   y X = 0.00001 si X<=0



Los valores de Ra para diversas latitudes se presentan en el Anexo 1. Cuadro 2. Estos valores representan Ra en el día 15 de cada mes. Estos mismos valores se desvían de valores promedio de los valores diarios del mes en menos del 1% para todas las latitudes durante periodos libres de hielo y se incluyen para simplificar el cálculo. Estos valores se desvían levemente de los valores en los Cuadros Smithsonianos. Para los meses invernales en latitudes mayores a 55° (N o S), las ecuaciones de Ra, tienen validez limitada. se debe comparar con los valores presentados en los Cuadros Smithsonianos para evaluar posibles desviaciones.

Dado todo los anterior, para el proyecto a desarrollar, cuyo "cultivo" es pasto en un jardín; éste tiene un Kc similar a la alfalfa. El lugar en el que se encuentra ubicado se encuentra en 20° latitud Norte.

El Kc, varía principalmente en función de las características particulares del cultivo, variando solo en una pequeña proporción en función del clima.



**Cantidad de Agua**

La cantidad de agua requerida para compensarla pérdida por evapotranspiración de un campo cultivado, se define como requerimiento de agua del cultivo. Aunque los valores para ETc (evapotranspiración del cultivo) y requerimiento de agua del cultivo son idénticos, el requerimiento de agua del cultivo se refiere a la cantidad de agua que necesita ser suplida, mientras que la ETc se refiere a la cantidad de agua que se pierde por evapotranspiración. El requerimiento de agua de riego generalmente, se refiere a la diferencia entre el requerimiento del cultivo y la precipitación efectiva. El requerimiento de agua de riego, también incluye agua adicional para el lavado de sales y para la compensación por la no uniformidad de la aplicación del agua.

Para que un cultivo reciba la cantidad necesaria de agua se requiere un poco más de este líquido, lo que se denomina **Lámina Bruta de Riego**. Esta cantidad depende del sistema que se tenga. Para el goteo se estima una eficiencia (Er) del 90 al 95%, para la aspersión se estima una eficiencia del 80 al 85%; con esta eficiencia obtenemos la cantidad de milímetros que debemos aplicar, de la siguiente manera:

​                      Requerimiento de riego (RR) o Lámina Bruta ( db) = ETc/Eficiencia            (Ecuación 9)

​                                                                              RR=5.33/.80

​                                                                                 RR= 6.6625 mm = 0.0066625 m

Con el dato anterior podemos obtener el volumen de agua de cada área a regar   (G).
   
​                                      G = RR * A   m3                                                     (Ecuación 10)

 Donde: 

RR o db               Requerimiento de riego o lámina bruta (m)

A                     Área a regar (m2)     


Seccion 1: (Oficina) 94 m2              G =0.0066625 * 94 = 0.6227 m3
Seccion 2: (Casa) 124 m2                G =0.0066625 * 124 = 0.8215 m3
Seccion 3: (Lago) 140 m2                G =0.0066625 * 140 = 0.924 m3
 

Ahora necesito saber ¿cuánto tiempo debo regar para darle a la planta esta cantidad de 

agua?, a esto se le llama Tiempo de aplicación (Ta):

Ta = G / Ga

Donde: 
G =es el volumen de agua por area

Ga = Gasto de agua por sección
     Sumatoria de número de aspersores * gasto de cada uno (Lt/min)

Seccion 1: 10 rociadores con un Ga = 9 Lt/min cada uno = 90 Lt/min = 0.090 m3/min
Seccion 2: 5 aspersores con un Ga = 18 Lt/min cada uno = 90 Lt/min = 0.090 m3/min
Seccion 3: 5 aspersores con un Ga = 18 Lt/min cada uno = 90 Lt/min = 0.090 m3/min

Entonces el Tiempo de aplicación de agua seria: 

Seccion: 1     Ta =  0.6227/0.090   = 6.91 min            
Seccion 2      Ta =  0.98215/0.090  = 9.12 min                   
Seccion 3      Ta =  0.924/0.090    = 10.26 min                                 
 




 

 

 

# Anexo 1

### Cuadro 1

![image-20220614224905008](C:\Users\csama\AppData\Roaming\Typora\typora-user-images\image-20220614224905008.png)

### Cuadro 1 (*Continuación...*)

![image-20220614225000006](C:\Users\csama\AppData\Roaming\Typora\typora-user-images\image-20220614225000006.png)

### Cuadro 2

![image-20220614225109406](C:\Users\csama\AppData\Roaming\Typora\typora-user-images\image-20220614225109406.png)
