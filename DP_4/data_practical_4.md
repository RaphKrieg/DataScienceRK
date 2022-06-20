Data Wrangling Data Practical 4
================
Raphaël Krieg
20 juin 2022

-   [Filtering](#filtering)
-   [Selecting](#selecting)
-   [Arranging](#arranging)
-   [Group by and Summarise](#group-by-and-summarise)
-   [Merging](#merging)
-   [References](#references)

``` r
library(knitr)
library(dplyr)
library(readr)
library(dslabs)
```

## Filtering

Let’s `filter()` the data for the Japan and put them in a dataframe.

``` r
Japan_country_filter <- gapminder %>% 
  filter(country == "Japan")
```

Now let’s do the same for the Brazil.

``` r
Brazil_country_filter <- gapminder %>% 
  filter(country == "Brazil")
```

## Selecting

Now `select()` some interesting variable inside our new DF.

``` r
Japan_selected <- Japan_country_filter %>%
  select(fertility, population, year)
  
str(Japan_selected)
```

    ## 'data.frame':    57 obs. of  3 variables:
    ##  $ fertility : num  2 1.98 1.97 1.97 1.97 1.98 2 2.02 2.05 2.08 ...
    ##  $ population: num  92500754 93357259 94263646 95227653 96253064 ...
    ##  $ year      : int  1960 1961 1962 1963 1964 1965 1966 1967 1968 1969 ...

``` r
head(Japan_selected) %>% kable()
```

| fertility | population | year |
|----------:|-----------:|-----:|
|      2.00 |   92500754 | 1960 |
|      1.98 |   93357259 | 1961 |
|      1.97 |   94263646 | 1962 |
|      1.97 |   95227653 | 1963 |
|      1.97 |   96253064 | 1964 |
|      1.98 |   97341852 | 1965 |

``` r
tail(Japan_selected) %>% kable()
```

|     | fertility | population | year |
|:----|----------:|-----------:|-----:|
| 52  |      1.39 |  127252900 | 2011 |
| 53  |      1.41 |  127139821 | 2012 |
| 54  |      1.42 |  126984964 | 2013 |
| 55  |      1.43 |  126794564 | 2014 |
| 56  |      1.45 |  126573481 | 2015 |
| 57  |        NA |         NA | 2016 |

Same for Brazil.

``` r
Brazil_selected <- Brazil_country_filter %>%
  select(fertility, population, year)
  
str(Brazil_selected)
```

    ## 'data.frame':    57 obs. of  3 variables:
    ##  $ fertility : num  6.21 6.19 6.14 6.06 5.95 5.82 5.66 5.49 5.33 5.17 ...
    ##  $ population: num  72493585 74706888 77007549 79368453 81751802 ...
    ##  $ year      : int  1960 1961 1962 1963 1964 1965 1966 1967 1968 1969 ...

``` r
head(Brazil_selected) %>% kable()
```

| fertility | population | year |
|----------:|-----------:|-----:|
|      6.21 |   72493585 | 1960 |
|      6.19 |   74706888 | 1961 |
|      6.14 |   77007549 | 1962 |
|      6.06 |   79368453 | 1963 |
|      5.95 |   81751802 | 1964 |
|      5.82 |   84130061 | 1965 |

``` r
tail(Brazil_selected) %>% kable()
```

|     | fertility | population | year |
|:----|----------:|-----------:|-----:|
| 52  |      1.82 |  200517584 | 2011 |
| 53  |      1.81 |  202401584 | 2012 |
| 54  |      1.80 |  204259377 | 2013 |
| 55  |      1.79 |  206077898 | 2014 |
| 56  |      1.78 |  207847528 | 2015 |
| 57  |        NA |         NA | 2016 |

## Arranging

``` r
Japan_selected %>%
  arrange(year)
```

    ##    fertility population year
    ## 1       2.00   92500754 1960
    ## 2       1.98   93357259 1961
    ## 3       1.97   94263646 1962
    ## 4       1.97   95227653 1963
    ## 5       1.97   96253064 1964
    ## 6       1.98   97341852 1965
    ## 7       2.00   98494630 1966
    ## 8       2.02   99711082 1967
    ## 9       2.05  100988866 1968
    ## 10      2.08  102323674 1969
    ## 11      2.10  103707537 1970
    ## 12      2.11  105142875 1971
    ## 13      2.11  106616535 1972
    ## 14      2.09  108085729 1973
    ## 15      2.05  109495053 1974
    ## 16      2.00  110804519 1975
    ## 17      1.94  111992858 1976
    ## 18      1.89  113067848 1977
    ## 19      1.84  114054587 1978
    ## 20      1.80  114993274 1979
    ## 21      1.78  115912104 1980
    ## 22      1.76  116821569 1981
    ## 23      1.75  117708919 1982
    ## 24      1.74  118552097 1983
    ## 25      1.73  119318921 1984
    ## 26      1.72  119988663 1985
    ## 27      1.70  120551455 1986
    ## 28      1.67  121021830 1987
    ## 29      1.64  121432942 1988
    ## 30      1.61  121831143 1989
    ## 31      1.57  122249285 1990
    ## 32      1.54  122702527 1991
    ## 33      1.50  123180357 1992
    ## 34      1.47  123658854 1993
    ## 35      1.44  124101546 1994
    ## 36      1.41  124483305 1995
    ## 37      1.39  124794817 1996
    ## 38      1.37  125048424 1997
    ## 39      1.35  125266403 1998
    ## 40      1.34  125481050 1999
    ## 41      1.32  125714674 2000
    ## 42      1.31  125974298 2001
    ## 43      1.30  126249509 2002
    ## 44      1.30  126523884 2003
    ## 45      1.30  126773081 2004
    ## 46      1.31  126978754 2005
    ## 47      1.32  127136576 2006
    ## 48      1.33  127250015 2007
    ## 49      1.34  127317900 2008
    ## 50      1.36  127340884 2009
    ## 51      1.37  127319802 2010
    ## 52      1.39  127252900 2011
    ## 53      1.41  127139821 2012
    ## 54      1.42  126984964 2013
    ## 55      1.43  126794564 2014
    ## 56      1.45  126573481 2015
    ## 57        NA         NA 2016

We can see above that the fertility rate drops along the years. However
the population seems to increase. Suggesting that the increase of
popluation has inertia. If the Fertility rate continues to drop, the
popluation should also decrease.

``` r
Brazil_selected %>%
  arrange(year)
```

    ##    fertility population year
    ## 1       6.21   72493585 1960
    ## 2       6.19   74706888 1961
    ## 3       6.14   77007549 1962
    ## 4       6.06   79368453 1963
    ## 5       5.95   81751802 1964
    ## 6       5.82   84130061 1965
    ## 7       5.66   86494987 1966
    ## 8       5.49   88853679 1967
    ## 9       5.33   91213009 1968
    ## 10      5.17   93585746 1969
    ## 11      5.02   95982453 1970
    ## 12      4.90   98402200 1971
    ## 13      4.78  100844391 1972
    ## 14      4.68  103320787 1973
    ## 15      4.59  105846274 1974
    ## 16      4.50  108431284 1975
    ## 17      4.42  111076063 1976
    ## 18      4.34  113776467 1977
    ## 19      4.26  116532153 1978
    ## 20      4.17  119341444 1979
    ## 21      4.07  122199721 1980
    ## 22      3.97  125107382 1981
    ## 23      3.85  128054757 1982
    ## 24      3.72  131014337 1983
    ## 25      3.59  133950551 1984
    ## 26      3.45  136836428 1985
    ## 27      3.31  139664639 1986
    ## 28      3.17  142437479 1987
    ## 29      3.04  145150468 1988
    ## 30      2.92  147801816 1989
    ## 31      2.81  150393143 1990
    ## 32      2.72  152916852 1991
    ## 33      2.64  155379009 1992
    ## 34      2.58  157812220 1993
    ## 35      2.54  160260508 1994
    ## 36      2.50  162755054 1995
    ## 37      2.47  165303155 1996
    ## 38      2.45  167893835 1997
    ## 39      2.43  170516482 1998
    ## 40      2.40  173153066 1999
    ## 41      2.36  175786441 2000
    ## 42      2.32  178419396 2001
    ## 43      2.26  181045592 2002
    ## 44      2.20  183627339 2003
    ## 45      2.14  186116363 2004
    ## 46      2.07  188479240 2005
    ## 47      2.00  190698241 2006
    ## 48      1.94  192784521 2007
    ## 49      1.90  194769696 2008
    ## 50      1.86  196701298 2009
    ## 51      1.84  198614208 2010
    ## 52      1.82  200517584 2011
    ## 53      1.81  202401584 2012
    ## 54      1.80  204259377 2013
    ## 55      1.79  206077898 2014
    ## 56      1.78  207847528 2015
    ## 57        NA         NA 2016

The fertility rate in 1960 was significantly higher in Brazil than in
Japan. We see similar pattern as decribed above. People have less
children as the population increases. Better health care and high life
expectancy could also explain why the population is increase as the
fertility rate is decreasing. People need “less” children to unsure a
future.

## Group by and Summarise

``` r
na.omit(gapminder) %>%
  group_by(country) %>%
  summarize(total_fertility = sum (fertility))
```

    ## # A tibble: 178 x 2
    ##    country             total_fertility
    ##    <fct>                         <dbl>
    ##  1 Albania                        83.9
    ##  2 Algeria                       278. 
    ##  3 Angola                        185. 
    ##  4 Antigua and Barbuda            48.5
    ##  5 Argentina                     150. 
    ##  6 Armenia                        36.8
    ##  7 Australia                     114. 
    ##  8 Austria                        92.2
    ##  9 Azerbaijan                     49.8
    ## 10 Bahamas                       121. 
    ## # ... with 168 more rows

``` r
na.omit(gapminder) %>%
  group_by(country) %>%
  summarize(total_fertility = sum (fertility)) %>%
  arrange(desc(total_fertility)) %>%
  head()
```

    ## # A tibble: 6 x 2
    ##   country       total_fertility
    ##   <fct>                   <dbl>
    ## 1 Rwanda                   376.
    ## 2 Burundi                  374.
    ## 3 Malawi                   357.
    ## 4 Zambia                   349.
    ## 5 Burkina Faso             347.
    ## 6 Cote d'Ivoire            345.

``` r
na.omit(gapminder) %>%
  group_by(country) %>%
  summarize(total_fertility = sum (fertility)) %>%
  arrange(desc(total_fertility)) %>%
  tail()
```

    ## # A tibble: 6 x 2
    ##   country                total_fertility
    ##   <fct>                            <dbl>
    ## 1 Czech Republic                    30.4
    ## 2 Slovenia                          29.3
    ## 3 Montenegro                        26.5
    ## 4 Estonia                           24.9
    ## 5 Bosnia and Herzegovina            24.0
    ## 6 Ireland                           23.8

We can see that the Rwanda is the most fertile country across the years
and that Ireland is the least one.

## Merging

Let’s ‘merge’ the `results_us_election_2016` and `murders` datasets.

``` r
head(full_join(results_us_election_2016, murders)) %>% kable()
```

    ## Joining, by = "state"

| state        | electoral_votes | clinton | trump | others | abb | region        | population | total |
|:-------------|----------------:|--------:|------:|-------:|:----|:--------------|-----------:|------:|
| California   |              55 |    61.7 |  31.6 |    6.7 | CA  | West          |   37253956 |  1257 |
| Texas        |              38 |    43.2 |  52.2 |    4.5 | TX  | South         |   25145561 |   805 |
| Florida      |              29 |    47.8 |  49.0 |    3.2 | FL  | South         |   19687653 |   669 |
| New York     |              29 |    59.0 |  36.5 |    4.5 | NY  | Northeast     |   19378102 |   517 |
| Illinois     |              20 |    55.8 |  38.8 |    5.4 | IL  | North Central |   12830632 |   364 |
| Pennsylvania |              20 |    47.9 |  48.6 |    3.6 | PA  | Northeast     |   12702379 |   457 |

We could `arrange` the data by the number of murders in realtionship
with the number of votes for a particular candidate. Ratio with the
population would inform us if there is more murder in region voting for
a particular candidate.

# References

Jennifer Bryan (NA). gapminder: Data from Gapminder.
<https://github.com/jennybc/gapminder>,
<http://www.gapminder.org/data/>, <https://doi.org/10.5281/>

Rogers, S. (2011, October 5). The murder map of London’s boroughs. The
Guardian.
<http://www.theguardian.com/news/datablog/interactive/2011/oct/05/murder-london-map>

WIlliams, Jack, 2022, “Elections Performance Index 2016”,
<https://doi.org/10.7910/DVN/TSUQOA>, Harvard Dataverse, V2,
UNF:6:p1RbweyWRBJUm7A957ZaAQ== \[fileUNF\]
