SOC 6100 Fall 2018 Assignment 01 R Notebook
================
Malcolm S. Townes
(September 15, 2018)

Introduction
------------

This is an R Notebook for Assignment 01 in SOC 6100 Fall 2018.

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

    ## -- Attaching packages ----------------------------------------------- tidyverse 1.2.1 --

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

    ## -- Conflicts -------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(here) # enables file portability
```

    ## here() starts at E:/SOC6100/Assignments/Assignment01

``` r
library(readr) # functions for reading data
library(dplyr) # functions for data wrangling
library(janitor) # functions for data cleaning
```

    ## Warning: package 'janitor' was built under R version 3.4.4

``` r
library(naniar) # functions for analyzing missing data
```

Load Raw Data
-------------

The following code chunk imports the raw data from the `CSV` file.

``` r
setwd("E:/SOC6100")
DataRaw <- read.table("Data/DataNBERPatentCitations/apat63_99/apat63_99.txt", sep = ",", header = TRUE, fill = TRUE, dec = ".") # import raw data
setwd("E:/SOC6100/Assignments/Assignment01")
```

Subset Data
-----------

The following code chunk creates a subset for the data of interest.

``` r
DataSubset <- filter(DataRaw, GYEAR>=1999) # subset data
```

    ## Warning: package 'bindrcpp' was built under R version 3.4.4

``` r
DataSubset <- as_tibble(DataSubset) # convert data frame to tibble
```

Inspect Data
------------

The following code chunk evaluates the subsetted data. It first checks for missing data for each variable. It then checks for missing data for each variable in each observation. Then it checks for duplicate observations with the `PATENT` variable to determine if that variable can be used as a unique identifier for each observation. Finally, it checks for duplicate observations across all variables to ensure that each observation is unique.

``` r
miss_var_summary(DataSubset, order = TRUE)
```

    ## # A tibble: 23 x 3
    ##    variable n_miss pct_miss
    ##    <chr>     <int>    <dbl>
    ##  1 CLAIMS   153486   100   
    ##  2 SECDUPBD 148958    97.0 
    ##  3 SECDLWBD 148958    97.0 
    ##  4 GENERAL  148403    96.7 
    ##  5 FWDAPLAG 148402    96.7 
    ##  6 SELFCTUB  27063    17.6 
    ##  7 SELFCTLB  27063    17.6 
    ##  8 ASSIGNEE  22782    14.8 
    ##  9 ORIGINAL   5137     3.35
    ## 10 RATIOCIT   4616     3.01
    ## # ... with 13 more rows

``` r
miss_case_summary(DataSubset, order = TRUE)
```

    ## # A tibble: 153,486 x 3
    ##     case n_miss pct_miss
    ##    <int>  <int>    <dbl>
    ##  1   858     11     47.8
    ##  2   951     11     47.8
    ##  3  1402     11     47.8
    ##  4  1482     11     47.8
    ##  5  2308     11     47.8
    ##  6  2659     11     47.8
    ##  7  3262     11     47.8
    ##  8  3291     11     47.8
    ##  9  3306     11     47.8
    ## 10  3424     11     47.8
    ## # ... with 153,476 more rows

``` r
get_dupes(DataSubset, PATENT)
```

    ## No duplicate combinations found of: PATENT

    ## # A tibble: 0 x 24
    ## # ... with 24 variables: PATENT <int>, dupe_count <int>, GYEAR <int>,
    ## #   GDATE <int>, APPYEAR <int>, COUNTRY <fct>, POSTATE <fct>,
    ## #   ASSIGNEE <int>, ASSCODE <int>, CLAIMS <int>, NCLASS <int>, CAT <int>,
    ## #   SUBCAT <int>, CMADE <int>, CRECEIVE <int>, RATIOCIT <dbl>,
    ## #   GENERAL <dbl>, ORIGINAL <dbl>, FWDAPLAG <dbl>, BCKGTLAG <dbl>,
    ## #   SELFCTUB <dbl>, SELFCTLB <dbl>, SECDUPBD <dbl>, SECDLWBD <dbl>

``` r
get_dupes(DataSubset)
```

    ## No variable names specified - using all columns.

    ## No duplicate combinations found of: PATENT, GYEAR, GDATE, APPYEAR, COUNTRY, POSTATE, ASSIGNEE, ASSCODE, CLAIMS, ... and 14 other variables

    ## # A tibble: 0 x 24
    ## # ... with 24 variables: PATENT <int>, GYEAR <int>, GDATE <int>,
    ## #   APPYEAR <int>, COUNTRY <fct>, POSTATE <fct>, ASSIGNEE <int>,
    ## #   ASSCODE <int>, CLAIMS <int>, NCLASS <int>, CAT <int>, SUBCAT <int>,
    ## #   CMADE <int>, CRECEIVE <int>, RATIOCIT <dbl>, GENERAL <dbl>,
    ## #   ORIGINAL <dbl>, FWDAPLAG <dbl>, BCKGTLAG <dbl>, SELFCTUB <dbl>,
    ## #   SELFCTLB <dbl>, SECDUPBD <dbl>, SECDLWBD <dbl>, dupe_count <int>

Clean Data
----------

I did not perform any additional cleaning of the subsetted data.

``` r
View(DataSubset, "Cleaned Data")
```

Save Data
---------

The following code chunk saves the cleaned data to a new file.

``` r
write.csv(DataSubset,here("Data/DataClean/NBERPatCit1999.csv"), append = FALSE)
```

    ## Warning in write.csv(DataSubset, here("Data/DataClean/
    ## NBERPatCit1999.csv"), : attempt to set 'append' ignored
