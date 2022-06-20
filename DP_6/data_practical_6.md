Data Visualization II Data Practical 6
================
Raphaël Krieg
20 juin 2022

-   [Question: Does the speed increases the distance required to
    stop?](#question-does-the-speed-increases-the-distance-required-to-stop)

``` r
library(readr)
library(dslabs)
library(tidyverse)
library(knitr)
library(ggplot2)
```

Let’s have a look at the `cars` dataframe.

``` r
str(cars)
```

    ## 'data.frame':    50 obs. of  2 variables:
    ##  $ speed: num  4 4 7 7 8 9 10 10 10 11 ...
    ##  $ dist : num  2 10 4 22 16 10 18 26 34 17 ...

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

## Question: Does the speed increases the distance required to stop?

``` r
ggplot(cars, aes(speed, dist))+
  geom_point()+
  geom_smooth(method = "lm", se = FALSE)
```

    ## `geom_smooth()` using formula 'y ~ x'

![](data_practical_6_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

We can see a strong correlation backing the hypothesis formulated above.
