# Get posterior samples of networks of interactions of extant lineages at given time points in the past

Get posterior samples of networks of interactions of extant lineages at
given time points in the past

## Usage

``` r
get_sampled_networks(at_ages, state = 2, ages = NULL)
```

## Arguments

- at_ages:

  List of lists, with samples and posterior probabilities for each
  interaction of extant lineages at given ages. Usually calculated
  `posterior_at_ages`, see example.

- state:

  Which state? Default is 2. For analyses using the 3-state model,
  choose `1`, `2` or both using `c(1, 2)` (where 1 is a potential host
  and 2 an actual host). Note that this is also applied to the extant
  network.

- ages:

  Vector of ages (time points in the past) at which samples were
  retrieved. By default, uses all ages present in `pp_at_ages`.

## Value

A list of arrays, one for each age. Arrays contain sampled networks.

## Examples

``` r
# read data that comes with the package
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path,"/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path,"/host_tree_pieridae.phy"))
history <- read_history(paste0(data_path,"/history_thin_pieridae.txt"), burnin = 0)

# choose ages
ages <- c(60, 50, 40, 0)

# calculate posterior probability of interactions
at_ages <- posterior_at_ages(history, ages, tree, host_tree)

# get sampled networks
sampled_nets <- get_sampled_networks(at_ages)
```
