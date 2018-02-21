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



Preeliminares 
========================================================
type: sub-section



¿Porqué R?
========================================================

R 
- Gratuito
- Software Libre (Open Source)
- Flexible
- Permite integrarse con otros sistemas u aplicaciones
- Gran cantidad de usuarios y desarrolladores
- CRAN: +5000 paquetes disponibles
- La mayoría de U actualmente enseñan análisis con R


Algo de historia
========================================================

<small>Mientras S cambiaba de dueño y denominación, Ross Ihaka y Robert Gentleman, decidieron implementar su propio dialecto. Era 1991 cuando estos dos neozelandeses crearon R. Tardaron dos años en anunciarlo públicamente y otros dos años más en licenciarlo bajo GPL. Y posiblemente esta decisión sea la responsable de que a día de hoy R tenga cada vez más repercusión, y sea más fácil encontrar cursos y tutoriales para este lenguaje que para su predecesor.</small>



¿Qué es R?
========================================================

Como Lenguaje/entorno 
- Leguaje Orientado a objeto
- Parte del lenguaje "S", es simple y eficaz
- Manipulación de datos
- Realización de cálculos matriciales
- Gran facilidad y potencia para creación de gráficos 
- R ofrece una amplia variedad de técnicas estadísticas y gráficas, además es extensible (¡normalmente las nuevas técnicas se programan primero en R!)
- Soporte para Linux, Mac y Windows



Datos sobre R
========================================================

fuente: [Revolution Analytics] (http://blog.revolutionanalytics.com/2014/04/seven-quick-facts-about-r.html)
- Saber R implica ser mejor pagado en IT (dice.com, 2014 Ene)
- Lenguaje "Data Science"  más utilizado después de SQL (O'Reilly, 2014 Ene)
- Top 15 de todos los lenguajes de programación (rankings RedMonk, 2014 Ene) 
- Lenguaje "Data Science" que más rápido crece (KDNuggets, 2013 Ago) 
- #1 de búsqueda en Google para software de análisis (Google Trends, 2014 Mar) 
- 76% de analistas usa R, 36% lo usa como herramienta principal (2015 Data Science Survey)



R - Ecosistema
========================================================

- Paquetes libres y pagados que extienden las capacidades de R
- Software de análisis basado en R
- Interfaces gráficas de desarrollo (IDEs)
- Interfaces gráficas de usuario GUIs 
- Integración de Bases de datos con R
- Integración de herramientas de BI con R




R desarrollos, derivados y forks
========================================================

- [BIOCONDUCTOR](http://www.bioconductor.org/) Herramientas para analizar Genoma
- [ORACLE R ENTERPRISE](http://www.oracle.com/technetwork/database/database-technologies/r/r-enterprise/overview/index.html) Integra R con Oracle Data Base
- [Microsoft/Revolution R Open RRO](https://mran.microsoft.com/)Microsoft R Application Network
- [STATCONN](http://www.statconn.com/) Integra R con MS Excel, Word, etc
- [RAPPORTER](http://rapporter.net/welcome/en) Reportería y análisis en la nube
- [RSTUDIO](https://www.rstudio.com/) Desarrollos como RStudio Server, Shiny server y paquetes en general
- [Revolution Analytics](http://blog.revolutionanalytics.com/) Comprada por Microsoft
- [pqR](http://www.pqr-project.org/) Pretty quick R
- Otros: renjin, FastR, CXXR, Riposte, TERR




IDEs & GUIs de R
========================================================

**IDEs**
- [Eclipse] (http://lukemiller.org/index.php/2010/04/eclipse-and-statet-a-nice-working-environment-for-r/)
- [Revolution R Enterprise DevelopR IDE] (http://www.revolutionanalytics.com/revolution-r-enterprise-developr)
- [RStudio] (http://www.rstudio.com/products/RStudio/)
- [Emacs] (http://www.gnu.org/software/emacs/)
- [Tinn-R] (http://nbcgib.uesc.br/lec/software/editores/tinn-r/en)



IDEs & GUIs de R
========================================================

**GUIs**
- [R Commander] (http://socserv.mcmaster.ca/jfox/Misc/Rcmdr/) - GUI Usado en Investigacion de Mercado
- [RKward] (http://rkward.sourceforge.net/wiki/Main_Page) - En linux
- [Deducer] (http://www.deducer.org/) - Una GUI basada en java
- [Rattle] (http://rattle.togaware.com/) - Especializado en DataMining
- [JGR] (http://www.rforge.net/JGR/) - Java GUI for R



Objetivos del curso
========================================================

Utilizar R o sus paquetes básicos para 
- Realizar análisis con R
- Programar a un nivel básico con R
- Entender scripts, funciones, código que otro haya escrito en R

En otras palabras: 

**Aprender R básico, pero a fondo**



R y RStudio - Preeliminares
========================================================
type: sub-section



Instalar R
========================================================

**En windows y Mac**
- Descargar R desde [CRAN] (http://cran.r-project.org/) 
- Instalarlo como cualquier otro software

**En Linux (Distribuciones)**
- Distribuciones basadas en Debian/Ubuntu tienen R en los repositorios oficiales
- Distribuciones basadas en Fedora/RedHat deben habilitar EPEL para tener R
- En Debian Estable para tener nuevas versiones se debe utilizar un ["backports"] (http://cran.r-project.org/bin/linux/debian/README)



Recursos y ayuda en R
========================================================
**Web**
- Web site oficial www.r-project.org
- [CRAN Task Views] (http://cran.r-project.org/web/views/) .- Paquetes agrupados por área de estudio/aplicación

**Dentro de R**
- Comando ayuda inicial (html): `help.start()`
- Ayuda sobre un comando: `help('comando')` y `?mean`
- Ejemplos en la ayuda de un comando: `example('mean')`
- Busqueda general: `help.search('comando')` y `??mean`
- Comando/Objeto que contienen: `apropos('comando')` y `find('comando', simple.words= FALSE)`




RStudio
========================================================

- Todo en 1-ventana: Console, Workspace, History, Working directory, Files, Plot, Packages y Help
- Integracion de la consola de R
- Ejecutar codigo desde script
- Resaltado de sintaxis
- Completado de sintaxis
- Manejo de proyectos con soporte para Git y Subversion
- Herramientas para Investigación Reproducible (knitr)



Instalar RStudio
========================================================

- Debe estar R ya instalado
- Descargar según Sistema Operativo [web oficial] (http://www.rstudio.com/products/rstudio/download/)
- En Windows/Mac es next&next
- En linux Debian/Ubuntu/Mint se puede instalar desde el .deb y next&next 
- En linux desde consola hay que seguir las instrucciones de la web oficial
- En linux Red Hat/CentOS/Fedora tener cuidado con las dependencias



Instalar RStudio
========================================================

Abrir RStudio
![Abrir RStudio](Imagenes/Abrir_RStudio.png)



RStudio - Primera impresion
========================================================

Interfaz de RStudio se divide en 4 paneles:

![Partes RStudio](Imagenes/Partes_RStudio.JPG)



RStudio - Primera impresion
========================================================

1. Script: Pantalla donde se escriben las líneas de código
2. Environment/History: Pantalla donde se puede observar la data almacenada, los valores determinados.
3. File/plots/packages/help/viewer: en esta pantalla esta particionada en varias pestañas como:
  - Files.- Explorador de carpetas y archivos
  - Plots/Viewer.- Visor de gráficos o aplicaciones
  - Packages/Ayuda.- Muestra paquetes instalados del R y la ayuda de R
  - Help.- las ayudas internas del sistema
4. Consola: Donde se muestra el código ejecutado y el resultado



Realizar un script en RStudio
========================================================

- Nuevo script: `ctrl + shift + n`
- Completado de comando: `tab` , `ctrl + barra espaciadora`
- Ejecutar selección o linea actual:  `ctrl + enter`
- Ir al source editor: `ctrl + 1`
- Ir a la consola: `ctrl + 2`



Realizar un script en RStudio
========================================================

- Insertar simbolo de asignación `<-`: `alt + -`
- Comentar/des-comentar: `ctrl + shift + c`
- Reformatear linea: `ctrl + i`
- RStudio permite "plegar" código
- Crear secciones de código: `ctrl + shift + r` o `#### nombre ####`
- Saltar a (función o sección): `alt + shift + J`
- Ir a una función: `ctrl + .`




Proyectos en RStudio
========================================================

- Carpeta que contiene todos los scripts y archivos .RData y .Rhistory
- Permite tener nuestros análisis ordenados
- Al abrir un proyecto antiguo RStudio lo abre con las pestañas que se tenía activas
- Permite colaboracion utilizando GIT o Subversion
- Se sugiere tener una estructura interior, por ejemplo:
  - Scripts, Data, Exports, Info



Iniciar un Proyecto en RStudio
========================================================

![Proyecto RStudio](Imagenes/CreateProyect_RSTUDIO.png)
***
- Nuevo Proyecto.-    Project > New Project > New Directory > Empty Project > Poner nombre al Proyecto (se creará una carpeta con ese nombre) > Create Project
- En la carpeta del proyecto crear las carpetas: Data, Exports, Scripts, Recursos (Recomendado)






Manejo de paquetes
========================================================

- Instalación: `install.packages('nombre_paquete')`
- Ver paquetes instalados: `installed.packages()`
- Activar/Cargar: `library('nombre_paquete')`
- Desactivar/Des-cargar: `detach('package:nombre_paquete')`
- Paquetes cargados: `search()`
- RStudio tiene pestaña Packages que permite instalación visual





Generalidades 1
========================================================

- Case sensitivity (`Abc` es diferente de `abc`)
- R, aparte de objetos, tiene:
 - Expresión.- Se evalúa, se imprime y el valor se pierde

```r
  5+5 # Expresión
```

```
[1] 10
```
 - Asignación.- Evalúa la expresión y guarda el resultado en una variable (no lo imprime)

```r
  a <- 5+5 # Asigna el valor a la variable "a"
```



Generalidades 2
========================================================

- Comandos se separan por `;` o `enter`
- Comandos pueden ser agrupados por `{}`
- Para comentar se usa `#`
- SAS y SPSS presentan extensos resultados, mientras que en R la salida es mínima (*En R un análisis se realiza mediante una serie de pasos, con resultados intermedios guardados en objetos*)



Workspace, environments y objetos
========================================================

- Environment es un conjunto de objetos y un puntero
- El environment por defecto es el workspace o .GlobalEnv 
- Acceder a .GlobalEnv: `globalenv()`
- Objetos en el workspace: `ls()` y `objects()`
- Para eliminar objetos: `rm`
- Obtener los objetos de un environment específico: `ls(envir=  name_env)`
  - ejemplo: `ls(envir=  globalenv())`  
- El workspace se graba predeterminado con el nombre `.RData`
- RStudio permite el acceso desde su pestaña "Environment"



Workspace, environments y objetos
========================================================

- Guardar workspace `save.image()`
- Guardar workspace bajo nombre/ruta definida `save.image(file= ruta.RData)`
- Guardar algunos objetos `save(lista_objetos, file = 'file_name.RData')`
- Cargar un archivo .RData `load(file = ‘filename.Rdata’)`
- En Windows/Mac o en Linux con RStudio `load(file = file.choose())` abre una ventana para la selección de archivo a cargar



Historico de comandos (History)
========================================================

- En la consola se puede acceder a los comandos anteriores con las flechas del teclado
- RStudio, abrir un histórico desplegable en la consola: `Ctrl + Up`
- Obtener el histórico: `history(max.show = 25)`
  - En la GUI oficial para Windows/Mac abrirá una nueva ventana, en linux se presentará en el mismo terminal
  - En RStudio `history()` nos lleva a la pestaña "History"
- Guardar el historico: `savehistory(file = '.Rhistory')` 
- Cargar el historico desde un archivo: `loadhistory(file = '.Rhistory')` 



Entendimiento y creación de las estructuras fundamentales de R
========================================================
type: sub-section



Asignaciones
========================================================

- asigna el valor `5` a la variable `a`   :
  - `a <- 5`
  - `5 -> a`
  - `assign("a", 5)`  
- asigna globalmente el valor `5` a la variable `a`, (dentro de una función `a` seguirá valiendo 5)    
  - `a <<- 5`
  -   `5 ->> a` 
- No se recomiendo usar `a = 5`
- RStudio - Verificar en la pestaña Environment la variable `a`



Asignaciones
========================================================

- Una función de un objeto puede ser asignada al objeto, es decir 

```r
a <- 5 # Expresión
a
```

```
[1] 5
```

```r
a <- 2*a
a
```

```
[1] 10
```



R como calculadora
========================================================


```r
2 + 3*5
```

```
[1] 17
```

```r
log((1+2+3)/4) # log natural 
```

```
[1] 0.4054651
```

```r
pi^2 # pi y potencia
```

```
[1] 9.869604
```


R como calculadora
========================================================


```r
abs(-2) # valor abosluto 
```

```
[1] 2
```

```r
factorial(3) # factorial
```

```
[1] 6
```

```r
floor(5.7) # funcion piso
```

```
[1] 5
```



Generar secuencias, repeticiones y aleatorios
========================================================


```r
1:10 # secuencia de 1 a 10, de 1 en 1
```

```
 [1]  1  2  3  4  5  6  7  8  9 10
```

```r
seq(from= 0, to= 20, by= 5) # función seq
```

```
[1]  0  5 10 15 20
```

```r
seq(from= 5, by= 5, length.out= 5) # función seq
```

```
[1]  5 10 15 20 25
```



Generar secuencias, repeticiones y aleatorios
========================================================


```r
rep(x= 3, times= 5) # repetir 5 veces el # 3
```

```
[1] 3 3 3 3 3
```

```r
runif(n= 10, min= 1, max= 5) # Genera aleatorios uniformes
```

```
 [1] 1.623804 2.216760 1.545115 3.720127 1.842774 2.130849 3.757894
 [8] 2.752943 4.016592 4.579483
```

```r
rnorm(n= 10, mean= 100, sd= 10) # Genera aleatorios normales
```

```
 [1] 104.91294 110.08402 102.70004 107.92549  97.15561 106.70777  85.19784
 [8] 102.17331 104.51538 116.87670
```



Operadores de relación
========================================================


```r
3 == 4 # Igualdad
```

```
[1] FALSE
```

```r
3 != 4 # Desigualdad
```

```
[1] TRUE
```

```r
3 > 4  # Mayor que 
```

```
[1] FALSE
```

```r
3 <= 4 # Menor igual que
```

```
[1] TRUE
```



Operadores lógicos
========================================================


```r
! FALSE  # No
```

```
[1] TRUE
```

```r
TRUE & FALSE  # Y
```

```
[1] FALSE
```

```r
TRUE | FALSE  # O
```

```
[1] TRUE
```

```r
xor(TRUE,TRUE) # Ó excluyente
```

```
[1] FALSE
```

```r
TRUE & NA # Cuidado especial con los NA
```

```
[1] NA
```



Operadores lógicos
========================================================


```r
xor(TRUE,TRUE) # Ó excluyente
```

```
[1] FALSE
```

```r
TRUE & NA # Cuidado especial con los NA
```

```
[1] NA
```



Tipos de datos
========================================================

```r
1  # Entero
```

```
[1] 1
```

```r
3.5  # Numérico
```

```
[1] 3.5
```

```r
im <- 3.5 - 8i # Complejo
Im(im) # Parte imaginaria
```

```
[1] -8
```

```r
Re(im) # Parte real
```

```
[1] 3.5
```



Tipos de datos
========================================================

```r
'a'  # Caracter
```

```
[1] "a"
```

```r
data  <- factor(x= c('alto', 'bajo', 'mediano', 'alto')) # Convertir datos a factores
data 
```

```
[1] alto    bajo    mediano alto   
Levels: alto bajo mediano
```


Tipos de datos - factor
========================================================
- Util para tipos de datos ordinales
- x: es el vector de información 
- levels: los niveles del factor labels: nombre de los niveles 
- El factor puede tener un orden específico

```r
# Crear un factor ordenado
data  <- factor(x= c('alto', 'bajo', 'alto', 'alto'), levels = c('bajo', 'mediano', 'alto'))
data # Mostrar el factor
```

```
[1] alto bajo alto alto
Levels: bajo mediano alto
```




Tipos de datos
========================================================

```r
TRUE  # LOGICO
```

```
[1] TRUE
```

```r
FALSE # LOGICO
```

```
[1] FALSE
```

```r
NA    # No disponible, perdido
```

```
[1] NA
```
Nota: Los `NA` requieren un tratamiento especial



Tipos de datos
========================================================

```r
1/0   # Infinito
```

```
[1] Inf
```

```r
-1/0   # Infinito negativo
```

```
[1] -Inf
```

```r
Inf/Inf # No un Numero
```

```
[1] NaN
```


Tipos de datos
========================================================

Qué creen que resulte de lo siguiente?

```r
(0:3)^Inf
```


Tipos de datos
========================================================

Qué creen que resulte de lo siguiente?

```r
0:3 # es una secuencia
```

```
[1] 0 1 2 3
```

```r
(0:3)^Inf  # ahora se eleva cada elemnto a Inf
```

```
[1]   0   1 Inf Inf
```



Estructuras de datos ú Objetos
========================================================
- Vector
- Matriz
- Data.frame
- Serie de Tiempo
- Data.table



Vectores
========================================================
- En R no existen escalares, sino vectores de dim = 1

```r
x <- 1 
is.vector(x)
```

```
[1] TRUE
```
- Creación con función `c()`

```r
x <- c(11, 12, 13, 14) # crea x
x  # presenta x
```

```
[1] 11 12 13 14
```



Vectores
========================================================
- concatenar vectores

```r
z <- c('a', 'b', 'c') # crea z
z  # presenta z
```

```
[1] "a" "b" "c"
```

```r
y <- c(x, 21, 31, x) # crea y
y  # presenta y
```

```
 [1] 11 12 13 14 21 31 11 12 13 14
```



Vectores
========================================================
- Repetir vectores

```r
rep(z, times=5) # repetir todo el vector 5 veces
```

```
 [1] "a" "b" "c" "a" "b" "c" "a" "b" "c" "a" "b" "c" "a" "b" "c"
```

```r
rep(z, each=5)  # repetir cada elemento 5 veces
```

```
 [1] "a" "a" "a" "a" "a" "b" "b" "b" "b" "b" "c" "c" "c" "c" "c"
```



Vectores
========================================================
- Operaciones entre vectores

```r
x # presenta x
```

```
[1] 11 12 13 14
```

```r
y <- c(10, 20, 30, 40) # Crea y
x + 3*y - 1
```

```
[1]  40  71 102 133
```



Vectores
========================================================
- Vectores lógicos

```r
x # presenta x
```

```
[1] 11 12 13 14
```

```r
v_logico <- (x >= 13)
v_logico
```

```
[1] FALSE FALSE  TRUE  TRUE
```

```r
v_logico2 <- (x >= 13) & (x > 13)
v_logico2
```

```
[1] FALSE FALSE FALSE  TRUE
```



Vectores
========================================================
- comando `paste()`

```r
z <- paste(c("X","Y"), 1:5, sep="+1.")
z
```

```
[1] "X+1.1" "Y+1.2" "X+1.3" "Y+1.4" "X+1.5"
```



Matrices o arrays
========================================================
- Array es una generalización multidimensional de los vectores
- Matrices es un array de dos dimensiones

```r
m1 <- matrix(1:12, nrow= 4) # Creacion de matriz
m1
```

```
     [,1] [,2] [,3]
[1,]    1    5    9
[2,]    2    6   10
[3,]    3    7   11
[4,]    4    8   12
```



Matrices o arrays
========================================================

```r
m2 <- matrix(letters[1:12], ncol= 4) # Creacion de matriz
m2
```

```
     [,1] [,2] [,3] [,4]
[1,] "a"  "d"  "g"  "j" 
[2,] "b"  "e"  "h"  "k" 
[3,] "c"  "f"  "i"  "l" 
```

```r
m3 <- array(letters[1:12], dim= c(3,4)) # Creacion de matriz
m3
```

```
     [,1] [,2] [,3] [,4]
[1,] "a"  "d"  "g"  "j" 
[2,] "b"  "e"  "h"  "k" 
[3,] "c"  "f"  "i"  "l" 
```



Matrices o arrays
========================================================

```r
a1 <- array(1:24, dim= c(3,4,2)) # Creacion de array
a1
```

```
, , 1

     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12

, , 2

     [,1] [,2] [,3] [,4]
[1,]   13   16   19   22
[2,]   14   17   20   23
[3,]   15   18   21   24
```



Matrices o arrays
========================================================

```r
a2 <- array(1:12, dim= c(2,3,2)) # Creacion de array
a2
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



Matrices o arrays
========================================================

```r
a3 <- array(seq(from= 10,to= 120,by= 10), dim= c(2,3,2)) # Creacion de array
a3
```

```
, , 1

     [,1] [,2] [,3]
[1,]   10   30   50
[2,]   20   40   60

, , 2

     [,1] [,2] [,3]
[1,]   70   90  110
[2,]   80  100  120
```



Matrices o arrays
========================================================

```r
a4 <- 2*a2 + a3 - 1
a4
```

```
, , 1

     [,1] [,2] [,3]
[1,]   11   35   59
[2,]   23   47   71

, , 2

     [,1] [,2] [,3]
[1,]   83  107  131
[2,]   95  119  143
```



Matrices o arrays
========================================================
R tiene varias funciones para manejar matrices, por ejemplo:

```r
m1 <- matrix(1:4, ncol= 2) 
m1
```

```
     [,1] [,2]
[1,]    1    3
[2,]    2    4
```

```r
m2 <- matrix(5:8, ncol= 2) 
m2
```

```
     [,1] [,2]
[1,]    5    7
[2,]    6    8
```



Matrices o arrays
========================================================

```r
m1 * m2 # Multiplicacion posicion a posicion
```

```
     [,1] [,2]
[1,]    5   21
[2,]   12   32
```



Matrices o arrays
========================================================

```r
m1 %*% m2 # Multiplicacion matricial
```

```
     [,1] [,2]
[1,]   23   31
[2,]   34   46
```



Matrices o arrays
========================================================

```r
eigen(m1) # valores y vectores propios
```

```
eigen() decomposition
$values
[1]  5.3722813 -0.3722813

$vectors
           [,1]       [,2]
[1,] -0.5657675 -0.9093767
[2,] -0.8245648  0.4159736
```



Matrices o arrays
========================================================
Nombre de filas y columnas

```r
m1 #Mostramos m1
```

```
     [,1] [,2]
[1,]    1    3
[2,]    2    4
```

```r
rownames(m1) <- c('a', 'b')
colnames(m1) <- c('AB', 'CD')
m1  #Mostramos m1, con nombres
```

```
  AB CD
a  1  3
b  2  4
```



Listas
========================================================
- Una lista es un objeto que consiste en una colección ordenada de objetos conocidos como sus componentes
- Se usa list() para crear una lista

```r
lst <- list(1,2,3)
lst
```

```
[[1]]
[1] 1

[[2]]
[1] 2

[[3]]
[1] 3
```



Listas
========================================================
- Los componentes no deben ser necesariamente del mismo tipo de dato y pueden ser nombrados

```r
lst <- list(ID= 123, Materia="Matematicas", Veces_Tomada= 3, Promedios= c(55,50,65))
lst
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




Listas
========================================================
- Para concatenar listas se utiliza el comando c()

```r
lst1 <- list(ID= 123, Materia="Matematicas", Veces_Tomada= 3, Promedios= c(55,50,65))
lst2 <- list(ID= 223, Materia="Matematicas", Veces_Tomada= 2, Promedios= c(45,85))
c(lst1, lst2)
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

$ID
[1] 223

$Materia
[1] "Matematicas"

$Veces_Tomada
[1] 2

$Promedios
[1] 45 85
```
 


Listas
========================================================
- ¿Qué creen que resulte al usar el comando list()?

```r
list(lst1, lst2)
```


Listas
========================================================
- ¿Se puede concatenar usando el comando list()?

```r
list(lst1, lst2)
```

```
[[1]]
[[1]]$ID
[1] 123

[[1]]$Materia
[1] "Matematicas"

[[1]]$Veces_Tomada
[1] 3

[[1]]$Promedios
[1] 55 50 65


[[2]]
[[2]]$ID
[1] 223

[[2]]$Materia
[1] "Matematicas"

[[2]]$Veces_Tomada
[1] 2

[[2]]$Promedios
[1] 45 85
```
  


Data.frames
========================================================
- Data.frame es un caso particular de lista, donde
  - Las componentes son vectores
  - Cada vector puede se de un tipo de dato distinto
  - Cada elemento, columna es una variable
  - Las columnas tienen el mismo largo
- Se podría decir que 1 data.frame es como una tabla en una hoja de excel



Data.frames
========================================================
Crear un data.frame

```r
Nombre <- c('Ana', 'Berni', 'Carlos')
Edad <- c(20,19,20)
Ciudad <- factor(c('Gye', 'Uio', 'Cue'))
df_1  <- data.frame(Nombre, Edad, Ciudad)
df_1
```

```
  Nombre Edad Ciudad
1    Ana   20    Gye
2  Berni   19    Uio
3 Carlos   20    Cue
```



Data.frames
========================================================
Crear un data.frame

```r
df_2  <- data.frame( a= Nombre, b= Edad, c= Ciudad)
df_2
```

```
       a  b   c
1    Ana 20 Gye
2  Berni 19 Uio
3 Carlos 20 Cue
```



Data.frames
========================================================
Crear un data.frame

```r
df_3  <- data.frame( Nombre= c('Ana', 'Berni', 'Carlos'), Edad = c(20,19,20), Ciudad= factor(c('Gye', 'Uio', 'Cue')) )
df_3
```

```
  Nombre Edad Ciudad
1    Ana   20    Gye
2  Berni   19    Uio
3 Carlos   20    Cue
```



Data.frames
========================================================
Modificar rownames

```r
rownames(df_3) <- paste('id_',1:3,sep='')
df_3
```

```
     Nombre Edad Ciudad
id_1    Ana   20    Gye
id_2  Berni   19    Uio
id_3 Carlos   20    Cue
```



Data.frames
========================================================
Modificar nombre de las variables

```r
names(df_3) <- c('Name', 'Age', 'City')
df_3
```

```
       Name Age City
id_1    Ana  20  Gye
id_2  Berni  19  Uio
id_3 Carlos  20  Cue
```



Data.frames
========================================================
Visualizar primeras filas

```r
head(df_3, n=2)
```

```
      Name Age City
id_1   Ana  20  Gye
id_2 Berni  19  Uio
```



Data.frames
========================================================
Visualizar últimas filas

```r
tail(df_3, n=2)
```

```
       Name Age City
id_2  Berni  19  Uio
id_3 Carlos  20  Cue
```





