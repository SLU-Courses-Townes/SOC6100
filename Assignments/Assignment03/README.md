# SOC 6100 Fall 2018 Assignment 03

## Folder Description

This folder contains subfolders and files for Assignment 03 in the Fall 2018 session of SOC 6100 Regression Analysis and Multivariable Methods. This course is a requirement for the Ph.D. program in public and social policy at Saint Louis University.

## Folder Contents

This folder contains the following subfolders and files:

* Data/ - shapefiles and geodatabases necessary to complete the lab
* Docs/ - files to perform the tasks as outlined in the assignment instructions
* Results/ - plots as required by the assignment instructions
* .gitkeep
* README.md

## Reason for Creating Folder

Malcolm Townes created this folder to organize the work for the assignment according to best practices for analysis development and reproducible research.


## About the Data 

### Source
The data for this assignment comes from the National Bureau of Economic Research (NBER) data file on U.S. Patent Citations, which is available at the following:

www.nber.org/patents/[http://www.nber.org/patents/]

The raw data contains data on 23 variables for 2,923,922 observations covering the period from 1963 to 1999.

### Data Modifications
Data modifications comprised the creation a subset of the raw data. The subsetted data contains 24 variables and 2,000 randomly selected observations from the period 1995 to 1999. Included among the variables is a recipricol transformation variable (`CRECEIVEtr`) of the `CRECEIVE` variable. 