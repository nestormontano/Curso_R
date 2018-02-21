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



Manipulación de Datos - Básico
========================================================
type: sub-section



Indexado|Selección - Vector
========================================================

Creacion de un vector

```r
# Crear un vector para ejemplos
v1 <- seq(from= 10, to= 100, by= 10) # Crear
names(v1) <- letters[1:10]
v1
```

```
  a   b   c   d   e   f   g   h   i   j 
 10  20  30  40  50  60  70  80  90 100 
```



Indexado|Selección - Vector
========================================================

Acceder a elementos según un vector lógico

```r
# Selección según un vector lógico
v1>50 & v1<80
```

```
    a     b     c     d     e     f     g     h     i     j 
FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE 
```

```r
v1[v1>50 & v1<80]
```

```
 f  g 
60 70 
```




Indexado|Selección - Vector
========================================================

Acceder a un elemento

```r
# Acceder a un elemento
v1[4] 
```

```
 d 
40 
```

```r
v1['b']
```

```
 b 
20 
```



Indexado|Selección - Vector
========================================================
class: small-code
Acceder a elementos segun vector de índices

```r
# Selección según vector de índices
v1[1:3]
```

```
 a  b  c 
10 20 30 
```

```r
v1[c(1, 9, 5)]
```

```
 a  i  e 
10 90 50 
```

```r
v1[c(2.1, 2.9)] # Se trunca a la parte entera
```

```
 b  b 
20 20 
```



Indexado|Selección - Vector
========================================================
class: small-code
Acceder a elementos excluyendo índices

```r
# Excluir índices
v1[-(4:8)]
```

```
  a   b   c   i   j 
 10  20  30  90 100 
```

```r
v1[-c(1, 5, 9)] 
```

```
  b   c   d   f   g   h   j 
 20  30  40  60  70  80 100 
```



Indexado|Selección - Vector
========================================================

Usa indexado para modificar parte del objeto

```r
# Modificar parte del objeto
v1[c(8, 5)] <- c(800, 500)
v1
```

```
  a   b   c   d   e   f   g   h   i   j 
 10  20  30  40 500  60  70 800  90 100 
```



Indexado|Selección - Vector
========================================================
class: small-code
Casos especiales

```r
v1[c(2, NA, 5, NULL, 9, NaN, 3, 0)]
```

```
   b <NA>    e    i <NA>    c 
  20   NA  500   90   NA   30 
```

```r
v1[c(2, 5, FALSE, TRUE)]
```

```
  b   e   a 
 20 500  10 
```

```r
v1[c(NA, 'b', NULL, 'c', 0, 'd', 'x')]
```

```
<NA>    b    c <NA>    d <NA> 
  NA   20   30   NA   40   NA 
```



Indexado|Selección - Vector
========================================================
class: small-code
Casos especiales

```r
v1[c(TRUE, FALSE)]
```

```
  a   c   e   g   i 
 10  30 500  70  90 
```

```r
v1[c(TRUE, FALSE, TRUE)]
```

```
  a   c   d   f   g   i   j 
 10  30  40  60  70  90 100 
```

```r
v1[11] <- 110
v1[14] <- 110
v1
```

```
  a   b   c   d   e   f   g   h   i   j                 
 10  20  30  40 500  60  70 800  90 100 110  NA  NA 110 
```



Indexado|Selección - Matriz
========================================================

Creacion de una matriz

```r
# Crear matriz para ejemplos
m1 <- matrix(seq(10, 120, by= 10), nrow=  3)
rownames(m1) <- letters[1:3]
colnames(m1) <- LETTERS[1:4]
m1
```

```
   A  B  C   D
a 10 40 70 100
b 20 50 80 110
c 30 60 90 120
```



Indexado|Selección - Matriz
========================================================
class: small-code
Acceder a elementos según un vector lógico

```r
# Selección según un vector lógico
m1>50 & m1<80
```

```
      A     B     C     D
a FALSE FALSE  TRUE FALSE
b FALSE FALSE FALSE FALSE
c FALSE  TRUE FALSE FALSE
```

```r
m1[m1>50 & m1<80]
```

```
[1] 60 70
```

```r
m1[rep(c(TRUE,FALSE), 6)]
```

```
[1]  10  30  50  70  90 110
```



Indexado|Selección - Matriz
========================================================
class: small-code
Acceder a un elemento

```r
# Acceder a un elemento
m1[4] 
```

```
[1] 40
```

```r
m1[2,3]
```

```
[1] 80
```

```r
m1['b', 'C']
```

```
[1] 80
```

```r
m1[c(2,3)] #c(2,3) lo toma como vector
```

```
[1] 20 30
```



Indexado|Selección - Matriz
========================================================

[2, 3] != c(2, 3)

```r
# Acceder a un elemento
m1[2,3]
```

```
[1] 80
```

```r
m1[c(2,3)] #c(2,3) lo toma como vector
```

```
[1] 20 30
```


Indexado|Selección - Matriz
========================================================

Acceder a columa o filas completas

```r
# Acceder a columa o filas completas
m1[2, ] 
```

```
  A   B   C   D 
 20  50  80 110 
```

```r
m1[ , 3]
```

```
 a  b  c 
70 80 90 
```


Indexado|Selección - Matriz
========================================================

Acceder a columa o filas completas

```r
# drop=FALSE Para q no retorne vectores sino matrices
m1[ , 3, drop=FALSE]
```

```
   C
a 70
b 80
c 90
```

```r
m1['c', , drop=FALSE]
```

```
   A  B  C   D
c 30 60 90 120
```



Indexado|Selección - Matriz
========================================================

Acceder a columa o filas completas

```r
# Acceder a columa o filas completas
m1[c(2,3), ]
```

```
   A  B  C   D
b 20 50 80 110
c 30 60 90 120
```

```r
m1[ , c(4,2)]
```

```
    D  B
a 100 40
b 110 50
c 120 60
```



Indexado|Selección - Matriz
========================================================

Acceder a columa o filas completas

```r
# Acceder a columa o filas completas
m1[c('c','a'), ]
```

```
   A  B  C   D
c 30 60 90 120
a 10 40 70 100
```

```r
m1[ , c('D','B')]
```

```
    D  B
a 100 40
b 110 50
c 120 60
```



Indexado|Selección - Matriz
========================================================

Acceder a elementos segun vector de índices

```r
# Acceder a elementos en "x" índices
m1[1:3]
```

```
[1] 10 20 30
```

```r
m_index <- matrix(c(1:3,3:1), ncol= 2)
m_index
```

```
     [,1] [,2]
[1,]    1    3
[2,]    2    2
[3,]    3    1
```



Indexado|Selección - Matriz
========================================================

Acceder a elementos segun vector de índices

```r
# Acceder a elementos en "x" índices
m1[m_index]
```

```
[1] 70 50 30
```



Indexado|Selección - Matriz
========================================================

Acceder a elementos excluyendo índices - No Permitido

```r
# Excluir índices
m1[-c(1, 5, 9)] 
```

```
[1]  20  30  40  60  70  80 100 110 120
```

```r
m_index_n <- -m_index
m_index_n
```

```
     [,1] [,2]
[1,]   -1   -3
[2,]   -2   -2
[3,]   -3   -1
```

```r
# m1[m_index_n] #Genera un error
```



Indexado|Selección - Matriz
========================================================

Pero sí se permite si se excluye filas o columnas

```r
# Excluir filas/columnas
m1[-c(1, 3), ] 
```

```
  A   B   C   D 
 20  50  80 110 
```

```r
m1[ , -c(1, 3)] 
```

```
   B   D
a 40 100
b 50 110
c 60 120
```



Indexado|Selección - Matriz
========================================================
class: small-code
Usa indexado para modificar parte del objeto

```r
# Modificar parte del objeto
m1[c(11,12)] <- 99
m1
```

```
   A  B  C   D
a 10 40 70 100
b 20 50 80  99
c 30 60 90  99
```

```r
m1[m_index] <- 0
m1
```

```
   A  B  C   D
a 10 40  0 100
b 20  0 80  99
c  0 60 90  99
```



Indexado|Selección - Matriz
========================================================

Casos especiales

```r
m2 <- m1
m2[c(2, NA, 5, NULL, 9, NaN, 3, 0)]
```

```
[1] 20 NA  0 90 NA  0
```

```r
m2[c(2, 5, FALSE, TRUE)]
```

```
[1] 20  0 10
```

```r
m2[c(NA, 'b', NULL, 'c', 0, 'd', 'x')]
```

```
[1] NA NA NA NA NA NA
```



Indexado|Selección - Matriz
========================================================
class: small-code
Casos especiales

```r
m2[c(TRUE, FALSE)]
```

```
[1] 10  0  0  0 90 99
```

```r
m2[c(TRUE, FALSE, TRUE)]
```

```
[1]  10   0  40  60   0  90 100  99
```

```r
m2[11] <- 110
m2[14] <- 110
m2
```

```
 [1]  10  20   0  40   0  60   0  80  90 100 110  99  NA 110
```



Indexado|Selección - Matriz
========================================================

Casos especiales

```r
m1[ , c(TRUE,FALSE)]
```

```
   A  C
a 10  0
b 20 80
c  0 90
```

```r
m1[c(1,NA), ]
```

```
      A  B  C   D
a    10 40  0 100
<NA> NA NA NA  NA
```



Indexado|Selección - Array
========================================================

Aplica lo mismo que para matriz

```r
a1 <- array(1:12, dim= c(2,3,2))
a1
```

```
, , 1

     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

, , 2

     [,1] [,2] [,3]
[1,]    7    9   11
[2,]    8   10   12
```



Indexado|Selección - Array
========================================================

Aplica lo mismo que para matriz

```r
a_index <- matrix(c(1,2,1,2,3,2), ncol= 3, byrow= TRUE)
a_index
```

```
     [,1] [,2] [,3]
[1,]    1    2    1
[2,]    2    3    2
```

```r
a1[a_index]
```

```
[1]  3 12
```




Indexado|Selección - Listas
========================================================
class: small-code
Creacion de una lista

```r
# Crear un vector para ejemplos
lst1 <- list(ID= 123, Materia="Matematicas", Veces_Tomada= 3, Promedios= c(55,50,65))
lst1
```

```
$ID
[1] 123

$Materia
[1] "Matematicas"

$Veces_Tomada
[1] 3

$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================

Acceder a un elemento

```r
# Acceder a un elemento
lst1[[2]] 
```

```
[1] "Matematicas"
```

```r
lst1$Veces_Tomada
```

```
[1] 3
```

```r
lst1$Promedios
```

```
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================

Acceder a un elemento

```r
# Acceder a un elemento
lst1$Promedios[2]
```

```
[1] 50
```

```r
lst1[[4]][2]
```

```
[1] 50
```



Indexado|Selección - Listas
========================================================

**Diferenciar [[]] de []**

```r
# Cuarto objeto de la lista
lst1[[4]]
```

```
[1] 55 50 65
```

```r
# SubLista que contiene la cuarta entrada de la lista
lst1[4]
```

```
$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================

Diferenciar [[]] de []

```r
lst1[[4]][2]
```

```
[1] 50
```

```r
lst1[4][2]
```

```
$<NA>
NULL
```

```r
lst1[4][[1]][2]
```

```
[1] 50
```



Indexado|Selección - Listas
========================================================

**Diferenciar [[]] de []**

"Si considera a la lista "x" como un tren, entonces x[[5]] es el objeto en el vagón 5; mientras que x[4:6] es un tren que tiene los vagones 4 al 6"

de: @RLangTip



Indexado|Selección - Listas
========================================================

Subconjunto según un vector lógico

```r
# lst1 == 3 # ERROR
# lst1[[c(TRUE,FALSE)]] # ERROR
lst1[c(TRUE, FALSE, FALSE, TRUE)]
```

```
$ID
[1] 123

$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================
class: small-code
Subconjunto segun vector de índices

```r
lst1[c(4,2)]
```

```
$Promedios
[1] 55 50 65

$Materia
[1] "Matematicas"
```

```r
# lst1[[c(3,2)]] # ERROR
lst1[[c(4,2)]] # 2do elemento del 4to elemento
```

```
[1] 50
```

```r
# lst1[[4,2]] # ERROR
```



Indexado|Selección - Listas
========================================================
class: small-code
Subconjunto excluyendo índices

```r
# Excluir índices
lst1[-(2:3)]
```

```
$ID
[1] 123

$Promedios
[1] 55 50 65
```

```r
lst1[-c(1, 3)] 
```

```
$Materia
[1] "Matematicas"

$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================
class: small-code
Usa indexado para modificar parte del objeto

```r
# Modificar parte del objeto
lst1[c(1, 3)] <- list(12399,399)
lst1
```

```
$ID
[1] 12399

$Materia
[1] "Matematicas"

$Veces_Tomada
[1] 399

$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================
class: small-code
Usa indexado para modificar parte del objeto

```r
# Modificar parte del objeto
lst1[[2]] <- 'Matematicas_2'
lst1
```

```
$ID
[1] 12399

$Materia
[1] "Matematicas_2"

$Veces_Tomada
[1] 399

$Promedios
[1] 55 50 65
```



Indexado|Selección - Listas
========================================================
class: small-code
<small>Casos especiales</small>

```r
lst1[c(2, NA, 4, NULL, 1, NaN, 3, 0)]
```

```
$Materia
[1] "Matematicas_2"

$<NA>
NULL

$Promedios
[1] 55 50 65

$ID
[1] 12399

$<NA>
NULL

$Veces_Tomada
[1] 399
```


Indexado|Selección - Listas
========================================================
class: small-code
<small>Casos especiales</small>

```r
lst1[c(2, 4, FALSE, TRUE)]
```

```
$Materia
[1] "Matematicas_2"

$Promedios
[1] 55 50 65

$ID
[1] 12399
```



Indexado|Selección - Listas
========================================================
class: small-code
<small>Casos especiales</small>

```r
lst1[c(NA, 'ID', NULL, 4)]
```

```
$<NA>
NULL

$ID
[1] 12399

$<NA>
NULL
```



Indexado|Selección - Listas
========================================================
class: small-code
<small>Casos especiales</small>

```r
lst1[6]
```

```
$<NA>
NULL
```

```r
lst1[6] <- 110
lst1
```

```
$ID
[1] 12399

$Materia
[1] "Matematicas_2"

$Veces_Tomada
[1] 399

$Promedios
[1] 55 50 65

[[5]]
NULL

[[6]]
[1] 110
```





Indexado|Selección - Data Frame
========================================================
class: small-code
<small>Recordar que un data frame es una lista de vectores, por tanto el indexado es parecido, tambien un dataframe se compone de filas y columnas, por tanto el indexado es también parecido al de una matriz</small>

```r
# Cargar un Data frame
df_1  <- data.frame( Nombre= c('Ana', 'Berni', 'Carlos', 'Daniel', 'Ericka'), Edad = c(20,19,20,19,18), Ciudad= factor(c('Gye', 'Uio', 'Cue', 'Gye', 'Cue')) )
rownames(df_1) <- letters[1:5]
df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Gye
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   19    Gye
e Ericka   18    Cue
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Selección de variables/columnas

```r
# Selección de variables/columnas
df_1$Edad
```

```
[1] 20 19 20 19 18
```

```r
df_1[ ,2]
```

```
[1] 20 19 20 19 18
```

```r
df_1[ ,'Edad']
```

```
[1] 20 19 20 19 18
```

```r
df_1[[2]]
```

```
[1] 20 19 20 19 18
```



Indexado|Selección - Data Frame
========================================================

Selección de variables/columnas

```r
# Selección de variables/columnas
df_1[ ,'Edad']
```

```
[1] 20 19 20 19 18
```

```r
df_1[[2]]
```

```
[1] 20 19 20 19 18
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Acceder a columa o filas completas

```r
# Acceder a columa o filas completas
df_1[ , c(2,3)]
```

```
  Edad Ciudad
a   20    Gye
b   19    Uio
c   20    Cue
d   19    Gye
e   18    Cue
```

```r
df_1[ , c('Edad','Ciudad')]
```

```
  Edad Ciudad
a   20    Gye
b   19    Uio
c   20    Cue
d   19    Gye
e   18    Cue
```



Indexado|Selección - Data Frame
========================================================

Acceder a columa o filas completas

```r
# Acceder a columa o filas completas
df_1[c(2,3), ]
```

```
  Nombre Edad Ciudad
b  Berni   19    Uio
c Carlos   20    Cue
```

```r
df_1[c('b','c'), ]
```

```
  Nombre Edad Ciudad
b  Berni   19    Uio
c Carlos   20    Cue
```



Indexado|Selección - Data Frame
========================================================

Selección de variables/columnas

```r
# Aquí en realidad se está obteniendo un dataframe, no un vector
# Simil al caso de las listas
df_1[2]
```

```
  Edad
a   20
b   19
c   20
d   19
e   18
```



Indexado|Selección - Data Frame
========================================================

Acceder a filas según un vector lógico

```r
# Selección según un vector lógico
df_1$Edad < 20
```

```
[1] FALSE  TRUE FALSE  TRUE  TRUE
```

```r
df_1[df_1$Edad < 20, ]
```

```
  Nombre Edad Ciudad
b  Berni   19    Uio
d Daniel   19    Gye
e Ericka   18    Cue
```



Indexado|Selección - Data Frame
========================================================

Acceder a filas según un vector lógico

```r
# Selección según un vector lógico
df_1[c(TRUE, FALSE, TRUE, FALSE, FALSE), ]
```

```
  Nombre Edad Ciudad
a    Ana   20    Gye
c Carlos   20    Cue
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Acceder a columnas según un vector lógico

```r
# Selección de columnas con vector lógico
df_1[ , c(TRUE, FALSE, TRUE)]
```

```
  Nombre Ciudad
a    Ana    Gye
b  Berni    Uio
c Carlos    Cue
d Daniel    Gye
e Ericka    Cue
```

```r
df_1[c(TRUE, FALSE, TRUE)]
```

```
  Nombre Ciudad
a    Ana    Gye
b  Berni    Uio
c Carlos    Cue
d Daniel    Gye
e Ericka    Cue
```



Indexado|Selección - Data Frame
========================================================

Seleccionar fila y columna determinada

```r
# Seleccionar fila y columna determinada
df_1[2, 3] 
```

```
[1] Uio
Levels: Cue Gye Uio
```

```r
df_1['b', 'Ciudad'] 
```

```
[1] Uio
Levels: Cue Gye Uio
```



Indexado|Selección - Data Frame
========================================================

Seleccionar fila y columna determinada

```r
# Seleccionar fila y columna determinada
df_1$Ciudad[2]
```

```
[1] Uio
Levels: Cue Gye Uio
```

```r
df_1$Ciudad['b'] # ERROR
```

```
[1] <NA>
Levels: Cue Gye Uio
```



Indexado|Selección - Data Frame
========================================================

Seleccionar filas y columna determinada

```r
# Acceder a un elemento
df_1[2:3, c(3,1)] 
```

```
  Ciudad Nombre
b    Uio  Berni
c    Cue Carlos
```

```r
df_1[c('b','c'), c('Ciudad', 'Nombre')]
```

```
  Ciudad Nombre
b    Uio  Berni
c    Cue Carlos
```



Indexado|Selección - Data Frame
========================================================
class: small-code
[2, 3] != c(2, 3)

```r
# Acceder a un elemento
df_1[2,3]
```

```
[1] Uio
Levels: Cue Gye Uio
```

```r
# Muestra las columnas correspondientes
df_1[c(2,3)] 
```

```
  Edad Ciudad
a   20    Gye
b   19    Uio
c   20    Cue
d   19    Gye
e   18    Cue
```



Indexado|Selección - Data Frame
========================================================

Acceder a elementos segun vector de índices

```r
# Acceder a elementos en "x" índices
m_index <- matrix(c(1:3,3:1), ncol= 2)
m_index
```

```
     [,1] [,2]
[1,]    1    3
[2,]    2    2
[3,]    3    1
```



Indexado|Selección - Data Frame
========================================================

Acceder a elementos segun vector de índices

```r
# Acceder a elementos en "x" índices
df_1[m_index]
```

```
[1] "Gye"    "19"     "Carlos"
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Acceder a elementos excluyendo filas/columnas

```r
# Excluir columnas
df_1[-c(2)] 
```

```
  Nombre Ciudad
a    Ana    Gye
b  Berni    Uio
c Carlos    Cue
d Daniel    Gye
e Ericka    Cue
```

```r
df_1[ ,-c(2)] 
```

```
  Nombre Ciudad
a    Ana    Gye
b  Berni    Uio
c Carlos    Cue
d Daniel    Gye
e Ericka    Cue
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Acceder a elementos excluyendo filas/columnas

```r
# Excluir filas
df_1[-c(1, 3), ] 
```

```
  Nombre Edad Ciudad
b  Berni   19    Uio
d Daniel   19    Gye
e Ericka   18    Cue
```

```r
# Excluir filas y columnas
df_1[-c(1, 3), -c(1)] 
```

```
  Edad Ciudad
b   19    Uio
d   19    Gye
e   18    Cue
```



Indexado|Selección - Data Frame
========================================================

Pero sí se permite si se excluye filas o columnas

```r
# Excluir filas/columnas
m1[-c(1, 3), ] 
```

```
 A  B  C  D 
20  0 80 99 
```

```r
m1[ , -c(1, 3)] 
```

```
   B   D
a 40 100
b  0  99
c 60  99
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Usa indexado para modificar parte del objeto

```r
# Modificar parte del objeto
df_1[ df_1$Nombre == 'Daniel', c('Edad')] <- 29
# df_1$Ciudad[1] <- 'aaa'  # ERROR, manejo factores
df_1$Ciudad[1] <- 'Cue'
df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Casos especiales

```r
df_2 <- df_1
#  df_2[ ,c(1, NA,3)] # ERROR
df_2[c(1, NA,3), ]
```

```
   Nombre Edad Ciudad
a     Ana   20    Cue
NA   <NA>   NA   <NA>
c  Carlos   20    Cue
```



Indexado|Selección - Data Frame
========================================================
class: small-code
Casos especiales

```r
df_2[ ,c(TRUE, FALSE)] # Selecciona columnas
```

```
  Nombre Ciudad
a    Ana    Cue
b  Berni    Uio
c Carlos    Cue
d Daniel    Gye
e Ericka    Cue
```

```r
df_2[c(TRUE, FALSE), ] # Selecciona filas
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
e Ericka   18    Cue
```



Indexado|Selección - which
========================================================
class: small-code
which devuelve los indices que cumplen la condición

```r
v1 # Mostrar v1
```

```
  a   b   c   d   e   f   g   h   i   j                 
 10  20  30  40 500  60  70 800  90 100 110  NA  NA 110 
```

```r
v1 >= 100 # Vector Lógico
```

```
    a     b     c     d     e     f     g     h     i     j             
FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE    NA 
            
   NA  TRUE 
```

```r
which(v1 >= 100) # Indices TRUE
```

```
 e  h  j       
 5  8 10 11 14 
```



Indexado|Selección - which
========================================================

which en un data frame

```r
which(df_1$Edad >= 20) # Indices TRUE
```

```
[1] 1 3 4
```

```r
df_1[which(df_1$Edad >= 20), ]
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Indexado|Selección - which
========================================================

which en un data frame

```r
which(df_1$Edad >= 20) # Indices TRUE
```

```
[1] 1 3 4
```

```r
df_1[which(df_1$Edad >= 20), ]
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Indexado|Selección - NAs
========================================================
class: small-code
Data.frame con NA

```r
df_2 <- rbind(df_1, c('Ana', NA, 'Gye'))
df_2 #mostrar df_2
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
6    Ana <NA>    Gye
```

```r
df_2[df_2$Edad >= 20, ] # Notar NA
```

```
   Nombre Edad Ciudad
a     Ana   20    Cue
c  Carlos   20    Cue
d  Daniel   29    Gye
NA   <NA> <NA>   <NA>
```


Indexado|Selección - NAs
========================================================
class: small-code
Data.frame con NA

```r
df_2 #mostrar df_2
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
6    Ana <NA>    Gye
```

```r
df_2[which(df_2$Edad >= 20), ] # Notar NA
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```


Ordenar - Vector
========================================================
class: small-code
Comando sort odena el vector

```r
v1
```

```
  a   b   c   d   e   f   g   h   i   j                 
 10  20  30  40 500  60  70 800  90 100 110  NA  NA 110 
```

```r
sort(v1)
```

```
  a   b   c   d   f   g   i   j           e   h 
 10  20  30  40  60  70  90 100 110 110 500 800 
```

```r
sort(v1, na.last= NA)
```

```
  a   b   c   d   f   g   i   j           e   h 
 10  20  30  40  60  70  90 100 110 110 500 800 
```



Ordenar - Vector
========================================================
class: small-code
Comando sort odena el vector

```r
sort(v1, na.last= TRUE)
```

```
  a   b   c   d   f   g   i   j           e   h         
 10  20  30  40  60  70  90 100 110 110 500 800  NA  NA 
```

```r
sort(v1, na.last= FALSE)
```

```
          a   b   c   d   f   g   i   j           e   h 
 NA  NA  10  20  30  40  60  70  90 100 110 110 500 800 
```



Ordenar - Vector
========================================================
class: small-code
Comando order, devuelve los indices 

```r
order(v1)
```

```
 [1]  1  2  3  4  6  7  9 10 11 14  5  8 12 13
```

```r
order(v1, na.last= NA)
```

```
 [1]  1  2  3  4  6  7  9 10 11 14  5  8
```

```r
order(v1, na.last= TRUE)
```

```
 [1]  1  2  3  4  6  7  9 10 11 14  5  8 12 13
```



Ordenar - Vector
========================================================
class: small-code
Comando rank, devuelve un ranking manejando igualdades

```r
rank(v1)
```

```
   a    b    c    d    e    f    g    h    i    j                     
 1.0  2.0  3.0  4.0 11.0  5.0  6.0 12.0  7.0  8.0  9.5 13.0 14.0  9.5 
```

```r
# Notar los valores 9.5
rank(v1, ties.method = 'min')     
```

```
 a  b  c  d  e  f  g  h  i  j             
 1  2  3  4 11  5  6 12  7  8  9 13 14  9 
```



Ordenar - Vector
========================================================
class: small-code
Comando rank, devuelve un ranking manejando igualdades

```r
rank(v1)
```

```
   a    b    c    d    e    f    g    h    i    j                     
 1.0  2.0  3.0  4.0 11.0  5.0  6.0 12.0  7.0  8.0  9.5 13.0 14.0  9.5 
```

```r
# Notar los valores 9.5
rank(v1, ties.method = 'min')     
```

```
 a  b  c  d  e  f  g  h  i  j             
 1  2  3  4 11  5  6 12  7  8  9 13 14  9 
```



Ordenar - Matrix
========================================================
class: small-code
Recordar Matriz es un vector con dimensión

```r
m1
```

```
   A  B  C   D
a 10 40  0 100
b 20  0 80  99
c  0 60 90  99
```

```r
sort(m1) # Sort devuelve un vector
```

```
 [1]   0   0   0  10  20  40  60  80  90  99  99 100
```



Ordenar - Data.Frame
========================================================

sort sólo acepta vectores

```r
df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
```

```r
# sort(df_1) # ERROR
```



Ordenar - Data.Frame
========================================================

Se utiliza order

```r
order( df_1$Edad, df_1$Ciudad) # Devuelve indices
```

```
[1] 5 2 1 3 4
```

```r
df_1[order( df_1$Edad, df_1$Ciudad), ]
```

```
  Nombre Edad Ciudad
e Ericka   18    Cue
b  Berni   19    Uio
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Ordenar - Data.Frame
========================================================
class: small-code
Descendente?

```r
order( -df_1$Edad, df_1$Ciudad) # Devuelve indices
```

```
[1] 4 1 3 2 5
```

```r
df_1[order( df_1$Edad, df_1$Ciudad), ]
```

```
  Nombre Edad Ciudad
e Ericka   18    Cue
b  Berni   19    Uio
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Ordenar - Data.Frame
========================================================
class: small-code
Uso de with

```r
with( df_1, order( -Edad, Ciudad)) # Devuelve indices
```

```
[1] 4 1 3 2 5
```

```r
df_1[with( df_1, order( -Edad, Ciudad)) , ]
```

```
  Nombre Edad Ciudad
d Daniel   29    Gye
a    Ana   20    Cue
c Carlos   20    Cue
b  Berni   19    Uio
e Ericka   18    Cue
```



Transponer|Rotar - Vectores
========================================================
class: small-code
Transponer

```r
v1
```

```
  a   b   c   d   e   f   g   h   i   j                 
 10  20  30  40 500  60  70 800  90 100 110  NA  NA 110 
```

```r
t(v1)
```

```
      a  b  c  d   e  f  g   h  i   j              
[1,] 10 20 30 40 500 60 70 800 90 100 110 NA NA 110
```



Transponer|Rotar - Matrices
========================================================

Transponer

```r
m1
```

```
   A  B  C   D
a 10 40  0 100
b 20  0 80  99
c  0 60 90  99
```

```r
t(m1)
```

```
    a  b  c
A  10 20  0
B  40  0 60
C   0 80 90
D 100 99 99
```



Transponer|Rotar - Data.frame
========================================================
class: small-code
Transponer

```r
df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
```

```r
t(df_1) # Devuelve una matriz
```

```
       a     b       c        d        e       
Nombre "Ana" "Berni" "Carlos" "Daniel" "Ericka"
Edad   "20"  "19"    "20"     "29"     "18"    
Ciudad "Cue" "Uio"   "Cue"    "Gye"    "Cue"   
```



Subconjuntos - usando indexado
========================================================

Por medio de indexado

```r
v1[v1 > 100]
```

```
   e    h      <NA> <NA>      
 500  800  110   NA   NA  110 
```

```r
df_1[ df_1$Edad >= 20, ]
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Subconjuntos - comando subset
========================================================

Subset

```r
subset(v1, v1 > 100)
```

```
  e   h         
500 800 110 110 
```

```r
subset(df_1, Edad >= 20)
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
c Carlos   20    Cue
d Daniel   29    Gye
```



Subconjuntos - comando subset
========================================================

En resumen, subset presenta las filas que cumplen la condicion

```r
subset(m1, m1[,4] >= 110)
```

```
     A B C D
```

```r
# m2 <- subset(m1, m1[3,] < 100) ## ERROR
subset(m1, c(T,F,T))
```

```
   A  B  C   D
a 10 40  0 100
c  0 60 90  99
```

```r
# subset(m1, c(T,F,F,T)) ## ERROR
```



Subconjuntos - comando subset
========================================================

Subset en matrices

```r
m1_na <- m1
m1_na[3, 4] <- NA
m1_na
```

```
   A  B  C   D
a 10 40  0 100
b 20  0 80  99
c  0 60 90  NA
```

```r
subset(m1_na, m1[,4] >= 110)
```

```
     A B C D
```



Subconjuntos - subset vs indexado
========================================================

Facilita el trabajo y elimina directamente NAs

```r
# Crear data.frame con NA
df_2 <- rbind(df_1, c('Ana', NA, 'Gye'))
df_2
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
6    Ana <NA>    Gye
```



Subconjuntos - subset vs indexado
========================================================

Facilita el trabajo y elimina directamente NAs

```r
df_2[df_2$Edad >= 20, ]
```

```
   Nombre Edad Ciudad
a     Ana   20    Cue
c  Carlos   20    Cue
d  Daniel   29    Gye
NA   <NA> <NA>   <NA>
```



Subconjuntos - subset vs indexado
========================================================

Permite seleccionar columnas

```r
subset(df_2, Edad >= 20, select= c(Nombre, Edad) )
```

```
  Nombre Edad
a    Ana   20
c Carlos   20
d Daniel   29
```



Subconjuntos - subset vs indexado
========================================================

Permite seleccionar columnas

```r
subset(df_2, Edad >= 20, select= c(-Nombre) )
```

```
  Edad Ciudad
a   20    Cue
c   20    Cue
d   29    Gye
```



Subconjuntos - subset vs indexado
========================================================

Se recomienda utilizar subset sólo en scripts, no dentro de funciones por posibles problemas con la "Non standar Evaluation", más información en [http://adv-r.had.co.nz/Computing-on-the-language.html#subset] (http://adv-r.had.co.nz/Computing-on-the-language.html#subset)



Unir datos - Aumentar filas
========================================================

Comando rbind

```r
df_1 # mostrar df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
```



Unir datos - Aumentar filas
========================================================

Comando rbind

```r
df_2 # mostrar df_2
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
6    Ana <NA>    Gye
```



Unir datos - Aumentar filas
========================================================
class: small-code
Comando rbind   
(PD: ver que hace con rownames)

```r
rbind(df_1, df_2) # df_1 + df_2 
```

```
   Nombre Edad Ciudad
a     Ana   20    Cue
b   Berni   19    Uio
c  Carlos   20    Cue
d  Daniel   29    Gye
e  Ericka   18    Cue
a1    Ana   20    Cue
b1  Berni   19    Uio
c1 Carlos   20    Cue
d1 Daniel   29    Gye
e1 Ericka   18    Cue
6     Ana <NA>    Gye
```



Unir datos - Aumentar filas
========================================================
class: small-code
Comando rbind permite aumentar las filas de un conjunto de datos debajo del otro.

```r
# Crear dataframe df_3
df_3 <- data.frame(a= 1:3, b= letters[1:3])
df_3
```

```
  a b
1 1 a
2 2 b
3 3 c
```

```r
# Crear dataframe df_4, que es df_1 con otros nombres de columna
df_4 <- df_1 
names(df_4) <- LETTERS[1:3]
```



Unir datos - Aumentar filas
========================================================

Objetos a unir deben tener mismo numero de columnas

```r
# rbind(df_1, df_3) ## ERROR
# rbind(df_1, df_4) ## ERROR
```



Unir datos - Aumentar filas
========================================================

rbind toma control de factores

```r
df_3 <- data.frame(aa= LETTERS[1:3], a= 1:3, b= letters[1:3])
names(df_3) <- names(df_1)
df_3
```

```
  Nombre Edad Ciudad
1      A    1      a
2      B    2      b
3      C    3      c
```



Unir datos - Aumentar filas
========================================================

rbind toma control de factores

```r
df_4 <- rbind(df_1, df_3)
df_4
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
1      A    1      a
2      B    2      b
3      C    3      c
```



Unir datos - Eliminar filas
========================================================


```r
df_4 <- df_4[-c(1,3,7), ]
df_4
```

```
  Nombre Edad Ciudad
b  Berni   19    Uio
d Daniel   29    Gye
e Ericka   18    Cue
1      A    1      a
3      C    3      c
```



Unir datos - Aumentar filas
========================================================

rbind toma control de factores

```r
str(df_4)
```

```
'data.frame':	5 obs. of  3 variables:
 $ Nombre: Factor w/ 8 levels "Ana","Berni",..: 2 4 5 6 8
 $ Edad  : num  19 29 18 1 3
 $ Ciudad: Factor w/ 6 levels "Cue","Gye","Uio",..: 3 2 1 4 6
```



Unir datos - Aumentar columnas|variables
========================================================

Comando cbind permite aumentar las columnas de un conjunto de datos a lado del otro

```r
df_5 <- data.frame(A= 1:5, B= letters[1:5])
cbind(df_1, df_5)
```

```
  Nombre Edad Ciudad A B
a    Ana   20    Cue 1 a
b  Berni   19    Uio 2 b
c Carlos   20    Cue 3 c
d Daniel   29    Gye 4 d
e Ericka   18    Cue 5 e
```



Unir datos - Aumentar columnas|variables
========================================================

Se puede crear una variable directamente

```r
df_5$C <- seq(10,50,10)
df_5
```

```
  A B  C
1 1 a 10
2 2 b 20
3 3 c 30
4 4 d 40
5 5 e 50
```



Unir datos - Aumentar variables
========================================================

Crear una variable como transformacion de otra

```r
df_1$Edad_2 <- df_1$Edad/2 + 100
df_1
```

```
  Nombre Edad Ciudad Edad_2
a    Ana   20    Cue  110.0
b  Berni   19    Uio  109.5
c Carlos   20    Cue  110.0
d Daniel   29    Gye  114.5
e Ericka   18    Cue  109.0
```



Unir datos - Eliminar columnas|variables
========================================================
class: small-code

```r
df_1$Edad_2 <- NULL
df_1
```

```
  Nombre Edad Ciudad
a    Ana   20    Cue
b  Berni   19    Uio
c Carlos   20    Cue
d Daniel   29    Gye
e Ericka   18    Cue
```

```r
df_5 <- df_5[ , -c(1,3), drop = FALSE] 
df_5
```

```
  B
1 a
2 b
3 c
4 d
5 e
```



Unir datos - Eliminar columnas|variables
========================================================


```r
df_5 <- data.frame(A= 1:5, B= letters[1:5], C= seq(10,50,10))
df_5
```

```
  A B  C
1 1 a 10
2 2 b 20
3 3 c 30
4 4 d 40
5 5 e 50
```


Unir datos - Eliminar columnas|variables
========================================================
<small>Obtener las columnas que no se llamen 'A' o 'C'</small>

```r
df_5 <- df_5[ , !(names(df_5) %in% c('A', 'C')), drop = FALSE] 
df_5
```

```
  B
1 a
2 b
3 c
4 d
5 e
```



Unir datos - Merge|Join|Buscarv
========================================================

- Se tienen dos data.frames con columnas o variables que hacen las veces de “key” o “id” de los mismos
- Se desea agregar al primer conjunto el contenido del segundo conjunto de datos si y sólo si el “key” o “id” del segundo conjunto corresponde con el “key” o “id” del primer conjunto de datos. 
- Parecido al Buscarv y Vlookup de excel
- Equivalente al Join de Bases de datos



Unir datos - Merge|Join|Buscarv
========================================================

Comando Merge 

```r
df_6 <- data.frame(A= c('Ana', 'Daniel','Jose'), B= c(100,200,300))
df_6
```

```
       A   B
1    Ana 100
2 Daniel 200
3   Jose 300
```



Unir datos - Merge|Join|Buscarv
========================================================

Comando Merge 

```r
merge(x= df_1, y= df_6, by.x= 'Nombre', by.y= 'A')
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2 Daniel   29    Gye 200
```



Unir datos - Merge|Join|Buscarv
========================================================

Mantener todo los datos del primer objeto como en un left join o un buscarv


```r
merge(x= df_1, y= df_6, by.x= 'Nombre', by.y= 'A', all.x= TRUE)
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2  Berni   19    Uio  NA
3 Carlos   20    Cue  NA
4 Daniel   29    Gye 200
5 Ericka   18    Cue  NA
```



Unir datos - Merge|Join|Buscarv
========================================================

Mantener todo los datos del segudo objeto como en un right join


```r
merge(x= df_1, y= df_6, by.x= 'Nombre', by.y= 'A', all.y= TRUE)
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2 Daniel   29    Gye 200
3   Jose   NA   <NA> 300
```



Unir datos - Merge|Join|Buscarv
========================================================

Mantener todo los datos de ambos objetos como en un full join


```r
merge(x= df_1, y= df_6, by.x= 'Nombre', by.y= 'A', all= TRUE)
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2  Berni   19    Uio  NA
3 Carlos   20    Cue  NA
4 Daniel   29    Gye 200
5 Ericka   18    Cue  NA
6   Jose   NA   <NA> 300
```



Unir datos - Merge|Join|Buscarv
========================================================

Merge con varias columnas


```r
df_6 <- cbind(df_6, data.frame(Z= c(20,40,30)))
df_6
```

```
       A   B  Z
1    Ana 100 20
2 Daniel 200 40
3   Jose 300 30
```



Unir datos - Merge|Join|Buscarv
========================================================

Merge con varias columnas   
PD: Ver el ordenamiento en el resultado


```r
merge(x= df_1, y= df_6, by.x= c('Nombre', 'Edad'), by.y= c('A','Z'), all= TRUE)
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2  Berni   19    Uio  NA
3 Carlos   20    Cue  NA
4 Daniel   29    Gye  NA
5 Daniel   40   <NA> 200
6 Ericka   18    Cue  NA
7   Jose   30   <NA> 300
```



Unir datos - Merge|Join|Buscarv
========================================================

Para que no se ordenen los datos al hacer el merge


```r
merge(x= df_1, y= df_6, by.x= c('Nombre', 'Edad'), by.y= c('A','Z'), all= TRUE, sort= FALSE)
```

```
  Nombre Edad Ciudad   B
1    Ana   20    Cue 100
2  Berni   19    Uio  NA
3 Carlos   20    Cue  NA
4 Daniel   29    Gye  NA
5 Ericka   18    Cue  NA
6 Daniel   40   <NA> 200
7   Jose   30   <NA> 300
```



Unir datos - Merge|Join|Buscarv
========================================================
class: small-code
Para realizar merge de varios dataframes se usa Reduce


```r
df_11 <- cbind(Nombre= df_1[,1, drop=FALSE], df_11=11)
df_12 <- cbind(Nombre= df_1[,1, drop=FALSE], df_12=12)
df_13 <- cbind(Nombre= df_1[,1, drop=FALSE], df_13=13)
Reduce(function(...){
  merge(..., by= 'Nombre', all= TRUE)
  }, list(df_1, df_11, df_12, df_13))
```

```
  Nombre Edad Ciudad df_11 df_12 df_13
1    Ana   20    Cue    11    12    13
2  Berni   19    Uio    11    12    13
3 Carlos   20    Cue    11    12    13
4 Daniel   29    Gye    11    12    13
5 Ericka   18    Cue    11    12    13
```



%in% y match entre dos vectores
========================================================

- `match(x= , table= )`   
Si *x[i]* es encontrado en *table[j]*, entonces en la `i-ésima` posición del vector resultante se tendrá el valor `j`, para los más pequeños j posible
- `%in% `   
Devuelve un vector lógico indicando si existe match en cada elemento del primer objeto 




%in% y match entre dos vectores
========================================================
class: small-code


```r
# Definir semilla para reproducibilidad
set.seed(5) 
# crear un data.frame base 
df_base <- data.frame(Alum = LETTERS[1:6], Mat = sample(x = 1:10, size = 6, replace = TRUE), Len = sample(x = 1:10, size = 6, replace = TRUE))
df_base
```

```
  Alum Mat Len
1    A   3   6
2    B   7   9
3    C  10  10
4    D   3   2
5    E   2   3
6    F   8   5
```



%in% y match entre dos vectores
========================================================


```r
# crear un data.frame que contendra los valores a modificar 
df_modificatorio <- data.frame(Alum = c("E", "C"), Mat = c(99, 88)) 
# presentar data.frame 
df_modificatorio
```

```
  Alum Mat
1    E  99
2    C  88
```



%in% y match entre dos vectores
========================================================

```r
# %in%
df_base$Alum %in% df_modificatorio$Alum
```

```
[1] FALSE FALSE  TRUE FALSE  TRUE FALSE
```

```r
df_modificatorio$Alum %in% df_base$Alum
```

```
[1] TRUE TRUE
```



%in% y match entre dos vectores
========================================================

```r
# match
match(x= df_base$Alum, table= df_modificatorio$Alum, nomatch= 0)
```

```
[1] 0 0 2 0 1 0
```

```r
match(x= df_modificatorio$Alum, table= df_base$Alum, nomatch= 0)
```

```
[1] 5 3
```



%in% y match entre dos vectores
========================================================
class: small-code
Indexar con %in%  o  match

```r
# %in%
df_base[df_base$Alum %in% df_modificatorio$Alum, ]
```

```
  Alum Mat Len
3    C  10  10
5    E   2   3
```

```r
df_modificatorio[df_modificatorio$Alum %in% df_base$Alum, ]
```

```
  Alum Mat
1    E  99
2    C  88
```



%in% y match entre dos vectores
========================================================
class: small-code
Indexar con %in%  o  match

```r
# match
df_base[match(x = df_modificatorio$Alum, table = df_base$Alum, nomatch = 0), ]
```

```
  Alum Mat Len
5    E   2   3
3    C  10  10
```

```r
df_modificatorio[match(x= df_base$Alum, table= df_modificatorio$Alum, nomatch= 0), ]
```

```
  Alum Mat
2    C  88
1    E  99
```



%in% y match entre dos vectores
========================================================
class: small-code
Comportamiento con valores repetidos

```r
# Aumentar una fila con Alum repetido
df_base <- rbind(df_base, c("E", 1, 1))
df_base
```

```
  Alum Mat Len
1    A   3   6
2    B   7   9
3    C  10  10
4    D   3   2
5    E   2   3
6    F   8   5
7    E   1   1
```

```r
df_modificatorio <- rbind(df_modificatorio, data.frame(Alum= "Z", Mat= 20))
df_modificatorio
```

```
  Alum Mat
1    E  99
2    C  88
3    Z  20
```



%in% y match entre dos vectores
========================================================
class: small-code
Comportamiento con valores repetidos

```r
# %in%
df_base[df_base$Alum %in% df_modificatorio$Alum, ]
```

```
  Alum Mat Len
3    C  10  10
5    E   2   3
7    E   1   1
```

```r
df_modificatorio[df_modificatorio$Alum %in% df_base$Alum, ]
```

```
  Alum Mat
1    E  99
2    C  88
```



%in% y match entre dos vectores
========================================================
class: small-code
Comportamiento con valores repetidos, match sólo devuelve el primer repetido

```r
# match
df_base[match(x = df_modificatorio$Alum, table = df_base$Alum, nomatch = 0), ]
```

```
  Alum Mat Len
5    E   2   3
3    C  10  10
```

```r
df_modificatorio[match(x= df_base$Alum, table= df_modificatorio$Alum, nomatch= 0), ]
```

```
    Alum Mat
2      C  88
1      E  99
1.1    E  99
```



%in% y match entre dos vectores
========================================================
class: small-code
<small>¿Que hacer si se requiere modificar el df_base$Mat según los valores de df_modificatorio$Mat?</small>

```r
# Primer intento: ERROR, sólo actualiza un "E"
df_base[match(x = df_modificatorio$Alum, table = df_base$Alum, nomatch = 0), "Mat"] <- df_modificatorio[df_modificatorio$Alum %in% df_base$Alum, "Mat"]
df_base
```

```
  Alum Mat Len
1    A   3   6
2    B   7   9
3    C  88  10
4    D   3   2
5    E  99   3
6    F   8   5
7    E   1   1
```



%in% y match entre dos vectores
========================================================
class: small-code
¿Que hacer si se requiere modificar el df_base$Mat según los valores de df_modificatorio$Mat?

```r
# Creamos nuevamente el data.frame df_base 
set.seed(5) 
df_base <- data.frame(Alum = LETTERS[1:6], Mat = sample(x = 1:10, size = 6, replace = TRUE), Len = sample(x = 1:10, size = 6, replace = TRUE), stringsAsFactors = FALSE) 
df_base <- rbind(df_base, c("E", 1, 1)) 
df_base
```

```
  Alum Mat Len
1    A   3   6
2    B   7   9
3    C  10  10
4    D   3   2
5    E   2   3
6    F   8   5
7    E   1   1
```



%in% y match entre dos vectores
========================================================
class: small-code
¿Que hacer si se requiere modificar el df_base$Mat según los valores de df_modificatorio$Mat?

```r
# df_base- coincidentes en el orden de df_base
df_base[df_base$Alum %in% df_modificatorio$Alum, ]
```

```
  Alum Mat Len
3    C  10  10
5    E   2   3
7    E   1   1
```

```r
# df_modificatorio- coincidencias en el orden de df_base
df_modificatorio[match(x = df_base$Alum, table = df_modificatorio$Alum, nomatch = 0), ]
```

```
    Alum Mat
2      C  88
1      E  99
1.1    E  99
```



%in% y match entre dos vectores
========================================================
class: small-code
¿Que hacer si se requiere modificar el df_base$Mat según los valores de df_modificatorio$Mat?

```r
df_base[df_base$Alum %in% df_modificatorio$Alum, 'Mat'] <- df_modificatorio[match(x = df_base$Alum, table = df_modificatorio$Alum, nomatch = 0), 'Mat']
df_base
```

```
  Alum Mat Len
1    A   3   6
2    B   7   9
3    C  88  10
4    D   3   2
5    E  99   3
6    F   8   5
7    E  99   1
```



Attach
========================================================

Ubica el data.frame en la posición 2 del "search path" (que es donde busca R por las variables)

```r
mean(df_1$Edad)
```

```
[1] 21.2
```

```r
attach(df_1)
# Buscará Edad en las variables del data.frame
mean(Edad)
```

```
[1] 21.2
```



Attach
========================================================


```r
# Si se realiza asignaciones en realidad no se cambia el data.frame original
Edad <- Edad + 100
Edad
```

```
[1] 120 119 120 129 118
```

```r
detach(df_1)
df_1$Edad
```

```
[1] 20 19 20 29 18
```



Attach
========================================================


```r
# eliminar variable Edad creada 
rm(Edad)
# para preservar la asignación
attach(df_1)
df_1$Edad <- Edad + 100
detach(df_1)
df_1$Edad
```

```
[1] 120 119 120 129 118
```



Encontrar filas duplicadas
========================================================
class: small-code
unique() devuelve cada uno de los valores únicos del vector o dataframe


```r
unique(df_1$Ciudad)
```

```
[1] Cue Uio Gye
Levels: Cue Gye Uio
```

```r
unique(df_1)
```

```
  Nombre Edad Ciudad
a    Ana  120    Cue
b  Berni  119    Uio
c Carlos  120    Cue
d Daniel  129    Gye
e Ericka  118    Cue
```



Encontrar filas duplicadas
========================================================
class: small-code
duplicated() devuelve un vector lógico, FALSE si es la primer vez observado y TRUE si ya se ha observado


```r
duplicated(df_1$Ciudad)
```

```
[1] FALSE FALSE  TRUE FALSE  TRUE
```

```r
duplicated(df_1)
```

```
[1] FALSE FALSE FALSE FALSE FALSE
```

```r
df_1[!duplicated(df_1$Ciudad), ]
```

```
  Nombre Edad Ciudad
a    Ana  120    Cue
b  Berni  119    Uio
d Daniel  129    Gye
```



