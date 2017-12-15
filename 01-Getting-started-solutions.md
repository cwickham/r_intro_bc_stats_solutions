Getting Started with R and RStudio (solutions)
================

<!-- This file by Charlotte Wickham is licensed under a Creative Commons Attribution 4.0 International License. -->
``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.3.4     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.7.2     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.2.0

    ## ── Conflicts ───────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

R Notebooks
-----------

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code.

R code goes in **code chunks**, denoted by three backticks. Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd/Crtl+Shift+Enter*.

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy))
```

![](01-Getting-started-solutions_files/figure-markdown_github/unnamed-chunk-1-1.png)

Add a new code chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Cmd/Ctrl+Option+I*.

Here's a not very interesting chunk of R code:

``` r
2 + 2
```

    ## [1] 4

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Cmd+Shift+K* to preview the HTML file).

The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike *Knit*, *Preview* does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed.

Assigning variables
-------------------

What's the difference between the code in this chunk:

``` r
filter(mtcars, cyl == 4)
```

    ## # A tibble: 11 x 11
    ##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    ##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  22.8     4 108.0    93  3.85 2.320 18.61     1     1     4     1
    ##  2  24.4     4 146.7    62  3.69 3.190 20.00     1     0     4     2
    ##  3  22.8     4 140.8    95  3.92 3.150 22.90     1     0     4     2
    ##  4  32.4     4  78.7    66  4.08 2.200 19.47     1     1     4     1
    ##  5  30.4     4  75.7    52  4.93 1.615 18.52     1     1     4     2
    ##  6  33.9     4  71.1    65  4.22 1.835 19.90     1     1     4     1
    ##  7  21.5     4 120.1    97  3.70 2.465 20.01     1     0     3     1
    ##  8  27.3     4  79.0    66  4.08 1.935 18.90     1     1     4     1
    ##  9  26.0     4 120.3    91  4.43 2.140 16.70     0     1     5     2
    ## 10  30.4     4  95.1   113  3.77 1.513 16.90     1     1     5     2
    ## 11  21.4     4 121.0   109  4.11 2.780 18.60     1     1     4     2

And the code in this chunk?

``` r
four_cyls <- filter(mtcars, cyl == 4)
```

The difference in the code is `four_cyls <-`. In the second chunk, rather than returning the output of `filter(mtcars, cyl == 4)`, the output is stored (or "assigned") to a variable called `four_cyls`. `<-` is the assignment operator, it assigns the output of the right hand side into a variable with the name of the left hand side.

Function syntax
---------------

Take a look at this code:

``` r
heights <- pull(.data = starwars, var = height)
mean(heights, na.rm = TRUE)
```

    ## [1] 174.358

1.  What functions are being called?
2.  What arguments do they take?
3.  What values are being passed as which arguments?

In the first line, the function `pull()` is being called where the `.data` argument takes the value `starwars` and the `var` argument takes the value `height`.

In the second line, the function `mean()` is being called where the first argument takes the value `heights`. You would have to look at the help for `mean()`, (i.e. `?mean`) to find out that this first argument is called `x`. The other argument being provided is `na.rm`, set to the value `TRUE`.

Can you guess what the code does? `starwars` is a dataset that comes with the `dplyr` package, try `?starwars` to learn more about it. The code chunk above pulls out the heights of the starwars characters in that data, then finds the mean of those heights ignoring any missing values.

Syntax gone wrong
-----------------

1.  There was missing closing parenthesis `)`.

    ``` r
    sd(pull(.data = starwars, var = mass))
    ```

        ## [1] NA

    Notice how here we have one function, `pull()` nested inside another one, `sd()`. The result of `pull(.data = starwars, var = weight)` is passed into `sd()` as the first argument.

2.  The string was closed with a single quote `'` rather than a double quote `"`

    ``` r
    my_name <- "Charlotte"
    ```

3.  The `.data` argument to `pull()` wasn't expecting a character string, remove the quotes around `starwars` to fix the problem.

    ``` r
    pull(.data = starwars, var = height)
    ```

        ##  [1] 172 167  96 202 150 178 165  97 183 182 188 180 228 180 173 175 170
        ## [18] 180  66 170 183 200 190 177 175 180 150  NA  88 160 193 191 170 196
        ## [35] 224 206 183 137 112 183 163 175 180 178  94 122 163 188 198 196 171
        ## [52] 184 188 264 188 196 185 157 183 183 170 166 165 193 191 183 168 198
        ## [69] 229 213 167  79  96 193 191 178 216 234 188 178 206  NA  NA  NA  NA
        ## [86]  NA 165
