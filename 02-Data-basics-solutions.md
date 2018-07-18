Data Basics (solutions)
================

<!-- This file by Charlotte Wickham is licensed under a Creative Commons Attribution 4.0 International License. -->
``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.5
    ## ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
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
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p    
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p    
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p    
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p    
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p    
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p    
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p    
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p    
    ## # ... with 224 more rows, and 1 more variable: class <chr>

``` r
quakes
```

    ## # A tibble: 1,000 x 5
    ##      lat  long depth   mag stations
    ##    <dbl> <dbl> <int> <dbl>    <int>
    ##  1 -20.4  182.   562   4.8       41
    ##  2 -20.6  181.   650   4.2       15
    ##  3 -26    184.    42   5.4       43
    ##  4 -18.0  182.   626   4.1       19
    ##  5 -20.4  182.   649   4         11
    ##  6 -19.7  184.   195   4         12
    ##  7 -11.7  166.    82   4.8       43
    ##  8 -28.1  182.   194   4.4       15
    ##  9 -28.7  182.   211   4.7       35
    ## 10 -17.5  180.   622   4.3       19
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
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p    
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p    
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p    
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p    
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p    
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p    
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p    
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p    
    ## # ... with 224 more rows, and 1 more variable: class <chr>

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
    ##    `Lots of people`             X__1        X__2   X__3   X__4    X__5    
    ##    <chr>                        <chr>       <chr>  <chr>  <chr>   <chr>   
    ##  1 simply cannot resist writing <NA>        <NA>   <NA>   <NA>    some no…
    ##  2 at                           the         top    <NA>   of      their s…
    ##  3 or                           merging     <NA>   <NA>   <NA>    cells   
    ##  4 Name                         Profession  Age    Has k… Date o… Date of…
    ##  5 David Bowie                  musician    69     TRUE   17175   42379   
    ##  6 Carrie Fisher                actor       60     TRUE   20749   42731   
    ##  7 Chuck Berry                  musician    90     TRUE   9788    42812   
    ##  8 Bill Paxton                  actor       61     TRUE   20226   42791   
    ##  9 Prince                       musician    57     TRUE   21343   42481   
    ## 10 Alan Rickman                 actor       69     FALSE  16854   42383   
    ## 11 Florence Henderson           actor       82     TRUE   12464   42698   
    ## 12 Harper Lee                   author      89     FALSE  9615    42419   
    ## 13 Zsa Zsa Gábor                actor       99     TRUE   6247    42722   
    ## 14 George Michael               musician    53     FALSE  23187   42729   
    ## 15 Some                         <NA>        <NA>   <NA>   <NA>    <NA>    
    ## 16 <NA>                         also like … <NA>   <NA>   <NA>    <NA>    
    ## 17 <NA>                         <NA>        at the botto… <NA>    <NA>    
    ## 18 <NA>                         <NA>        <NA>   <NA>   <NA>    too!

``` r
iris <- read_spss("data/iris.sav")
iris
```

    ## # A tibble: 150 x 5
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species  
    ##           <dbl>       <dbl>        <dbl>       <dbl> <dbl+lbl>
    ##  1          5.1         3.5          1.4         0.2 1        
    ##  2          4.9         3            1.4         0.2 1        
    ##  3          4.7         3.2          1.3         0.2 1        
    ##  4          4.6         3.1          1.5         0.2 1        
    ##  5          5           3.6          1.4         0.2 1        
    ##  6          5.4         3.9          1.7         0.4 1        
    ##  7          4.6         3.4          1.4         0.3 1        
    ##  8          5           3.4          1.5         0.2 1        
    ##  9          4.4         2.9          1.4         0.2 1        
    ## 10          4.9         3.1          1.5         0.1 1        
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
    ##    date                longitude latitude ozone
    ##    <dttm>                  <dbl>    <dbl> <chr>
    ##  1 1985-10-01 00:00:00     -179.    -73.5 302  
    ##  2 1985-10-01 00:00:00     -178.    -73.5 302  
    ##  3 1985-10-01 00:00:00     -177.    -73.5 302  
    ##  4 1985-10-01 00:00:00     -176.    -73.5 302  
    ##  5 1985-10-01 00:00:00     -174.    -73.5 304  
    ##  6 1985-10-01 00:00:00     -173.    -73.5 304  
    ##  7 1985-10-01 00:00:00     -172.    -73.5 304  
    ##  8 1985-10-01 00:00:00     -171.    -73.5 304  
    ##  9 1985-10-01 00:00:00     -164.    -73.5 287  
    ## 10 1985-10-01 00:00:00     -163.    -73.5 287  
    ## # ... with 18,953 more rows

Your Turn 7
-----------

Can you see what is wrong with the Excel file when it is imported?

Scan the Arguments section of ?read\_excel, can you find an argument that might help? Try it!

``` r
deaths
```

    ## # A tibble: 18 x 6
    ##    `Lots of people`             X__1        X__2   X__3   X__4    X__5    
    ##    <chr>                        <chr>       <chr>  <chr>  <chr>   <chr>   
    ##  1 simply cannot resist writing <NA>        <NA>   <NA>   <NA>    some no…
    ##  2 at                           the         top    <NA>   of      their s…
    ##  3 or                           merging     <NA>   <NA>   <NA>    cells   
    ##  4 Name                         Profession  Age    Has k… Date o… Date of…
    ##  5 David Bowie                  musician    69     TRUE   17175   42379   
    ##  6 Carrie Fisher                actor       60     TRUE   20749   42731   
    ##  7 Chuck Berry                  musician    90     TRUE   9788    42812   
    ##  8 Bill Paxton                  actor       61     TRUE   20226   42791   
    ##  9 Prince                       musician    57     TRUE   21343   42481   
    ## 10 Alan Rickman                 actor       69     FALSE  16854   42383   
    ## 11 Florence Henderson           actor       82     TRUE   12464   42698   
    ## 12 Harper Lee                   author      89     FALSE  9615    42419   
    ## 13 Zsa Zsa Gábor                actor       99     TRUE   6247    42722   
    ## 14 George Michael               musician    53     FALSE  23187   42729   
    ## 15 Some                         <NA>        <NA>   <NA>   <NA>    <NA>    
    ## 16 <NA>                         also like … <NA>   <NA>   <NA>    <NA>    
    ## 17 <NA>                         <NA>        at the botto… <NA>    <NA>    
    ## 18 <NA>                         <NA>        <NA>   <NA>   <NA>    too!

Looks like the first few rows don't contain data, but some multi-column notations. There's also some at the end.

One solution is to use the arguments `skip` and `n_max`:

``` r
deaths <- read_excel("data/deaths.xls", skip = 4, n_max = 10)
deaths
```

    ## # A tibble: 10 x 6
    ##    Name               Profession   Age `Has kids` `Date of birth`    
    ##    <chr>              <chr>      <dbl> <lgl>      <dttm>             
    ##  1 David Bowie        musician      69 TRUE       1947-01-08 00:00:00
    ##  2 Carrie Fisher      actor         60 TRUE       1956-10-21 00:00:00
    ##  3 Chuck Berry        musician      90 TRUE       1926-10-18 00:00:00
    ##  4 Bill Paxton        actor         61 TRUE       1955-05-17 00:00:00
    ##  5 Prince             musician      57 TRUE       1958-06-07 00:00:00
    ##  6 Alan Rickman       actor         69 FALSE      1946-02-21 00:00:00
    ##  7 Florence Henderson actor         82 TRUE       1934-02-14 00:00:00
    ##  8 Harper Lee         author        89 FALSE      1926-04-28 00:00:00
    ##  9 Zsa Zsa Gábor      actor         99 TRUE       1917-02-06 00:00:00
    ## 10 George Michael     musician      53 FALSE      1963-06-25 00:00:00
    ## # ... with 1 more variable: `Date of death` <dttm>

Another is to use the `range` argument:

``` r
deaths <- read_excel("data/deaths.xls", range = "A5:F15")
deaths
```

    ## # A tibble: 10 x 6
    ##    Name               Profession   Age `Has kids` `Date of birth`    
    ##    <chr>              <chr>      <dbl> <lgl>      <dttm>             
    ##  1 David Bowie        musician      69 TRUE       1947-01-08 00:00:00
    ##  2 Carrie Fisher      actor         60 TRUE       1956-10-21 00:00:00
    ##  3 Chuck Berry        musician      90 TRUE       1926-10-18 00:00:00
    ##  4 Bill Paxton        actor         61 TRUE       1955-05-17 00:00:00
    ##  5 Prince             musician      57 TRUE       1958-06-07 00:00:00
    ##  6 Alan Rickman       actor         69 FALSE      1946-02-21 00:00:00
    ##  7 Florence Henderson actor         82 TRUE       1934-02-14 00:00:00
    ##  8 Harper Lee         author        89 FALSE      1926-04-28 00:00:00
    ##  9 Zsa Zsa Gábor      actor         99 TRUE       1917-02-06 00:00:00
    ## 10 George Michael     musician      53 FALSE      1963-06-25 00:00:00
    ## # ... with 1 more variable: `Date of death` <dttm>
