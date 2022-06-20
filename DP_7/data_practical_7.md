Data Modeling Data Practical 7
================
Raphaël Krieg
21 juin 2022

-   [I’m a Star Wars fan !](#im-a-star-wars-fan-)
    -   [Description of the dataset](#description-of-the-dataset)
    -   [Statistical test](#statistical-test)
-   [References](#references)

``` r
library(readr)
library(dslabs)
library(tidyverse)
library(knitr)
library(ggplot2)
```

# I’m a Star Wars fan !

### Description of the dataset

``` r
starwars1 <- na.omit(starwars)
starwars1
```

    ## # A tibble: 29 x 14
    ##    name    height  mass hair_color  skin_color eye_color birth_year sex   gender
    ##    <chr>    <int> <dbl> <chr>       <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke S~    172    77 blond       fair       blue            19   male  mascu~
    ##  2 Darth ~    202   136 none        white      yellow          41.9 male  mascu~
    ##  3 Leia O~    150    49 brown       light      brown           19   fema~ femin~
    ##  4 Owen L~    178   120 brown, grey light      blue            52   male  mascu~
    ##  5 Beru W~    165    75 brown       light      blue            47   fema~ femin~
    ##  6 Biggs ~    183    84 black       light      brown           24   male  mascu~
    ##  7 Obi-Wa~    182    77 auburn, wh~ fair       blue-gray       57   male  mascu~
    ##  8 Anakin~    188    84 blond       fair       blue            41.9 male  mascu~
    ##  9 Chewba~    228   112 brown       unknown    blue           200   male  mascu~
    ## 10 Han So~    180    80 brown       fair       brown           29   male  mascu~
    ## # ... with 19 more rows, and 5 more variables: homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

``` r
ggplot(starwars1, aes(y=eye_color))+
  geom_bar(aes(fill=homeworld))+  
  theme(axis.text.y = element_text(angle = 360, vjust = 0.3, hjust=1,size=6))
```

![](data_practical_7_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

H1 Planet origin has an impact on the color of your eyes. Ho Colorof
eyes is not influenced by the planet origin.

## Statistical test

``` r
chisq.test(table(starwars1$homeworld,starwars1$eye_color))
```

    ## Warning in chisq.test(table(starwars1$homeworld, starwars1$eye_color)): Chi-
    ## squared approximation may be incorrect

    ## 
    ##  Pearson's Chi-squared test
    ## 
    ## data:  table(starwars1$homeworld, starwars1$eye_color)
    ## X-squared = 164.58, df = 133, p-value = 0.0328

We cannot reject HO meaning that the homeworld seem to dictate which
color will be your eyes.

# References
