# Modified version of bipartite's computeModules function

Modified version of bipartite's computeModules function

## Usage

``` r
mycomputeModules(
  web,
  method = "Beckett",
  steps = 1e+06,
  tolerance = 1e-10,
  forceLPA = FALSE
)
```

## Arguments

- web:

  Incidence matrix

- method:

  Becket

- steps:

  steps

- tolerance:

  tolerance

- forceLPA:

  FALSE

## Value

Modularity Q

## Examples

``` r
if (FALSE) { # \dontrun{
data_path <- system.file("extdata", package = "evolnets")
extant_net <- read.csv(paste0(data_path, "/interaction_matrix_pieridae.csv"), row.names = 1)

mod <- mycomputeModules(extant_net)
} # }
```
