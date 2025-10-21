review_tidy_data
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

## `pivot_longer`

``` r
pulse_data =
  haven::read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names()
```

wide format to long format

``` r
pulse_data_tidy =
  pulse_data |> 
  pivot_longer(
    bdi_score_bl:bdi_score_12m, 
    names_to = "visit",
    names_prefix = "bdi_score_",
    values_to = "bdi"
  )
```

rewrite, combine, and extende (to add a mutate)

``` r
pulse_data =
  haven::read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names() |>
  pivot_longer(
    bdi_score_bl:bdi_score_12m, 
    names_to = "visit",
    names_prefix = "bdi_score_",
    values_to = "bdi"
  ) |> 
  relocate(id, visit) |> 
  mutate(visit = recode(visit, "bl" = "00m"))
```

## `pivot_wider`

Make up some data!

``` r
analysis_result =
  tibble(
    group = c("treatment","treatment","placebo","placebo"),
    time = c("pre","post","pre","post"),
    mean = c(4, 8,3.5, 4)
  )

analysis_result |> 
  pivot_wider(
    names_from = "time",
    values_from = "mean" 
  )
```

    ## # A tibble: 2 × 3
    ##   group       pre  post
    ##   <chr>     <dbl> <dbl>
    ## 1 treatment   4       8
    ## 2 placebo     3.5     4

## Binding rows using lord of the rings data. LotR

first step import each table.

``` r
fellowship_ring =
  readxl::read_excel("data/LotR_Words.xlsx", range = "B3:D6") |> 
  mutate(movie = "fellowship_ring")

two_towers =
  readxl::read_excel("data/LotR_Words.xlsx", range = "F3:H6") |> 
  mutate(movie = "two_towers")

return_king =
  readxl::read_excel("data/LotR_Words.xlsx", range = "J3:L6") |> 
  mutate(movie = "return_king")
```

Bind all the rows together

``` r
lotr_tidy =
  bind_rows(fellowship_ring, two_towers, return_king) |> 
  janitor::clean_names() |> 
  relocate(movie) |>
  pivot_longer(
    female:male,
    names_to = "gender",
    values_to = "words"
  )
```
