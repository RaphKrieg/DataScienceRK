Data Data Practical 3
================
Raphaël Krieg
20 juin 2022

-   [Dataset 1 - Built-in R dataset](#dataset-1---built-in-r-dataset)
-   [Dataset 2 - The Pudding Dataset](#dataset-2---the-pudding-dataset)
-   [Dataset 3 - The Dplyr Dataset](#dataset-3---the-dplyr-dataset)
-   [References](#references)

``` r
library(knitr)
library(dplyr)
library(readr)
library(dslabs)
```

### Dataset 1 - Built-in R dataset

In the following code-chunk, I load the built-in R dataset called
“trees”

``` r
data(trees)
str(trees)
```

    ## 'data.frame':    31 obs. of  3 variables:
    ##  $ Girth : num  8.3 8.6 8.8 10.5 10.7 10.8 11 11 11.1 11.2 ...
    ##  $ Height: num  70 65 63 72 81 83 66 75 80 75 ...
    ##  $ Volume: num  10.3 10.3 10.2 16.4 18.8 19.7 15.6 18.2 22.6 19.9 ...

We can see that there are 3 **numerical** variables: 1.
[Girth](https://en.wikipedia.org/wiki/Tree_girth_measurement) 2.
[Heigth](https://en.wikipedia.org/wiki/Tree_height_measurement) 3.
[Volume](https://en.wikipedia.org/wiki/Tree_volume_measurement)

These three variables are **quantitve and continuous**

### Dataset 2 - The Pudding Dataset

Here we have a fun exemple of the `mars_weather` dataset. For more
information about the different variables please follow this
[link](https://data.world/the-pudding/mars-weather)

``` r
mars_weather <- read.csv("https://raw.githubusercontent.com/the-pudding/data/master/mars-weather/mars-weather.csv")
str(mars_weather)
```

    ## 'data.frame':    1894 obs. of  10 variables:
    ##  $ id              : int  1895 1893 1894 1892 1889 1891 1890 1888 1887 1886 ...
    ##  $ terrestrial_date: chr  "2018-02-27" "2018-02-26" "2018-02-25" "2018-02-24" ...
    ##  $ sol             : int  1977 1976 1975 1974 1973 1972 1971 1970 1969 1968 ...
    ##  $ ls              : int  135 135 134 134 133 133 132 132 131 131 ...
    ##  $ month           : chr  "Month 5" "Month 5" "Month 5" "Month 5" ...
    ##  $ min_temp        : num  -77 -77 -76 -77 -78 -78 -78 -77 -76 -76 ...
    ##  $ max_temp        : num  -10 -10 -16 -13 -18 -14 -13 -16 -16 -19 ...
    ##  $ pressure        : num  727 728 729 729 730 730 731 731 732 732 ...
    ##  $ wind_speed      : num  NaN NaN NaN NaN NaN NaN NaN NaN NaN NaN ...
    ##  $ atmo_opacity    : chr  "Sunny" "Sunny" "Sunny" "Sunny" ...

This dataset includes **10 variables**

1.  *id* Type: Number. **Quantitative and disrcete**
2.  *terrestrial_date* Type: Date. **Qualitative and ordinal**
3.  *sol* Type: Number. **Quantitative and discrete**
4.  *Ls* Type: Number. **Quantitative and discrete**
5.  *month* Type: Text. **Qualitative and ordinal**
6.  *min_temp* Type: Number. **Quantitative and continuous**
7.  *max_temp* Type: Number. **Quantitative and continuous**
8.  *pressure* Type: Number. **Quantitative and continuous**
9.  *wind_speed* Type: Number. **Quantitative and continuous**
10. *atmo_opacity* Type: Text. **Qualitative and nominal**

### Dataset 3 - The Dplyr Dataset

The next dataset is recovered from the extended built-in Datasets from R
via the dplyr package.

[Information](https://search.r-project.org/CRAN/refmans/FlexDir/html/oliveoil.html)
about the dataset `olive`.

``` r
str(olive)
```

    ## 'data.frame':    572 obs. of  10 variables:
    ##  $ region     : Factor w/ 3 levels "Northern Italy",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ area       : Factor w/ 9 levels "Calabria","Coast-Sardinia",..: 5 5 5 5 5 5 5 5 5 5 ...
    ##  $ palmitic   : num  10.75 10.88 9.11 9.66 10.51 ...
    ##  $ palmitoleic: num  0.75 0.73 0.54 0.57 0.67 0.49 0.66 0.61 0.6 0.55 ...
    ##  $ stearic    : num  2.26 2.24 2.46 2.4 2.59 2.68 2.64 2.35 2.39 2.13 ...
    ##  $ oleic      : num  78.2 77.1 81.1 79.5 77.7 ...
    ##  $ linoleic   : num  6.72 7.81 5.49 6.19 6.72 6.78 6.18 7.34 7.09 6.33 ...
    ##  $ linolenic  : num  0.36 0.31 0.31 0.5 0.5 0.51 0.49 0.39 0.46 0.26 ...
    ##  $ arachidic  : num  0.6 0.61 0.63 0.78 0.8 0.7 0.56 0.64 0.83 0.52 ...
    ##  $ eicosenoic : num  0.29 0.29 0.29 0.35 0.46 0.44 0.29 0.35 0.33 0.3 ...

This dataset has **10 variables**

1.  *region* Type: Factor **Qualitative and discrete**
2.  *area* Type: Factor.**Qualitative and discrete**
3.  to 10. Are chemicals values. **Quantitatives and continuous**

# References

Atkinson, A. C. (1985) Plots, Transformations and Regression. Oxford
University Press.

Azzalini, A., Menardi, G. (2014). Clustering via Nonparametric Density
Estimation: The R Package pdfCluster. Journal of Statistical Software,
57(11), 1-26, URL <http://www.jstatsoft.org/v57/i11/>.

Azzalini A., Torelli N. (2007). Clustering via nonparametric density
estimation. Statistics and Computing, 17, 71-80.

Data sets. (2022). \[HTML\]. The Pudding.
<https://github.com/the-pudding/data/blob/44a0a67f932489ed5ae0552b04bd9f82b97125dd/mars-weather/mars-weather.csv>
(Original work published 2017)
