# Calculate the posterior probability of ancestral host repertoires at time points in the past (ages)

Calculate the posterior probability of ancestral host repertoires at
time points in the past (ages)

## Usage

``` r
posterior_at_ages(
  history,
  ages,
  tree,
  host_tree,
  extant_prob = FALSE,
  state = 2,
  drop_empty = TRUE
)
```

## Arguments

- history:

  Data frame with posterior samples of interaction histories. Output
  from
  [`read_history()`](https://evonetslab.github.io/evolnets/reference/read_history.md).

- ages:

  Vector of ages (time points in the past) at which samples will be
  retrieved. The present (`age = 0`) must be included.

- tree:

  Symbiont tree.

- host_tree:

  Host tree.

- extant_prob:

  Should posterior probabilities be calculated for extant network?
  Default to `FALSE`. `TRUE` only makes sense if interactions in the
  extant network were also inferred. When `FALSE`, only the first MCMC
  sample will be retrieved at `age = 0`.

- state:

  Which state? Default is 2. For analyses using the 3-state model, give
  `c(1, 2)` to include both states (where 1 is a potential host and 2 an
  actual host).

- drop_empty:

  Logical. Remove taxa without any interactions?

## Value

A list of three lists, containing:

- "`samples`":

  Arrays of samples x nodes x hosts, containing the state of each
  sample.

- "`post_states`":

  Arrays of nodes x hosts x state containing the posterior probability
  for each state.

- "`post_repertoires`":

  Arrays of nodes x hosts x repertoire containing the posterior
  probability for 1) the `"realized"` repertoire which is defined as
  state 2, and 2) the `"fundamental"` repertoire which is defined as
  having any state (usually 1 or 2).

Each array in these lists is for one of the `ages`. The number of
samples is the number of iterations in `history`.

## Examples

``` r
# read symbiont and host tree
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path, "/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path, "/host_tree_pieridae.phy"))

# read histories sampled during MCMC
history <- read_history(paste0(data_path, "/history_thin_pieridae.txt"), burnin = 0)

# get samples at ages
ages <- c(80, 70, 0)
at_ages <- posterior_at_ages(history, ages, tree, host_tree)
samples_at_ages <- at_ages$samples

# get posterior probabilities of states at ages
pp_at_ages <- at_ages$post_states
```
