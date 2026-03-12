# Calculate support for modules from summary networks based on modules of sampled networks

Validate modules from summary networks by calculating the frequency with
which pairs of nodes are placed in the same module in networks sampled
across MCMC

## Usage

``` r
support_for_modules(
  mod_samples,
  modules_across_ages,
  threshold = 0.7,
  edge_list = TRUE,
  include_all = FALSE,
  colors = NULL,
  module_levels = NULL,
  axis_text = FALSE
)
```

## Arguments

- mod_samples:

  Data frame produced by
  [`modules_from_samples()`](https://maribraga.github.io/evolnets/reference/modules_from_samples.md)
  containing module membership of each node for each sampled network at
  each time slice before the present.

- modules_across_ages:

  Data frame containing the module information for the summary network.
  A `list` object returned from
  [`modules_across_ages()`](https://maribraga.github.io/evolnets/reference/modules_across_ages.md)
  or a `data.frame` object defining the modules in the networks. If a
  `data.frame` is passed, it must contain three columns: `$age` - the
  age of the network, `$name` - taxon names, `$module` - the module the
  taxon was assigned to.

- threshold:

  Minimum frequency with which two nodes are placed in the same module
  to consider it supported. Only pairs with frequency higher than this
  threshold are plotted with the color of the module from the summary
  network.

- edge_list:

  Logical. Whether to return a list of edge lists or a list of matrices
  of pairwise frequency.

- include_all:

  Logical. Include all nodes or only those present at the time slice?

- colors:

  Optional. Vector of module colors in the plot.

- module_levels:

  Optional. Order of modules in the color vector.

- axis_text:

  Logical. Plot taxon names?

## Value

A list containing:

1.  `plot`: A plot of pairwise frequency with which the two nodes are
    placed in the same module in the ancestral network for each time
    slice in `ages`. Cells in the diagonal show how often a host is
    sampled in a network (symbionts are always present);

2.  `pairwise_membership`: A list of edge lists or matrices with the
    pairwise frequencies at each time slice;

3.  `mean_support`: A list of mean and geometric mean pairwise frequency
    for each module at each time slice.

## Examples

``` r
if (FALSE) { # \dontrun{
ages <- c(60, 50, 40, 0)
at_ages <- posterior_at_ages(history, ages, tree, host_tree)

weighted_net_50 <- get_summary_network(at_ages, pt = 0.5, weighted = TRUE)
all_mod <- modules_across_ages(weighted_net_50, tree)

# find modules for each sampled network
mod_samples <- modules_from_samples(at_ages)

# calculate support
support <- support_for_modules(mod_samples, all_mod)
support$plot
support$means
} # }
```
