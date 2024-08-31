### Ejercicio 2:
_La gerenta de operaciones de una planta desea estudiar las fallas que se observan en el proceso de envasado. Los datos sin procesar que se muestran a continuación, corresponden a la falla
principal registrada en 50 envases con fallas, los cuales se tomaron de la producción de una semana. Se codificó con A al etiquetado incorrecto, con B al envase roto, con C al envase
manchado, con D al envase arrugado, con E al etiquetado ilegible y con F al envase agrietado._  
a) Plantee un problema de interés para el estudio.  
b) Realice el análisis descriptivo completo de los datos obtenidos. Interprete los resultados.  
c) ¿Sobre qué tipo de falla aconsejaría trabajar con prioridad para corregirla y a futuro evitarla?  
Redacte un breve informe (un párrafo) respondiendo al problema planteado.  

**Respuestas**  
a) Un problema de interés podría ser conocer el tipo de falla más frecuente.  
b) Población: envases con fallas.  n=50  Variable: tipo principal de falla.  Unidad elemental: cada envase con falla  
Para ingresar los datos, vamos utilizar a la base compartida en el siguiente [link](https://docs.google.com/spreadsheets/d/1xKcbw0QxgRQ1wqeUUSqDMvSKyJDyDlw0KyCG5Sb0-Q0/edit#gid=802639518), ir a la página correspondiente al ejercicio 2 (ej 2). Luego seleccionar los datos y copiarlos al _portapapeles_ utilizando ctrl+c.  
En la consola o script de trabajo correr la siguiente línea:
```
datos_2<-read.delim("clipboard",col.names = c("Fallas")) # al ser una sola columna no es necesario utilizar c(""), yo lo hago para mantener la misma linea.
```
Con los comandos _table_ y _as.data.frame_ generamos la tabla de frecuencias:  
```
tabla<-as.data.frame(table(datos_2))
sum(tabla$Freq) # de esta manera corroboramos que estén todos los datos ya que la suma debe dar igual a n.
sum(tabla[,2]) # esta es otra manera de indicarle la columna que quiero sumar. La puedo llamar por nombre como en la linea anterior utilizando '$' o le puedo indicar entre '[]' el número de columna. Recordar que en R el orden es [fila,columna].
min(tabla2$Freq) #chequeo los valores mínimos y máximos max(tabla2$Freq)
class(tabla) # de este modo verifico qué clase de objeto es. Puede ser matrix, data frame, string, character, numeric, factor...
```
A continuación generamos una nueva columna llamada Prop en la cual almacenaremos los valores de las proporciones  
```
tabla$Prop<-tabla$Freq/sum(tabla$Freq) # Agrego la columna 'Prop' en la cual ingreso el cálculo de las proporciones o frecuencias relativas.
```
Luego realizaremos un gráfico de barras horizontales
```
windows() # este comando es para ajustar el gráfico al espacio de trabajo, no es necesario correrlo
barplot(table(datos_2), # datos
        main= "Frecuencia de fallas",
        xlim=c(0,20), # vector que indica los valores mínimos y máximos del eje horizontal
        xlab="Frecuencia", # rotulo del eje horizontal
        ylab="Tipos de Falla", # rotulo del eje vertical
        horiz=TRUE) # pedimos que sea horizontal 
```
Les recomendamos explorar todas las opciones que la funcion barplot ofrece para mejorar nuestro gráfico, pueden acceder al siguiente [link](https://r-coder.com/grafico-barras-r/).  
c) La falla B es la de mayor frecuencia.

### Ejercicio 4:
_De una máquina que fabrica piezas especiales, se registra el número de piezas defectuosas producidas por día. Para un mes en particular (30 días), se conoce lo siguiente: Solo 1 día de los que estuvo en funcionamiento produjo 4 piezas defectuosas y ningún otro día superó ese valor. En 19 días no produjo piezas defectuosas. El 10% de los días produjo 2 piezas defectuosas. El 80% de los días produjo a lo sumo 1 pieza defectuosa._
a) Plantee un objetivo de interés para el estudio.  
b) Determine unidad elemental, población y variable en estudio.  
c) Construya una tabla de frecuencias de la distribución del número diario de piezas defectuosas que produjo la máquina en el período considerado.  
d) Construya un gráfico que muestre los datos de la tabla.  

**Respuestas**  
a) Un objetivo de interés puede ser _"Determinar la eficiencia del proceso a través del análisis de la distribución diaria del número de piezas defectuosas podrucidas por ésa máquina durante un mes"._  
b) Unidad elemental: cada día de producción. Población: todos los días de producción de la máquina durante un mes. Variable en estudio: número de piezas defectuosas producidas por la máquina, por día.  
c) Para construir la tabla de frecuencias primero debemos interpretar los datos, la variabla cantidad de piezas defectuosas toma los valores 0, 1, 2, 3 y 4. Luego, sabemos que a Y=4 le corresponde una frecuencia de 1; a Y=0 le corresponde una frecuencia de 19 (ya que fueron 19 días en los cuales no se registraron piezas defectuosas); a Y=2 le corresponde 3 y a Y=1 le corresponde (0.8*30)-19 = 5 días.  
En R podríamos armar la tabla con el siguiente código:  
```
tabla_4<-data.frame(
   "Fallas"=c(0,1,2,3,4),
   "Frecuencia"=c(19,5,3,2,1))
```
d)
```
barplot(tabla_4$Días~tabla_4$Fallas, # con el ~ indicamos y vs x
        ylab="Frecuencia (días)", # indicamos los nombres del eje y
        xlab="Cantidad de fallas", # indicamos los nombres del eje x
        ylim=c(0,(max(tabla_4$Días)+5)), # seteamos la extensión del eje y en función del valor más alto observado
        space=c(3, 3, 3, 3), # ajustamos las distancias entre bastones o barras
        col="lightgreen") # asignamos un color
```
### Ejercicio 7:
_Los siguientes datos corresponden a 20 observaciones del tiempo (en segundos) que un cliente esperó al teléfono al representante de un determinado servicio: 7 - 7 - 15 - 21 - 15 - 22 - 40 - 8 - 40 - 6 - 18 - 14 - 5 - 7 - 8 - 3 - 8 - 4 - 40 - 5_  
a) Identifique unidad de observación, población, población estadística.  
b) Indique si la población es finita o infinita.  
c) Realice el gráfico que considere adecuado teniendo en cuenta que son pocos datos.  
d) Plantee un parámetro que sea de interés estimar como objetivo en este problema.  

**Respuestas**  
a) unidad de observación: llamada telefónica  
variable: tiempo de espera  
población: todas las llamadas telefónicas  
población estadística: todos los tiempos de espera del cliente  
b) finita  
c) Si descargamos el archivo .xlsx podemos leer los datos de la siguiente manera, siempre y cuando hayamos seteado el directorio de trabajo y guardado el archivo en dicho directorio:  
```
library("readxl")
datos_7<- read_excel("Datos U2.xlsx", 
                   sheet = "ej 7") #se indica la hoja donde están los datos a copiar
```
Para renombrar la columa podemos utilizar la función 'colnames' de rbase pero vamos usar otro recurso y comenzar a introducirnos en el universo de [Tidyverse](https://www.tidyverse.org/packages/), que es un conjunto de paquetes que permiten mejorar el acceso, manipulación y visualización de datos.
```
install.packages("tidyverse")
library("tidyverse")
colnames(datos_7) # chequeamos el nombre
datos<-rename(datos_7, # indicamos el objeto sobre el que vamos a aplicar la función
              Tiempo='Tiempo de espera') # indicamos primero a qué queremos cambiar y luego qué debe cambiar
colnames(datos_7) # chequeamos el cambio
```
_Considerando que el enunciado indica que son pocos datos diferentes, podemos realizar un diagrama de tallo y hoja_.  
Utilizaremos la función stem de rbase, encontraremos la salida en la consola
```
stem(datos_7$Tiempo) # con el símbolo $ indicamos sobre qué columna (variable) queremos que realice el diagrama
```
d) Tiempo de espera promedio.  

### Ejercicio 12:
_Un fabricante de componentes electrónicos está interesado en conocer el comportamiento del tiempo de vida de cierto tipo de baterías para computadoras que produce. Para ello analiza la duración (en horas) de una muestra de 15 baterías y obtiene los siguientes valores: 123 - 121 - 116 - 122 - 109 - 180 - 126 - 111 - 118 - 115 - 125 - 117 - 110 - 112 - 124_
a) Construya un diagrama de tallo y hoja y un diagrama de puntos.  
b) Obtenga e interprete diferentes medidas de localización de este conjunto.  
c) Indique si se trata de estadísticos o parámetros. Justifique  

**Respuestas**  
a) Ingresamos los datos corriendo la siguiente linea en la consola o script de trabajo:  
```
datos_12<-data.frame("T_vida"=c(123,121,116,122,109,180,126,111,118,115,125,117,110,112,124)) # generamos un data frame con la columna llamada T_vida con los valores indicados"  
```
El diagrama de tallo y hoja puede verse en la consola o podemos pedirlo en la sección de plots:  
```
stem(datos_12$T_vida,scale = 2) # gráfico en la consola
plot.new() # si quiero verlo en la sección de plots
out <- capture.output(stem(datos$T_vida, scale = 2)) # que va en la salida
text(0, 1, paste(out, collapse = "\n"), adj = c(0, 1))
```
Para realizar el gráfico de puntos, utilizaremos la función ggplot de tidyverse. Para comprender la sintaxis de ggplot, que se realiza en capas, puede recurrirse a la [CheatSheet](https://github.com/ImoPupato/Ejercicios-TUIA/blob/main/CheatSheet-ggplot2.pdf).
```
ggplot(datos_12, # indico qué objeto usar, 
  aes(T_vida)) + # qué variable mapear
  geom_dotplot(dotsize=0.7, color="black", fill="lightgreen", binwidth = 3) + # tipo de gráfico y características estéticas
  labs(x = "Tiempo de vida de batrías (horas)") + # nombre del eje x
  theme_classic() + # elimino el fondo del gráfico
  scale_y_continuous(expand=c(0,0), NULL, breaks = NULL) + # elimino el eje y
  scale_x_continuous(breaks = seq(min(datos_12$T_vida), max(datos_12$T_vida), by = 5))  # ajusto 'by' para aumentar los valores observados en el eje de variación
```
Como recomendación, se pueden ir graficando de a una las lineas (a excepción de la primera y segunda que deben ir juntas) para ver los cambios que cada una genera.  

b) Con el comando _summary_ obtenemos algunas medidas de posición:  
```
summary(datos_12)
```
c) Los datos son obtenidos por muestreo por lo que se trata de estadísticos.  

Podemos, además, pedir un boxplot utilizando rbase:  
```
boxplot(datos_12, 
        main= "Tiempo de vida de las baterías (horas)", 
        horizontal=TRUE, 
        col="lightgreen") 
```
### Ejercicio 16:
_Reconsidere la Actividad 12, relativa al tiempo de vida de cierto tipo de baterías._  
a) Obtenga e interprete medidas de variabilidad.  
b) Indique cuál/es de estas medidas no se ven afectadas por la presencia de valores atípicos.  

**Respuestas**  
a) Con la función sd podemos obtener el desvío estándar como medida de dispersión:  
```
sd(datos_12$T_vida) # debemos indicar la columna sobre la cual va a calcular el desvío estándar
```
Otras medidas de dispersión pueden ser el rango y el rango intercuartílico:  
```
range(datos_12$T_vida) # rango, valores máximos y mínimos observados  
IQR(datos_12$T_vida) # máxima diferencia observada en el 50% central de los datos
```
b) Tanto la media como el desvío estándar son suceptibles a valores extremos o atípicos por lo que, en nuestro caso es recomendable describir al conjunto de datos a través de Q2 (mediana) y el Rango o el Rango Intercuartil.  

### Ejercicio 20:
_Reconsidere la Actividad 4, relativa al número de piezas defectuosas producidas por día en una fábrica._  
a) Obtenga e interprete las medidas que se necesitan para construir el diagrama de caja y bigotes y constrúyalo.  
b) ¿Puede obtener alguna/s medida/s de dispersión a partir del diagrama de caja? Si es así, indique cuáles son e informe el valor de las mismas.  

**Respuestas**  
a) Con la función 'summary' tenemos todas las medidas necesarias para construir el boxplot (Q1, Q2, Q3, min y max). Pero antes debemos reorganizar los datos para poder utilizar la función:  
```
datos_20<- data.frame("x"=c(rep(0,19),rep(1,5),rep(2,3),rep(3,2),rep(4,1)))
summary(datos_20)
```
min= La menor cantidad de fallas observadas por día es 0  
Q1= El 25% de los días se obtuvieron piezas sin fallas  
Q2= El 50% de los días se obtuvieron piezas sin fallas  
Q3= El 75% de los días se obtuvieron piezas con 1 falla o menos    
max= El máximo de fallas obtenido es 4  
b) A través del boxplot podemos obtener el rango y el rango intercuartil. El rango es 0-4 y el rango intercuartil es 1.

```
boxplot(data,
        horizontal = TRUE,
        xlab="Cantidad de Fallas",
        col="lightgreen")
```
