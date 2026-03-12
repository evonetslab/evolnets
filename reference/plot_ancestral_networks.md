# Plot ancestral networks with module information

Plot ancestral networks with module information

## Usage

``` r
plot_ancestral_networks(
  summary_networks,
  matched_modules,
  tree,
  module_levels = NULL,
  colors = NULL,
  node_size = NULL,
  level_names = c("Host", "Symbiont")
)
```

## Arguments

- summary_networks:

  A list of incidence matrices (summary network) for each time slice in
  `ages`. Output of `get_summary_network()`

- matched_modules:

  A list of lists containing the module information for each node at
  each network. Output of
  [`modules_across_ages()`](https://maribraga.github.io/evolnets/reference/modules_across_ages.md).

- tree:

  The phylogeny of the symbiont clade (e.g. parasites, herbivores).
  Object of class `phylo`.

- module_levels:

  Order in which the modules should be organized. Affects which color
  each module will be assigned. If NULL, takes the order of appearance
  in `matched_modules$module`.

- colors:

  Color vector used to plot module information.

- node_size:

  Size of the nodes in every network. If NULL, the default size is
  plotted.

- level_names:

  Optional string vector with two elements used by legend: name of the
  clade modeled as "host" and the name of the clade modeled as
  "symbiont".

## Value

A list of plots of class `patchwork`. Each element contains the tree and
network at a given time slice.

## Examples

``` r
if (FALSE) { # \dontrun{
  # read data that comes with the package
  data_path <- system.file("extdata", package = "evolnets")
  tree <- read_tree_from_revbayes(paste0(data_path,"/tree_pieridae.tre"))
  host_tree <- ape::read.tree(paste0(data_path,"/host_tree_pieridae.phy"))
  history <- read_history(paste0(data_path,"/history_thin_pieridae.txt"), burnin = 0)

  # find and match modules of summary networks at ages
  ages <- c(60, 50, 40, 0)
  at_ages <- posterior_at_ages(history, ages, tree, host_tree)
  summary_networks <- get_summary_networks(at_ages, threshold = 0.5, weighted = TRUE)
  all_mod <- modules_across_ages(summary_networks, tree)

  # plot
  plot <- plot_ancestral_networks(summary_networks, all_mod, tree)
  patchwork::wrap_plots(plot, guides = "collect")
} # }
```
