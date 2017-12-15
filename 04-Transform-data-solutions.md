Transform Data (solutions)
================

<!-- This file by Charlotte Wickham is licensed under a Creative Commons Attribution 4.0 International License, adapted from the orignal work at https://github.com/rstudio/master-the-tidyverse by RStudio. -->
``` r
library(tidyverse)
library(gapminder)

# Toy dataset to use
pollution <- tribble(
       ~city,   ~size, ~amount, 
  "New York", "large",      23,
  "New York", "small",      14,
    "London", "large",      22,
    "London", "small",      16,
   "Beijing", "large",      121,
   "Beijing", "small",      56
)
```

gapminder
---------

``` r
gapminder
```

    ## # A tibble: 1,704 x 6
    ##        country continent  year lifeExp      pop gdpPercap
    ##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453
    ##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530
    ##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007
    ##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971
    ##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811
    ##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134
    ##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114
    ##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959
    ##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414
    ## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414
    ## # ... with 1,694 more rows

Your Turn 1
-----------

-   `filter()` selects rows
-   logical tests

See if you can use the logical operators to manipulate our code below to show:

The data for Canada

``` r
filter(gapminder, country == "Canada")
```

    ## # A tibble: 12 x 6
    ##    country continent  year lifeExp      pop gdpPercap
    ##     <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
    ##  1  Canada  Americas  1952  68.750 14785584  11367.16
    ##  2  Canada  Americas  1957  69.960 17010154  12489.95
    ##  3  Canada  Americas  1962  71.300 18985849  13462.49
    ##  4  Canada  Americas  1967  72.130 20819767  16076.59
    ##  5  Canada  Americas  1972  72.880 22284500  18970.57
    ##  6  Canada  Americas  1977  74.210 23796400  22090.88
    ##  7  Canada  Americas  1982  75.760 25201900  22898.79
    ##  8  Canada  Americas  1987  76.860 26549700  26626.52
    ##  9  Canada  Americas  1992  77.950 28523502  26342.88
    ## 10  Canada  Americas  1997  78.610 30305843  28954.93
    ## 11  Canada  Americas  2002  79.770 31902268  33328.97
    ## 12  Canada  Americas  2007  80.653 33390141  36319.24

All data for countries in Oceania

``` r
filter(gapminder, continent == "Oceania")
```

    ## # A tibble: 24 x 6
    ##      country continent  year lifeExp      pop gdpPercap
    ##       <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
    ##  1 Australia   Oceania  1952   69.12  8691212  10039.60
    ##  2 Australia   Oceania  1957   70.33  9712569  10949.65
    ##  3 Australia   Oceania  1962   70.93 10794968  12217.23
    ##  4 Australia   Oceania  1967   71.10 11872264  14526.12
    ##  5 Australia   Oceania  1972   71.93 13177000  16788.63
    ##  6 Australia   Oceania  1977   73.49 14074100  18334.20
    ##  7 Australia   Oceania  1982   74.74 15184200  19477.01
    ##  8 Australia   Oceania  1987   76.32 16257249  21888.89
    ##  9 Australia   Oceania  1992   77.56 17481977  23424.77
    ## 10 Australia   Oceania  1997   78.83 18565243  26997.94
    ## # ... with 14 more rows

Rows where the life expectancy is greater than 82

``` r
filter(gapminder, lifeExp > 82)
```

    ## # A tibble: 2 x 6
    ##            country continent  year lifeExp       pop gdpPercap
    ##             <fctr>    <fctr> <int>   <dbl>     <int>     <dbl>
    ## 1 Hong Kong, China      Asia  2007  82.208   6980412  39724.98
    ## 2            Japan      Asia  2007  82.603 127467972  31656.07

Your Turn 2
-----------

Use Boolean operators to alter the code below to return only the rows that contain:

-   Canada before 1970

``` r
filter(gapminder, country == "Canada", year < 1970)
```

    ## # A tibble: 4 x 6
    ##   country continent  year lifeExp      pop gdpPercap
    ##    <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
    ## 1  Canada  Americas  1952   68.75 14785584  11367.16
    ## 2  Canada  Americas  1957   69.96 17010154  12489.95
    ## 3  Canada  Americas  1962   71.30 18985849  13462.49
    ## 4  Canada  Americas  1967   72.13 20819767  16076.59

-   Countries where life expectancy in 2007 is below 50

``` r
filter(gapminder, year == 2007, lifeExp < 50)
```

    ## # A tibble: 19 x 6
    ##                     country continent  year lifeExp       pop gdpPercap
    ##                      <fctr>    <fctr> <int>   <dbl>     <int>     <dbl>
    ##  1              Afghanistan      Asia  2007  43.828  31889923  974.5803
    ##  2                   Angola    Africa  2007  42.731  12420476 4797.2313
    ##  3                  Burundi    Africa  2007  49.580   8390505  430.0707
    ##  4 Central African Republic    Africa  2007  44.741   4369038  706.0165
    ##  5         Congo, Dem. Rep.    Africa  2007  46.462  64606759  277.5519
    ##  6            Cote d'Ivoire    Africa  2007  48.328  18013409 1544.7501
    ##  7            Guinea-Bissau    Africa  2007  46.388   1472041  579.2317
    ##  8                  Lesotho    Africa  2007  42.592   2012649 1569.3314
    ##  9                  Liberia    Africa  2007  45.678   3193942  414.5073
    ## 10                   Malawi    Africa  2007  48.303  13327079  759.3499
    ## 11               Mozambique    Africa  2007  42.082  19951656  823.6856
    ## 12                  Nigeria    Africa  2007  46.859 135031164 2013.9773
    ## 13                   Rwanda    Africa  2007  46.242   8860588  863.0885
    ## 14             Sierra Leone    Africa  2007  42.568   6144562  862.5408
    ## 15                  Somalia    Africa  2007  48.159   9118773  926.1411
    ## 16             South Africa    Africa  2007  49.339  43997828 9269.6578
    ## 17                Swaziland    Africa  2007  39.613   1133066 4513.4806
    ## 18                   Zambia    Africa  2007  42.384  11746035 1271.2116
    ## 19                 Zimbabwe    Africa  2007  43.487  12311143  469.7093

-   Countries where life expectancy in 2007 is below 50, and are not in Africa.

``` r
filter(gapminder, year == 2007, lifeExp < 50, !(continent == "Africa"))
```

    ## # A tibble: 1 x 6
    ##       country continent  year lifeExp      pop gdpPercap
    ##        <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan      Asia  2007  43.828 31889923  974.5803

Your Turn 3
-----------

Alter the code to:

-   Add an africa column, which contains TRUE is the country is on the Africa continent.
-   Add a rank\_pop column to rank each row in gapminder from largest pop to smallest pop.

``` r
mutate(gapminder, 
  africa = continent == "Africa",
  rank_pop = min_rank(desc(pop)))
```

    ## # A tibble: 1,704 x 8
    ##        country continent  year lifeExp      pop gdpPercap africa rank_pop
    ##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>  <lgl>    <int>
    ##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453  FALSE      762
    ##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530  FALSE      706
    ##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007  FALSE      638
    ##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971  FALSE      576
    ##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811  FALSE      536
    ##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134  FALSE      497
    ##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114  FALSE      544
    ##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959  FALSE      524
    ##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414  FALSE      476
    ## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414  FALSE      388
    ## # ... with 1,694 more rows

Your Turn 4
-----------

Use summarise() to compute three statistics about the data:

-   The first (minimum) year in the dataset
-   The last (maximum) year in the dataset
-   The number of countries represented in the data (Hint: use cheatsheet)

``` r
gapminder %>% 
  summarise(first = min(year), 
            last = max(year),
            n_countries = n_distinct(country))
```

    ## # A tibble: 1 x 3
    ##   first  last n_countries
    ##   <dbl> <dbl>       <int>
    ## 1  1952  2007         142

Your Turn 5
-----------

Extract the rows where continent == "Africa" and year == 2007.

Then use summarise() and summary functions to find:

1.  The number of unique countries
2.  The median life expectancy

``` r
gapminder %>% 
  filter(continent == "Africa", year == 2007) %>% 
  summarise(n_countries = n_distinct(country),
    med_life_exp = median(lifeExp))
```

    ## # A tibble: 1 x 2
    ##   n_countries med_life_exp
    ##         <int>        <dbl>
    ## 1          52      52.9265

Your Turn 6
-----------

Find the median life expectancy by continent

``` r
gapminder %>%
  group_by(continent) %>% 
  summarise(med_life_exp = median(lifeExp)) 
```

    ## # A tibble: 5 x 2
    ##   continent med_life_exp
    ##      <fctr>        <dbl>
    ## 1    Africa      47.7920
    ## 2  Americas      67.0480
    ## 3      Asia      61.7915
    ## 4    Europe      72.2410
    ## 5   Oceania      73.6650

Your Turn 7
-----------

Brainstorm with your neighbor the sequence of operations to find: the country with biggest jump in life expectancy (between any two consecutive records) for each continent.

1.  Find jumps between time points for all countries:

    1.  Group by country
    2.  Add jump variable

2.  Rank jump within continent

    1.  Group by continent
    2.  Add rank of jump variable

3.  Filter out countries with rank 1

Your Turn 8
-----------

Find the country with biggest jump in life expectancy (between any two consecutive records) for each continent.

``` r
# One of many solutions
gapminder %>%
  group_by(country) %>%
  mutate(jump = lifeExp - lag(lifeExp)) %>%
  group_by(continent) %>%
  mutate(rank = min_rank(desc(jump))) %>%
  filter(rank == 1)
```

    ## # A tibble: 5 x 8
    ## # Groups:   continent [5]
    ##       country continent  year lifeExp     pop  gdpPercap   jump  rank
    ##        <fctr>    <fctr> <int>   <dbl>   <int>      <dbl>  <dbl> <int>
    ## 1    Bulgaria    Europe  1957  66.610 7651254  3008.6707  7.010     1
    ## 2    Cambodia      Asia  1982  50.957 7272485   624.4755 19.737     1
    ## 3 El Salvador  Americas  1987  63.154 4842194  4140.4421  6.550     1
    ## 4 New Zealand   Oceania  1992  76.330 3437674 18363.3249  2.010     1
    ## 5      Rwanda    Africa  1997  36.087 7212583   589.9445 12.488     1

------------------------------------------------------------------------

Take aways
==========

-   Extract cases with `filter()`
-   Make new variables, with `mutate()`
-   Make tables of summaries with `summarise()`
-   Do groupwise operations with `group_by()`
-   Connect operations with `%>%`
