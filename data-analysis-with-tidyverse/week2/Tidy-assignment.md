Tidying Data Assignment
================

# Please complete all the tasks listed below. After completing the tasks download the .Rmd file and upload in the peer review item for grading.

# Additionally please write text between the code chunks explaining what each code chunk is about.

# Refer the linked online textbook in case of any issues.

Load the tidyverse library

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

##### Question 1.

The built in billboard dataset is not tidy. Describe why it is not tidy
and then tidy the dataset.

``` r
# First gather up all the week entries into a row for each week for each song (where there is an entry)

billboard %>%
  pivot_longer(
    cols = starts_with("wk"),
    names_to = "week",
    names_prefix = "wk",
    values_to = "rank",
    values_drop_na = TRUE
  )
```

    ## # A tibble: 5,307 × 5
    ##    artist  track                   date.entered week   rank
    ##    <chr>   <chr>                   <date>       <chr> <dbl>
    ##  1 2 Pac   Baby Don't Cry (Keep... 2000-02-26   1        87
    ##  2 2 Pac   Baby Don't Cry (Keep... 2000-02-26   2        82
    ##  3 2 Pac   Baby Don't Cry (Keep... 2000-02-26   3        72
    ##  4 2 Pac   Baby Don't Cry (Keep... 2000-02-26   4        77
    ##  5 2 Pac   Baby Don't Cry (Keep... 2000-02-26   5        87
    ##  6 2 Pac   Baby Don't Cry (Keep... 2000-02-26   6        94
    ##  7 2 Pac   Baby Don't Cry (Keep... 2000-02-26   7        99
    ##  8 2Ge+her The Hardest Part Of ... 2000-09-02   1        91
    ##  9 2Ge+her The Hardest Part Of ... 2000-09-02   2        87
    ## 10 2Ge+her The Hardest Part Of ... 2000-09-02   3        92
    ## # … with 5,297 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

``` r
# Then, convert the week variable to a number and figure out the date corresponding to each week on the chart

billboard %>%
  pivot_longer(
    cols = starts_with("wk"),
    names_to = "week",
    names_prefix = "wk",
    values_to = "rank",
    values_drop_na = TRUE
  ) %>%
  mutate(date = date.entered + (as.integer(week) - 1) * 7)
```

    ## # A tibble: 5,307 × 6
    ##    artist  track                   date.entered week   rank date      
    ##    <chr>   <chr>                   <date>       <chr> <dbl> <date>    
    ##  1 2 Pac   Baby Don't Cry (Keep... 2000-02-26   1        87 2000-02-26
    ##  2 2 Pac   Baby Don't Cry (Keep... 2000-02-26   2        82 2000-03-04
    ##  3 2 Pac   Baby Don't Cry (Keep... 2000-02-26   3        72 2000-03-11
    ##  4 2 Pac   Baby Don't Cry (Keep... 2000-02-26   4        77 2000-03-18
    ##  5 2 Pac   Baby Don't Cry (Keep... 2000-02-26   5        87 2000-03-25
    ##  6 2 Pac   Baby Don't Cry (Keep... 2000-02-26   6        94 2000-04-01
    ##  7 2 Pac   Baby Don't Cry (Keep... 2000-02-26   7        99 2000-04-08
    ##  8 2Ge+her The Hardest Part Of ... 2000-09-02   1        91 2000-09-02
    ##  9 2Ge+her The Hardest Part Of ... 2000-09-02   2        87 2000-09-09
    ## 10 2Ge+her The Hardest Part Of ... 2000-09-02   3        92 2000-09-16
    ## # … with 5,297 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

``` r
# Sort the data by artist, track and week. Here are what your first entries should be (formatting can be different):
billboard %>%
  pivot_longer(
    cols = starts_with("wk"),
    names_to = "week",
    names_prefix = "wk",
    values_to = "rank",
    values_drop_na = TRUE
  ) %>%
  mutate(date = date.entered + (as.integer(week) - 1) * 7) %>%
  arrange(artist, track, week)
```

    ## # A tibble: 5,307 × 6
    ##    artist  track                   date.entered week   rank date      
    ##    <chr>   <chr>                   <date>       <chr> <dbl> <date>    
    ##  1 2 Pac   Baby Don't Cry (Keep... 2000-02-26   1        87 2000-02-26
    ##  2 2 Pac   Baby Don't Cry (Keep... 2000-02-26   2        82 2000-03-04
    ##  3 2 Pac   Baby Don't Cry (Keep... 2000-02-26   3        72 2000-03-11
    ##  4 2 Pac   Baby Don't Cry (Keep... 2000-02-26   4        77 2000-03-18
    ##  5 2 Pac   Baby Don't Cry (Keep... 2000-02-26   5        87 2000-03-25
    ##  6 2 Pac   Baby Don't Cry (Keep... 2000-02-26   6        94 2000-04-01
    ##  7 2 Pac   Baby Don't Cry (Keep... 2000-02-26   7        99 2000-04-08
    ##  8 2Ge+her The Hardest Part Of ... 2000-09-02   1        91 2000-09-02
    ##  9 2Ge+her The Hardest Part Of ... 2000-09-02   2        87 2000-09-09
    ## 10 2Ge+her The Hardest Part Of ... 2000-09-02   3        92 2000-09-16
    ## # … with 5,297 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

``` r
#>  A tibble: 5,307 x 5
#   artist  track                   date.entered  week  rank   date
 #    <chr>   <chr>                   <date>       <int> <dbl>   <date>
 #  1 2 Pac   Baby Don't Cry (Keep... 2000-02-26       1    87 2000-02-26
 #  2 2 Pac   Baby Don't Cry (Keep... 2000-02-26       2    82 2000-03-04
 #  3 2 Pac   Baby Don't Cry (Keep... 2000-02-26       3    72 2000-03-11
 #  4 2 Pac   Baby Don't Cry (Keep... 2000-02-26       4    77 2000-03-18
 #  5 2 Pac   Baby Don't Cry (Keep... 2000-02-26       5    87 2000-03-25
 #  6 2 Pac   Baby Don't Cry (Keep... 2000-02-26       6    94 2000-04-01
 #  7 2 Pac   Baby Don't Cry (Keep... 2000-02-26       7    99 2000-04-08
 #  8 2Ge+her The Hardest Part Of ... 2000-09-02       1    91 2000-09-02
 #  9 2Ge+her The Hardest Part Of ... 2000-09-02       2    87 2000-09-09
 # 10 2Ge+her The Hardest Part Of ... 2000-09-02       3    92 2000-09-16
 # … with 5,297 more rows
```

##### Question 2.

Tidy the “fish_encounters” dataset of fish spotting by monitoring
stations. Make the NA into 0 using the option “values_fill = list(seen =
0)”

``` r
fish_encounters %>%
  complete(fish, station, fill = list(seen = 0))
```

    ## # A tibble: 209 × 3
    ##    fish  station  seen
    ##    <fct> <fct>   <int>
    ##  1 4842  Release     1
    ##  2 4842  I80_1       1
    ##  3 4842  Lisbon      1
    ##  4 4842  Rstr        1
    ##  5 4842  Base_TD     1
    ##  6 4842  BCE         1
    ##  7 4842  BCW         1
    ##  8 4842  BCE2        1
    ##  9 4842  BCW2        1
    ## 10 4842  MAE         1
    ## # … with 199 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

##### Question 3.

Import the flowers1 dataset. Tidy and pivot the data. Hint: use
“read_csv2()” to read in the dataset

``` r
flowers1 <- read_csv2("flowers1.csv")
```

    ## ℹ Using "','" as decimal and "'.'" as grouping mark. Use `read_delim()` for more control.

    ## Rows: 48 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ";"
    ## chr (1): Variable
    ## dbl (3): Time, replication, Value
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
flowers1 %>%
  pivot_wider(
    names_from = Variable,
    values_from = c(Value),
  )
```

    ## # A tibble: 24 × 4
    ##     Time replication Flowers Intensity
    ##    <dbl>       <dbl>   <dbl>     <dbl>
    ##  1     1           1    62.3       150
    ##  2     1           2    77.4       150
    ##  3     1           3    55.3       300
    ##  4     1           4    54.2       300
    ##  5     1           5    49.6       450
    ##  6     1           6    61.9       450
    ##  7     1           7    39.4       600
    ##  8     1           8    45.7       600
    ##  9     1           9    31.3       750
    ## 10     1          10    44.9       750
    ## # … with 14 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

##### Question 4.

Import the flowers2 dataset. Tidy the dataset by turning the one column
into 3 separate columns

``` r
flowers2 <- read_csv2("flower2.csv")
```

    ## ℹ Using "','" as decimal and "'.'" as grouping mark. Use `read_delim()` for more control.

    ## Rows: 24 Columns: 2
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ";"
    ## chr (1): Flowers/Intensity
    ## dbl (1): Time
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
flowers2 %>% 
  separate("Flowers/Intensity",c("Flowers", "Intensity"), "/")
```

    ## # A tibble: 24 × 3
    ##    Flowers Intensity  Time
    ##    <chr>   <chr>     <dbl>
    ##  1 62.3    150           1
    ##  2 77.4    150           1
    ##  3 55.3    300           1
    ##  4 54.2    300           1
    ##  5 49.6    450           1
    ##  6 61.9    450           1
    ##  7 39.4    600           1
    ##  8 45.7    600           1
    ##  9 31.3    750           1
    ## 10 44.9    750           1
    ## # … with 14 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

##### Question 5.

In the following dataset, turn the implicit missing values to explicit

``` r
output <- tibble(
      treatment   = c("a", "b", "a", "c", "b"),
      gender   = factor(c("M", "F", "F", "M", "M"), levels = c("M", "F", "O")),
      return = c(1.5, 0.75,  0.5,  1.8,  NA)
    )
output  %>%
  complete(treatment, gender)
```

    ## # A tibble: 9 × 3
    ##   treatment gender return
    ##   <chr>     <fct>   <dbl>
    ## 1 a         M        1.5 
    ## 2 a         F        0.5 
    ## 3 a         O       NA   
    ## 4 b         M       NA   
    ## 5 b         F        0.75
    ## 6 b         O       NA   
    ## 7 c         M        1.8 
    ## 8 c         F       NA   
    ## 9 c         O       NA

\#####Question 6.

Import the weather dataset as weather. Use “pivot_longer()” to put the
days all in one column, then use “pivot_wider” to separate tmax and tmin
into separate columns. Print the summary of the final resulting dataset

``` r
weather <- read_csv(url("https://raw.githubusercontent.com/JaneWall/data_STAT412612/master/weather.csv"))
```

    ## Rows: 22 Columns: 35
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): id, element
    ## dbl (25): year, month, d1, d2, d3, d4, d5, d6, d7, d8, d10, d11, d13, d14, d...
    ## lgl  (8): d9, d12, d18, d19, d20, d21, d22, d24
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
weather %>% 
  pivot_longer(
    cols = starts_with("d"),
    names_to = "Day",
    values_to = "Temp",
  )  %>% 
  pivot_wider(
    names_from = element,
    values_from = c(Temp)
  )
```

    ## # A tibble: 341 × 6
    ##    id       year month Day    tmax  tmin
    ##    <chr>   <dbl> <dbl> <chr> <dbl> <dbl>
    ##  1 MX17004  2010     1 d1       NA    NA
    ##  2 MX17004  2010     1 d2       NA    NA
    ##  3 MX17004  2010     1 d3       NA    NA
    ##  4 MX17004  2010     1 d4       NA    NA
    ##  5 MX17004  2010     1 d5       NA    NA
    ##  6 MX17004  2010     1 d6       NA    NA
    ##  7 MX17004  2010     1 d7       NA    NA
    ##  8 MX17004  2010     1 d8       NA    NA
    ##  9 MX17004  2010     1 d9       NA    NA
    ## 10 MX17004  2010     1 d10      NA    NA
    ## # … with 331 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

###### Question 7.

Load the built in “anscombe” data frame and use “pivot_longer()” to
separate all the x and y columns and categorize them into 4 sets

``` r
anscombe %>%
  pivot_longer(
    everything(),
    names_to = c(".value", "set"),
    names_pattern = "(.)(.)"
  )
```

    ## # A tibble: 44 × 3
    ##    set       x     y
    ##    <chr> <dbl> <dbl>
    ##  1 1        10  8.04
    ##  2 2        10  9.14
    ##  3 3        10  7.46
    ##  4 4         8  6.58
    ##  5 1         8  6.95
    ##  6 2         8  8.14
    ##  7 3         8  6.77
    ##  8 4         8  5.76
    ##  9 1        13  7.58
    ## 10 2        13  8.74
    ## # … with 34 more rows
    ## # ℹ Use `print(n = ...)` to see more rows
