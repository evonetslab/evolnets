# Plot a network with modules as an adjacency matrix, with aligned phylogenies.

Plot a network with modules as an adjacency matrix, with aligned
phylogenies.

## Usage

``` r
plot_matrix_phylo(
  net,
  at_nodes,
  tree,
  host_tree,
  type = "states",
  state = 2,
  repertoire = "fundamental",
  modules = NULL,
  module_order = NULL,
  find_modules = TRUE,
  threshold = 0.9,
  point_size = 3,
  dodge_width = 0.025,
  colors = NULL,
  ladderize = FALSE
)
```

## Arguments

- net:

  An adjacency matrix for a bipartite network. This should be the extant
  network. Parasites should be the rows, hosts should be columns. If all
  values are 0 or 1 an binary network is represented, otherwise a
  weighted network is assumed.

- at_nodes:

  A list of length 2, output from
  [`posterior_at_nodes()`](https://maribraga.github.io/evolnets/reference/posterior_at_nodes.md).

- tree:

  The phylogeny of the symbiont clade (e.g. parasites, herbivores).
  Object of class `phylo`.

- host_tree:

  The phylogeny belonging to the hosts. Object of class `phylo`.

  See the examples on how to change the color scale.

- type:

  One of `'states'` or `'repertoires'`. If `'states'`, will plot the
  presence of a state when its posterior probability is higher than
  `threshold`. If `'repertoires'`, will plot the same but for the given
  `repertoire`.

- state:

  Which state? Default is 2. For analyses using the 3-state model,
  choose `1` or `2` (where 1 is a potential host and 2 an actual host).
  Only used if `type` is `'states'`.

- repertoire:

  Either the `'realized'` repertoire which is defined as state 2, or the
  `'fundamental'` repertoire (default) which is defined as having any
  state (usually 1 or 2), and in the 3-state model includes both actual
  and potential hosts.

- modules:

  A `moduleWeb` or a `data.frame` object defining the modules in the
  network. If a `data.frame` is passed, it must contain three columns:
  \$name with taxon names, \$module with the module the taxon was
  assigned to, and \$type which defines if the taxon is a "host" or a
  "symbiont".

- module_order:

  A character vector giving the order that modules should be plotted.
  Should contain each module only once.

- find_modules:

  Logical. Search for modules if nothing is provided in `modules`?

- threshold:

  The posterior probability above which the ancestral states should be
  shown. Defaults to 90% (`0.9`). Numeric vector of length 1.

- point_size:

  How large the ancestral state points should be, default at 3. Play
  with this and `dodge_width` to get a pleasing result. Numeric vector
  of length 1.

- dodge_width:

  How far the points should be pushed apart, when there is multiple
  states at a single node, default at 0.025. Play with this and
  `point_size` to get a pleasing result. Numeric vector of length 1.

- colors:

  Override the default colors. Should be a character vector with as many
  color values as there are modules.

- ladderize:

  Logical. Whether to ladderize the tree. Default to FALSE.

  The ancestral states are automatically colored by module. To change
  what colors are used, you can add color scales to the resulting
  `ggplot`, e.g.
  [`ggplot2::scale_color_manual()`](https://ggplot2.tidyverse.org/reference/scale_manual.html).

## Value

An assembly of plots, of class `patchwork`.

## Examples

``` r
if (FALSE) { # \dontrun{
  # read data that comes with the package
  data_path <- system.file("extdata", package = "evolnets")
  tree <- read_tree_from_revbayes(paste0(data_path,"/tree_pieridae.tre"))
  host_tree <- ape::read.tree(paste0(data_path,"/host_tree_pieridae.phy"))
  history <- read_history(paste0(data_path,"/history_thin_pieridae.txt"), burnin = 0)
  extant_net <- read.csv(paste0(data_path,"/interaction_matrix_pieridae.csv"), row.names = 1)

  # calculate posterior probability of interactions at internal nodes
  at_nodes <- posterior_at_nodes(history, tree, host_tree, 66 + 1:65)

  # plot
  plot_matrix_phylo(extant_net, at_nodes, tree, host_tree)
  # manual_colors
  plot_matrix_phylo(extant_net, at_nodes, tree, host_tree, colors = rainbow(20))
} # }
```
