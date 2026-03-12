# Posterior distribution of network structure indices across ancestral networks

Calculate z-scores for nestedness (NODF) or modularity (Q) for each MCMC
sample at time points in the past based on null networks where all
interactions have the same probability. By calculating z-scores, we can
compare ancestral networks at different ages.

## Usage

``` r
index_at_ages_samples(
  sampled_networks,
  index,
  ages = NULL,
  nnull = 100,
  use_future = FALSE
)
```

## Arguments

- sampled_networks:

  List of ancestral networks sampled across MCMC at given ages. Usually
  from the output of `get_sampled_networks`, see example.

- index:

  Index to be calculated for each ancestral network. "NODF" to calculate
  nestedness or "Q" to calculate modularity.

- ages:

  Vector of ages (time points in the past) of ancestral networks. By
  default, uses all ages present in `sampled_networks`.

- nnull:

  Number of null networks to generate to calculate the z-score. Default
  is 100.

- use_future:

  Parallelize with package `future`? Logical. Only applicable to
  modularity calculation.

## Value

A data.frame of z-scores and p-values across samples and ages.

## Examples

``` r
# read data that comes with the package
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path,"/tree_pieridae.tre"))
host_tree <- ape::read.tree(paste0(data_path,"/host_tree_pieridae.phy"))
history <- read_history(paste0(data_path,"/history_thin_pieridae.txt"), burnin = 0)

# get sampled networks at ages in the past
ages <- c(60,50,40,0)
samples_at_ages <- posterior_at_ages(history, ages, tree, host_tree)
sampled_networks <- get_sampled_networks(samples_at_ages)

# calculate posterior distribution of nestedness
Nz <- index_at_ages_samples(sampled_networks, index = "NODF")

#  calculate posterior distribution of modularity with parallelization (slower)
# Qz <- index_at_ages_samples(sampled_networks, index = "Q", use_future = TRUE)
```
