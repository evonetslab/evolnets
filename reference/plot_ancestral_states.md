# Plot ancestral states on the phylogeny.

Plot ancestral states on the phylogeny.

## Usage

``` r
plot_ancestral_states(
  tree,
  at_nodes,
  modules,
  module_order = NULL,
  type = "states",
  state = 2,
  repertoire = "fundamental",
  layout = "rectangular",
  threshold = 0.9,
  point_size = 3,
  point_shape = NULL,
  dodge_width = 0.025,
  legend = TRUE,
  colors = NULL,
  state_alpha = c(0.5, 1),
  ladderize = FALSE
)
```

## Arguments

- tree:

  The phylogeny, a `phylo` object.

- at_nodes:

  A list of length 2, output from
  [`posterior_at_nodes()`](https://maribraga.github.io/evolnets/reference/posterior_at_nodes.md).

- modules:

  A `moduleWeb` or a `data.frame` object defining the modules in the
  network. If a `data.frame` is passed, it must contain three columns:
  \$name with taxon names, \$module with the module the taxon was
  assigned to, and \$type which defines if the taxon is a "host" or a
  "symbiont".

- module_order:

  A character vector giving the order that modules should be plotted.
  Should contain each module only once.

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

- layout:

  One of `'rectangular'`, `'slanted'`, `'fan'`, `'circular'`,
  `'radial'`, `'equal_angle'`, `'daylight'` or `'ape'`.

- threshold:

  The posterior probability above which the ancestral states should be
  shown. Defaults to 90% (`0.9`). Numeric vector of length 1.

- point_size:

  How large the ancestral state points should be, default at 3. Play
  with this and `dodge_width` to get a pleasing result. Numeric vector
  of length 1.

- point_shape:

  What point shape should be used for the ancestral states? When left
  `NULL`, a reasonable default will be chosen. Otherwise, a numeric
  vector of length 1.

- dodge_width:

  How far the points should be pushed apart, when there is multiple
  states at a single node, default at 0.025. Play with this and
  `point_size` to get a pleasing result. Numeric vector of length 1.

- legend:

  Whether to display a legend for the colors. Logical vector of length
  1.

- colors:

  Override the default colors. Should be a character vector with as many
  color values as there are modules.

- state_alpha:

  A numeric vector of length 2. Gives the alpha (transparency) values
  for the interaction type in the three-state model

- ladderize:

  Logical. Whether to ladderize the tree. Default to FALSE.

  The ancestral states are automatically colored by module. To change
  what colors are used, you can add color scales to the resulting
  `ggplot`, e.g.
  [`ggplot2::scale_color_manual()`](https://ggplot2.tidyverse.org/reference/scale_manual.html).

## Value

A `ggplot` object.

## Examples

``` r
if (FALSE) { # \dontrun{
  # read data that comes with the package
  data_path <- system.file("extdata", package = "evolnets")
  tree <- read_tree_from_revbayes(paste0(data_path,"/tree_pieridae.tre"))
  host_tree <- read.tree(paste0(data_path,"/host_tree_pieridae.phy"))
  history <- read_history(paste0(data_path,"/history_thin_pieridae.txt"), burnin = 0)
  extant_net <- read.csv(paste0(data_path,"/interaction_matrix_pieridae.csv"), row.names = 1)

  # calculate posterior probability of interactions at internal nodes
  at_nodes <- posterior_at_nodes(history, tree, host_tree, 66 + 1:65)

  # find modules in the extant network
  mods <- mycomputeModules(extant_net)

  # plot ancestral states
  plot_ancestral_states(tree, at_nodes, mods)
  # Manual colors
  plot_ancestral_states(tree, at_nodes, mods, colors = rainbow(20))
} # }
```
