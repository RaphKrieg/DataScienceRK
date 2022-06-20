Data Visualization I Data Practical 5
================
Raphaël Krieg
20 juin 2022

-   [Dataset description and modification wide into
    long.](#dataset-description-and-modification-wide-into-long)
-   [Data visualization via ggplot.](#data-visualization-via-ggplot)
-   [Uniting](#uniting)
-   [Separating](#separating)
-   [References](#references)

``` r
library(readr)
library(dslabs)
library(tidyverse)
library(knitr)
library(ggplot2)
```

## Dataset description and modification wide into long.

I chose the `divorce_margarine` dataset. We have the *divorce rate in
the state of Maine* in the U.S and the *consumption of margarine per
capita*. Both are **numeric** and **continuous**. The last variable is
the *year*, a **quantitative discrete** variable.

``` r
str(divorce_margarine)
```

    ## 'data.frame':    10 obs. of  3 variables:
    ##  $ divorce_rate_maine              : num  5 4.7 4.6 4.4 4.3 4.1 4.2 4.2 4.2 4.1
    ##  $ margarine_consumption_per_capita: num  8.2 7 6.5 5.3 5.2 4 4.6 4.5 4.2 3.7
    ##  $ year                            : int  2000 2001 2002 2003 2004 2005 2006 2007 2008 2009

``` r
names(divorce_margarine)[1] <-'Divorce'
names(divorce_margarine)[2] <-'Margarine'
names(divorce_margarine)[3] <-'Year'
df_wide <- data.frame(divorce_margarine)
df_wide %>% kable()
```

| Divorce | Margarine | Year |
|--------:|----------:|-----:|
|     5.0 |       8.2 | 2000 |
|     4.7 |       7.0 | 2001 |
|     4.6 |       6.5 | 2002 |
|     4.4 |       5.3 | 2003 |
|     4.3 |       5.2 | 2004 |
|     4.1 |       4.0 | 2005 |
|     4.2 |       4.6 | 2006 |
|     4.2 |       4.5 | 2007 |
|     4.2 |       4.2 | 2008 |
|     4.1 |       3.7 | 2009 |

``` r
str(divorce_margarine)
```

    ## 'data.frame':    10 obs. of  3 variables:
    ##  $ Divorce  : num  5 4.7 4.6 4.4 4.3 4.1 4.2 4.2 4.2 4.1
    ##  $ Margarine: num  8.2 7 6.5 5.3 5.2 4 4.6 4.5 4.2 3.7
    ##  $ Year     : int  2000 2001 2002 2003 2004 2005 2006 2007 2008 2009

``` r
names(divorce_margarine)[1] <-'Divorce'
names(divorce_margarine)[2] <-'Margarine'
names(divorce_margarine)[3] <-'Year'
data_long <- gather(divorce_margarine, condition, measurement, Divorce:Year, factor_key=TRUE)
data_long %>% kable()
```

| condition | measurement |
|:----------|------------:|
| Divorce   |         5.0 |
| Divorce   |         4.7 |
| Divorce   |         4.6 |
| Divorce   |         4.4 |
| Divorce   |         4.3 |
| Divorce   |         4.1 |
| Divorce   |         4.2 |
| Divorce   |         4.2 |
| Divorce   |         4.2 |
| Divorce   |         4.1 |
| Margarine |         8.2 |
| Margarine |         7.0 |
| Margarine |         6.5 |
| Margarine |         5.3 |
| Margarine |         5.2 |
| Margarine |         4.0 |
| Margarine |         4.6 |
| Margarine |         4.5 |
| Margarine |         4.2 |
| Margarine |         3.7 |
| Year      |      2000.0 |
| Year      |      2001.0 |
| Year      |      2002.0 |
| Year      |      2003.0 |
| Year      |      2004.0 |
| Year      |      2005.0 |
| Year      |      2006.0 |
| Year      |      2007.0 |
| Year      |      2008.0 |
| Year      |      2009.0 |

## Data visualization via ggplot.

``` r
ggplot(divorce_margarine, aes(Divorce, Margarine)) + 
  geom_line (colour = "grey50") + 
  geom_point(aes(colour = Margarine))
```

![](data_practical_5_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

## Uniting

``` r
united_marga_divo <- divorce_margarine %>% unite(unified)
head(united_marga_divo) %>% kable()
```

| unified      |
|:-------------|
| 5_8.2_2000   |
| 4.7_7\_2001  |
| 4.6_6.5_2002 |
| 4.4_5.3_2003 |
| 4.3_5.2_2004 |
| 4.1_4\_2005  |

## Separating

``` r
separate_marga_divo <- united_marga_divo %>% separate(unified, into=c("Margarine","Divorce", "year"), sep="_")
head(separate_marga_divo) %>% kable()
```

| Margarine | Divorce | year |
|:----------|:--------|:-----|
| 5         | 8.2     | 2000 |
| 4.7       | 7       | 2001 |
| 4.6       | 6.5     | 2002 |
| 4.4       | 5.3     | 2003 |
| 4.3       | 5.2     | 2004 |
| 4.1       | 4       | 2005 |

# References

divorce_margarine function—RDocumentation. (n.d.). Retrieved June 20,
2022, from
<https://www.rdocumentation.org/packages/dslabs/versions/0.7.4/topics/divorce_margarine>
