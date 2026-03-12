# Calculate the posterior probability of ancestral host repertoires

Group of functions to calculate the posterior probabilities of ancestral
host repertoires at internal nodes of the symbiont tree.

## Usage

``` r
posterior_at_nodes(history, tree, host_tree, nodes = NULL, state = c(2))
```

## Arguments

- history:

  Data frame with posterior samples of interaction histories returned
  from
  [`read_history()`](https://maribraga.github.io/evolnets/reference/read_history.md).

- tree:

  Symbiont tree

- host_tree:

  Host tree

- nodes:

  Vector of internal nodes for which to calculate the posterior
  probability of `state`.

- state:

  Which state? Default is 2. For analyses using the 3-state model, give
  `c(1, 2)` to include both states (where 1 is a potential host and 2 an
  actual host).

## Value

A list with three elements:

- "`samples`":

  An array of samples x nodes x hosts, containing the state of each
  sample.

- "`post_states`":

  An array of nodes x hosts x state containing the posterior probability
  for each state.

- "`post_repertoires`":

  An array of nodes x hosts x repertoire containing the posterior
  probability for 1) the `"realized"` repertoire which is defined as
  state 2, and 2) the `"fundamental"` repertoire which is defined as
  having any state (usually 1 or 2).

The number of samples is the number of iterations in `history`.

## Examples

``` r
# read parasite and host tree
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path, "/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path, "/host_tree_pieridae.phy"))

# read histories sampled during MCMC
history <- read_history(paste0(data_path, "/history_thin_pieridae.txt"), burnin = 0)

# calculate the posterior probability of host repertoires
# at chosen internal nodes of the parasite tree
nodes <- c(129:131)
pp_at_nodes <- posterior_at_nodes(history, tree, host_tree, nodes)
```
