
# GIS-Funktionen {#rgis}




## Nützliche Resourcen

### Links

### Packages
Ich verwende vor allem das `raster` Package um Rasterdaten zu bearbeiten und das `sf` Package für alle anderen räumlichen Datentypen (Punktdaten, Liniendaten, Polygone).

## Allgemeine Funktionen

Eine Tabelle (data.frame oder tibble) mit x und y Koordinaten in ein Objekt der Klasse `sf` umwandeln.


```r
bundeshaus <- 
  tibble(
    c("Bern Bundesplatz"),
    x = c(2600472.500),
    y = c(1199555.500)
  ) %>% 
  st_as_sf(coords = c("x", "y"), crs = 2056)
```

Daten von einem .csv File einlesen und in ein Rasterobjekt verwandeln.


```r
dhm <- read_csv("daten/digitales_hoehenmodel.csv.zip") %>% 
  rasterFromXYZ(crs = 21781)
```

Die folgenden Koordinatensysteme brauche ich relativ häufig.


```r
ch1903 <- CRS("+init=epsg:21781")       # Old Swiss grid 1903
chLV95 <- CRS("+init=epsg:2056")        # New Swiss grid 1903+ 
wgs84 <-   CRS("+init=epsg:4326")       # WGS 84 
```

Mit den folgenden Funktionen können Daten zwischen Koordinatensystemn umgewandelt werden.


```r
# Für sf objects
bundeshaus %>% st_transform(crs = 21781)

# For raster objects
dhm %>%  projectRaster(crs = 2056)
```



