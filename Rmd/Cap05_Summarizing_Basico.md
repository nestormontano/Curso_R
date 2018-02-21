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



Resumiendo información - Summarizing
========================================================
type: sub-section




Resumiendo filas o columnas
========================================================

rowSums, colSums, rowMeans, colMeans calcula sumas o medias de filas o columnas según indica su nombre, son un caso particular de apply.


```r
# Cargar paquete con datasets para utilizar
library('datasets')
# Ver cabecera de iris, dataframe a usar
head(iris, n=4)
```

```
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
```



Resumiendo filas o columnas
========================================================

Reciben sólo matrices

```r
rowSums(iris[1:3 , -5])
```

```
   1    2    3 
10.2  9.5  9.4 
```

```r
colSums(iris[ , -5])
```

```
Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
       876.5        458.6        563.7        179.9 
```



Resumiendo filas o columnas
========================================================

Reciben sólo matrices

```r
rowMeans(iris[1:3 , -5])
```

```
    1     2     3 
2.550 2.375 2.350 
```

```r
colMeans(iris[ , -5])
```

```
Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    5.843333     3.057333     3.758000     1.199333 
```



Aplicar una función a una fila o columna usando apply()
========================================================

Para aplicar una función a parte de un array/matrix se usa apply

```r
# Aplicar la funcion mean a las 3 primeras filas de iris
apply(iris[1:3 , -5], 1, mean)
```

```
    1     2     3 
2.550 2.375 2.350 
```

```r
# Aplicar la funcion mean a las columnas de iris
apply(iris[ , -5], 2, mean)
```

```
Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    5.843333     3.057333     3.758000     1.199333 
```



Aplicar una función a una fila o columna usando apply()
========================================================


```r
# Crear una matriz con un NA para pruebas
m1 <- 1:20
dim(m1) <- c(5, 4)
m1[3, 3] <- NA
m1
```

```
     [,1] [,2] [,3] [,4]
[1,]    1    6   11   16
[2,]    2    7   12   17
[3,]    3    8   NA   18
[4,]    4    9   14   19
[5,]    5   10   15   20
```



Aplicar una función a una fila o columna usando apply()
========================================================


```r
# Aplicar función max a las filas de m1
apply(X= m1, MARGIN= 1, FUN= max)
```

```
[1] 16 17 NA 19 20
```

```r
# Aplicar función max a las columnas de m1
apply(X= m1, MARGIN= 2, FUN= max)
```

```
[1]  5 10 NA 20
```



Aplicar una función a una fila o columna usando apply()
========================================================


```r
# Aplicar función max a las filas de m1
apply(X= m1, MARGIN= 1, FUN= max, na.rm= TRUE)
```

```
[1] 16 17 18 19 20
```

```r
# Aplicar función max a las columnas de m1
apply(X= m1, MARGIN= 2, FUN= max, na.rm= TRUE)
```

```
[1]  5 10 15 20
```



Aplicar una función a una fila o columna usando apply()
========================================================


```r
# Aplicar función paste a las filas de m1
apply(X= m1, MARGIN= 1, FUN= paste, collapse=',')
```

```
[1] "1,6,11,16"  "2,7,12,17"  "3,8,NA,18"  "4,9,14,19"  "5,10,15,20"
```

```r
# Aplicar función personalizada a las columnas de m1
apply(X= m1, MARGIN= 2, FUN= function(x, y){
  y*sum(x, na.rm= TRUE)
}, y= 10)
```

```
[1] 150 400 520 900
```



Familia *apply() 
========================================================

- Las funciones **lapply()**, **sapply()**, y **vapply()** sirven para aplicar una función sobre un vector o lista.
- lapply() retorna una lista de la misma dimensión del objeto, donde cada elemento es el resultado de aplicar la función deseada a cada elemento de la lista original.
- Recordar que un data.frame es un caso particular de lista



Familia *apply() 
========================================================

- sapply(), y vapply() son mejoras a lapply, sapply retorna por default un vector o matrix mientras que vapply exige que se le indique la forma del output
- lapply *list apply*, sapply *simplified apply*




Familia *apply() 
========================================================


```r
# crear una lista
lst_1 <- list(a= c(NA,1:3), b= 21:29, c= matrix(1:9, 3), d= 7)
lst_1
```

```
$a
[1] NA  1  2  3

$b
[1] 21 22 23 24 25 26 27 28 29

$c
     [,1] [,2] [,3]
[1,]    1    4    7
[2,]    2    5    8
[3,]    3    6    9

$d
[1] 7
```



Familia *apply() 
========================================================


```r
# lapply retorna una lista
lapply(X= lst_1, FUN= median)
```

```
$a
[1] NA

$b
[1] 25

$c
[1] 5

$d
[1] 7
```



Familia *apply() 
========================================================


```r
# sapply simplifica por default a vector/matriz
sapply(X= lst_1, FUN= median)
```

```
 a  b  c  d 
NA 25  5  7 
```

```r
# vapply retorna elementos similares a FUN.VALUE
vapply(X= lst_1, FUN= median, FUN.VALUE= 1)
```

```
 a  b  c  d 
NA 25  5  7 
```



Familia *apply() 
========================================================


```r
# lapply retorna una lista
lapply(X= lst_1, FUN= sum)
```

```
$a
[1] NA

$b
[1] 225

$c
[1] 45

$d
[1] 7
```



Familia *apply() 
========================================================


```r
# sapply simplifica por default a vector/matriz
sapply(X= lst_1, FUN= sum)
```

```
  a   b   c   d 
 NA 225  45   7 
```

```r
# vapply retorna elementos similares a FUN.VALUE
vapply(X= lst_1, FUN= sum, FUN.VALUE= 1)
```

```
  a   b   c   d 
 NA 225  45   7 
```



Familia *apply() 
========================================================


```r
# lapply retorna una lista
lapply(X= lst_1, FUN= sum, na.rm= TRUE)
```

```
$a
[1] 6

$b
[1] 225

$c
[1] 45

$d
[1] 7
```



Familia *apply() 
========================================================


```r
# sapply simplifica por default a vector/matriz
sapply(X= lst_1, FUN= sum, na.rm= TRUE)
```

```
  a   b   c   d 
  6 225  45   7 
```

```r
# vapply retorna elementos similares a FUN.VALUE
vapply(X= lst_1, FUN= sum, na.rm= TRUE, FUN.VALUE= 1)
```

```
  a   b   c   d 
  6 225  45   7 
```



Familia *apply() 
========================================================

Operadores binarios deben ser citada ''


```r
# lapply retorna una lista
lapply(X= lst_1, FUN= '^', 2)
```

```
$a
[1] NA  1  4  9

$b
[1] 441 484 529 576 625 676 729 784 841

$c
     [,1] [,2] [,3]
[1,]    1   16   49
[2,]    4   25   64
[3,]    9   36   81

$d
[1] 49
```



Familia *apply() 
========================================================

Operadores binarios deben ser citada ''


```r
# sapply simplifica por default a vector/matriz
sapply(X= lst_1, FUN= '^', 2)
```

```
$a
[1] NA  1  4  9

$b
[1] 441 484 529 576 625 676 729 784 841

$c
     [,1] [,2] [,3]
[1,]    1   16   49
[2,]    4   25   64
[3,]    9   36   81

$d
[1] 49
```

```r
# vapply será error pues no hay como coercionar la salida a 
# vector o matriz
# vapply(X= lst_1, FUN= '^', 2) ## ERROR
```



Familia *apply() 
========================================================


```r
# lapply retorna una lista
lapply(X= lst_1, FUN= fivenum)
```

```
$a
[1] 1.0 1.5 2.0 2.5 3.0

$b
[1] 21 23 25 27 29

$c
[1] 1 3 5 7 9

$d
[1] 7 7 7 7 7
```



Familia *apply() 
========================================================


```r
# sapply simplifica por default a vector/matriz
sapply(X= lst_1, fivenum)
```

```
       a  b c d
[1,] 1.0 21 1 7
[2,] 1.5 23 3 7
[3,] 2.0 25 5 7
[4,] 2.5 27 7 7
[5,] 3.0 29 9 7
```



Familia *apply() 
========================================================


```r
# vapply en FUN.VALUE se especifica la estructura resultante de la función
vapply(X= lst_1, FUN= fivenum, FUN.VALUE= rep(pi,5) )
```

```
       a  b c d
[1,] 1.0 21 1 7
[2,] 1.5 23 3 7
[3,] 2.0 25 5 7
[4,] 2.5 27 7 7
[5,] 3.0 29 9 7
```



Familia *apply() 
========================================================


```r
# vapply en FUN.VALUE se especifica la estructura resultante de la función
vapply(X= lst_1, FUN= fivenum, FUN.VALUE =  c(Min= 0, Q1= 0, Median = 0, Q3= 0, Max= 0))
```

```
         a  b c d
Min    1.0 21 1 7
Q1     1.5 23 3 7
Median 2.0 25 5 7
Q3     2.5 27 7 7
Max    3.0 29 9 7
```



Familia *apply() 
========================================================


```r
set.seed(7)
# crear un data.frame
df_1 <- data.frame(
  Alum= LETTERS[1:10], 
  Mat= round(runif(n= 10, min= 5, max= 10), 0),
  Len= c(NA, round(runif(n= 9, min= 5, max= 10), 0)),
  Edad= c(19,20)
  )
df_1
```

```
   Alum Mat Len Edad
1     A  10  NA   19
2     B   7   6   20
3     C   6   6   19
4     D   5   9   20
5     E   6   5   19
6     F   9   7   20
7     G   7   5   19
8     H  10   8   20
9     I   6   5   19
10    J   7  10   20
```



Familia *apply() 
========================================================


```r
# lapply retorna una lista, con NA en el primer elemento pues no es numerico
lapply(X= df_1, FUN= fivenum)
```

```
$Alum
[1] NA NA NA NA NA

$Mat
[1]  5  6  7  9 10

$Len
[1]  5  5  6  8 10

$Edad
[1] 19.0 19.0 19.5 20.0 20.0
```



Familia *apply() 
========================================================


```r
# lapply a df_1 columnas numericas
df_1_lapply <- lapply(X= df_1[ ,2:4], FUN= fivenum)
df_1_lapply 
```

```
$Mat
[1]  5  6  7  9 10

$Len
[1]  5  5  6  8 10

$Edad
[1] 19.0 19.0 19.5 20.0 20.0
```



Familia *apply() 
========================================================


```r
# Recordar que resultado de lapply es una lista
str(df_1_lapply)
```

```
List of 3
 $ Mat : num [1:5] 5 6 7 9 10
 $ Len : num [1:5] 5 5 6 8 10
 $ Edad: num [1:5] 19 19 19.5 20 20
```

```r
class(df_1_lapply)
```

```
[1] "list"
```



Familia *apply() 
========================================================


```r
# sapply simplifica por default a vector/matriz
df_1_sapply <- sapply(X= df_1[ ,2:4], fivenum)
df_1_sapply
```

```
     Mat Len Edad
[1,]   5   5 19.0
[2,]   6   5 19.0
[3,]   7   6 19.5
[4,]   9   8 20.0
[5,]  10  10 20.0
```

```r
class(df_1_sapply)
```

```
[1] "matrix"
```



Familia *apply() 
========================================================


```r
# vapply en FUN.VALUE se especifica la estructura resultante de la función
df_1_vapply <- vapply(X=  df_1[ ,2:4], FUN= fivenum, FUN.VALUE =  c(Min= 0, Q1= 0, Median = 0, Q3= 0, Max= 0))
df_1_vapply
```

```
       Mat Len Edad
Min      5   5 19.0
Q1       6   5 19.0
Median   7   6 19.5
Q3       9   8 20.0
Max     10  10 20.0
```

```r
class(df_1_vapply)
```

```
[1] "matrix"
```



Familia *apply() 
========================================================

Ejemplo: seleccionar columnas de un tipo específico de datos

```r
# Usamos sapply para obtener clase de cada variable del datarame
sapply(df_1, class)
```

```
     Alum       Mat       Len      Edad 
 "factor" "numeric" "numeric" "numeric" 
```

```r
# Filtrar
df_1[ ,sapply(df_1, class) == 'numeric']
```

```
   Mat Len Edad
1   10  NA   19
2    7   6   20
3    6   6   19
4    5   9   20
5    6   5   19
6    9   7   20
7    7   5   19
8   10   8   20
9    6   5   19
10   7  10   20
```



Familia *apply() 
========================================================

- La funcione **mapply()** sirve para aplicar una función sobre los elementos de los vectores dados, es decir mapply aplica la función tomando los primeros elementos de cada uno de los vectores dados, luego tomando los segundos elementos, los terceros elementos, y así sucesivamente



Familia *apply() 
========================================================


```r
# Mapply ejemplo basico, retorna una lista
mapply(rep, 1:4, 4:1)
```

```
[[1]]
[1] 1 1 1 1

[[2]]
[1] 2 2 2

[[3]]
[1] 3 3

[[4]]
[1] 4
```



Familia *apply() 
========================================================


```r
# Mapply ejemplo basico, retorna una lista
mapply(rep, times = 1:4, x = 4:1)
```

```
[[1]]
[1] 4

[[2]]
[1] 3 3

[[3]]
[1] 2 2 2

[[4]]
[1] 1 1 1 1
```



Familia *apply() 
========================================================


```r
# Mapply retorna vector o matriz cuando es posible
mapply('*', 1:4, 4:1)
```

```
[1] 4 6 6 4
```



Familia *apply() 
========================================================


```r
# Mapply retorna vector o matriz cuando es posible
mapply('c', 1:4, 4:1)
```

```
     [,1] [,2] [,3] [,4]
[1,]    1    2    3    4
[2,]    4    3    2    1
```



Familia *apply() 
========================================================


```r
# Mapply ejemplo basico
mapply(paste,  1:5, LETTERS[1:5],sep= c('%', '&', '#', '-', '*'))
```

```
[1] "1%A" "2&B" "3#C" "4-D" "5*E"
```



Familia *apply() 
========================================================


```r
# Mapply ejemplo basico
mapply(paste,  1:5, LETTERS[1:5], c('%', '&', '#', '-', '*'))
```

```
[1] "1 A %" "2 B &" "3 C #" "4 D -" "5 E *"
```



Familia *apply() 
========================================================

- La funcione **tapply()** sirve para aplicar una función sobre un vector que a su vez está agrupado por otro



Familia *apply() 
========================================================


```r
# Crear una variable clasificadora al dataframe df_1
df_1$Ciudad <- c('Gye', 'Uio', 'Cue','Gye', 'Uio', 'Cue', 'Gye', 'Uio', 'Cue', 'Gye')
df_1
```

```
   Alum Mat Len Edad Ciudad
1     A  10  NA   19    Gye
2     B   7   6   20    Uio
3     C   6   6   19    Cue
4     D   5   9   20    Gye
5     E   6   5   19    Uio
6     F   9   7   20    Cue
7     G   7   5   19    Gye
8     H  10   8   20    Uio
9     I   6   5   19    Cue
10    J   7  10   20    Gye
```



Familia *apply() 
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_tapply <- tapply(X= df_1$Len, INDEX= df_1$Ciudad, FUN= mean, na.rm= TRUE)
df_tapply
```

```
     Cue      Gye      Uio 
6.000000 8.000000 6.333333 
```

```r
# Retorna un array
class(df_tapply)
```

```
[1] "array"
```



Familia *apply() 
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad y Edad
df_tapply <- tapply(X= df_1$Mat, INDEX= df_1[ ,c('Ciudad', 'Edad')], FUN= mean, na.rm= TRUE)
df_tapply
```

```
      Edad
Ciudad  19  20
   Cue 6.0 9.0
   Gye 8.5 6.0
   Uio 6.0 8.5
```

```r
# Retorna un array
class(df_tapply)
```

```
[1] "matrix"
```



Familia *apply() 
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad y Edad
df_tapply <- tapply(X= df_1$Mat, INDEX= df_1[ ,c('Ciudad', 'Edad')])
df_tapply
```

```
 [1] 2 6 1 5 3 4 2 6 1 5
```

```r
# Retorna un array
class(df_tapply)
```

```
[1] "integer"
```



Función aggregate
========================================================

- La funcion **aggregate()** es parecido a tapply, pero agregate acepta dataframes como elemento a "cortar"



Función aggregate
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_aggr <- aggregate(x= df_1$Mat, by= list(Ciudad= df_1$Ciudad), FUN= mean, na.rm= TRUE)
df_aggr
```

```
  Ciudad        x
1    Cue 7.000000
2    Gye 7.250000
3    Uio 7.666667
```

```r
# Retorna un data.frame
class(df_aggr)
```

```
[1] "data.frame"
```



Función aggregate
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_aggr <- aggregate(x= df_1[ ,2:4], by= list(Ciudad= df_1$Ciudad, Edad= df_1$Edad), FUN= mean, na.rm= TRUE)
df_aggr
```

```
  Ciudad Edad Mat Len Edad
1    Cue   19 6.0 5.5   19
2    Gye   19 8.5 5.0   19
3    Uio   19 6.0 5.0   19
4    Cue   20 9.0 7.0   20
5    Gye   20 6.0 9.5   20
6    Uio   20 8.5 7.0   20
```

```r
# Retorna un data.frame
class(df_aggr)
```

```
[1] "data.frame"
```



Función aggregate
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_aggr <- aggregate(formula= Mat ~ Ciudad + Edad, data= df_1, FUN= mean)
df_aggr
```

```
  Ciudad Edad Mat
1    Cue   19 6.0
2    Gye   19 8.5
3    Uio   19 6.0
4    Cue   20 9.0
5    Gye   20 6.0
6    Uio   20 8.5
```

```r
# Retorna un data.frame
class(df_aggr)
```

```
[1] "data.frame"
```



Función aggregate
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_aggr <- aggregate(formula= cbind(Mat, Len, Edad) ~ Ciudad + Edad, data= df_1, FUN= mean)
df_aggr
```

```
  Ciudad Edad Mat Len Edad
1    Cue   19 6.0 5.5   19
2    Gye   19 7.0 5.0   19
3    Uio   19 6.0 5.0   19
4    Cue   20 9.0 7.0   20
5    Gye   20 6.0 9.5   20
6    Uio   20 8.5 7.0   20
```

```r
# Retorna un data.frame
class(df_aggr)
```

```
[1] "data.frame"
```




Función by()
========================================================

- La funcion **by()** un dataframe es cortado por columnas en dataframes de acuerdo al valor de uno o más factores, y a cada subconjunto se le aplica la funcion FUN.



Función by()
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_by <- by(data= df_1[ ,2:4], INDICES= df_1$Ciudad, FUN= colMeans, na.rm= TRUE)
df_by
```

```
df_1$Ciudad: Cue
     Mat      Len     Edad 
 7.00000  6.00000 19.33333 
-------------------------------------------------------- 
df_1$Ciudad: Gye
  Mat   Len  Edad 
 7.25  8.00 19.50 
-------------------------------------------------------- 
df_1$Ciudad: Uio
      Mat       Len      Edad 
 7.666667  6.333333 19.666667 
```

```r
# Retorna un data.frame
class(df_by)
```

```
[1] "by"
```



Función by()
========================================================


```r
# Obtener promedio de notas de Matematicas por ciudad
df_by <- by(data= df_1[ ,2:4], INDICES= df_1[ , c('Ciudad', 'Edad')], FUN= colMeans, na.rm= TRUE)
df_by
```

```
Ciudad: Cue
Edad: 19
 Mat  Len Edad 
 6.0  5.5 19.0 
-------------------------------------------------------- 
Ciudad: Gye
Edad: 19
 Mat  Len Edad 
 8.5  5.0 19.0 
-------------------------------------------------------- 
Ciudad: Uio
Edad: 19
 Mat  Len Edad 
   6    5   19 
-------------------------------------------------------- 
Ciudad: Cue
Edad: 20
 Mat  Len Edad 
   9    7   20 
-------------------------------------------------------- 
Ciudad: Gye
Edad: 20
 Mat  Len Edad 
 6.0  9.5 20.0 
-------------------------------------------------------- 
Ciudad: Uio
Edad: 20
 Mat  Len Edad 
 8.5  7.0 20.0 
```

```r
# Retorna un data.frame
class(df_by)
```

```
[1] "by"
```




Paquete plyr
========================================================

- Se considera que a veces sobre el 80 por ciento del esfuerzo se dedica a la limpieza de los datos antes de realizar el análisis real (Exploratory Data Mining and Data Cleaning, Dasu T. and Johnson T.)
- Hadley Wickham en 2011 creó el paquete plyr con la llamada ["split-apply-combine strategy"] (http://www.jstatsoft.org/v40/i01/paper)
- Basicamente se divide el objeto en varias partes, a cada parte se aplica la función deseada y finalmente el output resultante se combina para devolver un solo objeto como resultado



Paquete plyr
========================================================

- El paquete se conforma por funciones de tipo *xyply*, donde *xy* indican la entrada y la salida de la funcion, así por ejemplo ddply() indica que recibe un dataframe y devuelve un dataframe, en resumen se tiene (filas como input y columnad como output):


```
          dataframe list    array  
dataframe "ddply"   "dlply" "daply"
list      "ldply"   "llply" "laply"
array     "adply"   "alply" "aaply"
```


Paquete plyr
========================================================

Se usará los datos "iris" de Fisher, el cual contiene las medidas en centímetros de estas variables: sepal length
and width, and petal length and width, para 50 flores de cada una de las tres especies 
de Iris (setosa Iris, Iris versicolor, e Iris virginica)


```r
# Cargar paquete dataset y ver q tiene Iris
library('datasets')
head(iris, n=4)
```

```
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
```



Paquete plyr
========================================================

Divide iris segun la columna Species, calcula el largo del data.frame para cada parte y devuelveme los resultads en un solo objeto dataframe


```r
library (plyr)
# Usando variables
ddply(.data= iris, .variables= c('Species'), .fun= nrow)
```

```
     Species V1
1     setosa 50
2 versicolor 50
3  virginica 50
```



Paquete plyr
========================================================

Divide iris segun la columna Species, calcula el largo del data.frame para cada parte y devuelveme los resultads en un solo objeto dataframe


```r
# Usando formula
ddply(.data= iris, .variables= ~Species, .fun= nrow)
```

```
     Species V1
1     setosa 50
2 versicolor 50
3  virginica 50
```



Paquete plyr
========================================================

Divide iris segun la columna Species, calcula la Media por columnas del data.frame (hay q quitarle la columna Species que no es numérica) para cada parte y devuelveme los resultads en un solo objeto dataframe


```r
ddply(.data= iris, .variables= c('Species'), 
      .fun= function(x) colMeans(x[ ,-which(colnames(x)=="Species")]))
```

```
     Species Sepal.Length Sepal.Width Petal.Length Petal.Width
1     setosa        5.006       3.428        1.462       0.246
2 versicolor        5.936       2.770        4.260       1.326
3  virginica        6.588       2.974        5.552       2.026
```



Paquete plyr
========================================================

Divide iris segun la columna Species, calcula la Media por columnas del data.frame (hay q quitarle la columna Species que no es numérica) para cada parte y devuelveme los resultads en un solo objeto dataframe


```r
ddply(.data= iris, .variables= ~Species, .fun= function(x) colMeans(x[ ,-which(colnames(x)=="Species")]))
```

```
     Species Sepal.Length Sepal.Width Petal.Length Petal.Width
1     setosa        5.006       3.428        1.462       0.246
2 versicolor        5.936       2.770        4.260       1.326
3  virginica        6.588       2.974        5.552       2.026
```



Paquete plyr
========================================================

Divide iris segun la columna Species, calcula varios indicadores


```r
ddply(.data= iris, .variables= c('Species'), function(X){
  SL.SUM <- sum(X$Sepal.Length, na.rm= TRUE)
  SW.SUM <- sum(X$Sepal.Width, na.rm= TRUE)
  SW.MEDN <- median(X$Sepal.Width, na.rm= TRUE)
  data.frame(SL.SUM, SW.SUM, SW.MEDN)
})
```

```
     Species SL.SUM SW.SUM SW.MEDN
1     setosa  250.3  171.4     3.4
2 versicolor  296.8  138.5     2.8
3  virginica  329.4  148.7     3.0
```



Paquete plyr
========================================================

function= summarise, se crea un nuevo dataframe con la variable clasificadores y el resultado de los calculos


```r
ddply(.data= iris, .variables= c('Species'), .fun= summarise, 
  SL.SUM = sum(Sepal.Length, na.rm= TRUE),
  SW.SUM = sum(Sepal.Width, na.rm= TRUE),
  SW.MEDN = median(Sepal.Width, na.rm= TRUE) )
```

```
     Species SL.SUM SW.SUM SW.MEDN
1     setosa  250.3  171.4     3.4
2 versicolor  296.8  138.5     2.8
3  virginica  329.4  148.7     3.0
```



Paquete plyr
========================================================

function= transform


```r
df_iris_tr <- ddply(.data= iris, .variables= c('Species'), .fun= transform, 
  SL.SUM = sum(Sepal.Length, na.rm= TRUE),
  SW.SUM = sum(Sepal.Width, na.rm= TRUE),
  SW.MEDN = median(Sepal.Width, na.rm= TRUE) )
```



Paquete plyr
========================================================

function= transform, se adjunta el resultado de los calculos al dataframe original segun corresponda


```r
head(df_iris_tr, n=5)
```

```
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species SL.SUM SW.SUM
1          5.1         3.5          1.4         0.2  setosa  250.3  171.4
2          4.9         3.0          1.4         0.2  setosa  250.3  171.4
3          4.7         3.2          1.3         0.2  setosa  250.3  171.4
4          4.6         3.1          1.5         0.2  setosa  250.3  171.4
5          5.0         3.6          1.4         0.2  setosa  250.3  171.4
  SW.MEDN
1     3.4
2     3.4
3     3.4
4     3.4
5     3.4
```



Paquete plyr
========================================================

function= transform, se adjunta el resultado de los calculos al dataframe original segun corresponda


```r
tail(df_iris_tr, n=5)
```

```
    Sepal.Length Sepal.Width Petal.Length Petal.Width   Species SL.SUM
146          6.7         3.0          5.2         2.3 virginica  329.4
147          6.3         2.5          5.0         1.9 virginica  329.4
148          6.5         3.0          5.2         2.0 virginica  329.4
149          6.2         3.4          5.4         2.3 virginica  329.4
150          5.9         3.0          5.1         1.8 virginica  329.4
    SW.SUM SW.MEDN
146  148.7       3
147  148.7       3
148  148.7       3
149  148.7       3
150  148.7       3
```



Paquete plyr
========================================================

function= mutate, hace lo mismo que transform adicionando que permite trabajar con las nuevas variables creadas


```r
df_iris_tr <- ddply(.data= iris, .variables= c('Species'), .fun= mutate, 
  SL.SUM = sum(Sepal.Length, na.rm= TRUE),
  SW.SUM = sum(Sepal.Width, na.rm= TRUE),
  TOT_SUM = SL.SUM + SW.SUM)
```



Paquete plyr
========================================================

function= mutate, hace lo mismo que transform adicionando que permite trabajar con las nuevas variables creadas


```r
head(df_iris_tr, n=5)
```

```
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species SL.SUM SW.SUM
1          5.1         3.5          1.4         0.2  setosa  250.3  171.4
2          4.9         3.0          1.4         0.2  setosa  250.3  171.4
3          4.7         3.2          1.3         0.2  setosa  250.3  171.4
4          4.6         3.1          1.5         0.2  setosa  250.3  171.4
5          5.0         3.6          1.4         0.2  setosa  250.3  171.4
  TOT_SUM
1   421.7
2   421.7
3   421.7
4   421.7
5   421.7
```



Paquete plyr
========================================================

function= mutate, hace lo mismo que transform adicionando que permite trabajar con las nuevas variables creadas


```r
tail(df_iris_tr, n=5)
```

```
    Sepal.Length Sepal.Width Petal.Length Petal.Width   Species SL.SUM
146          6.7         3.0          5.2         2.3 virginica  329.4
147          6.3         2.5          5.0         1.9 virginica  329.4
148          6.5         3.0          5.2         2.0 virginica  329.4
149          6.2         3.4          5.4         2.3 virginica  329.4
150          5.9         3.0          5.1         1.8 virginica  329.4
    SW.SUM TOT_SUM
146  148.7   478.1
147  148.7   478.1
148  148.7   478.1
149  148.7   478.1
150  148.7   478.1
```



========================================================



========================================================




