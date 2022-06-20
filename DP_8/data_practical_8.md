Linear model I Data Practical 8
================
Raphaël Krieg
21 juin 2022

-   [Loading a dataset (Reading a .csv
    file)](#loading-a-dataset-reading-a-csv-file)
-   [Data analysis](#data-analysis)
-   [Best positive predictor](#best-positive-predictor)
-   [Best negative predictor](#best-negative-predictor)
-   [Correlation doesn’t mean
    causation](#correlation-doesnt-mean-causation)
-   [References](#references)

``` r
library(readr)
library(dslabs)
library(tidyverse)
library(knitr)
library(ggplot2)
```

## Loading a dataset (Reading a .csv file)

``` r
data_wine <- read_csv("https://raw.githubusercontent.com/aniruddhachoudhury/Red-Wine-Quality/master/winequality-red.csv")
```

    ## Rows: 1599 Columns: 12
    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## dbl (12): fixed acidity, volatile acidity, citric acid, residual sugar, chlo...
    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
str(data_wine)
```

    ## spec_tbl_df [1,599 x 12] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ fixed acidity       : num [1:1599] 7.4 7.8 7.8 11.2 7.4 7.4 7.9 7.3 7.8 7.5 ...
    ##  $ volatile acidity    : num [1:1599] 0.7 0.88 0.76 0.28 0.7 0.66 0.6 0.65 0.58 0.5 ...
    ##  $ citric acid         : num [1:1599] 0 0 0.04 0.56 0 0 0.06 0 0.02 0.36 ...
    ##  $ residual sugar      : num [1:1599] 1.9 2.6 2.3 1.9 1.9 1.8 1.6 1.2 2 6.1 ...
    ##  $ chlorides           : num [1:1599] 0.076 0.098 0.092 0.075 0.076 0.075 0.069 0.065 0.073 0.071 ...
    ##  $ free sulfur dioxide : num [1:1599] 11 25 15 17 11 13 15 15 9 17 ...
    ##  $ total sulfur dioxide: num [1:1599] 34 67 54 60 34 40 59 21 18 102 ...
    ##  $ density             : num [1:1599] 0.998 0.997 0.997 0.998 0.998 ...
    ##  $ pH                  : num [1:1599] 3.51 3.2 3.26 3.16 3.51 3.51 3.3 3.39 3.36 3.35 ...
    ##  $ sulphates           : num [1:1599] 0.56 0.68 0.65 0.58 0.56 0.56 0.46 0.47 0.57 0.8 ...
    ##  $ alcohol             : num [1:1599] 9.4 9.8 9.8 9.8 9.4 9.4 9.4 10 9.5 10.5 ...
    ##  $ quality             : num [1:1599] 5 5 5 6 5 5 5 7 7 5 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   `fixed acidity` = col_double(),
    ##   ..   `volatile acidity` = col_double(),
    ##   ..   `citric acid` = col_double(),
    ##   ..   `residual sugar` = col_double(),
    ##   ..   chlorides = col_double(),
    ##   ..   `free sulfur dioxide` = col_double(),
    ##   ..   `total sulfur dioxide` = col_double(),
    ##   ..   density = col_double(),
    ##   ..   pH = col_double(),
    ##   ..   sulphates = col_double(),
    ##   ..   alcohol = col_double(),
    ##   ..   quality = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

## Data analysis

I want to know the best predictor for the quality of the wine.
Explanatory variables could be any of the above projected onto the
quality variable.

``` r
cor.test(data_wine$`fixed acidity`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`fixed acidity` and data_wine$quality
    ## t = 4.996, df = 1597, p-value = 6.496e-07
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.07548957 0.17202667
    ## sample estimates:
    ##       cor 
    ## 0.1240516

``` r
cor.test(data_wine$`volatile acidity`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`volatile acidity` and data_wine$quality
    ## t = -16.954, df = 1597, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.4313210 -0.3482032
    ## sample estimates:
    ##        cor 
    ## -0.3905578

``` r
cor.test(data_wine$`citric acid`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`citric acid` and data_wine$quality
    ## t = 9.2875, df = 1597, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.1793415 0.2723711
    ## sample estimates:
    ##       cor 
    ## 0.2263725

``` r
cor.test(data_wine$`residual sugar`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`residual sugar` and data_wine$quality
    ## t = 0.5488, df = 1597, p-value = 0.5832
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.03531327  0.06271056
    ## sample estimates:
    ##        cor 
    ## 0.01373164

``` r
cor.test(data_wine$chlorides, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$chlorides and data_wine$quality
    ## t = -5.1948, df = 1597, p-value = 2.313e-07
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.17681041 -0.08039344
    ## sample estimates:
    ##        cor 
    ## -0.1289066

``` r
cor.test(data_wine$`free sulfur dioxide`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`free sulfur dioxide` and data_wine$quality
    ## t = -2.0269, df = 1597, p-value = 0.04283
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.099430290 -0.001638987
    ## sample estimates:
    ##         cor 
    ## -0.05065606

``` r
cor.test(data_wine$`total sulfur dioxide`, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$`total sulfur dioxide` and data_wine$quality
    ## t = -7.5271, df = 1597, p-value = 8.622e-14
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.2320162 -0.1373252
    ## sample estimates:
    ##        cor 
    ## -0.1851003

``` r
cor.test(data_wine$density, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$density and data_wine$quality
    ## t = -7.0997, df = 1597, p-value = 1.875e-12
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.2220365 -0.1269870
    ## sample estimates:
    ##        cor 
    ## -0.1749192

``` r
cor.test(data_wine$pH, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$pH and data_wine$quality
    ## t = -2.3109, df = 1597, p-value = 0.02096
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.106451268 -0.008734972
    ## sample estimates:
    ##         cor 
    ## -0.05773139

``` r
cor.test(data_wine$sulphates, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$sulphates and data_wine$quality
    ## t = 10.38, df = 1597, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.2049011 0.2967610
    ## sample estimates:
    ##       cor 
    ## 0.2513971

``` r
cor.test(data_wine$alcohol, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$alcohol and data_wine$quality
    ## t = 21.639, df = 1597, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.4373540 0.5132081
    ## sample estimates:
    ##       cor 
    ## 0.4761663

``` r
cor.test(data_wine$quality, data_wine$quality)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data_wine$quality and data_wine$quality
    ## t = Inf, df = 1597, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  1 1
    ## sample estimates:
    ## cor 
    ##   1

## Best positive predictor

Alcohol seems to be the best predictor of a high rating with a positive
correlation of **0.4761663**

## Best negative predictor

Volatile acidity seems to negatively correlate (**-0.3905578**) with the
rating of a wine. The less there is, the higher the rating will be. It’s
quite logic in fact, nobody want an unstable wine that could be acidic.

``` r
general<-lm(data_wine$alcohol ~ data_wine$quality)
summary(general)
```

    ## 
    ## Call:
    ## lm(formula = data_wine$alcohol ~ data_wine$quality)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -2.2517 -0.6233 -0.2233  0.5483  4.8767 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        6.88160    0.16532   41.62   <2e-16 ***
    ## data_wine$quality  0.62835    0.02904   21.64   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.9374 on 1597 degrees of freedom
    ## Multiple R-squared:  0.2267, Adjusted R-squared:  0.2263 
    ## F-statistic: 468.3 on 1 and 1597 DF,  p-value: < 2.2e-16

## Correlation doesn’t mean causation

Generally speaking, correlation doesn’t mean causation. In our case, the
alcohol rate could actually cause the higher ratings because I cannot
imagine a relation going on the opposite side (E.g ratings cannot
influence the alcohol rate in a specific bottle).

``` r
ggplot(data_wine,aes(alcohol, quality, color=alcohol)) +
    geom_point()+
    geom_smooth(method = "lm", se = TRUE,color="black")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](data_practical_8_files/figure-gfm/unnamed-chunk-8-1.png)<!-- --> #
Important remark

Even though the correlation was strong between the alcohol rate and the
ratings, the graph above shows very clearly that the regression line
fits very poorly the various data points. We can firmly say that there
is absolutely no causation between the two variables and that the
correlation between them is very artificial. In order to truly
understand what makes a good Wine, we need to investigate further ahead.

# References

Chodhury, A. (2022). Red-Wine-Quality \[Jupyter Notebook\].
<https://github.com/aniruddhachoudhury/Red-Wine-Quality/blob/6956eb70b1d1d89486055f09001903882a554d31/winequality-red.csv>
(Original work published 2018)
