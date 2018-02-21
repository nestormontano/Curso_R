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



Manejo de datos tipo Factor en R
========================================================
type: sub-section



Factores
========================================================

- Factores son variables que pueden tomar un número limitado de valores
- Factores son el equivalente a las variables categoricas



Factores - creacion
========================================================


```r
# Crear un factor
v_character <- c('alto', 'medio', 'bajo', 'medio', 'bajo')
v_character
```

```
[1] "alto"  "medio" "bajo"  "medio" "bajo" 
```

```r
# factores son creados con funcion factor()
v_fact <- factor(v_character)
v_fact
```

```
[1] alto  medio bajo  medio bajo 
Levels: alto bajo medio
```



Factores - creacion
========================================================


```r
# Se le puede asignar nuevos labels a los niveles desde su creación
v_fact_2 <- factor( v_character, labels= c('I', 'II', 'III'))
v_fact_2
```

```
[1] I   III II  III II 
Levels: I II III
```

```r
# O cambiar los niveles luego de haberse creado el factor
levels(v_fact_2) <- c('N_1', 'N_2', 'N_3')
v_fact_2
```

```
[1] N_1 N_3 N_2 N_3 N_2
Levels: N_1 N_2 N_3
```



Factores - ordenar niveles
========================================================


```r
# En analisis estadisticos los datos se ordenan alfabeticamente
table(v_fact)
```

```
v_fact
 alto  bajo medio 
    1     2     2 
```

```r
# Para ordenar los niveles 
v_fact_or <- factor(v_character, levels= c('bajo', 'medio', 'alto'))
table(v_fact_or)
```

```
v_fact_or
 bajo medio  alto 
    2     2     1 
```



Factores - ordenar niveles
========================================================


```r
# Obtener los niveles del factor
levels(v_fact)
```

```
[1] "alto"  "bajo"  "medio"
```

```r
levels(v_fact_or)
```

```
[1] "bajo"  "medio" "alto" 
```

```r
nlevels(v_fact_2)
```

```
[1] 3
```



Factores desde vector numerico
========================================================


```r
# Crear un factor desde un vector numerico
fert <- c(10, 20, 20, 50, 10, 20, 10, 50, 20)
fert <- factor( fert, levels= c(10, 20, 50), ordered= TRUE)
fert
```

```
[1] 10 20 20 50 10 20 10 50 20
Levels: 10 < 20 < 50
```



Factores - subconjuntos
========================================================


```r
# Creamos un factor
set.seed(12)
lets <- sample(letters, size= 100, replace= TRUE)
lets <- factor(lets)
table( lets)
```

```
lets
a b c d e f g h i j k l m n o p q r s t u v w x y z 
3 3 4 3 7 3 5 2 5 9 5 4 1 2 7 2 3 3 5 4 3 7 3 1 3 3 
```



Factores - subconjuntos
========================================================


```r
# Al crear el factor se crean los niveles del mismo
table( lets)
```

```
lets
a b c d e f g h i j k l m n o p q r s t u v w x y z 
3 3 4 3 7 3 5 2 5 9 5 4 1 2 7 2 3 3 5 4 3 7 3 1 3 3 
```

```r
# Al hacer una selección se muestra también los niveles no presentes 
table( lets[1:5])
```

```

a b c d e f g h i j k l m n o p q r s t u v w x y z 
0 1 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 
```



Factores - subconjuntos
========================================================


```r
# Con drop= TRUE se eliminan niveles no presentes
table( lets[1:5, drop= TRUE] )
```

```

b e h v y 
1 1 1 1 1 
```

```r
# Tambien se podria crear un nuevo factor
table( factor(lets[1:5]))
```

```

b e h v y 
1 1 1 1 1 
```



Factores - Concatenar factores
========================================================


```r
# Crear 2 vectores de la clase factor
fact1 <- factor( c('a', letters[1:10]))
fact2 <- factor( c(11:20, 13))
fact1
```

```
 [1] a a b c d e f g h i j
Levels: a b c d e f g h i j
```

```r
fact2
```

```
 [1] 11 12 13 14 15 16 17 18 19 20 13
Levels: 11 12 13 14 15 16 17 18 19 20
```



Factores - Concatenar factores
========================================================


```r
# Al concatenar con c() se concatenan los valores, no los niveles
c(fact1, fact2)
```

```
 [1]  1  1  2  3  4  5  6  7  8  9 10  1  2  3  4  5  6  7  8  9 10  3
```

```r
# Para concatenar de manera correcta se realiza
factor( c( levels(fact1)[fact1], levels(fact2)[fact2] ))
```

```
 [1] a  a  b  c  d  e  f  g  h  i  j  11 12 13 14 15 16 17 18 19 20 13
Levels: 11 12 13 14 15 16 17 18 19 20 a b c d e f g h i j
```



Factores desde variables continuas
========================================================


```r
# Crear un vector con datos aleatorios
v_continuo <- runif(n= 10, min= 0, max= 1)
v_continuo
```

```
 [1] 0.4829763 0.8410553 0.4551459 0.8605173 0.6761024 0.7275831 0.9783257
 [8] 0.1952677 0.1466545 0.4981209
```

```r
# Funcion Cut permite crear rangos
cut( v_continuo, 4)
```

```
 [1] (0.355,0.562] (0.77,0.979]  (0.355,0.562] (0.77,0.979]  (0.562,0.77] 
 [6] (0.562,0.77]  (0.77,0.979]  (0.146,0.355] (0.146,0.355] (0.355,0.562]
Levels: (0.146,0.355] (0.355,0.562] (0.562,0.77] (0.77,0.979]
```



Factores desde variables continuas
========================================================


```r
# Funcion Cut permite con cortes predefinidos
cut( v_continuo, breaks = c(0, 0.25, 0.5, 0.75, 1))
```

```
 [1] (0.25,0.5] (0.75,1]   (0.25,0.5] (0.75,1]   (0.5,0.75] (0.5,0.75]
 [7] (0.75,1]   (0,0.25]   (0,0.25]   (0.25,0.5]
Levels: (0,0.25] (0.25,0.5] (0.5,0.75] (0.75,1]
```

```r
# Funcion Cut permite con cortes predefinidos y labels
cut( v_continuo, breaks = c(0, 0.25, 0.5, 0.75, 1), labels= c('bajo', 'medio bajo', 'medio alto', 'alto'))
```

```
 [1] medio bajo alto       medio bajo alto       medio alto medio alto
 [7] alto       bajo       bajo       medio bajo
Levels: bajo medio bajo medio alto alto
```



Factores desde fechas
========================================================


```r
# Crear vector de fechas
v_dias <- seq(from= as.Date('2005-1-1'), to= as.Date('2005-12-31'), by= 'day')
# Escoger los meses deñl vector
v_meses = format(v_dias, '%b')
# Convertirlo a factor
f_meses <- factor(v_meses, levels= unique(v_meses), ordered= TRUE)
# Table
table(f_meses)
```

```
f_meses
 Ene.  Feb.  Mar.  Abr.  May.  Jun.  Jul.  Ago. Sept.  Oct.  Nov.  Dic. 
   31    28    31    30    31    30    31    31    30    31    30    31 
```



Factores desde fechas
========================================================


```r
# Utilizar cut para vector tipo date
v_semanas <- cut(v_dias, breaks= 'week')
head( v_semanas, n= 4)
```

```
[1] 2004-12-27 2004-12-27 2005-01-03 2005-01-03
53 Levels: 2004-12-27 2005-01-03 2005-01-10 2005-01-17 ... 2005-12-26
```

```r
tail( v_semanas, n= 4)
```

```
[1] 2005-12-26 2005-12-26 2005-12-26 2005-12-26
53 Levels: 2004-12-27 2005-01-03 2005-01-10 2005-01-17 ... 2005-12-26
```

```r
nlevels(v_semanas)
```

```
[1] 53
```



Factores - combinar dos factores
========================================================


```r
fact1
```

```
 [1] a a b c d e f g h i j
Levels: a b c d e f g h i j
```

```r
fact2
```

```
 [1] 11 12 13 14 15 16 17 18 19 20 13
Levels: 11 12 13 14 15 16 17 18 19 20
```

```r
# Funcion interation combina los niveles
nuevo_factor <- interaction( fact1, fact2)
```



Factores - combinar dos factores
========================================================


```r
# Funcion interation combina los niveles
nuevo_factor
```

```
 [1] a.11 a.12 b.13 c.14 d.15 e.16 f.17 g.18 h.19 i.20 j.13
100 Levels: a.11 b.11 c.11 d.11 e.11 f.11 g.11 h.11 i.11 j.11 a.12 ... j.20
```

```r
nlevels( nuevo_factor)
```

```
[1] 100
```


