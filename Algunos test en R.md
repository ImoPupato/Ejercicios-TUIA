- Intervalo para μ
```R
t.test(x, #vector con los valores
       alternative = "two.sided",
       mu = , #valor del parámetro 
       conf.level = 0.95) # nivel de confianza (1-𝛼)
```
En la salida vamos a encontrar la sentencia: 
```R
95 percent confidence interval:
  Límite inferior   Límite superior
```

- Intervalo para π
```R
prop.test(x, # número de casos favorables o exitos (puede estar como vector o trabla)
       n, # número de casos totales
       alternative = "two.sided",
       conf.level = 0.95) # nivel de confianza (1-𝛼)
```

- Intervalo para $σ^2$ *(hay que instalar un paquete)*
```R
library("EnvStats")
varTest(x, #vector con los valores
       alternative = "two.sided",
       conf.level = 0.95, correct = TRUE) # nivel de confianza (1-𝛼)
```
