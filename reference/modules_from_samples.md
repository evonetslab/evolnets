# Find modules in networks sampled across MCMC at specific time slices

Find modules in networks sampled across MCMC at specific time slices

## Usage

``` r
modules_from_samples(sampled_networks)
```

## Arguments

- sampled_networks:

  List of sampled networks at time slices produced by
  [`get_sampled_networks()`](https://evonetslab.github.io/evolnets/reference/get_sampled_networks.md).

## Value

Data frame with module membership information for each sampled network
at each time slice.

## Examples

``` r
if (FALSE) { # \dontrun{
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path, "/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path, "/host_tree_pieridae.phy"))
history <- read_history(paste0(data_path, "/history_thin_pieridae.txt"), burnin = 0)

ages <- c(60, 50, 40, 0)
at_ages <- posterior_at_ages(history, ages, tree, host_tree)
sampled_networks <- get_sampled_networks(at_ages)
#
mod_samples <- modules_from_samples(sampled_networks)
} # }
```
