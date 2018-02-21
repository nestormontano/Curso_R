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



Manejo de datos Date-Time en R
========================================================
type: sub-section




Comando as.Date
========================================================


```r
# Transformar texto a data (fecha)
as.Date('2014-09-15')
```

```
[1] "2014-09-15"
```

```r
as.Date('2014/09/15')
```

```
[1] "2014-09-15"
```

```r
as.Date('9/15/2014', format= '%m/%d/%Y')
```

```
[1] "2014-09-15"
```



as.Date
========================================================

Opciones para parámetro "format"

```
  Code           Value
1   %d     Dia del mes
2   %m    Mes (número)
3   %b Mes (abreviado)
4   %B  Mes (completo)
5   %y Año (2 digitos)
6   %Y Año (4 digitos)
```



as.Date
========================================================

Opciones para parámetro "format"

```r
as.Date('Septiembre 26, 2014',format= '%B %d, %Y')
```

```
[1] "2014-09-26"
```

```r
as.Date('Sep 26, 2014',format= '%B %d, %Y')
```

```
[1] NA
```

```r
as.Date('22JUN14',format= '%d%b%y')
```

```
[1] NA
```



as.Date
========================================================

Los tipo de objetos date se guardan internamente como numeros de dias desde 1970-01-01

```r
as.numeric(as.Date('2014-09-01'))
```

```
[1] 16314
```

```r
as.Date(16314, origin= '1970-01-01')
```

```
[1] "2014-09-01"
```



Extraer dia, mes, etc
========================================================


```r
# Funciones para extraer información
weekdays(as.Date('2014-09-01'))
```

```
[1] "lunes"
```

```r
months(as.Date('2014-09-01'))
```

```
[1] "Septiembre"
```

```r
quarters(as.Date('2014-09-01'))
```

```
[1] "Q3"
```



Extraer dia, mes, etc
========================================================


```r
# Fecha de hoy
as.Date(Sys.time())
```

```
[1] "2017-10-15"
```



The chron Package
========================================================

El paquete chron convierte objetos tipo date y times a objetos tipo "chron"

```r
library(chron)
dtimes <- c("2014-06-09 12:45:40","2014-01-29 09:30:40",
"2002-09-04 16:45:40","2002-11-13 20:00:40")
dtparts <- t(as.data.frame(strsplit(dtimes,' ')))
row.names(dtparts) = NULL
```



The chron Package
========================================================

El paquete chron convierte objetos tipo date y times a objetos tipo "chron"

```r
dtparts
```

```
     [,1]         [,2]      
[1,] "2014-06-09" "12:45:40"
[2,] "2014-01-29" "09:30:40"
[3,] "2002-09-04" "16:45:40"
[4,] "2002-11-13" "20:00:40"
```



The chron Package
========================================================

El paquete chron convierte objetos tipo date y times a objetos tipo "chron"

```r
thetimes <- chron(dates= dtparts[,1], times= dtparts[,2], format= c('y-m-d', 'h:m:s'))
thetimes
```

```
[1] (14-06-09 12:45:40) (14-01-29 09:30:40) (02-09-04 16:45:40)
[4] (02-11-13 20:00:40)
```



Calculos con objetos tipo date
========================================================


```r
# Crear un data.frame de fechas
date_1 <- as.Date('2014-09-01')
date_2 <- as.Date('2014-09-11')
df_dates <- data.frame(Fechas= as.Date(date_1:date_2, origin= '1970-01-01'))
df_dates
```

```
       Fechas
1  2014-09-01
2  2014-09-02
3  2014-09-03
4  2014-09-04
5  2014-09-05
6  2014-09-06
7  2014-09-07
8  2014-09-08
9  2014-09-09
10 2014-09-10
11 2014-09-11
```



Calculos con objetos tipo date
========================================================


```r
# Calculos con objetos tipo date
mean(df_dates$Fechas)
```

```
[1] "2014-09-06"
```

```r
max(df_dates$Fechas)
```

```
[1] "2014-09-11"
```

```r
min(df_dates$Fechas)
```

```
[1] "2014-09-01"
```



Calculos con objetos tipo date
========================================================


```r
range(df_dates$Fechas)
```

```
[1] "2014-09-01" "2014-09-11"
```

```r
# Objetos de la clase difftime
df_dates$Fechas[10] - df_dates$Fechas[1] 
```

```
Time difference of 9 days
```

```r
# df_dates$Fechas[10] + df_dates$Fechas[1]  ## ERROR
difftime(df_dates$Fechas[10], df_dates$Fechas[1], units= 'weeks')
```

```
Time difference of 1.285714 weeks
```



Calculos con objetos tipo date
========================================================


```r
# Armado de secuencias
seq(from= as.Date('2014-09-01'), by= 'days', length= 5)
```

```
[1] "2014-09-01" "2014-09-02" "2014-09-03" "2014-09-04" "2014-09-05"
```

```r
seq(from= as.Date('2014-09-01'), to= as.Date('2014-10-01'), by= 'weeks')
```

```
[1] "2014-09-01" "2014-09-08" "2014-09-15" "2014-09-22" "2014-09-29"
```



Calculos con objetos tipo date
========================================================


```r
# Extraer informacion usando format
format(df_dates$Fechas,'%a')
```

```
 [1] "lun." "mar." "mié." "jue." "vie." "sáb." "dom." "lun." "mar." "mié."
[11] "jue."
```

```r
format(df_dates$Fechas,'%A')
```

```
 [1] "lunes"     "martes"    "miércoles" "jueves"    "viernes"  
 [6] "sábado"    "domingo"   "lunes"     "martes"    "miércoles"
[11] "jueves"   
```

```r
format(df_dates$Fechas,'%d')
```

```
 [1] "01" "02" "03" "04" "05" "06" "07" "08" "09" "10" "11"
```



Calculos con objetos tipo date
========================================================


```r
# Extraer informacion usando format
format(df_dates$Fechas,'%m')
```

```
 [1] "09" "09" "09" "09" "09" "09" "09" "09" "09" "09" "09"
```

```r
format(df_dates$Fechas,'%b')
```

```
 [1] "Sept." "Sept." "Sept." "Sept." "Sept." "Sept." "Sept." "Sept."
 [9] "Sept." "Sept." "Sept."
```

```r
format(df_dates$Fechas,'%Y')
```

```
 [1] "2014" "2014" "2014" "2014" "2014" "2014" "2014" "2014" "2014" "2014"
[11] "2014"
```



Paquete lubridate
========================================================


```r
library(lubridate)
# Convertir texto a data
mdy('Ene-01-2000')
```

```
[1] "2000-01-20"
```

```r
dmy('01 Dic 2000')
```

```
[1] NA
```

```r
# Convertir texto a data-time
ymd_hms("2013 Julio 24 23h55m26s")
```

```
[1] "2013-07-24 23:55:26 UTC"
```



Paquete lubridate
========================================================


```r
# Convertir texto a data
dmy(c('terminado el 25 de Agosto de 2014', 'dado el 15 12 2013', '21-09-2015'))
```

```
[1] "2014-08-25" "2013-12-15" "2015-09-21"
```

```r
# Al convertir se debe conservar el orden definido, sino devuelve NA
dmy(c('terminado el 25 de Agosto de 2014', 'dado el 15 12 2013', '2015-21-09'))
```

```
[1] "2014-08-25" "2013-12-15" NA          
```



Paquete lubridate
========================================================

Modificar elementos de la fecha

```r
txt_fecha <- as.Date('2014-09-15')
txt_fecha
```

```
[1] "2014-09-15"
```

```r
month(txt_fecha) <- 2
txt_fecha
```

```
[1] "2014-02-15"
```

```r
day(txt_fecha) <- 7
txt_fecha
```

```
[1] "2014-02-07"
```



Paquete lubridate
========================================================


```r
# Obtener elementos del objeto
hour(txt_fecha)
```

```
[1] 0
```

```r
day(txt_fecha)
```

```
[1] 7
```

```r
week(txt_fecha)
```

```
[1] 6
```



Paquete lubridate
========================================================


```r
# Obtener elementos del objeto
month(txt_fecha)
```

```
[1] 2
```

```r
year(txt_fecha)
```

```
[1] 2014
```

```r
tz(txt_fecha)
```

```
[1] "UTC"
```



Paquete lubridate
========================================================


```r
# Dia de la semana
wday(txt_fecha)
```

```
[1] 6
```

```r
wday(txt_fecha, label=T)
```

```
[1] Fri
Levels: Sun < Mon < Tues < Wed < Thurs < Fri < Sat
```

```r
# Dia del año
yday(txt_fecha)
```

```
[1] 38
```



Paquete lubridate
========================================================


```r
# Crear lapsos de tiempo
dminutes(10)
```

```
[1] "600s (~10 minutes)"
```

```r
ddays(5)
```

```
[1] "432000s (~5 days)"
```

```r
dyears(5)
```

```
[1] "157680000s (~5 years)"
```

```r
# dmonths no existe pues el tiempo que dura cada mes no es fijo
```



Paquete lubridate
========================================================


```r
# Aritmética con fechas
as.Date('2014-09-15') + ddays(25)
```

```
[1] "2014-10-10"
```

```r
as.Date('2014-09-15') - dyears(5)
```

```
[1] "2009-09-16"
```



Paquete lubridate
========================================================


```r
# Obtener la fecha hora de hoy
as.Date(now())
```

```
[1] "2017-10-15"
```

```r
as.Date(today())
```

```
[1] "2017-10-15"
```



Paquete lubridate
========================================================


```r
# Funcion techo para fechas
ceiling_date( as.Date('2014-04-19'), unit = 'month')
```

```
[1] "2014-05-01"
```

```r
ceiling_date( as.Date('2014-04-19'), unit = 'year')
```

```
[1] "2015-01-01"
```

```r
ceiling_date( as.Date('2014-04-19'), unit = 'month') - ddays(1)
```

```
[1] "2014-04-30"
```


