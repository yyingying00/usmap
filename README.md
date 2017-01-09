# usmap
[![Version](https://badge.fury.io/gh/pdil%2Fusmap.svg)](https://github.com/pdil/usmap/releases) [![Build Status](https://travis-ci.org/pdil/usmap.svg?branch=master)](https://travis-ci.org/pdil/usmap) [![codecov](https://codecov.io/gh/pdil/usmap/branch/master/graph/badge.svg)](https://codecov.io/gh/pdil/usmap)

<img src="https://github.com/pdil/us-map/blob/master/blank-state-map.png" width="400" height="272" />
<img src="https://github.com/pdil/us-map/blob/master/blank-county-map.png" width="400" height="272" />

## Purpose
Typically in R it is difficult to create nice US [choropleths](https://en.wikipedia.org/wiki/Choropleth_map) that include Alaska and Hawaii. The functions presented here attempt to elegantly solve this problem by manually moving these states to a new location and providing a fortified data frame for mapping and visualization. This allows the user to easily add data to color the map.

## Shape Files
The shape files that we use to plot the maps in R are located in the `data-raw` folder. For more information refer to the [US Census Bureau](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html). Maps at both the state and county levels are included for convenience (zip code maps may be included in the future).

## Installation
To install the package from this repository, run the following code in an R console:
```{r}
install.package("devtools")
devtools::install_github("pdil/usmap")
```
Installing using ```devtools::install_github``` will provide the most recent developer build of ```usmap```.

When ```usmap``` is released and approved by CRAN it can be installed using ```install.packages("usmap")```.

## Features
* Obtain map with certain region breakdown
```{r}
state_map <- us_map(regions = "states")
county_map <- us_map(regions = "counties")
```
* Include only certain states
```{r}
new_england_states <- c("Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont")
new_england_map <- us_map(regions = "states", include = new_england_states)
```
* Look up FIPS codes for states and counties
```{r}
fips("New Jersey")
# "34"

fips("NJ", county = "Mercer")
# "34021"
```
* Retrieve states or counties with FIPS codes
```{r}
fips_info(c("34", "35"))
#         full abbr fips
# 1 New Jersey   NJ   34 
# 2 New Mexico   NM   35

fips_info(c("34021", "35021"))
#         full abbr         county  fips
# 1 New Jersey   NJ  Mercer County 34021
# 2 New Mexico   NM Harding County 35021
```

#### Code for above maps
```{r}
# States map
usmap::plot_usmap(regions = "states")

# Counties map
usmap::plot_usmap(regions = "counties")
```
