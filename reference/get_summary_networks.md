# Get summary networks from posterior probabilities of interactions of extant lineages at given time points in the past

Get summary networks from posterior probabilities of interactions of
extant lineages at given time points in the past

## Usage

``` r
get_summary_networks(
  at_ages,
  threshold,
  ages = NULL,
  weighted = TRUE,
  type = "states",
  state = 2,
  repertoire = "fundamental"
)
```

## Arguments

- at_ages:

  List of lists, with samples and posterior probabilities for each
  interaction of extant lineages at given ages. Usually calculated
  `posterior_at_ages`, see example.

- threshold:

  Probability threshold to include an interaction in the network.
  Interactions with posterior `probability < threshold` will be dropped.

- ages:

  Vector of ages (time points in the past) at which samples were
  retrieved. By default, uses all ages present in `pp_at_ages`.

- weighted:

  Logical. Use posterior probabilities as interaction weights?

- type:

  One of `'states'` or `'repertoires'`. If `'states'`, will plot the
  presence of a state when its posterior probablity is higher than
  `threshold`. If `'repertoires'`, will plot the same but for the given
  `repertoire`. Note that this is also applied to the extant network.

- state:

  Which state? Default is 2. For analyses using the 3-state model,
  choose `1`, `2` or both using `c(1, 2)` (where 1 is a potential host
  and 2 an actual host). Only used if `type` is `'states'`. Note that
  this is also applied to the extant network.

- repertoire:

  Either the `'realized'` repertoire which is defined as state 2, or the
  `'fundamental'` repertoire (default) which is defined as having any
  state (usually 1 or 2), and in the 3-state model includes both actual
  and potential hosts. Note that this is also applied to the extant
  network.

## Value

A list of incidence matrices (summary network) for each time slice in
`ages`.

## Examples

``` r
# read data that comes with the package
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path, "/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path, "/host_tree_pieridae.phy"))
history <- read_history(paste0(data_path, "/history_thin_pieridae.txt"), burnin = 0)

# choose ages in the past
ages <- c(60, 50, 40, 0)

# calculate posterior probabilities of interactions
at_ages <- posterior_at_ages(history, ages, tree, host_tree)

# get ancestral summary networks
weighted_net_50 <- get_summary_networks(at_ages, threshold = 0.5, weighted = TRUE)
binary_net_90 <- get_summary_networks(at_ages, threshold = 0.9, weighted = FALSE)
```
