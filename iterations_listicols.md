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
    ## -2.42293 -0.69383 -0.11706 -0.04659  0.61019  3.38362

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
    ##  [1] 3.0703545 3.4988402 3.7081048 3.7692544 2.8426882 1.8033226 0.4880577
    ##  [8] 3.6323204 3.4654447 4.0951470 3.0540456 6.0113697 1.8951356 2.1449849
    ## [15] 3.1160571 2.6582061 3.5768459 3.4726425 2.1701650 2.1811912
    ## 
    ## $b
    ##  [1]   0.9759309   2.9326921  -0.5036909  -3.3939282   1.2990133  -5.5502280
    ##  [7]   4.5279368   1.0070714 -11.5911565   3.9366334   4.1917857   0.9057318
    ## [13]  -3.4834748  -3.3530902   1.6945736   1.4931162   3.1517667  -9.9689707
    ## [19]   6.1638755  -2.7451631   6.3215631  -4.4015357   3.8767811  -0.4775318
    ## [25]   8.1757265  12.8717776   2.1058140  -5.3327825  -6.6696752  -1.1411772
    ## 
    ## $c
    ##  [1]  9.956423  9.498524  9.948919  9.946679 10.087922  9.663355  9.959296
    ##  [8] 10.170085  9.888420  9.948650  9.865481  9.850626 10.121924  9.866349
    ## [15] 10.015007 10.164769  9.862948 10.059358 10.202996 10.224631  9.570318
    ## [22]  9.787762 10.166052 10.168784  9.881969  9.901994 10.006451  9.834278
    ## [29] 10.032284  9.875313  9.783092 10.200188  9.752712 10.116502  9.991100
    ## [36] 10.023677 10.302614 10.030501 10.215881 10.278270
    ## 
    ## $d
    ##  [1] -3.206914 -3.184543 -3.245055 -2.219922 -2.553113 -2.636324 -2.189349
    ##  [8] -2.525012 -2.632231 -2.923168 -2.709849 -4.068408 -3.545359 -3.138771
    ## [15] -2.587554 -2.319334 -2.010212 -2.285028 -2.462766 -3.807291

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

    ##  [1] 3.0703545 3.4988402 3.7081048 3.7692544 2.8426882 1.8033226 0.4880577
    ##  [8] 3.6323204 3.4654447 4.0951470 3.0540456 6.0113697 1.8951356 2.1449849
    ## [15] 3.1160571 2.6582061 3.5768459 3.4726425 2.1701650 2.1811912

``` r
list_norm[[2]]
```

    ##  [1]   0.9759309   2.9326921  -0.5036909  -3.3939282   1.2990133  -5.5502280
    ##  [7]   4.5279368   1.0070714 -11.5911565   3.9366334   4.1917857   0.9057318
    ## [13]  -3.4834748  -3.3530902   1.6945736   1.4931162   3.1517667  -9.9689707
    ## [19]   6.1638755  -2.7451631   6.3215631  -4.4015357   3.8767811  -0.4775318
    ## [25]   8.1757265  12.8717776   2.1058140  -5.3327825  -6.6696752  -1.1411772

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.03  1.12

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.234  5.29

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
    ##  [1] 3.0703545 3.4988402 3.7081048 3.7692544 2.8426882 1.8033226 0.4880577
    ##  [8] 3.6323204 3.4654447 4.0951470 3.0540456 6.0113697 1.8951356 2.1449849
    ## [15] 3.1160571 2.6582061 3.5768459 3.4726425 2.1701650 2.1811912
    ## 
    ## $b
    ##  [1]   0.9759309   2.9326921  -0.5036909  -3.3939282   1.2990133  -5.5502280
    ##  [7]   4.5279368   1.0070714 -11.5911565   3.9366334   4.1917857   0.9057318
    ## [13]  -3.4834748  -3.3530902   1.6945736   1.4931162   3.1517667  -9.9689707
    ## [19]   6.1638755  -2.7451631   6.3215631  -4.4015357   3.8767811  -0.4775318
    ## [25]   8.1757265  12.8717776   2.1058140  -5.3327825  -6.6696752  -1.1411772
    ## 
    ## $c
    ##  [1]  9.956423  9.498524  9.948919  9.946679 10.087922  9.663355  9.959296
    ##  [8] 10.170085  9.888420  9.948650  9.865481  9.850626 10.121924  9.866349
    ## [15] 10.015007 10.164769  9.862948 10.059358 10.202996 10.224631  9.570318
    ## [22]  9.787762 10.166052 10.168784  9.881969  9.901994 10.006451  9.834278
    ## [29] 10.032284  9.875313  9.783092 10.200188  9.752712 10.116502  9.991100
    ## [36] 10.023677 10.302614 10.030501 10.215881 10.278270
    ## 
    ## $d
    ##  [1] -3.206914 -3.184543 -3.245055 -2.219922 -2.553113 -2.636324 -2.189349
    ##  [8] -2.525012 -2.632231 -2.923168 -2.709849 -4.068408 -3.545359 -3.138771
    ## [15] -2.587554 -2.319334 -2.010212 -2.285028 -2.462766 -3.807291

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
    ## 1  3.03  1.12

``` r
mean_and_sd(listcol_df$samp[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.234  5.29

can I just map?

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.03  1.12
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.234  5.29
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.98 0.187
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.81 0.562

So.. can I add a list column??

``` r
listcol_df =
listcol_df |> 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map_dbl(samp, median))
```

## Weather Data

Operations on nested data: check it out on the p8105.com

``` r
library(p8105.datasets)
data("weather_df")
```

``` r
weather_nest = 
  nest(weather_df, data = date:tmin)

weather_nest
```

    ## # A tibble: 3 × 3
    ##   name           id          data              
    ##   <chr>          <chr>       <list>            
    ## 1 CentralPark_NY USW00094728 <tibble [730 × 4]>
    ## 2 Molokai_HI     USW00022534 <tibble [730 × 4]>
    ## 3 Waterhole_WA   USS0023B17S <tibble [730 × 4]>

``` r
weather_nest |> pull(name)
```

    ## [1] "CentralPark_NY" "Molokai_HI"     "Waterhole_WA"

``` r
weather_nest |> pull(data)
```

    ## [[1]]
    ## # A tibble: 730 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2021-01-01   157   4.4   0.6
    ##  2 2021-01-02    13  10.6   2.2
    ##  3 2021-01-03    56   3.3   1.1
    ##  4 2021-01-04     5   6.1   1.7
    ##  5 2021-01-05     0   5.6   2.2
    ##  6 2021-01-06     0   5     1.1
    ##  7 2021-01-07     0   5    -1  
    ##  8 2021-01-08     0   2.8  -2.7
    ##  9 2021-01-09     0   2.8  -4.3
    ## 10 2021-01-10     0   5    -1.6
    ## # ℹ 720 more rows
    ## 
    ## [[2]]
    ## # A tibble: 730 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2021-01-01     0  27.8  22.2
    ##  2 2021-01-02     0  28.3  23.9
    ##  3 2021-01-03     0  28.3  23.3
    ##  4 2021-01-04     0  30    18.9
    ##  5 2021-01-05     0  28.9  21.7
    ##  6 2021-01-06     0  27.8  20  
    ##  7 2021-01-07     0  29.4  21.7
    ##  8 2021-01-08     0  28.3  18.3
    ##  9 2021-01-09     0  27.8  18.9
    ## 10 2021-01-10     0  28.3  18.9
    ## # ℹ 720 more rows
    ## 
    ## [[3]]
    ## # A tibble: 730 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2021-01-01   254   3.2   0  
    ##  2 2021-01-02   152   0.9  -3.2
    ##  3 2021-01-03     0   0.2  -4.2
    ##  4 2021-01-04   559   0.9  -3.2
    ##  5 2021-01-05    25   0.5  -3.3
    ##  6 2021-01-06    51   0.8  -4.8
    ##  7 2021-01-07     0   0.2  -5.8
    ##  8 2021-01-08    25   0.5  -8.3
    ##  9 2021-01-09     0   0.1  -7.7
    ## 10 2021-01-10   203   0.9  -0.1
    ## # ℹ 720 more rows

SUppose I want to regress `tmax` on `tmin` for each station.

``` r
weather_lm = function(df) {
  lm(tmax ~ tmin, data = df)
}
```
