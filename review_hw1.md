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
