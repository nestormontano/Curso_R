<style>
.small-code pre code {
  font-size: 1em;
}
</style>



PROGRAMACIÓN Y DATA SCIENCE CON R
========================================================
author: Nestor Montaño
date: Octubre.2017
autosize: true
transition: rotate
<small> 
Vicerrectorado de Formación Académica y Profesional    
Universidad de Guayaquil
</small>






Estadística Inferencial - Pruebas de hipótesis
========================================================
type: sub-section







Algunas de las Pruebas disponibles
========================================================



Prueba de Hipótesis                                                   | En R
--------------------------------------------------------------------- | -------------------
T-test para la media de una muestra                                   | t.test(x, mu, alternative)
Prueba de los rangos con signo de Wilcoxon para la mediana            | wilcox.test(x, mu, alternative)
Prueba de hipótesis para proporciones                                 | prop.test(x, n, p)
Prueba ji-cuadrado de bondad de ajuste (frecuencias vs probabilidades)| chisq.test(x, p)
Prueba de Normalidad de Shapiro                                       | shapiro.test(x)
Prueba de bondad de ajuste de Kolmogorov Smirnov                      | ks.test(x, y, ...)
T-test para comparar medias de dos muestras (Varianzas iguales)       | t.test(x, y, alternative, var.equal= TRUE)






Algunas de las Pruebas disponibles
========================================================



Prueba de Hipótesis                                                   | En R
--------------------------------------------------------------------- | -------------------
T-test para comparar medias de dos muestras (Varianzas diferentes)    | t.test(x, y, alternative, var.equal= FALSE)
Prueba Mann-Whitney / Wilcoxon rank para dos muestras                 | wilcox.test(x, y, alternative)
T-test para comparar medias de dos muestras pareadas                  | t.test(x, y, alternative, paired= TRUE)
Prueba Mann-Whitney / Wilcoxon rank para dos muestras pareadas        | wilcox.test(x, y, alternative, paired= TRUE)
Prueba F para comparas la varianza de dos muestras normales           | var.test(x, y, ratio= 1)
Prueba Ansari-Bradley para comparar la varianza de dos muestras       | ansari.test(x, y)
Prueba para correlacion entre dos variables pariadas (cor= 0)         | cor.test(x, y)





Algunas de las Pruebas disponibles
========================================================



Prueba de Hipótesis                                                   | En R
--------------------------------------------------------------------- | -------------------
Prueba ji-cuadrado de Pearson para independencia de dos variables categoricas   | chisq.test(x, y) o  chisq.test(table)
Prueba exacta de Fisher para independencia de dos variables categoricas         | fisher.test(x, y) o  fisher.test(table)
ANOVA de una via (todas las medias son iguales)                       | aov(x~ y, data), summary
ANOVA: Prueba T para comparar cada par de niveles                     | pairwise.t.test(x, y)
ANOVA: Calcular Test HSD de Tukey                                     | TukeyHSD(results, conf.level = 0.95)
Prueba de Kruskal Wallis para igualdad de la distribución de cada subgrupo   | kruskal.test(x~ y, data)
ANOVA Factorial                                                       | aov(x~ y * z, data), summary
ANCOVA                                                                | aov(x~ y + z, data), summary
MANOVA                                                                | manova(cbind(x1, x2)~ y1 + y2 , data), summary





Caso - Data de Banco
========================================================

Le han pedido determinar si los tiempos que demora cada transacción del cliente dependen de la sucursal en donde se realiza el trámite.   
*Para determinar esto debemos ejecutar un análisis de varianza donde nuestra variable es el tiempo de demora de cada transacción y el factor es la sucursal.*






Importar Data
========================================================
class: small-code

Importar los datos a utilizar y cambiar los tipos de datos (como en el capitulo 4)


```r
# Cargar paquete
library("openxlsx")
# Leer data
data_banco <- read.xlsx("Data/Data_Banco.xlsx", sheet = "Data")
# La Satisfaccion es una variable categórica ordinal
data_banco$Satisfaccion <- factor(data_banco$Satisfaccion, levels= c('Muy Malo', 'Malo', 'Regular', 'Bueno', 'Muy Bueno'))
# La Sucursal y el Cajero deben ser categórica nominales
data_banco$Sucursal <- as.character(data_banco$Sucursal)
data_banco$Cajero <- as.character(data_banco$Cajero)
```





Caso - Data de Banco
========================================================
class: small-code
Realizar Anova

```r
## Anova
results <- aov( Tiempo_Servicio_seg ~ as.factor(Sucursal),
                data= data_banco)
summary(results)
```

```
                       Df   Sum Sq Mean Sq F value Pr(>F)    
as.factor(Sucursal)     4   950649  237662   353.6 <2e-16 ***
Residuals           24294 16327084     672                   
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```



Caso - Data de Banco
========================================================

Le han pedido determinar si los tiempos que demora cada transacción del cliente dependen de la sucursal en donde se realiza el trámite.   
*Para determinar esto debemos ejecutar un análisis de varianza donde nuestra variable es el tiempo de demora de cada transacción y el factor es la sucursal.*    
**El valor “<2e-16 ***” indica que se rechaza Ho. Ahora ¿Cuál sucursal es diferente?**



Caso - Data de Banco
========================================================
class: small-code
Encontrar la sucursales que difieren

```r
## Encontrar la sucursal diferente
## Pruebas t entre todos los niveles
pairwise.t.test(data_banco$Tiempo_Servicio_seg,
                as.factor(data_banco$Sucursal))
```

```

	Pairwise comparisons using t tests with pooled SD 

data:  data_banco$Tiempo_Servicio_seg and as.factor(data_banco$Sucursal) 

    267    443    586    62    
443 <2e-16 -      -      -     
586 0.65   <2e-16 -      -     
62  <2e-16 <2e-16 <2e-16 -     
85  <2e-16 0.96   <2e-16 <2e-16

P value adjustment method: holm 
```



Caso - Data de Banco
========================================================
class: small-code
Encontrar la sucursales que difieren

```r
## Prueba Tukey Honest Significance Test
TukeyHSD(results, conf.level = 0.95)
```




Caso - Data de Banco
========================================================

Ahora le piden analizar también el tipo de transacción e incluso si la transacción y hay transacciones que demoran más en una sucursal que en otra

*Análisis de varianza donde nuestra variable es el tiempo de demora de cada transacción y el factor es el tipo de transacción*



Caso - Data de Banco
========================================================
class: small-code

```r
## ANOVA 2 factores ---------
results <- aov( Tiempo_Servicio_seg ~ as.factor(Sucursal) * Transaccion,
                data= data_banco)
summary(results)
```

```
                                   Df   Sum Sq Mean Sq F value Pr(>F)    
as.factor(Sucursal)                 4   950649  237662  379.93 <2e-16 ***
Transaccion                         2  1050276  525138  839.48 <2e-16 ***
as.factor(Sucursal):Transaccion     8    85925   10741   17.17 <2e-16 ***
Residuals                       24284 15190884     626                   
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```





Caso - Data de Banco
========================================================
class: small-code
Encontrar la sucursales que difieren

```r
## Prueba Tukey Honest Significance Test
TukeyHSD(results, conf.level = 0.95)
```




Caso - Data de Banco
========================================================
class: small-code
Encontrar la sucursales que difieren

```r
## Explorar el resultado de TukeyHSD para pasarlo a data.frame
tukey_objeto <- TukeyHSD(results, conf.level = 0.95)
tukey_objeto
View(tukey_objeto)
as.data.frame(tukey_objeto)
str(tukey_objeto )

View(as.data.frame(tukey_objeto$`as.factor(Sucursal)`) )
View(as.data.frame(tukey_objeto$Transaccion) )
View(as.data.frame(tukey_objeto$`as.factor(Sucursal):Transaccion`))
```



Caso - Data de Banco
========================================================

Finalmente, le preguntan si los niveles de satisfacción reportados dependen del tipo de transacción realizada.

*Realizaremos una prueba de hipótesis para evaluar si el nivel de satisfacción está relacionado con el tipo de transacción*



Caso - Data de Banco
========================================================
class: small-code

```r
## Tabla de contingencia
tb_conting_obs <- table(data_banco$Satisfaccion,
			 data_banco$Transaccion)

## Prueba de hipotesis
chisq.test(tb_conting_obs) 
```

```

	Pearson's Chi-squared test

data:  tb_conting_obs
X-squared = 380.71, df = 8, p-value < 2.2e-16
```



Problema - Gasto en Publicidad
========================================================

Se pide evaluar si la venta aumenta mientras se realizan promociones con famosos



Problema - Gasto en Publicidad
========================================================
class: small-code
<small>Importar data</small>

```r
# Importacion de datos ----------------------------------------------------
## Data de venta
data_venta_publicidad <- read.xlsx(xlsxFile = "Data/Venta_vs_Publicidad.xlsx", detectDates = TRUE)  
str(data_venta_publicidad)
```

```
'data.frame':	79 obs. of  8 variables:
 $ SEMANAS         : Date, format: "2015-01-05" "2015-01-12" ...
 $ VENTA           : num  151034 186849 133808 135690 199173 ...
 $ PUBLICIDAD_TOTAL: num  1200 1750 1450 1700 1900 1550 1150 2400 650 2000 ...
 $ TV              : num  300 612 450 544 722 ...
 $ RADIO           : num  276 473 493 289 361 ...
 $ PERIODICO       : num  624 473 218 408 209 ...
 $ REDES           : num  0 192 290 459 608 ...
 $ USA_FAMOSO      : chr  "NO" "NO" "NO" "NO" ...
```



Problema - Gasto en Publicidad
========================================================
class: small-code
<small>T-test para comparar medias de dos muestras (Varianzas diferentes)</small>

```r
## Prueba de hipotesis
t.test(x = data_venta_publicidad$VENTA[ data_venta_publicidad$USA_FAMOSO == "SI"], 
       y = data_venta_publicidad$VENTA[ data_venta_publicidad$USA_FAMOSO == "NO"],
       alternative = "greater",
       var.equal = FALSE)
```

```

	Welch Two Sample t-test

data:  data_venta_publicidad$VENTA[data_venta_publicidad$USA_FAMOSO ==  and data_venta_publicidad$VENTA[data_venta_publicidad$USA_FAMOSO ==     "SI"] and     "NO"]
t = 0.046654, df = 47.527, p-value = 0.4815
alternative hypothesis: true difference in means is greater than 0
95 percent confidence interval:
 -18282.48       Inf
sample estimates:
mean of x mean of y 
 152389.1  151866.1 
```




Problema - Gasto en Publicidad
========================================================
class: small-code
<small>Prueba Mann-Whitney / Wilcoxon rank para dos muestras</small>

```r
## Prueba de hipotesis
wilcox.test(x = data_venta_publicidad$VENTA[ data_venta_publicidad$USA_FAMOSO == "SI"], 
            y = data_venta_publicidad$VENTA[ data_venta_publicidad$USA_FAMOSO == "NO"], 
            alternative = "greater")
```

```

	Wilcoxon rank sum test with continuity correction

data:  data_venta_publicidad$VENTA[data_venta_publicidad$USA_FAMOSO ==  and data_venta_publicidad$VENTA[data_venta_publicidad$USA_FAMOSO ==     "SI"] and     "NO"]
W = 705, p-value = 0.4897
alternative hypothesis: true location shift is greater than 0
```





Caso Banco - Prueba de Bondad de ajuste
========================================================
class: small-code
<small>¿Se puede decir que el tiempo de atención en el banco sigue una distribución normal?</small>

```r
## Prueba de hipotesis
ks.test( data_banco$Tiempo_Servicio_seg, "dnorm", 
         mean(data_banco$Tiempo_Servicio_seg), 
         data_banco$Tiempo_Servicio_seg)
```

```

	One-sample Kolmogorov-Smirnov test

data:  data_banco$Tiempo_Servicio_seg
D = 0.99991, p-value < 2.2e-16
alternative hypothesis: two-sided
```



Ejemplo de Bondad de ajuste entre dos muestras
========================================================
class: small-code


```r
## Se crean dos vectores simulados
x <- rnorm(100, mean = 10, sd = 2)
y <- runif(80, min = 0, max = 14)
# Comparar si los vectores vienen de la misma distribucion
ks.test(x, y)
```

```

	Two-sample Kolmogorov-Smirnov test

data:  x and y
D = 0.585, p-value = 1.377e-14
alternative hypothesis: two-sided
```



 
Gracias
========================================================
type: sub-section
