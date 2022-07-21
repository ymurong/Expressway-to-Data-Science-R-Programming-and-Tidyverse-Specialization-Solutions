Problem Set 2
================

### Introduction

Reference the [tidyverse style guide](https://style.tidyverse.org/)
while completing the exercises.

These exercises are ungraded.

#### Question 1.

Read and understand the three functions below. Try to rename them such
that the function names are short and descriptive.

    f1 <- has_prefix(string, prefix) {
      substr(string, 1, nchar(prefix)) == prefix
    }

    f2 <- remove_last_element(x) {
      if (length(x) <= 1) return(NULL)
      x[-length(x)]
    }

    f3 <- first_n_elements(x, y) {
      rep(y, length.out = length(x))
    }

#### Question 2.

Write a function that prints “input must be numeric” if the function
input is not numeric and returns two times the number otherwise.

``` r
times_2 <- function(x){
  if(!is.numeric(x)){
    stop("input must be numeric")
  }
  return(x*2)
}

times_2(2)
```

    ## [1] 4

#### Question 3.

Implement a fizzbuzz function. It takes a single number as input. If the
number is divisible by three, it returns “fizz”. If it’s divisible by
five it returns “buzz”. If it’s divisible by three and five, it returns
“fizzbuzz”. Otherwise, it returns the number. Make sure you first write
working code before you create the function.

``` r
fizzbuzz <- function(x){
  if (x %% 3 == 0) {
    return("fizz")
  }
  if (x %% 5 == 0) {
    return("buzz")
  }
  if (x %% 3 == 0 & x %% 5 == 0) {
    return("fizzbuzz")
  }
  return(x)
}

assert("something went wrong",{
  fizzbuzz(3) == "fizz"
  fizzbuzz(5) == "buzz"
  fizzbuzz(15) == "fizzbuzz"
  fizzbuzz(4) == 4
})
```

#### Question 4.

Use the cut() function to simplify the given set of nested if-else
statements.

    if (temp <= 0) {
      "freezing"
      } else if (temp <= 10) {
      "cold"
      } else if (temp <= 20) {
      "cool"
      } else if (temp <= 30) {
      "warm"
      } else {
      "hot"
    }

``` r
x = c(-30,5,15,25,35)
cut(x, breaks = c(-Inf, 0, 10, 20, 30, Inf),
    labels = c("freezing", "cold", "cool", "warm", "hot"))
```

    ## [1] freezing cold     cool     warm     hot     
    ## Levels: freezing cold cool warm hot
