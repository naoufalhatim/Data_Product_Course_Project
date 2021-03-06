---
title       : Demographic Information of Sri Lanka
subtitle    : Course Project - Shiny Application and Reproducible Pitch
author      : S. Sarmilan
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
#knit        : slidify::knit2slides
github      :
    user: Sarmilan-Siva
    repo: Data_Product_Course_Project
---

## Objective

Main objective of this Shiny App is to show Sri Lankan demographic information such as Sex, Ethinicity and Religion district wise in the Sri Lankan map.

Pie chart is used to visualize multiple variables associated to district level geographical coordinates of Sri Lanka, as follows:

  1. Sex - Male, Female
  2. Ethinicity - Sinhalese, Tamils, IndianTamils, Muslims, Other Ethinic Groups
  3. Religion - Buddhist, Hindu, Islam, Christians, Other Religious Groups

--- .class #id 

## Data Sources and Preprocessing

Data was taken from the Humanitarian Data Exchange (HDX), which is an open platform for sharing data. This dataset include Sri Lanka census of population and housing 2012 with demographic information up to GND (4th Admin) level.

The data was pre-processed to:
  1. Get district (2nd Admin) level summary.
  2. Find latitude and longitude of the districts using `ggmap` package.


--- .class #id 

## Sample Code

Sample output is plotted for the `Northern` provience for `Ethinicity`.


```r
library(leaflet)
library(leaflet.minicharts)

SLdist2L <- read.csv("../data/SLdist2L.csv")
SLnort <- SLdist2L[which(SLdist2L$PROVINCE_N == "Northern"),]

MapN <- leaflet() %>%
  addProviderTiles(providers$OpenStreetMap.HOT) %>%
  addMinicharts(
        SLnort$lon, SLnort$lat,
        chartdata = SLnort[,c("Sinhalese", "Tamils", "IndianTamils", "Muslims", "OtherEthGR")],
        type = "pie", showLabels = TRUE,
        layerId = SLnort$DISTRICT_N,
        opacity = 0.8, colorPalette = c("#082d17", "#1b6337", "#36bc6a", "#57e58e", "#7c847f"),
        width = 80 * sqrt(SLnort$Pop) / sqrt(max(SLnort$Pop)), transitionTime = 0)
```

--- .class #id 

## Map with Charts

![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-1-1.png)















