Data Basics (solutions)
================

<!-- This file by Charlotte Wickham is licensed under a Creative Commons Attribution 4.0 International License. -->
``` r
library(tidyverse)
library(haven)
library(readxl)
```

Tabular Data
============

You might not see much difference between these two in this notebook, but one is a tibble and one is a data frame:

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer      model displ  year   cyl      trans   drv   cty   hwy
    ##           <chr>      <chr> <dbl> <int> <int>      <chr> <chr> <int> <int>
    ##  1         audi         a4   1.8  1999     4   auto(l5)     f    18    29
    ##  2         audi         a4   1.8  1999     4 manual(m5)     f    21    29
    ##  3         audi         a4   2.0  2008     4 manual(m6)     f    20    31
    ##  4         audi         a4   2.0  2008     4   auto(av)     f    21    30
    ##  5         audi         a4   2.8  1999     6   auto(l5)     f    16    26
    ##  6         audi         a4   2.8  1999     6 manual(m5)     f    18    26
    ##  7         audi         a4   3.1  2008     6   auto(av)     f    18    27
    ##  8         audi a4 quattro   1.8  1999     4 manual(m5)     4    18    26
    ##  9         audi a4 quattro   1.8  1999     4   auto(l5)     4    16    25
    ## 10         audi a4 quattro   2.0  2008     4 manual(m6)     4    20    28
    ## # ... with 224 more rows, and 2 more variables: fl <chr>, class <chr>

``` r
quakes
```

    ## # A tibble: 1,000 x 5
    ##       lat   long depth   mag stations
    ##     <dbl>  <dbl> <int> <dbl>    <int>
    ##  1 -20.42 181.62   562   4.8       41
    ##  2 -20.62 181.03   650   4.2       15
    ##  3 -26.00 184.10    42   5.4       43
    ##  4 -17.97 181.66   626   4.1       19
    ##  5 -20.42 181.96   649   4.0       11
    ##  6 -19.68 184.31   195   4.0       12
    ##  7 -11.70 166.10    82   4.8       43
    ##  8 -28.11 181.93   194   4.4       15
    ##  9 -28.74 181.74   211   4.7       35
    ## 10 -17.47 179.59   622   4.3       19
    ## # ... with 990 more rows

Your turn 1
-----------

Take a look at these two datasets, by typing their names into the console:

-   quakes
-   mpg

Printing a data frame in R will print all columns and all the rows (until meeting some maximum printing value). In contrast, printing a tibble will print only as many columns as will fit on your screen and only 10 rows of the the data. Tibbles are a special type of data frame and have a few other special behaviours too. In this example, mpg is a tibble and quakes is a data frame.

Your turn 2
-----------

Try running each line one by one, with Cmd/Ctrl + r. What do they do?

``` r
dim(x = mpg)     
```

    ## [1] 234  11

``` r
names(x = mpg)   
```

    ##  [1] "manufacturer" "model"        "displ"        "year"        
    ##  [5] "cyl"          "trans"        "drv"          "cty"         
    ##  [9] "hwy"          "fl"           "class"

``` r
glimpse(x = mpg) 
```

    ## Observations: 234
    ## Variables: 11
    ## $ manufacturer <chr> "audi", "audi", "audi", "audi", "audi", "audi", "...
    ## $ model        <chr> "a4", "a4", "a4", "a4", "a4", "a4", "a4", "a4 qua...
    ## $ displ        <dbl> 1.8, 1.8, 2.0, 2.0, 2.8, 2.8, 3.1, 1.8, 1.8, 2.0,...
    ## $ year         <int> 1999, 1999, 2008, 2008, 1999, 1999, 2008, 1999, 1...
    ## $ cyl          <int> 4, 4, 4, 4, 6, 6, 6, 4, 4, 4, 4, 6, 6, 6, 6, 6, 6...
    ## $ trans        <chr> "auto(l5)", "manual(m5)", "manual(m6)", "auto(av)...
    ## $ drv          <chr> "f", "f", "f", "f", "f", "f", "f", "4", "4", "4",...
    ## $ cty          <int> 18, 21, 20, 21, 16, 18, 18, 18, 16, 20, 19, 15, 1...
    ## $ hwy          <int> 29, 29, 31, 30, 26, 26, 27, 26, 25, 28, 27, 25, 2...
    ## $ fl           <chr> "p", "p", "p", "p", "p", "p", "p", "p", "p", "p",...
    ## $ class        <chr> "compact", "compact", "compact", "compact", "comp...

``` r
View(x = mpg)  
```

-   `dim()` prints the dimensions, number of observations then number of variables
-   `names()` prints the column names
-   `glimpse()` gives an overview of the data, including all variable names, their types, and the first few entries.
-   `View()` opens up a GUI viewer.

Your turn 3
-----------

How many rows of data are in quakes?

You could use `dim()`, `glimpse()` or `View()`:

``` r
dim(quakes)
```

    ## [1] 1000    5

``` r
# or more specifically
nrow(quakes)
```

    ## [1] 1000

What are the names of the variables in quakes?

``` r
names(quakes)
```

    ## [1] "lat"      "long"     "depth"    "mag"      "stations"

Your turn 4
-----------

Run the chunk to get help on `mpg`. What is this data?

``` r
?mpg
```

> "This dataset contains a subset of the fuel economy data that the EPA makes available on <http://fueleconomy.gov>. It contains only models which had a new release every year between 1999 and 2008 - this was used as a proxy for the popularity of the car."

Vector Data
===========

Your turn 5
-----------

Take another look at mpg. What kind of data is in each column?

``` r
mpg # and view in the notebook
```

    ## # A tibble: 234 x 11
    ##    manufacturer      model displ  year   cyl      trans   drv   cty   hwy
    ##           <chr>      <chr> <dbl> <int> <int>      <chr> <chr> <int> <int>
    ##  1         audi         a4   1.8  1999     4   auto(l5)     f    18    29
    ##  2         audi         a4   1.8  1999     4 manual(m5)     f    21    29
    ##  3         audi         a4   2.0  2008     4 manual(m6)     f    20    31
    ##  4         audi         a4   2.0  2008     4   auto(av)     f    21    30
    ##  5         audi         a4   2.8  1999     6   auto(l5)     f    16    26
    ##  6         audi         a4   2.8  1999     6 manual(m5)     f    18    26
    ##  7         audi         a4   3.1  2008     6   auto(av)     f    18    27
    ##  8         audi a4 quattro   1.8  1999     4 manual(m5)     4    18    26
    ##  9         audi a4 quattro   1.8  1999     4   auto(l5)     4    16    25
    ## 10         audi a4 quattro   2.0  2008     4 manual(m6)     4    20    28
    ## # ... with 224 more rows, and 2 more variables: fl <chr>, class <chr>

``` r
glimpse(mpg)
```

    ## Observations: 234
    ## Variables: 11
    ## $ manufacturer <chr> "audi", "audi", "audi", "audi", "audi", "audi", "...
    ## $ model        <chr> "a4", "a4", "a4", "a4", "a4", "a4", "a4", "a4 qua...
    ## $ displ        <dbl> 1.8, 1.8, 2.0, 2.0, 2.8, 2.8, 3.1, 1.8, 1.8, 2.0,...
    ## $ year         <int> 1999, 1999, 2008, 2008, 1999, 1999, 2008, 1999, 1...
    ## $ cyl          <int> 4, 4, 4, 4, 6, 6, 6, 4, 4, 4, 4, 6, 6, 6, 6, 6, 6...
    ## $ trans        <chr> "auto(l5)", "manual(m5)", "manual(m6)", "auto(av)...
    ## $ drv          <chr> "f", "f", "f", "f", "f", "f", "f", "4", "4", "4",...
    ## $ cty          <int> 18, 21, 20, 21, 16, 18, 18, 18, 16, 20, 19, 15, 1...
    ## $ hwy          <int> 29, 29, 31, 30, 26, 26, 27, 26, 25, 28, 27, 25, 2...
    ## $ fl           <chr> "p", "p", "p", "p", "p", "p", "p", "p", "p", "p",...
    ## $ class        <chr> "compact", "compact", "compact", "compact", "comp...

There are character, double and integer variables.

Importing Data
==============

Your Turn 6
-----------

Take a look in the data/ directory in the project folder.

Try reading in each of:

-   `deaths.xls`
-   `nimbus.csv`
-   `iris.sav`

``` r
deaths <- read_excel("data/deaths.xls")
deaths
```

    ## # A tibble: 18 x 6
    ##                `Lots of people`                     X__1   X__2     X__3
    ##                           <chr>                    <chr>  <chr>    <chr>
    ##  1 simply cannot resist writing                     <NA>   <NA>     <NA>
    ##  2                           at                      the    top     <NA>
    ##  3                           or                  merging   <NA>     <NA>
    ##  4                         Name               Profession    Age Has kids
    ##  5                  David Bowie                 musician     69     TRUE
    ##  6                Carrie Fisher                    actor     60     TRUE
    ##  7                  Chuck Berry                 musician     90     TRUE
    ##  8                  Bill Paxton                    actor     61     TRUE
    ##  9                       Prince                 musician     57     TRUE
    ## 10                 Alan Rickman                    actor     69    FALSE
    ## 11           Florence Henderson                    actor     82     TRUE
    ## 12                   Harper Lee                   author     89    FALSE
    ## 13                Zsa Zsa Gábor                    actor     99     TRUE
    ## 14               George Michael                 musician     53    FALSE
    ## 15                         Some                     <NA>   <NA>     <NA>
    ## 16                         <NA> also like to write stuff   <NA>     <NA>
    ## 17                         <NA>                     <NA> at the  bottom,
    ## 18                         <NA>                     <NA>   <NA>     <NA>
    ## # ... with 2 more variables: X__4 <chr>, X__5 <chr>

``` r
iris <- read_spss("data/iris.sav")
iris
```

    ## # A tibble: 150 x 5
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
    ##           <dbl>       <dbl>        <dbl>       <dbl> <dbl+lbl>
    ##  1          5.1         3.5          1.4         0.2         1
    ##  2          4.9         3.0          1.4         0.2         1
    ##  3          4.7         3.2          1.3         0.2         1
    ##  4          4.6         3.1          1.5         0.2         1
    ##  5          5.0         3.6          1.4         0.2         1
    ##  6          5.4         3.9          1.7         0.4         1
    ##  7          4.6         3.4          1.4         0.3         1
    ##  8          5.0         3.4          1.5         0.2         1
    ##  9          4.4         2.9          1.4         0.2         1
    ## 10          4.9         3.1          1.5         0.1         1
    ## # ... with 140 more rows

``` r
nimbus <- read_csv("data/nimbus.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   date = col_datetime(format = ""),
    ##   longitude = col_double(),
    ##   latitude = col_double(),
    ##   ozone = col_character()
    ## )

``` r
nimbus
```

    ## # A tibble: 18,963 x 4
    ##          date longitude latitude ozone
    ##        <dttm>     <dbl>    <dbl> <chr>
    ##  1 1985-10-01  -179.375    -73.5   302
    ##  2 1985-10-01  -178.125    -73.5   302
    ##  3 1985-10-01  -176.875    -73.5   302
    ##  4 1985-10-01  -175.625    -73.5   302
    ##  5 1985-10-01  -174.375    -73.5   304
    ##  6 1985-10-01  -173.125    -73.5   304
    ##  7 1985-10-01  -171.875    -73.5   304
    ##  8 1985-10-01  -170.625    -73.5   304
    ##  9 1985-10-01  -164.375    -73.5   287
    ## 10 1985-10-01  -163.125    -73.5   287
    ## # ... with 18,953 more rows

Your Turn 7
-----------

Can you see what is wrong with the Excel file when it is imported?

Scan the Arguments section of ?read\_excel, can you find an argument that might help? Try it!

``` r
deaths
```

    ## # A tibble: 18 x 6
    ##                `Lots of people`                     X__1   X__2     X__3
    ##                           <chr>                    <chr>  <chr>    <chr>
    ##  1 simply cannot resist writing                     <NA>   <NA>     <NA>
    ##  2                           at                      the    top     <NA>
    ##  3                           or                  merging   <NA>     <NA>
    ##  4                         Name               Profession    Age Has kids
    ##  5                  David Bowie                 musician     69     TRUE
    ##  6                Carrie Fisher                    actor     60     TRUE
    ##  7                  Chuck Berry                 musician     90     TRUE
    ##  8                  Bill Paxton                    actor     61     TRUE
    ##  9                       Prince                 musician     57     TRUE
    ## 10                 Alan Rickman                    actor     69    FALSE
    ## 11           Florence Henderson                    actor     82     TRUE
    ## 12                   Harper Lee                   author     89    FALSE
    ## 13                Zsa Zsa Gábor                    actor     99     TRUE
    ## 14               George Michael                 musician     53    FALSE
    ## 15                         Some                     <NA>   <NA>     <NA>
    ## 16                         <NA> also like to write stuff   <NA>     <NA>
    ## 17                         <NA>                     <NA> at the  bottom,
    ## 18                         <NA>                     <NA>   <NA>     <NA>
    ## # ... with 2 more variables: X__4 <chr>, X__5 <chr>

Looks like the first few rows don't contain data, but some multi-column notations. There's also some at the end.

One solution is to use the arguments `skip` and `n_max`:

``` r
deaths <- read_excel("data/deaths.xls", skip = 4, n_max = 10)
deaths
```

    ## # A tibble: 10 x 6
    ##                  Name Profession   Age `Has kids` `Date of birth`
    ##                 <chr>      <chr> <dbl>      <lgl>          <dttm>
    ##  1        David Bowie   musician    69       TRUE      1947-01-08
    ##  2      Carrie Fisher      actor    60       TRUE      1956-10-21
    ##  3        Chuck Berry   musician    90       TRUE      1926-10-18
    ##  4        Bill Paxton      actor    61       TRUE      1955-05-17
    ##  5             Prince   musician    57       TRUE      1958-06-07
    ##  6       Alan Rickman      actor    69      FALSE      1946-02-21
    ##  7 Florence Henderson      actor    82       TRUE      1934-02-14
    ##  8         Harper Lee     author    89      FALSE      1926-04-28
    ##  9      Zsa Zsa Gábor      actor    99       TRUE      1917-02-06
    ## 10     George Michael   musician    53      FALSE      1963-06-25
    ## # ... with 1 more variables: `Date of death` <dttm>

Another is to use the `range` argument:

``` r
deaths <- read_excel("data/deaths.xls", range = "A5:F15")
deaths
```

    ## # A tibble: 10 x 6
    ##                  Name Profession   Age `Has kids` `Date of birth`
    ##                 <chr>      <chr> <dbl>      <lgl>          <dttm>
    ##  1        David Bowie   musician    69       TRUE      1947-01-08
    ##  2      Carrie Fisher      actor    60       TRUE      1956-10-21
    ##  3        Chuck Berry   musician    90       TRUE      1926-10-18
    ##  4        Bill Paxton      actor    61       TRUE      1955-05-17
    ##  5             Prince   musician    57       TRUE      1958-06-07
    ##  6       Alan Rickman      actor    69      FALSE      1946-02-21
    ##  7 Florence Henderson      actor    82       TRUE      1934-02-14
    ##  8         Harper Lee     author    89      FALSE      1926-04-28
    ##  9      Zsa Zsa Gábor      actor    99       TRUE      1917-02-06
    ## 10     George Michael   musician    53      FALSE      1963-06-25
    ## # ... with 1 more variables: `Date of death` <dttm>
