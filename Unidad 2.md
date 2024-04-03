### Actividades propuestas (p.99)

#### Ejercicio 2:
_La gerenta de operaciones de una planta desea estudiar las fallas que se observan en el proceso de envasado. Los datos sin procesar que se muestran a continuación, corresponden a la falla
principal registrada en 50 envases con fallas, los cuales se tomaron de la producción de una semana. Se codificó con A al etiquetado incorrecto, con B al envase roto, con C al envase
manchado, con D al envase arrugado, con E al etiquetado ilegible y con F al envase agrietado._  
a) Plantee un problema de interés para el estudio.  
b) Realice el análisis descriptivo completo de los datos obtenidos. Interprete los resultados.  
c) ¿Sobre qué tipo de falla aconsejaría trabajar con prioridad para corregirla y a futuro evitarla?  
Redacte un breve informe (un párrafo) respondiendo al problema planteado.  

**Respuestas**  
a) Un problema de interés podría ser conocer el tipo de falla más frecuente.  
b) Realice el análisis descriptivo completo de los datos obtenidos. Interprete los resultados.  
Población: envases con fallas.  
n=50  
Variable: tipo principal de falla  
unidad elemental: cada envase con falla  
Para ingresar los datos, vamos utilizar a la base compartida en el siguiente [link](https://docs.google.com/spreadsheets/d/1xKcbw0QxgRQ1wqeUUSqDMvSKyJDyDlw0KyCG5Sb0-Q0/edit#gid=802639518), ir a la página correspondiente al ejercicio 2 (ej 2). Luego seleccionar los datos y copiarlos al _portapapeles_ utilizando ctrl+c.  
En la consola o script de trabajo correr la siguiente línea:
```
datos<-read.delim("clipboard",col.names = c("Fallas")) # al ser una sola columna no es necesario utilizar c(""), yo lo hago para mantener la misma linea.
```
Con los comandos _table_ y _as.data.frame_ generamos la tabla de frecuencias:  
```
tabla<-as.data.frame(table(datos))
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
barplot(table(datos), # datos
        main= "Frecuencia de fallas",
        xlim=c(0,20), # vector que indica los valores mínimos y máximos del eje horizontal
        xlab="Frecuencia", # rotulo del eje horizontal
        ylab="Tipos de Falla", # rotulo del eje vertical
        horiz=TRUE) # pedimos que sea horizontal 
```
Les recomendamos explorar todas las opciones que la funcion barplot ofrece para mejorar nuestro gráfico, pueden acceder al siguiente [link](https://r-coder.com/grafico-barras-r/).  
c) La falla B es la de mayor frecuencia.

#### Ejercicio 7:
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
datos<- read_excel("Datos U2.xlsx", 
                   sheet = "ej 7") #se indica la hoja donde están los datos a copiar
colnames(datos)<-"Tiempo" # renombramos la columna
summary(datos) # medidas resumen
stem(datos$Tiempo) # diagrama de tallo y hoja
```
d) Tiempo de espera promedio.  

#### Ejercicio 12:
_Un fabricante de componentes electrónicos está interesado en conocer el comportamiento del tiempo de vida de cierto tipo de baterías para computadoras que produce. Para ello analiza la duración (en horas) de una muestra de 15 baterías y obtiene los siguientes valores: 123 - 121 - 116 - 122 - 109 - 180 - 126 - 111 - 118 - 115 - 125 - 117 - 110 - 112 - 124_
a) Construya un diagrama de tallo y hoja y un diagrama de puntos.  
b) Obtenga e interprete diferentes medidas de localización de este conjunto.  
c) Indique si se trata de estadísticos o parámetros. Justifique  
**Respuestas**  
a) Ingresamos los datos corriendo la siguiente linea en la consola o script de trabajo:
```
datos<-c(123,121,116,122,109,180,126,111,118,115,125,117,110,112,124)
```
El diagrama de tallo y hoja puede verse en la consola o podemos pedirlo en la sección de plots:  
```
stem(datos,scale = 2) # gráfico en la consola
plot.new() # si quiero verlo en la sección de plots
out <- capture.output(stem(datos, scale = 2)) #que va en la salida
text(0, 1, paste(out, collapse = "\n"), adj = c(0, 1))
```
b) Con el comando _summary_ obtenemos algunas medidas de posición:
```
summary(datos)
```
Con la función sd podemos obtener el desvío estándar como medida de dispersión:
```
sd(datos)
```
c) Los datos obtenidos son de muestras por lo que se trata de estadísticos.  
Podemos, además, pedir un boxplot:
```
boxplot(datos, main= "Tiempo de vida de las baterías", horizontal=TRUE)
```
