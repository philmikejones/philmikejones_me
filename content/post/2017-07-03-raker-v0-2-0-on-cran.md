---
title: rakeR v0.2.0 on CRAN
author: Phil Mike Jones
date: '2017-07-03'
slug: raker-v0-2-0-on-cran
categories: [r, code]
tags: [rakeR, spatial microsimulation, ipf, rstats]
---

I am absolutely delighted to announce that the latest version of [rakeR, version 0.2.0, is on CRAN](https://cran.r-project.org/package=rakeR).
You can install it in `R` or RStudio with:

```{r eval=FALSE}
install.packages("rakeR")
```

## DOI

![rakeR DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.821588.svg)
 
rakeR now has a DOI.
This is probably more useful for me than it is for you but nevertheless, if you use rakeR please be sure to cite it and use the DOI: [https://doi.org/10.5281/zenodo.821506](https://doi.org/10.5281/zenodo.821506)

## Changes and improvements

### Speed improvements in `integerise()`
The most noticeable change is that the `integerise()` step, which previously took hours on a reasonable--sized data set, now takes *minutes*.
This means it is now feasible to integerise, make corrections if necessary, and iterate to check additional parameters or model fit.
It achieves this by using the [`wrswoR`](https://cran.r-project.org/package=wrswoR) package for weighted random sampling without replacement, a step in the `truncate, replicate, sample` phase of the simulation.
So far I've only tested and implemented the `wrswoR::sample_int_crank()` function but [pull requests](https://github.com/philmikejones/rakeR/pulls) are very welcome.
I've used `sample_int_crank()` for now because, a) it provides results very similar to those provided by base R, which is what most users will expect, and b) it's suitably fast.
When I have more time I will test others.

### Simplified API
I've simplified the API.
First, the integerisation steps have been rationalised.
Previously to integerise the steps involved were `weight()`, `integerise()`, and `simulate()` to produce simulated cases.
I removed the `simulate()` step, and this is now all done with `weight()` then `integerise()`.

This:

* reduces the number of steps involved in the simulation process,
* makes the integerisation process consistent with the process to return fractional weights (`weight()` then `extract()`).

The results of the previous `weight()` then `integerise()` functions were rarely, if ever, needed before super--setting of cases, so there was no need to keep the additional step.
I have, however, kept the `weight()` stage because:

* the results of `weight()` are useful in their own right, for example for validation,
* the results of `weight()` can be cached, then used to `extract()` and `integerise()` without repeating the `weight()` step.

`simulate()` is therefore deprecated, and will return a warning if you try to use it.
It will be removed in the next release of `rakeR`.

The second change to the API is to the `rake()` function, which now returns either the extracted weights or the integerised weights, specified with `output` (fractional weights is the default so be careful if you're expecting this to return integerised weights, as it did previously).

### Bug fixes
I've made a number of bug fixes and, thanks to [Andrew Smith](https://github.com/philmikejones/rakeR/pull/45), a couple of behaviours are now rationalised.
See [NEWS.md](https://github.com/philmikejones/rakeR/blob/master/NEWS.md) to see what's changed.
