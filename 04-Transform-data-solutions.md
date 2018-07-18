Transform Data (solutions)
================

<!-- This file by Charlotte Wickham is licensed under a Creative Commons Attribution 4.0 International License, adapted from the orignal work at https://github.com/rstudio/master-the-tidyverse by RStudio. -->
``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.5
    ## ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
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
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
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
    ##    <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Canada  Americas   1952    68.8 14785584    11367.
    ##  2 Canada  Americas   1957    70.0 17010154    12490.
    ##  3 Canada  Americas   1962    71.3 18985849    13462.
    ##  4 Canada  Americas   1967    72.1 20819767    16077.
    ##  5 Canada  Americas   1972    72.9 22284500    18971.
    ##  6 Canada  Americas   1977    74.2 23796400    22091.
    ##  7 Canada  Americas   1982    75.8 25201900    22899.
    ##  8 Canada  Americas   1987    76.9 26549700    26627.
    ##  9 Canada  Americas   1992    78.0 28523502    26343.
    ## 10 Canada  Americas   1997    78.6 30305843    28955.
    ## 11 Canada  Americas   2002    79.8 31902268    33329.
    ## 12 Canada  Americas   2007    80.7 33390141    36319.

All data for countries in Oceania

``` r
filter(gapminder, continent == "Oceania")
```

    ## # A tibble: 24 x 6
    ##    country   continent  year lifeExp      pop gdpPercap
    ##    <fct>     <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Australia Oceania    1952    69.1  8691212    10040.
    ##  2 Australia Oceania    1957    70.3  9712569    10950.
    ##  3 Australia Oceania    1962    70.9 10794968    12217.
    ##  4 Australia Oceania    1967    71.1 11872264    14526.
    ##  5 Australia Oceania    1972    71.9 13177000    16789.
    ##  6 Australia Oceania    1977    73.5 14074100    18334.
    ##  7 Australia Oceania    1982    74.7 15184200    19477.
    ##  8 Australia Oceania    1987    76.3 16257249    21889.
    ##  9 Australia Oceania    1992    77.6 17481977    23425.
    ## 10 Australia Oceania    1997    78.8 18565243    26998.
    ## # ... with 14 more rows

Rows where the life expectancy is greater than 82

``` r
filter(gapminder, lifeExp > 82)
```

    ## # A tibble: 2 x 6
    ##   country          continent  year lifeExp       pop gdpPercap
    ##   <fct>            <fct>     <int>   <dbl>     <int>     <dbl>
    ## 1 Hong Kong, China Asia       2007    82.2   6980412    39725.
    ## 2 Japan            Asia       2007    82.6 127467972    31656.

Your Turn 2
-----------

Use Boolean operators to alter the code below to return only the rows that contain:

-   Canada before 1970

``` r
filter(gapminder, country == "Canada", year < 1970)
```

    ## # A tibble: 4 x 6
    ##   country continent  year lifeExp      pop gdpPercap
    ##   <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Canada  Americas   1952    68.8 14785584    11367.
    ## 2 Canada  Americas   1957    70.0 17010154    12490.
    ## 3 Canada  Americas   1962    71.3 18985849    13462.
    ## 4 Canada  Americas   1967    72.1 20819767    16077.

-   Countries where life expectancy in 2007 is below 50

``` r
filter(gapminder, year == 2007, lifeExp < 50)
```

    ## # A tibble: 19 x 6
    ##    country                  continent  year lifeExp       pop gdpPercap
    ##    <fct>                    <fct>     <int>   <dbl>     <int>     <dbl>
    ##  1 Afghanistan              Asia       2007    43.8  31889923      975.
    ##  2 Angola                   Africa     2007    42.7  12420476     4797.
    ##  3 Burundi                  Africa     2007    49.6   8390505      430.
    ##  4 Central African Republic Africa     2007    44.7   4369038      706.
    ##  5 Congo, Dem. Rep.         Africa     2007    46.5  64606759      278.
    ##  6 Cote d'Ivoire            Africa     2007    48.3  18013409     1545.
    ##  7 Guinea-Bissau            Africa     2007    46.4   1472041      579.
    ##  8 Lesotho                  Africa     2007    42.6   2012649     1569.
    ##  9 Liberia                  Africa     2007    45.7   3193942      415.
    ## 10 Malawi                   Africa     2007    48.3  13327079      759.
    ## 11 Mozambique               Africa     2007    42.1  19951656      824.
    ## 12 Nigeria                  Africa     2007    46.9 135031164     2014.
    ## 13 Rwanda                   Africa     2007    46.2   8860588      863.
    ## 14 Sierra Leone             Africa     2007    42.6   6144562      863.
    ## 15 Somalia                  Africa     2007    48.2   9118773      926.
    ## 16 South Africa             Africa     2007    49.3  43997828     9270.
    ## 17 Swaziland                Africa     2007    39.6   1133066     4513.
    ## 18 Zambia                   Africa     2007    42.4  11746035     1271.
    ## 19 Zimbabwe                 Africa     2007    43.5  12311143      470.

-   Countries where life expectancy in 2007 is below 50, and are not in Africa.

``` r
filter(gapminder, year == 2007, lifeExp < 50, !(continent == "Africa"))
```

    ## # A tibble: 1 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       2007    43.8 31889923      975.

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
    ##    country     continent  year lifeExp      pop gdpPercap africa rank_pop
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl> <lgl>     <int>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779. FALSE       762
    ##  2 Afghanistan Asia       1957    30.3  9240934      821. FALSE       706
    ##  3 Afghanistan Asia       1962    32.0 10267083      853. FALSE       638
    ##  4 Afghanistan Asia       1967    34.0 11537966      836. FALSE       576
    ##  5 Afghanistan Asia       1972    36.1 13079460      740. FALSE       536
    ##  6 Afghanistan Asia       1977    38.4 14880372      786. FALSE       497
    ##  7 Afghanistan Asia       1982    39.9 12881816      978. FALSE       544
    ##  8 Afghanistan Asia       1987    40.8 13867957      852. FALSE       524
    ##  9 Afghanistan Asia       1992    41.7 16317921      649. FALSE       476
    ## 10 Afghanistan Asia       1997    41.8 22227415      635. FALSE       388
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
    ## 1          52         52.9

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
    ##   <fct>            <dbl>
    ## 1 Africa            47.8
    ## 2 Americas          67.0
    ## 3 Asia              61.8
    ## 4 Europe            72.2
    ## 5 Oceania           73.7

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
    ##   country     continent  year lifeExp     pop gdpPercap  jump  rank
    ##   <fct>       <fct>     <int>   <dbl>   <int>     <dbl> <dbl> <int>
    ## 1 Bulgaria    Europe     1957    66.6 7651254     3009.  7.01     1
    ## 2 Cambodia    Asia       1982    51.0 7272485      624. 19.7      1
    ## 3 El Salvador Americas   1987    63.2 4842194     4140.  6.55     1
    ## 4 New Zealand Oceania    1992    76.3 3437674    18363.  2.01     1
    ## 5 Rwanda      Africa     1997    36.1 7212583      590. 12.5      1

------------------------------------------------------------------------

Take aways
==========

-   Extract cases with `filter()`
-   Make new variables, with `mutate()`
-   Make tables of summaries with `summarise()`
-   Do groupwise operations with `group_by()`
-   Connect operations with `%>%`
