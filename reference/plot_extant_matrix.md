# Plot a network with modules as an adjacency matrix

Plot a network with modules as an adjacency matrix

## Usage

``` r
plot_extant_matrix(
  net,
  modules = NULL,
  module_order = NULL,
  find_modules = TRUE,
  parasite_order = NULL,
  host_order = NULL,
  state_alpha = c(0.5, 1)
)
```

## Arguments

- net:

  An adjacency matrix for a bipartite network. Parasites should be the
  rows, hosts should be columns. If all values are 0/1 (or 0/2), a
  binary network is represented; if all values are 0/1/2, a network with
  potential and actual interactions is represented; otherwise a weighted
  network is assumed.

- modules:

  A `moduleWeb` or a `data.frame` object defining the models in the
  network. If left `NULL` the modules are automatically calculated. If a
  `data.frame` is passed, it must contain three columns: \$name with
  taxon names, \$module with the module the taxon was assigned to, and
  \$type which defines if the taxon is a "host" or a "symbiont".

- module_order:

  A character vector giving the order that modules should be plotted.
  Should contain each module only once.

- find_modules:

  Logical. Search for modules if nothing is provided in `modules`?

- parasite_order:

  A character vector giving the order the parasite should be listed in.
  Should contain each parasite only once, and include the row names of
  `net`.

- host_order:

  A character vector giving the order the hosts should be listed in.
  Should contain each host only once, and include the column names of
  `net`.

- state_alpha:

  A numeric vector of length 2. Gives the alpha (transparency) values
  for the interaction type in the three-state model

## Value

A `ggplot` object.

## Examples

``` r
if (FALSE) { # \dontrun{
# The slow portion of this function is the calculation of the modules.
plot_extant_matrix(extant_net)

# Change our network to a weighted one:
extant_net_weighted <- extant_net
extant_net_weighted[extant_net == 1] <- runif(sum(extant_net))
plot_extant_matrix(extant_net_weighted)
} # }
```
