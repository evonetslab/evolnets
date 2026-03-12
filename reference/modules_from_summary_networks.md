# Identify modules for each summary network at each age

This function is called within
[`modules_across_ages()`](https://maribraga.github.io/evolnets/reference/modules_across_ages.md).

## Usage

``` r
modules_from_summary_networks(summary_networks, extant_modules = NULL)
```

## Arguments

- summary_networks:

  List of reconstructed summary networks for each age (output from
  `get_summary_network()`).

- extant_modules:

  A `moduleWeb` object defining the modules in the extant network.

## Value

A list of 2 elements: 1) a data frame containing the module membership
of each node at each age before matching; 2) a list of `moduleWeb`
objects for each age.

## Examples

``` r
if (FALSE) { # \dontrun{
unmatched_modules <- modules_from_summary_networks(summary_networks)
} # }
```
