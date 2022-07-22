Problem Set 4
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

Use the following definitions of cancellation codes to add a “Code”
column to hflights, then use
tail(hflights![Code\[!is.na(hflights](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;Code%5B%21is.na%28hflights "Code[!is.na(hflights")Code)\],
n = 20) to see that your replacement worked by looking at the last 20
entries that are not NA.

“A” = “carrier” “B” = “weather” “C” = “FF” “D” = “security” “E” = “not
cancelled”

``` r
lut <- c("A" = "carrier", "B"  =    "weather", "C"   =   "FF", "D"   =   "security", "E"   =   "not cancelled")
hflights$Code <- lut[hflights$CancellationCode]
tail(hflights$Code[!is.na(hflights$Code)], n = 20)
```

    ##  [1] "weather" "carrier" "weather" "FF"      "carrier" "carrier" "carrier"
    ##  [8] "carrier" "carrier" "carrier" "carrier" "carrier" "carrier" "carrier"
    ## [15] "carrier" "carrier" "carrier" "carrier" "carrier" "carrier"

#### Question 2.

What does the any_of() function do? Why might it be helpful in
conjunction with this vector when analyzing nycflights13 data?

`vars <- c("year", "month", "day", "dep_delay", "arr_delay")`

any_of() is especially useful to remove variables from a data frame
because calling it again does not cause an error:

#### Question 3.

Does the result of running the following code surprise you? How does the
select helpers deal with case by default? How can you change that
default?

`select(flights, contains("TIME", ignore.case=FALSE))`

CASE INSENSIBLE, USE ignore.case=FALSE

#### Question 4.

Use select to show only the columns of hflights that have the word time
or delay in the variable name or have the carrier id.

``` r
select(flights, contains("TIME") | contains("DELAY") | contains ('CARRIER'))
```

    ## # A tibble: 336,776 × 9
    ##    dep_time sched_…¹ arr_t…² sched…³ air_t…⁴ time_hour           dep_d…⁵ arr_d…⁶
    ##       <int>    <int>   <int>   <int>   <dbl> <dttm>                <dbl>   <dbl>
    ##  1      517      515     830     819     227 2013-01-01 05:00:00       2      11
    ##  2      533      529     850     830     227 2013-01-01 05:00:00       4      20
    ##  3      542      540     923     850     160 2013-01-01 05:00:00       2      33
    ##  4      544      545    1004    1022     183 2013-01-01 05:00:00      -1     -18
    ##  5      554      600     812     837     116 2013-01-01 06:00:00      -6     -25
    ##  6      554      558     740     728     150 2013-01-01 05:00:00      -4      12
    ##  7      555      600     913     854     158 2013-01-01 06:00:00      -5      19
    ##  8      557      600     709     723      53 2013-01-01 06:00:00      -3     -14
    ##  9      557      600     838     846     140 2013-01-01 06:00:00      -3      -8
    ## 10      558      600     753     745     138 2013-01-01 06:00:00      -2       8
    ## # … with 336,766 more rows, 1 more variable: carrier <chr>, and abbreviated
    ## #   variable names ¹​sched_dep_time, ²​arr_time, ³​sched_arr_time, ⁴​air_time,
    ## #   ⁵​dep_delay, ⁶​arr_delay
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 5.

Find all flights from nycflights13 that had an arrival delay of two or
more hours. Put the arrival delay first in your output so you can check
it.

``` r
flights %>%
  filter(arr_delay / 60 >= 2) %>%
  select(arr_delay, everything()) %>%
  arrange(desc(arr_delay))
```

    ## # A tibble: 10,200 × 19
    ##    arr_delay  year month   day dep_time sched_…¹ dep_d…² arr_t…³ sched…⁴ carrier
    ##        <dbl> <int> <int> <int>    <int>    <int>   <dbl>   <int>   <int> <chr>  
    ##  1      1272  2013     1     9      641      900    1301    1242    1530 HA     
    ##  2      1127  2013     6    15     1432     1935    1137    1607    2120 MQ     
    ##  3      1109  2013     1    10     1121     1635    1126    1239    1810 MQ     
    ##  4      1007  2013     9    20     1139     1845    1014    1457    2210 AA     
    ##  5       989  2013     7    22      845     1600    1005    1044    1815 MQ     
    ##  6       931  2013     4    10     1100     1900     960    1342    2211 DL     
    ##  7       915  2013     3    17     2321      810     911     135    1020 DL     
    ##  8       895  2013     7    22     2257      759     898     121    1026 DL     
    ##  9       878  2013    12     5      756     1700     896    1058    2020 AA     
    ## 10       875  2013     5     3     1133     2055     878    1250    2215 MQ     
    ## # … with 10,190 more rows, 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 6.

Find all flights from nycflights13 that were operated by United,
American, or Delta.

``` r
flights %>%
  filter(carrier %in% c('AA','UA','DL'))
```

    ## # A tibble: 139,504 × 19
    ##     year month   day dep_time sched_de…¹ dep_d…² arr_t…³ sched…⁴ arr_d…⁵ carrier
    ##    <int> <int> <int>    <int>      <int>   <dbl>   <int>   <int>   <dbl> <chr>  
    ##  1  2013     1     1      517        515       2     830     819      11 UA     
    ##  2  2013     1     1      533        529       4     850     830      20 UA     
    ##  3  2013     1     1      542        540       2     923     850      33 AA     
    ##  4  2013     1     1      554        600      -6     812     837     -25 DL     
    ##  5  2013     1     1      554        558      -4     740     728      12 UA     
    ##  6  2013     1     1      558        600      -2     753     745       8 AA     
    ##  7  2013     1     1      558        600      -2     924     917       7 UA     
    ##  8  2013     1     1      558        600      -2     923     937     -14 UA     
    ##  9  2013     1     1      559        600      -1     941     910      31 AA     
    ## 10  2013     1     1      559        600      -1     854     902      -8 UA     
    ## # … with 139,494 more rows, 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time, ⁵​arr_delay
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 7.

Find all flights from nycflights13 that arrived more than two hours
late.

``` r
flights %>%
  filter(arr_delay / 60 >= 2) %>%
  select(arr_delay, everything()) %>%
  arrange(desc(arr_delay))
```

    ## # A tibble: 10,200 × 19
    ##    arr_delay  year month   day dep_time sched_…¹ dep_d…² arr_t…³ sched…⁴ carrier
    ##        <dbl> <int> <int> <int>    <int>    <int>   <dbl>   <int>   <int> <chr>  
    ##  1      1272  2013     1     9      641      900    1301    1242    1530 HA     
    ##  2      1127  2013     6    15     1432     1935    1137    1607    2120 MQ     
    ##  3      1109  2013     1    10     1121     1635    1126    1239    1810 MQ     
    ##  4      1007  2013     9    20     1139     1845    1014    1457    2210 AA     
    ##  5       989  2013     7    22      845     1600    1005    1044    1815 MQ     
    ##  6       931  2013     4    10     1100     1900     960    1342    2211 DL     
    ##  7       915  2013     3    17     2321      810     911     135    1020 DL     
    ##  8       895  2013     7    22     2257      759     898     121    1026 DL     
    ##  9       878  2013    12     5      756     1700     896    1058    2020 AA     
    ## 10       875  2013     5     3     1133     2055     878    1250    2215 MQ     
    ## # … with 10,190 more rows, 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 8.

Find all flights from nycflights13 that had a departure delay by at
least an hour

``` r
flights %>%
  filter(dep_delay / 60 >= 1) %>%
  select(dep_delay, everything()) %>%
  arrange(desc(dep_delay))
```

    ## # A tibble: 27,059 × 19
    ##    dep_delay  year month   day dep_time sched_…¹ arr_t…² sched…³ arr_d…⁴ carrier
    ##        <dbl> <int> <int> <int>    <int>    <int>   <int>   <int>   <dbl> <chr>  
    ##  1      1301  2013     1     9      641      900    1242    1530    1272 HA     
    ##  2      1137  2013     6    15     1432     1935    1607    2120    1127 MQ     
    ##  3      1126  2013     1    10     1121     1635    1239    1810    1109 MQ     
    ##  4      1014  2013     9    20     1139     1845    1457    2210    1007 AA     
    ##  5      1005  2013     7    22      845     1600    1044    1815     989 MQ     
    ##  6       960  2013     4    10     1100     1900    1342    2211     931 DL     
    ##  7       911  2013     3    17     2321      810     135    1020     915 DL     
    ##  8       899  2013     6    27      959     1900    1236    2226     850 DL     
    ##  9       898  2013     7    22     2257      759     121    1026     895 DL     
    ## 10       896  2013    12     5      756     1700    1058    2020     878 AA     
    ## # … with 27,049 more rows, 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​arr_time, ³​sched_arr_time, ⁴​arr_delay
    ## # ℹ Use `print(n = ...)` to see more rows, and `colnames()` to see all variable names

#### Question 9.

Sort flights from nycflights13 to find the 5 most flights whose arrival
was delayed the longest. Find the 5 flights that left earliest (most
ahead of scheduled departure time).

``` r
flights %>%
  select(arr_delay, everything()) %>%
  arrange(desc(arr_delay)) %>%
  head(5)
```

    ## # A tibble: 5 × 19
    ##   arr_delay  year month   day dep_time sched_d…¹ dep_d…² arr_t…³ sched…⁴ carrier
    ##       <dbl> <int> <int> <int>    <int>     <int>   <dbl>   <int>   <int> <chr>  
    ## 1      1272  2013     1     9      641       900    1301    1242    1530 HA     
    ## 2      1127  2013     6    15     1432      1935    1137    1607    2120 MQ     
    ## 3      1109  2013     1    10     1121      1635    1126    1239    1810 MQ     
    ## 4      1007  2013     9    20     1139      1845    1014    1457    2210 AA     
    ## 5       989  2013     7    22      845      1600    1005    1044    1815 MQ     
    ## # … with 9 more variables: flight <int>, tailnum <chr>, origin <chr>,
    ## #   dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
    ## #   time_hour <dttm>, and abbreviated variable names ¹​sched_dep_time,
    ## #   ²​dep_delay, ³​arr_time, ⁴​sched_arr_time
    ## # ℹ Use `colnames()` to see all variable names

``` r
flights %>%
  select(dep_delay, everything()) %>%
  arrange(dep_delay) %>%
  head(5)
```

    ## # A tibble: 5 × 19
    ##   dep_delay  year month   day dep_time sched_d…¹ arr_t…² sched…³ arr_d…⁴ carrier
    ##       <dbl> <int> <int> <int>    <int>     <int>   <int>   <int>   <dbl> <chr>  
    ## 1       -43  2013    12     7     2040      2123      40    2352      48 B6     
    ## 2       -33  2013     2     3     2022      2055    2240    2338     -58 DL     
    ## 3       -32  2013    11    10     1408      1440    1549    1559     -10 EV     
    ## 4       -30  2013     1    11     1900      1930    2233    2243     -10 DL     
    ## 5       -27  2013     1    29     1703      1730    1947    1957     -10 F9     
    ## # … with 9 more variables: flight <int>, tailnum <chr>, origin <chr>,
    ## #   dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
    ## #   time_hour <dttm>, and abbreviated variable names ¹​sched_dep_time,
    ## #   ²​arr_time, ³​sched_arr_time, ⁴​arr_delay
    ## # ℹ Use `colnames()` to see all variable names
