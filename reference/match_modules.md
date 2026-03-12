# Match modules of different ancestral networks across time.

This function is called within
[`modules_across_ages()`](https://maribraga.github.io/evolnets/reference/modules_across_ages.md)
and gives the same name to modules from ancestral networks at different
ages that contain the same symbiont species or their parental species.

## Usage

``` r
match_modules(summary_networks, unmatched_modules, tree)
```

## Arguments

- summary_networks:

  List of reconstructed summary networks for each age.

- unmatched_modules:

  A data frame outputted from
  [`modules_from_summary_networks()`](https://maribraga.github.io/evolnets/reference/modules_from_summary_networks.md)
  containing: \$name of the network node (hosts and symbionts), \$age of
  the network, \$original_module assigned to the node, and \$type of the
  node (either "symbiont" or "host).

- tree:

  The phylogeny of the symbiont clade (e.g. parasite, herbivore), a
  `phylo` object.

## Value

A list of two elements: 1) a data frame containing the module
information for each node at each network; 2) a data frame of
correspondence between the original and the matched module names for
each network.

## Examples

``` r
if (FALSE) { # \dontrun{
unmatched_modules <- modules_from_summary_networks(summary_networks)
matched_modules <- match_modules(summary_networks, unmatched_modules[[1]], tree)
} # }
```
