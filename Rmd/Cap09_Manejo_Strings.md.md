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






Manejo de datos de tipo Caracter en R
========================================================
type: sub-section




Comando as.character
========================================================


```r
# as.character para convertir en texto
v_num <- 1:10
v_num
```

```
 [1]  1  2  3  4  5  6  7  8  9 10
```

```r
v_num_txt <- as.character(v_num)
v_num_txt
```

```
 [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10"
```



Comando as.character
========================================================


```r
# as.character para convertir en texto
v_fact <- factor(letters[1:5])
v_fact
```

```
[1] a b c d e
Levels: a b c d e
```

```r
v_fact_txt <- as.character(v_fact)
v_fact_txt
```

```
[1] "a" "b" "c" "d" "e"
```



Paquete stringr
========================================================

El paquete stringr permite manipular caracteres alojados en vectores, matrices o data.frames


```r
# Cargar paquete stringr
library('stringr')
```



Cantidad de caracteres 
========================================================

nchar() calcula la cantidad de caracteres de cada elemento, str_length() además preserva NA

```r
v_caracter <- c(head(state.name, n= 3), 'the one', NA)
v_caracter
```

```
[1] "Alabama" "Alaska"  "Arizona" "the one" NA       
```

```r
nchar(v_caracter)
```

```
[1]  7  6  7  7 NA
```

```r
str_length(v_caracter)
```

```
[1]  7  6  7  7 NA
```



Concatenar caracteres
========================================================

Para concatenar se usa cat(), paste(), sprintf() o str_c()

```r
x <- 7
y <- 10
cat('se tiene x=', x,'\n ','mientras que y=', y)
```

```
se tiene x= 7 
  mientras que y= 10
```

```r
sprintf('se tiene x= %s mientras que y= %s', x, y)
```

```
[1] "se tiene x= 7 mientras que y= 10"
```



Concatenar caracteres
========================================================

Para concatenar se usa cat(), paste(), sprintf() o str_c()

```r
paste('se tiene x=', x,'mientras que y=', y)
```

```
[1] "se tiene x= 7 mientras que y= 10"
```

```r
paste('se tiene x=', x,'mientras que y=', y, sep='')
```

```
[1] "se tiene x=7mientras que y=10"
```

```r
paste('se tiene x=', x,'mientras que y=', y, sep='*')
```

```
[1] "se tiene x=*7*mientras que y=*10"
```



Concatenar caracteres
========================================================

Cuando se desea concatenar los elementos de un vector de usa el parámetro collapse

```r
paste(c('abc', 'def', 'ghi', 'jkl'), sep= '+')
```

```
[1] "abc" "def" "ghi" "jkl"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), collapse= '+')
```

```
[1] "abc+def+ghi+jkl"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), collapse= ' ')
```

```
[1] "abc def ghi jkl"
```



Concatenar caracteres
========================================================

Cuando se desea concatenar los elementos de un vector de usa el parámetro collapse

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, sep= '+')
```

```
[1] "abc+1" "def+2" "ghi+3" "jkl+4"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, collapse= '+')
```

```
[1] "abc 1+def 2+ghi 3+jkl 4"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, collapse= '+', sep='?')
```

```
[1] "abc?1+def?2+ghi?3+jkl?4"
```



Concatenar caracteres
========================================================

Tambien se puede concatenar vectores, elemento a elemento; e incluso concatenar el vector resultante en un sólo string

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, sep= '+')
```

```
[1] "abc+1" "def+2" "ghi+3" "jkl+4"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, collapse= '+')
```

```
[1] "abc 1+def 2+ghi 3+jkl 4"
```

```r
paste(c('abc', 'def', 'ghi', 'jkl'), 1:4, collapse= '+', sep='?')
```

```
[1] "abc?1+def?2+ghi?3+jkl?4"
```



Concatenar caracteres
========================================================

str_c() es similar a paste(), pero usa sep= '' por defult.

```r
paste('se tiene x=', x, 'mientras que y=', y)
```

```
[1] "se tiene x= 7 mientras que y= 10"
```

```r
str_c('se tiene x=', x, 'mientras que y=', y)
```

```
[1] "se tiene x=7mientras que y=10"
```

```r
paste('se tiene x=', x, 'mientras que y=', y, sep='')
```

```
[1] "se tiene x=7mientras que y=10"
```

```r
str_c('se tiene x=', x, 'mientras que y=', y, sep= ' ')
```

```
[1] "se tiene x= 7 mientras que y= 10"
```



Cortar un caracter
========================================================

substring() muestra los caracteres segun el rango dado

```r
substring(text= v_caracter, first= 2, last= 6)
```

```
[1] "labam" "laska" "rizon" "he on" NA     
```

```r
substring(v_caracter, 1:2, 4:5)
```

```
[1] "Alab" "lask" "Ariz" "he o" NA    
```



Cortar un caracter
========================================================

substring() muestra los caracteres segun el rango dado

```r
substring('abcdef', 1:6, 1:6)
```

```
[1] "a" "b" "c" "d" "e" "f"
```

```r
substring('abcdef', 1:6, 2:7)
```

```
[1] "ab" "bc" "cd" "de" "ef" "f" 
```

```r
substring('abcdef', 1:3, 6:4)
```

```
[1] "abcdef" "bcde"   "cd"    
```


Cortar un caracter
========================================================

str_sub() es equivalente a substring()

```r
str_sub(string= v_caracter, start= 2, end= 6)
```

```
[1] "labam" "laska" "rizon" "he on" NA     
```

```r
str_sub(v_caracter, 1:2, 4:5)
```

```
[1] "Alab" "lask" "Ariz" "he o" NA    
```

```r
str_sub('abcdef', 1:6, 1:6)
```

```
[1] "a" "b" "c" "d" "e" "f"
```

```r
str_sub('abcdef', 1:6, 2:7)
```

```
[1] "ab" "bc" "cd" "de" "ef" "f" 
```



Cortar un caracter
========================================================

strsplit() corta un string de acuerdo a un patrón

```r
strsplit(x= v_caracter, split= 'a')
```

```
[[1]]
[1] "Al" "b"  "m" 

[[2]]
[1] "Al" "sk"

[[3]]
[1] "Arizon"

[[4]]
[1] "the one"

[[5]]
[1] NA
```



Cortar un caracter
========================================================

strsplit() corta un string de acuerdo a un patrón

```r
strsplit(x= 'corta un string de acuerdo a un patrón', split= ' ')
```

```
[[1]]
[1] "corta"   "un"      "string"  "de"      "acuerdo" "a"       "un"     
[8] "patrón" 
```

```r
unlist(strsplit(x= 'corta un string de acuerdo a un patrón', split= ' '))
```

```
[1] "corta"   "un"      "string"  "de"      "acuerdo" "a"       "un"     
[8] "patrón" 
```



Cortar un caracter
========================================================

strsplit() y str_split() para cortar un string de acuerdo a un patrón

```r
strsplit(x= 'abcdefg', split= '')
```

```
[[1]]
[1] "a" "b" "c" "d" "e" "f" "g"
```

```r
str_split(string= 'abcdefg', pattern= '')
```

```
[[1]]
[1] "a" "b" "c" "d" "e" "f" "g"
```



Cortar un caracter
========================================================

str_split_fixed() permite ajustar el maximo de partes a retornar y así crear una matriz con numero de columnas ajustadas

```r
str_split_fixed(string= v_caracter, pattern=  'a', n= 3)
```

```
     [,1]      [,2] [,3]
[1,] "Al"      "b"  "ma"
[2,] "Al"      "sk" ""  
[3,] "Arizon"  ""   ""  
[4,] "the one" ""   ""  
[5,] ""        ""   ""  
```



Encontrar un patrón
========================================================

grep() retorna los índices de los elementos que cumplen un patron determinado


```r
v_caracter
```

```
[1] "Alabama" "Alaska"  "Arizona" "the one" NA       
```

```r
grep(pattern= 'Al', x= v_caracter)
```

```
[1] 1 2
```

```r
v_caracter[grep(pattern= 'Al', x= v_caracter)]
```

```
[1] "Alabama" "Alaska" 
```



Encontrar un patrón
========================================================

grep() retorna los índices de los elementos que cumplen un patron determinado


```r
grep(pattern= 'Al', x= v_caracter, value= TRUE)
```

```
[1] "Alabama" "Alaska" 
```

```r
grep(pattern= 'o', x= v_caracter, value= TRUE)
```

```
[1] "Arizona" "the one"
```

```r
grep(pattern= '(Al)|(o)', x= v_caracter, value= TRUE)
```

```
[1] "Alabama" "Alaska"  "Arizona" "the one"
```



Encontrar un patrón
========================================================

grep() retorna los índices de los elementos que cumplen un patron determinado


```r
grep(pattern= '[0-9]', x= v_caracter, value= TRUE)
```

```
character(0)
```

```r
grep(pattern= '[b-f]', x= v_caracter, value= TRUE)
```

```
[1] "Alabama" "the one"
```

```r
grep(pattern= '[b,z]', x= v_caracter, value= TRUE)
```

```
[1] "Alabama" "Arizona"
```



Encontrar un patrón
========================================================

str_detect() es un wrap de grep, retorna un vector logico según si encontró o no el patrón buscado


```r
str_detect(pattern= '[0-9]', string= v_caracter)
```

```
[1] FALSE FALSE FALSE FALSE    NA
```

```r
str_detect(pattern= '[b-f]', string= v_caracter)
```

```
[1]  TRUE FALSE FALSE  TRUE    NA
```

```r
str_detect(pattern= '[b,z]', string= v_caracter)
```

```
[1]  TRUE FALSE  TRUE FALSE    NA
```



Encontrar un patrón
========================================================

str_extract() devuelve el primer elemento encontrados


```r
str_extract(pattern= '[0-9]', string= v_caracter)
```

```
[1] NA NA NA NA NA
```

```r
str_extract(pattern= '[b-f]', string= v_caracter)
```

```
[1] "b" NA  NA  "e" NA 
```

```r
str_extract(pattern= '[b,z]', string= v_caracter)
```

```
[1] "b" NA  "z" NA  NA 
```



Encontrar un patrón
========================================================

str_extract_all() devuelve los elementos encontrados


```r
str_extract_all(pattern= '[b-f]', string= v_caracter)
```

```
[[1]]
[1] "b"

[[2]]
character(0)

[[3]]
character(0)

[[4]]
[1] "e" "e"

[[5]]
[1] NA
```



Reemplazar texto
========================================================

sub() y gsub() permiten reemplazar un patron


```r
sub(pattern= '[b-f]', replacement= '***', x= v_caracter)
```

```
[1] "Ala***ama" "Alaska"    "Arizona"   "th*** one" NA         
```

```r
gsub(pattern= '[b-f]', replacement= '***', x= v_caracter)
```

```
[1] "Ala***ama"   "Alaska"      "Arizona"     "th*** on***" NA           
```



Reemplazar texto
========================================================

str_replace() y str_replace_all() permiten reemplazar un patron


```r
str_replace(pattern= '[b-f]', replacement= '***', string= v_caracter)
```

```
[1] "Ala***ama" "Alaska"    "Arizona"   "th*** one" NA         
```

```r
str_replace_all (pattern= '[b-f]', replacement= '***', string= v_caracter)
```

```
[1] "Ala***ama"   "Alaska"      "Arizona"     "th*** on***" NA           
```



Encontrar la posición de un patron dentro de un caracter
========================================================

str_locate() y str_locate_all() devuelven la posición del patrón buscado


```r
str_locate(pattern= '[b-f]', string= v_caracter)
```

```
     start end
[1,]     4   4
[2,]    NA  NA
[3,]    NA  NA
[4,]     3   3
[5,]    NA  NA
```



Encontrar la posición de un patron dentro de un caracter
========================================================

str_locate() y str_locate_all() devuelven la posición del patrón buscado


```r
str_locate_all (pattern= '[b-f]', string= v_caracter)
```

```
[[1]]
     start end
[1,]     4   4

[[2]]
     start end

[[3]]
     start end

[[4]]
     start end
[1,]     3   3
[2,]     7   7

[[5]]
     start end
[1,]    NA  NA
```



Eliminar espacios en blanco al inicio o final
========================================================

str_trim() permite eliminar espacios en blanco al inicio, final o ambos 


```r
v_caracter_2 <- c('  inicio', 'final   ', '  ambos   ', 'en medio')
str_trim(v_caracter_2, side= 'left')
```

```
[1] "inicio"   "final   " "ambos   " "en medio"
```

```r
str_trim(v_caracter_2, side= 'right')
```

```
[1] "  inicio" "final"    "  ambos"  "en medio"
```

```r
str_trim(v_caracter_2, side= 'both')
```

```
[1] "inicio"   "final"    "ambos"    "en medio"
```
