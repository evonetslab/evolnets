# Read symbiont tree file produced by RevBayes containing node indices

Read symbiont tree file produced by RevBayes containing node indices

## Usage

``` r
read_tree_from_revbayes(path_to_tree)
```

## Arguments

- path_to_tree:

  String path to the .txt file exported from RevBayes

## Value

A `phylo` object with node names given by RevBayes, which are important
to place the inferred ancestral states in the symbiont tree.

## Examples

``` r
if (FALSE) { # \dontrun{
tree <- read_tree_from_revbayes("symbiont_tree.tre")
} # }
```
