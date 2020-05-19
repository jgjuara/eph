# eph

<!-- badges: start -->
[![Travis-CI Build
Status](https://api.travis-ci.org/holatam/eph.svg?branch=master)](https://travis-ci.org/holatam/eph)
[![Coverage
status](https://codecov.io/gh/holatam/eph/branch/master/graph/badge.svg)](https://codecov.io/gh/holatam/eph?branch=master)
[![CRAN status](https://www.r-pkg.org/badges/version/eph)](https://cran.r-project.org/package=eph)
[![](http://cranlogs.r-pkg.org/badges/grand-total/eph?color=blue)](https://cran.r-project.org/package=eph)
[![](http://cranlogs.r-pkg.org/badges/last-month/eph?color=blue)](https://cran.r-project.org/package=eph)
[![DOI](https://zenodo.org/badge/142294444.svg)](https://zenodo.org/badge/latestdoi/142294444)
  <!-- badges: end -->



# Caja de Herramientas para el procesamiento de la Encuesta Permanente de Hogares

## Descripción
La librería `eph` tiene por objecto facilitar el trabajo de aquellos usuarios y usuarias de la [Encuesta Permanente de Hogares - INDEC](https://www.indec.gob.ar/bases-de-datos.asp) que deseen procesar datos de la misma mediante el lenguaje de programación [R](https://www.r-project.org/).


Sus principales funciones son:

- **`get_microdata()`**: Descarga las bases de microdatos directamente de la página de INDEC

- **`organize_labels()`**: Etiqueta las bases siguiendo el último [diseño de registro](https://www.indec.gob.ar/ftp/cuadros/menusuperior/eph/EPH_registro_t218.pdf)

- **`calculate_tabulates()`**: Crea tabulados uni o bivariados con ponderacion, totales parciales y porcentajes.

- **`calculate_poverty()`**: Replica el cálculo de pobreza e indigencia del INDEC, pero para las bases trimestrales^[el calculo oficial se realiza sobre bases semestrales no publicadas]

- **`get_poverty_lines()`**: Descarga de canasta basica alimentaria y canasta basica total

- **`organize_panels()`**: Arma un pool de datos para trabajar con panel en la EPH continua

## Cómo citar este paquete en tu artículo

Podés citar este paquete como "se obtuvieron y/o normalizaron los datos de la Encuesta Permanente de Hogares (EPH-INDEC) utilizando el paquete de R 'eph' (Kozlowski et al, 2020)".   
   
La referencia completa para incluir en la bibliografía es:   
   
```
Diego Kozlowski, Pablo Tiscornia, Guido Weksler, German Rosati and Natsumi Shokida (2020). eph: Argentina's Permanent Household Survey Data and Manipulation Utilities. R package version https://doi.org/10.5281/zenodo.3462677
```

Si necesitás la entrada bib: 

```{bib}
@Manual{kozlowski2020,
    title = {eph: Argentina's Permanent Household Survey Data and Manipulation Utilities},
    author = {Diego Kozlowski and Pablo Tiscornia and Guido Weksler and German Rosati and Natsumi Shokida},
    year = {2020},
    doi = {10.5281/zenodo.3462677},
    url = {https://holatam.github.io/eph/},
  }
```

## Instalación


Para la versión estable

```r

install.packages('eph')

```

Para la versión en desarrollo 

```r

# install.packages('devtools') si no tiene instalado devtools

devtools::install_github("holatam/eph")

```

## Modo de uso

### Descarga de microdatos -->

```r

# Cargo la libreria
library(eph)

# Obtengo la base de microdatos para individuos
base_2016t3_ind <- get_microdata(year = 2016, trimester = 3, type = 'individual')

# Obtengo la base de microdatos para hogares
base_2016t3_hog <- get_microdata(year = 2016, trimester = 3, type = 'hogar')

```

### Tabulados uni / bivariados con ponderación, totales parciales y porcentajes -->

```r

# Cargo la libreria
library(eph)

# Obtengo el tabulado con el cruce de variables entre Condición de actividad (`ESTADO`) y Sexo (`CH04`):
calculate_tabulates(base, x = "ESTADO", y = "CH04", add.totals = "row", add.percentage = "col")

 ESTADO/CH04      1      2
           0   0.1%   0.1%
           1  48.9%  34.4%
           2   3.7%   3.2%
           3  31.7%  48.5%
           4  15.6%  13.8%
       Total 100.0% 100.0%

```

### Etiquetas [labels] para base de microdatos -->

```r

# Cargo la librería
library(eph)

# Obtengo la base de microdatos para individuos
base_2016t3_ind <- get_microdata(year = 2016, trimester = 3, type = 'individual')

# Agrego las etiquetas a las variables y sus valores
base_2016t3_ind <- organize_labels(base_2016t3_ind, type='individual')

# Ejemplo 1:
# Obtengo el tabulado con el cruce de variables entre Condición de actividad (`ESTADO`) y Sexo (`CH04`), con etiquetas:
calculate_tabulates(base, x = "ESTADO", y = "CH04", add.totals = "row", add.percentage = "col")

                                                                  ESTADO/CH04  Varon  Mujer
 Entrevista individual no realizada (no respuesta al cuestionario individual)   0.1%   0.1%
                                                                      Ocupado  48.9%  34.4%
                                                                   Desocupado   3.7%   3.2%
                                                                     Inactivo  31.7%  48.5%
                                                            Menor de 10 años.  15.6%  13.8%
                                                                        Total 100.0% 100.0%
          
 
```

## Aportes de la comunidad

Este paquete se propone incorporar cualquier función de propósitos generales que utilice como base los datos de la Encuesta Permanente de Hogares. Todos los aportes en este sentido son bienvenidos.

Si trabajas con la EPH y querés agregar tu función, te recomendamos que leas el siguiente [issue](https://github.com/pablinte/eph/issues/5#issue-407890587) con consejos de como colaborar
