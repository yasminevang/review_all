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
    ## -2.65095 -0.62980 -0.05146 -0.01946  0.45305  2.41639

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
    ##  [1] 4.843671 3.001420 1.452704 1.628980 4.480618 2.691779 3.462325 4.566922
    ##  [9] 4.728220 2.790387 2.219319 2.352523 2.541591 3.355033 2.457467 3.125642
    ## [17] 2.991916 3.064525 3.485421 3.486145
    ## 
    ## $b
    ##  [1]  -7.2901355   0.8054013  -7.7555008  -1.1244862  -1.4806724   0.5415333
    ##  [7]  -6.1909798  -0.3513015  -2.5176289   8.1468023  10.3082020   4.6924252
    ## [13]  -0.7241884  -3.7821641  -0.9820027   6.4080868  -1.3814359   3.7219634
    ## [19] -10.0582828  -3.5100578   3.3517914   4.2099872   3.1617413   3.8487538
    ## [25]   5.7364850   3.0379118   1.2560183   3.7461011  -3.4957537   6.9980777
    ## 
    ## $c
    ##  [1]  9.998289 10.335490  9.852533 10.070205  9.867163  9.928319  9.489094
    ##  [8] 10.356018 10.074393  9.967236 10.006722 10.182509  9.798157 10.035950
    ## [15]  9.883053  9.757851  9.671657  9.939430 10.126256  9.900249  9.840615
    ## [22] 10.094778  9.749010 10.112447  9.900654  9.902115  9.961166 10.126505
    ## [29]  9.928631  9.827405  9.792263  9.522153 10.186177  9.781432 10.163079
    ## [36]  9.998483 10.221333  9.995363 10.225126  9.872544
    ## 
    ## $d
    ##  [1]  0.1703601 -3.3532322 -3.8312049 -2.5931632 -1.4895446 -2.8757671
    ##  [7] -3.0178111 -4.0407182 -2.4201500 -2.1159250 -3.7668472 -2.3084795
    ## [13] -4.2332764 -3.4056373 -4.6364402 -4.3901196 -2.4395218 -3.5841040
    ## [19] -2.0822901 -2.9097945

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

    ##  [1] 4.843671 3.001420 1.452704 1.628980 4.480618 2.691779 3.462325 4.566922
    ##  [9] 4.728220 2.790387 2.219319 2.352523 2.541591 3.355033 2.457467 3.125642
    ## [17] 2.991916 3.064525 3.485421 3.486145

``` r
list_norm[[2]]
```

    ##  [1]  -7.2901355   0.8054013  -7.7555008  -1.1244862  -1.4806724   0.5415333
    ##  [7]  -6.1909798  -0.3513015  -2.5176289   8.1468023  10.3082020   4.6924252
    ## [13]  -0.7241884  -3.7821641  -0.9820027   6.4080868  -1.3814359   3.7219634
    ## [19] -10.0582828  -3.5100578   3.3517914   4.2099872   3.1617413   3.8487538
    ## [25]   5.7364850   3.0379118   1.2560183   3.7461011  -3.4957537   6.9980777

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.14 0.958

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.644  4.93

Let’s use a for a loop:

``` r
output = vector("list", length = 4)

for (i in 1:4) {
output[[i]] = mean_and_sd(list_norm[[i]])
}
```
