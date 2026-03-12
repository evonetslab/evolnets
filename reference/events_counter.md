# Calculate the rate of host-repertoire evolution

Calculate the number of host gains, host losses, and the effective rate
of host repertoire evolution.

## Usage

``` r
count_events(history)

effective_rate(history, tree)

count_gl(history)

rate_gl(history, tree)
```

## Arguments

- history:

  A data frame containing the character history produced by RevBayes and
  read by
  [`read_history()`](https://maribraga.github.io/evolnets/reference/read_history.md).

- tree:

  A phylogenetic tree of the symbiont clade

## Functions

- `count_events()`: Get the average number of events along the symbiont
  tree and the highest posterior density interval with 95% probability
  (HPD95), based on all MCMC iterations in `history`.

- `effective_rate()`: Get the effective rate of evolution, i.e. number
  of events per branch unit, along each tree branch. Mean and HP95 are
  outputted.

- `count_gl()`: Get the average number of host gains and host losses

- `rate_gl()`: Get the average effective rate of host gain and host loss

## Examples

``` r
# read data that comes with the package
data_path <- system.file("extdata", package = "evolnets")
tree <- read_tree_from_revbayes(paste0(data_path, "/tree_pieridae.tre"))
history <- read_history(paste0(data_path, "/history_thin_pieridae.txt"), burnin = 0)

# all events
n_events <- count_events(history)
rate <- effective_rate(history, tree)

# gains and losses separately
gl_events <- count_gl(history)
gl_rates <- rate_gl(history, tree)
```
