Problem Set 1
================
yamur
2022-07-20

``` r
library("ggplot2")
```

## Problem Set 1

#### Question 1.

Write a roll function that simulates rolling two six-sided die. The
function should contain no input arguments.

``` r
roll <- function() {
  die <- 1:6
  dice <- sample(die, size = 2, replace = TRUE)
  sum(dice)
}
```

#### Question 2.

Rewrite the roll function to include an argument for the type of die
(e.g. three-, six-, eight-sided). Think about what other input arguments
should be allowed. How would you update your function to include them?

``` r
roll2 <- function(bones=1:6, size=3) {
  dice <- sample(bones, size, replace = TRUE)
  sum(dice)
}
```

#### Test

``` r
roll2()
```

    ## [1] 13

``` r
roll2(bones=1:4)
```

    ## [1] 10

#### Question 3.

Produce a historgram of 50,000 rolls of three eight-sided fair dice.

``` r
roll3 <- function(bones=1:8, size=2) {
  dice <- sample(bones, size = size, replace = TRUE)
  sum(dice)
}

roll3(bones = 1:8, size=3)
```

    ## [1] 7

``` r
# qplot makes a histogram when you give it a single vector.
rolls3 <- replicate(50000, roll3())
qplot(rolls3, binwidth = 1)
```

![](Problem-Set-1_files/figure-gfm/qplot-1.png)<!-- -->

#### Question 4.

Produce a historgram of 50,000 rolls of three eight-sided dice where the
dice are loaded so that the number 7 has a higher probability of being
rolled than the other numbers, assume all the other numbers have a 1/10
probability of being rolled.

``` r
roll4 <- function() {
  die <- 1:8
  dice <- sample(die, size = 3, replace = TRUE, 
    prob = c(1/10, 1/10, 1/10, 1/10, 1/10, 3/10,1/10,1/10))
  sum(dice)
}
```

``` r
# qplot makes a histogram when you give it a single vector.
rolls4 <- replicate(50000, roll4())
qplot(rolls4, binwidth = 1)
```

![](Problem-Set-1_files/figure-gfm/weighted%20dice%20qplot-1.png)<!-- -->

#### Question 5.

Rewrite the “rescale01()” function such that -Inf is mapped to 0 and Inf
is mapped to 1.

``` r
x <- c(1:10,-Inf, Inf)
rescale01 <- function(v){
  rng <- range(v, na.rm=FALSE,finite = TRUE)
  v <- (v-rng[1])/(rng[2]-rng[1])
  # -Inf is mapped to 0 and Inf is mapped to 1.
  ifelse(is.finite(v), v, ifelse(v > 0, 1, 0))
}
rescale01(x)
```

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000 0.0000000 1.0000000

#### Question 6.

Write both_na(), a function that takes two vectors of the same length
and returns the number of positions that have an NA in both vectors.

``` r
x <- c(0, 1, NA, NA, NA, 3, -4, NA)
y <- c(-3, NA, 0, NA, NA, NA, 0, 1)

# one line solution (for loop would also do the job but not efficient)
both_na <- function(x, y){
  which(is.na(x) & is.na(y))
}

both_na(x,y)
```

    ## [1] 4 5
