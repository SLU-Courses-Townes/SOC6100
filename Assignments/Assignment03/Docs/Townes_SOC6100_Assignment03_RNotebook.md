SOC 6100 Fall 2018 Assignment 03 R Notebook
================
Malcolm S. Townes
(October 28, 2018)

Introduction
------------

This is an R Notebook for Assignment 03 in SOC 6100 Fall 2018.

Project Set Up
--------------

The following code chunk enables the R Notebook to integrate seemlessly with the project organization format. This is normally included in the R Notebook to simplify file calls and enable file portability but it has been causing an error. Per Chris Prener of Saint Louis University, the error is generated because the `here::here()` function has not been tested with certain combinations of functions. To work around this problem, I've embedded the `here()` function where I enter a file path when necessary.

``` r
knitr::opts_knit$set(root.dir = here::here())
```

Load Dependencies
-----------------

The following code chunk loads package dependencies required to perform the necessary tasks. Basic tasks include importing, reading, wrangling, and cleaning data; selecting a subset of the data; checking for unique observations, and analyzing missing data.

``` r
library(tidyverse) # loads the basic R packages
```

    ## Warning: package 'tidyverse' was built under R version 3.4.4

    ## -- Attaching packages --------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## Warning: package 'ggplot2' was built under R version 3.4.4

    ## Warning: package 'tidyr' was built under R version 3.4.4

    ## Warning: package 'purrr' was built under R version 3.4.4

    ## Warning: package 'dplyr' was built under R version 3.4.4

    ## Warning: package 'stringr' was built under R version 3.4.4

    ## Warning: package 'forcats' was built under R version 3.4.4

    ## -- Conflicts ------------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(here) # enables file portability
```

    ## Warning: package 'here' was built under R version 3.4.4

    ## here() starts at D:/SOC6100/Assignments/Assignment03

``` r
library(readr) # functions for reading data
library(dplyr) # functions for data wrangling
library(janitor) # functions for data cleaning
```

    ## Warning: package 'janitor' was built under R version 3.4.4

``` r
library(naniar) # functions for analyzing missing data
library(ggplot2) # functions for data visualizations
```

Load Raw Data
-------------

The following code chunk loads the raw data for Assignment02, which was the cleaned data from Assignment01.

``` r
Assignment03DataRaw <- read.csv(here("Data/DataRaw/NBERPatCit95to99Sample.csv"))
```

Transform Dependent Variable
----------------------------

The following code chunk creates a new variable called `CRECEIVEtr` which is a transformation of the `CRECEIVE` variable. I applied this transformation to create a new dependent variable because the histogram of the data for the `CRECEIVE` variable was positively skewed (i.e., skewed right).

``` r
Assignment03DataClean <- mutate(Assignment03DataRaw, CRECEIVElog10 = log10(CRECEIVE), CRECEIVEln = log(CRECEIVE), CRECEIVErecip = (1/CRECEIVE))
```

    ## Warning: package 'bindrcpp' was built under R version 3.4.4

Save Data
---------

The following code chunk saves the cleaned data.

``` r
write.csv(Assignment03DataClean, here("Data/DataClean/Assignment03DataClean.csv"), append = FALSE)
```

    ## Warning in write.csv(Assignment03DataClean, here("Data/DataClean/
    ## Assignment03DataClean.csv"), : attempt to set 'append' ignored
