
# Verschiedenes {#misc}



## Units {#units}

Das Packet `units` ist nützlich um mit verschiedenen Einheiten umzugehen und diese einfach ineinander umwandeln zu können. Das Packet wird automatisch gebraucht, wenn Längen und Flächen von räumlichen Daten mit dem dem Packet `sf`berechnet werden. Im folgenden ein Beispiel mit räumlichen Flächenberechnungen

Example: How units are used in package `sf`:


```r
library(units)

# Load biogeographic region shapefile as example
dat <- st_read("daten//BGR/biogreg.shp", quiet = TRUE)

# Calculate area (they are of class units, the unit is square meteres)
(area <- st_area(dat))
```

```
## Units: [m^2]
##  [1]  108439676 1330857641 4250867716 4198648313  478255132 4801875024
##  [7]  268386654 1933997234  784897484  237302331 1617081664 1628143377
## [13] 8804154605 5828156490 4836468172  187214296
```

```r
# Change area to km^2
area %>% set_units("km^2")
```

```
## Units: [km^2]
##  [1]  108.4397 1330.8576 4250.8677 4198.6483  478.2551 4801.8750  268.3867
##  [8] 1933.9972  784.8975  237.3023 1617.0817 1628.1434 8804.1546 5828.1565
## [15] 4836.4682  187.2143
```

```r
# Change class to numeric
area %>% as.numeric()
```

```
##  [1]  108439676 1330857641 4250867716 4198648313  478255132 4801875024
##  [7]  268386654 1933997234  784897484  237302331 1617081664 1628143377
## [13] 8804154605 5828156490 4836468172  187214296
```

```r
# Note: if you want to make a calculations with units, other elements need to be of 
# class units as well
area > as_units(1000, "km^2")
```

```
##  [1] FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE
## [13]  TRUE  TRUE  TRUE FALSE
```

```r
area - as_units(10, "km^2")
```

```
## Units: [m^2]
##  [1]   98439676 1320857641 4240867716 4188648313  468255132 4791875024
##  [7]  258386654 1923997234  774897484  227302331 1607081664 1618143377
## [13] 8794154605 5818156490 4826468172  177214296
```


