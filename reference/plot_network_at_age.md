# Plot one ancestral network with module information at a given time

Plot one ancestral network with module information at a given time

## Usage

``` r
plot_network_at_age(
  subtree,
  tip_data,
  tgraph,
  module_levels,
  colors = NULL,
  tree,
  age,
  weighted = TRUE,
  weight_range = c(0, 1),
  two_state = FALSE,
  node_size = NULL,
  level_names = c("Host", "Symbiont")
)
```

## Arguments

- subtree:

  a `phylo` object of the original tree sliced at a given time in the
  past.

- tip_data:

  a `data.frame` containing the module information for each tip in the
  subtree.

- tgraph:

  a `tbl_graph` containing the nodes and edges of the ancestral network
  and the module information for each node.

- module_levels:

  Order in which the modules should be organized. Affects which color
  each module will be assigned.

- colors:

  Color vector used to plot module information.

- tree:

  The phylogeny of the symbiont clade (e.g. parasites, herbivores).
  Object of class `phylo`.

- age:

  Age of the ancestral network to be plotted as the tittle.

- weighted:

  Whether the network should have weighted edges.

- weight_range:

  The range of weights conscidered for the width of the edges.

- two_state:

  Whether the width of the edges should reflect the state (instead of
  the posterior probability).

- node_size:

  Size of the nodes in every network. If NULL, the default size is
  plotted.

- level_names:

  Optional string vector with two elements used by legend: name of the
  clade modeled as "host" and the name of the clade modeled as
  "symbiont".

## Value

An assembly of plots, of class `patchwork`.

## Examples

``` r
if (FALSE) { # \dontrun{
plot_network_at_age(subtree, tip_data, tgraph, module_levels, colors, tree, age)
} # }
```
