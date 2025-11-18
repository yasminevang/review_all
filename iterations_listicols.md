iterations_listicols
================

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
knitr::opts_chunk$set(
  fig.width = 6,
  fig.asp = .6 ,
  out.width = "90%"
)

theme_set(theme_minimal() + theme(legend.position = "bottom"))

options(
  ggplot2.continuous.colour = "viridis",
  ggplot2.continuous.fill = "virids"
)

scale_colour_discrete = scale_color_viridis_d
scale_fill_discrete = scale_fill_viridis_d
```

## Lists

You can put anything in a list.

``` r
l = list(
vec_numeric = 5: 8,
vec_logical = c(TRUE, TRUE, FALSE, TRUE, FALSE, FALSE),
mat = matrix(1:8, nrow = 2, ncol = 4),
summary = summary(rnorm(100))
)
```

access things in the list

``` r
l
```

    ## $vec_numeric
    ## [1] 5 6 7 8
    ## 
    ## $vec_logical
    ## [1]  TRUE  TRUE FALSE  TRUE FALSE FALSE
    ## 
    ## $mat
    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8
    ## 
    ## $summary
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -3.16162 -0.83979 -0.11604 -0.08553  0.69972  3.11947

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[1]]
```

    ## [1] 5 6 7 8

``` r
mean(l[["vec_numeric"]])
```

    ## [1] 6.5

## `for` loop

Create a new list.

``` r
list_norm =
  list(
    a = rnorm(20, mean = 3, sd = 1),
    b = rnorm(30, mean = 0, sd = 5),
    c = rnorm(40, mean = 10, sd = .2),
    d = rnorm(20, mean = -3, sd = 1)
  )
```

``` r
list_norm
```

    ## $a
    ##  [1] 4.045183 4.665096 2.875664 2.610208 2.546819 3.455167 2.055460 3.721612
    ##  [9] 3.689822 3.908361 1.806838 2.005218 2.032165 1.875138 2.406152 3.498519
    ## [17] 2.170233 3.270927 2.819088 3.568276
    ## 
    ## $b
    ##  [1]  -6.3309150   1.0408875  -4.2144952   0.2707757  -7.0455614  -0.8877290
    ##  [7]  -0.8433588  10.1709484   1.1976420  -8.0467582   2.8749209   4.6465076
    ## [13]   0.1047585  -1.5361200   1.0026272  11.7924481  -6.3976860   0.4821130
    ## [19]  -2.9892842   5.6339902  -1.8566673  -2.9813128  -0.4179896  -7.7019316
    ## [25]  -0.2993569  -1.4976732 -15.3728225  -0.3330486   1.0809934   2.8929991
    ## 
    ## $c
    ##  [1]  9.958811  9.983942  9.977206  9.652561 10.104226  9.846812 10.051194
    ##  [8] 10.262041  9.948157 10.207266  9.774077 10.031152  9.822146  9.980696
    ## [15]  9.743252 10.237988  9.883099  9.391028  9.543169 10.046528  9.831932
    ## [22]  9.790821  9.792804 10.178880 10.058562 10.188110  9.664106  9.953365
    ## [29] 10.234076  9.770873 10.105941  9.870877 10.032363 10.038227  9.939161
    ## [36] 10.260133  9.845973  9.768680  9.732798  9.493165
    ## 
    ## $d
    ##  [1] -3.112764 -2.392129 -2.845499 -1.435774 -3.920652 -3.574106 -3.877424
    ##  [8] -3.459815 -3.036511 -3.248728 -4.663779 -2.754113 -3.776456 -3.521651
    ## [15] -3.068885 -3.190941 -1.746083 -2.125726 -1.460087 -3.280278

Pause and get my old function.

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
  } else if (length(x) == 1) {
    stop("Cannot be computed for length 1 vectors")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)

  tibble(
    mean = mean_x, 
    sd = sd_x
  )
}
```

I can apply that function to each element

``` r
list_norm[[1]]
```

    ##  [1] 4.045183 4.665096 2.875664 2.610208 2.546819 3.455167 2.055460 3.721612
    ##  [9] 3.689822 3.908361 1.806838 2.005218 2.032165 1.875138 2.406152 3.498519
    ## [17] 2.170233 3.270927 2.819088 3.568276

``` r
list_norm[[2]]
```

    ##  [1]  -6.3309150   1.0408875  -4.2144952   0.2707757  -7.0455614  -0.8877290
    ##  [7]  -0.8433588  10.1709484   1.1976420  -8.0467582   2.8749209   4.6465076
    ## [13]   0.1047585  -1.5361200   1.0026272  11.7924481  -6.3976860   0.4821130
    ## [19]  -2.9892842   5.6339902  -1.8566673  -2.9813128  -0.4179896  -7.7019316
    ## [25]  -0.2993569  -1.4976732 -15.3728225  -0.3330486   1.0809934   2.8929991

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.95 0.841

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.852  5.36

Let’s use a for a loop:

``` r
output = vector("list", length = 4)

for (i in 1:4) {
output[[i]] = mean_and_sd(list_norm[[i]])
}
```

## Let’s try map!

``` r
output = map(list_norm, mean_and_sd)
```

what if you want a different function?

``` r
output = map(list_norm, median)
```
