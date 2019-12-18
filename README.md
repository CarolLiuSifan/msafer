
<!-- README.md is generated from README.Rmd. Please edit that file -->

# msafer

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![CRAN
status](https://www.r-pkg.org/badges/version/msafer)](https://CRAN.R-project.org/package=msafer)
[![Build
Status](https://travis-ci.com/kpien/msafer.svg?branch=master)](https://travis-ci.com/kpien/msafer)
<!-- badges: end -->

**msafer** is a package that frees users from having to manually find
the location of an error when using the function `map()`. When `map()`
returns an error, it’s unclear where this error occurs. The function
`map_safe()` takes in a vector, function and requirements, and spits out
`TRUE` or `FALSE` based on whether an error occurs when running the
function over the vector. `map_safe()` will return a list of logical
returns where it will be easy to identify the place of the error.

## Installation

You can install the development version of msafer from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("kpien/msafer")
```

## Example

For demonstration purposes, let’s create a sample list of dataframes
from the `starwars` and `mtcars` datasets.

``` r
sample_a <- dplyr::sample_n(dplyr::starwars, 34)
sample_b <- dplyr::sample_n(mtcars, 1:20)
a <- list(dplyr::starwars, sample_a, sample_b)
```

Pass `map_safe_merge()` the same arguments as `map()`. These would be
the list of dataframes, the function to map over all the dataframes, and
any arguments that the function needs. `map_safe_merge()` will return a
tibble with the file numbers and any errors that may have occurred while
trying to apply `map()`, grouping repeat errors together.

``` r
library(msafer)
map_safe_merge(a, dplyr::select, height)
#> # A tibble: 3 x 2
#>   result error_message                                           
#>   <lgl>  <chr>                                                   
#> 1 TRUE   NA                                                      
#> 2 TRUE   NA                                                      
#> 3 FALSE  "Error in .f(.x[[i]], ...): object 'height' not found\n"
```

## Developed By

Sifan(Carol) Liu, Kelly Pien, Huiqing(Lily) Jin
