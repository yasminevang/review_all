review_hw1
================

``` r
library(tidyverse)
```

The hw asks us to `install.packages("moderndive")` but in the console!
Do that here.

Let’s now load the code

``` r
library(moderndive)
data("early_january_weather")
```

Okay, this data set `early_january_weather` is telling us about the
hourly meteorological data for LGA, JFK, and EWR in the month of January
2013.

Variables are origin, date, hour, temp (F), dewp(F), humid,
wind_dir(degrees), wind_speed (mph), wind_gust(mph), precip (in),
pressure, visib, time_hour.

The data set has 358 rows and 15 variables or columns.

### Let’s make a scatterplot

``` r
early_df = ggplot(data = early_january_weather,
                  aes( x = time_hour, 
                       y = temp, 
                       color = humid)
                  )+ geom_point()

ggsave("review_all_early_df.pdf")
```

    ## Saving 7 x 5 in image

don’t forget to add `geom_point` at the end to have points on the plot.

to make a `ggsave`, create a title for your image and then add .pdf

### Next Problem

Let’s make a data frame:

``` r
new_df = tibble(
  yuh = rnorm(10),
  vec_log = yuh > 0,
  vec_char = c("a","b","c","d","e","f","g","h","i","j"),
  vec_f = factor(c("small", "small", "small", "medium","medium", "medium","medium", "large","large","large"))
)
```

key things: a vector is a sequence of things. think of a excel sheet
row. character means its a thing, numeric vector is numbers. when you
use `factor` then `c()` right after to list our the things you are
factoring into levels.

now lets try and take the mean of each variable

``` r
mean(pull(new_df, yuh))
```

    ## [1] 0.1120985

``` r
mean(pull(new_df, vec_log))
```

    ## [1] 0.4

``` r
mean(pull(new_df, vec_char))
```

    ## Warning in mean.default(pull(new_df, vec_char)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

the last mean will **not** work because you can’t pull the mean from
characters

so we change them to numeric

``` r
as.numeric(pull(new_df, vec_f))
```

    ##  [1] 3 3 3 2 2 2 2 1 1 1

okay it made some numbers now let see if we can get the mean

``` r
mean(as.numeric(pull(new_df, vec_f)))
```

    ## [1] 2

perfect! mean is 2.
