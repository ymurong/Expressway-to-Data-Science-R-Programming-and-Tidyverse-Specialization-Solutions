Problem Set 5
================

### Introduction

Reference the [tidyverse style guide](https://style.tidyverse.org/)
while completing the exercises.

These exercises are ungraded.

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

#### Question 1.

Using the nycflights13 data, calculate a new variable called “hr_delay”
and arrange the flights dataset in order of the arrival delays in hours
(longest delays at the top). Put the new variable you created just
before the departure time. Hint: use the experimental argument .before.

``` r
flights %>%
  mutate(hr_delay = arr_delay / 60 + dep_delay / 60 ) %>%
  relocate(hr_delay, .before = dep_time)
```

    ## # A tibble: 336,776 × 20
    ##     year month   day hr_delay dep_time sched_d…¹ dep_d…² arr_t…³ sched…⁴ arr_d…⁵
    ##    <int> <int> <int>    <dbl>    <int>     <int>   <dbl>   <int>   <int>   <dbl>
    ##  1  2013     1     1    0.217      517       515       2     830     819      11
    ##  2  2013     1     1    0.4        533       529       4     850     830      20
    ##  3  2013     1     1    0.583      542       540       2     923     850      33
    ##  4  2013     1     1   -0.317      544       545      -1    1004    1022     -18
    ##  5  2013     1     1   -0.517      554       600      -6     812     837     -25
    ##  6  2013     1     1    0.133      554       558      -4     740     728      12
    ##  7  2013     1     1    0.233      555       600      -5     913     854      19
    ##  8  2013     1     1   -0.283      557       600      -3     709     723     -14
    ##  9  2013     1     1   -0.183      557       600      -3     838     846      -8
    ## 10  2013     1     1    0.1        558       600      -2     753     745       8
    ## # … with 336,766 more rows, 10 more variables: carrier <chr>, flight <int>,
    ## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    ## #   hour <dbl>, minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time, ⁵​arr_delay
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 2.

What proportion of flights in nycflights13 are delayed by more than on
hour?

``` r
flights %>%
  filter((arr_delay+dep_delay)/60>1) %>%
  nrow() / nrow(flights)
```

    ## [1] 0.142819
