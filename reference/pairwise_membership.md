# Calculate frequency that pairs of nodes fall within the same module

Calculate frequency that pairs of nodes fall within the same module

## Usage

``` r
pairwise_membership(mod_samples, ages, edge_list = TRUE)
```

## Arguments

- mod_samples:

  Output from
  [`modules_from_samples()`](https://evonetslab.github.io/evolnets/reference/modules_from_samples.md)

- ages:

  Vector of network ages

- edge_list:

  Should output be an edge list?

## Value

An edge list with the frequency that each pair of nodes in the network
is placed in the same module across network samples.

## Examples

``` r
if (FALSE) { # \dontrun{
pairwise_membership(mod_samples, c(0))
} # }
```
