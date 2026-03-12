# Read history.txt file produced by RevBayes

Read history.txt file containing the posterior samples of interaction
histories

## Usage

``` r
read_history(path_to_hist, burnin = 0.1)
```

## Arguments

- path_to_hist:

  String path to the .txt file exported from RevBayes

- burnin:

  Fraction of iterations to be removed as burnin. Default to 10%.

## Value

A data.frame

## Examples

``` r
# read history file
if (FALSE) history <- read_history("/path/history.txt", burnin = 0.2) # \dontrun{}
```
