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
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.3997 -0.8093 -0.1165 -0.0340  0.7889  2.1251

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
    ##  [1] 3.539135 2.399594 1.952613 1.704990 3.774577 1.317447 3.139026 4.037261
    ##  [9] 3.347182 3.026480 2.816549 3.594119 2.174114 3.524700 3.286705 3.427865
    ## [17] 4.293264 3.355192 4.210195 2.611175
    ## 
    ## $b
    ##  [1]  1.87563795 -0.26905230 -4.11228856  8.05474300 -9.09651343 -1.09646531
    ##  [7]  0.14184150 -2.02894693  1.96760312 -0.80271094 -5.39302409 -0.10345454
    ## [13] -7.08671561 -0.17444019 -1.28490716  7.35316452  1.50579998 -6.85399279
    ## [19] -4.97932715 -4.00189747  6.02103133  0.30960643 -4.65585346  2.04625268
    ## [25]  8.88028021 -0.05981976 -4.75797085  9.33267974  2.44697062 -6.96258326
    ## 
    ## $c
    ##  [1] 10.165758 10.480249  9.956461 10.299007  9.738213  9.869922  9.640096
    ##  [8] 10.090779  9.866294 10.033709  9.761003 10.113608 10.252447 10.263230
    ## [15] 10.113009 10.242393  9.745189 10.022326  9.768889  9.867019  9.971497
    ## [22] 10.605674  9.632480  9.887935 10.116588  9.747886  9.978924 10.023068
    ## [29] 10.305941 10.144514  9.949623 10.004485 10.029485 10.124245  9.888781
    ## [36] 10.184842 10.120656  9.955978  9.720542  9.992837
    ## 
    ## $d
    ##  [1] -4.5595130 -2.7936143 -2.1515990 -3.9019370 -2.1892163 -5.0716163
    ##  [7] -2.6216066 -3.9441697 -5.2173123 -1.8716261 -5.0733713 -3.0654905
    ## [13] -4.1305382 -2.6933328 -1.9028380 -1.1452094 -0.8227042 -4.2121151
    ## [19] -1.5158917 -2.2016702

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

    ##  [1] 3.539135 2.399594 1.952613 1.704990 3.774577 1.317447 3.139026 4.037261
    ##  [9] 3.347182 3.026480 2.816549 3.594119 2.174114 3.524700 3.286705 3.427865
    ## [17] 4.293264 3.355192 4.210195 2.611175

``` r
list_norm[[2]]
```

    ##  [1]  1.87563795 -0.26905230 -4.11228856  8.05474300 -9.09651343 -1.09646531
    ##  [7]  0.14184150 -2.02894693  1.96760312 -0.80271094 -5.39302409 -0.10345454
    ## [13] -7.08671561 -0.17444019 -1.28490716  7.35316452  1.50579998 -6.85399279
    ## [19] -4.97932715 -4.00189747  6.02103133  0.30960643 -4.65585346  2.04625268
    ## [25]  8.88028021 -0.05981976 -4.75797085  9.33267974  2.44697062 -6.96258326

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.08 0.827

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.459  4.92

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

## List columns!

``` r
listcol_df = 
  tibble(
    name = c("a", "b", "c", "d"),
    samp = list_norm
  )
```

``` r
listcol_df |> pull(name)
```

    ## [1] "a" "b" "c" "d"

``` r
listcol_df |> pull(samp)
```

    ## $a
    ##  [1] 3.539135 2.399594 1.952613 1.704990 3.774577 1.317447 3.139026 4.037261
    ##  [9] 3.347182 3.026480 2.816549 3.594119 2.174114 3.524700 3.286705 3.427865
    ## [17] 4.293264 3.355192 4.210195 2.611175
    ## 
    ## $b
    ##  [1]  1.87563795 -0.26905230 -4.11228856  8.05474300 -9.09651343 -1.09646531
    ##  [7]  0.14184150 -2.02894693  1.96760312 -0.80271094 -5.39302409 -0.10345454
    ## [13] -7.08671561 -0.17444019 -1.28490716  7.35316452  1.50579998 -6.85399279
    ## [19] -4.97932715 -4.00189747  6.02103133  0.30960643 -4.65585346  2.04625268
    ## [25]  8.88028021 -0.05981976 -4.75797085  9.33267974  2.44697062 -6.96258326
    ## 
    ## $c
    ##  [1] 10.165758 10.480249  9.956461 10.299007  9.738213  9.869922  9.640096
    ##  [8] 10.090779  9.866294 10.033709  9.761003 10.113608 10.252447 10.263230
    ## [15] 10.113009 10.242393  9.745189 10.022326  9.768889  9.867019  9.971497
    ## [22] 10.605674  9.632480  9.887935 10.116588  9.747886  9.978924 10.023068
    ## [29] 10.305941 10.144514  9.949623 10.004485 10.029485 10.124245  9.888781
    ## [36] 10.184842 10.120656  9.955978  9.720542  9.992837
    ## 
    ## $d
    ##  [1] -4.5595130 -2.7936143 -2.1515990 -3.9019370 -2.1892163 -5.0716163
    ##  [7] -2.6216066 -3.9441697 -5.2173123 -1.8716261 -5.0733713 -3.0654905
    ## [13] -4.1305382 -2.6933328 -1.9028380 -1.1452094 -0.8227042 -4.2121151
    ## [19] -1.5158917 -2.2016702

``` r
listcol_df |> 
  filter(name == "a")
```

    ## # A tibble: 1 × 2
    ##   name  samp        
    ##   <chr> <named list>
    ## 1 a     <dbl [20]>

Let’s try some operations

``` r
mean_and_sd(listcol_df$samp[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.08 0.827

``` r
mean_and_sd(listcol_df$samp[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.459  4.92

can I just map?

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.08 0.827
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.459  4.92
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.218
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.05  1.37

So.. can I add a list column??

``` r
listcol_df =
listcol_df |> 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map_dbl(samp, median))
```
