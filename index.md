# evolnets

RevBayes and TreePPL offer models to infer host repertoire evolution,
but no tools to parse the outputs. *evolnets* has the necessary tools to
reconstruct ancestral ecological networks based on posterior
probabilities of interactions.

## Installation

You can install evolnets like so:

``` r
if(!require("devtools", quietly = TRUE)) {
  install.packages("devtools")
  library(devtools)
} else {
 library(devtools)
}

devtools::install_github("evonetslab/evolnets")
```

## About

The evolnets package provides three categories of important functions:
rates, ancestral states and samples.

- Rates: these functions are used to calculate effective rates of
  host-repertoire evolution:
  [`effective_rate( )`](https://evonetslab.github.io/evolnets/reference/events_counter.md),
  [`count_events( )`](https://evonetslab.github.io/evolnets/reference/events_counter.md),
  [`rate_gl( )`](https://evonetslab.github.io/evolnets/reference/events_counter.md),
  [`count_gl( )`](https://evonetslab.github.io/evolnets/reference/events_counter.md).

- Ancestral states: these functions are used to calculate the posterior
  probabilities of host-parasite interactions at internal nodes of the
  parasite tree or at specific time points in the past:
  [`posterior_at_nodes( )`](https://evonetslab.github.io/evolnets/reference/posterior_at_nodes.md),
  [`posterior_at_ages( )`](https://evonetslab.github.io/evolnets/reference/posterior_at_ages.md).

- Samples: these functions perform calculations for each sampled
  host-parasite network during MCMC: `samples_at_ages( )`,
  `Q_posterior_at_ages( )`, `NODF_posterior_at_ages( )`.

See the full documentation at the [evolnets’
website](https://evonetslab.github.io/evolnets/).
