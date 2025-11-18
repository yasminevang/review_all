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
    ## -2.14217 -0.64039 -0.04632 -0.03496  0.50045  2.48530

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
    ##  [1] 3.707186 1.070238 2.435274 4.483804 4.244995 4.979941 3.486147 1.544921
    ##  [9] 2.825818 2.071354 2.493060 3.045107 1.915343 2.770667 3.038131 2.561088
    ## [17] 4.433996 5.139696 4.568115 3.118058
    ## 
    ## $b
    ##  [1]  -9.00958468  -1.25577238  -1.82653428   2.01574021  -0.02012443
    ##  [6]   0.87360950  -2.49093487   1.91249434  -4.02203495  -1.48398128
    ## [11]   2.30162267   1.75749732   4.79723886   2.51214484   2.58009681
    ## [16]  -2.73591392  -7.98376503   5.67522012  13.44125974   1.26537333
    ## [21]  -1.63351992 -10.83803372   9.89371355   1.63998734   4.03793528
    ## [26]   1.92314296  -1.31540568   3.32891390   0.30142253   4.96751793
    ## 
    ## $c
    ##  [1]  9.996702 10.203495  9.900082 10.334082  9.858804 10.276937  9.773668
    ##  [8] 10.103009 10.123795  9.785948  9.916346 10.006328  9.997792  9.667343
    ## [15] 10.357928  9.734005 10.195979  9.810673 10.183196 10.031386 10.050059
    ## [22]  9.931024  9.838083 10.043476  9.648007  9.949115 10.134403  9.827302
    ## [29]  9.854809  9.961608  9.896577  9.770741  9.709931 10.068905 10.296027
    ## [36]  9.967128  9.988830  9.632809  9.930683  9.706861
    ## 
    ## $d
    ##  [1] -2.4891862 -2.9937293 -3.9339070 -4.0870926 -2.4785085 -2.8626674
    ##  [7] -2.7768183 -4.4710519 -2.7942952 -2.2668286 -0.7740301 -1.7971644
    ## [13] -2.8272259 -1.7428980 -3.0580312 -4.8191652 -3.5331252 -1.8368817
    ## [19] -3.9017574 -2.5332997

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

    ##  [1] 3.707186 1.070238 2.435274 4.483804 4.244995 4.979941 3.486147 1.544921
    ##  [9] 2.825818 2.071354 2.493060 3.045107 1.915343 2.770667 3.038131 2.561088
    ## [17] 4.433996 5.139696 4.568115 3.118058

``` r
list_norm[[2]]
```

    ##  [1]  -9.00958468  -1.25577238  -1.82653428   2.01574021  -0.02012443
    ##  [6]   0.87360950  -2.49093487   1.91249434  -4.02203495  -1.48398128
    ## [11]   2.30162267   1.75749732   4.79723886   2.51214484   2.58009681
    ## [16]  -2.73591392  -7.98376503   5.67522012  13.44125974   1.26537333
    ## [21]  -1.63351992 -10.83803372   9.89371355   1.63998734   4.03793528
    ## [26]   1.92314296  -1.31540568   3.32891390   0.30142253   4.96751793

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.20  1.16

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.687  4.96

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

``` r
output = map_dbl(list_norm, median)
```

``` r
output = map_df(list_norm, mean_and_sd)
```

``` r
output = map_df(list_norm, mean_and_sd, .id = "input")
```
