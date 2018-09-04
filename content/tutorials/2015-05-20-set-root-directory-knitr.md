---
title: "Set root directory for knitr"
date: 2015-05-20
author: "Phil Mike Jones"
categories: ["tutorials"]
tags: ["knitr", "rstudio", "rstats", "R markdown"]
---

Knitr, by default, looks in the same directory as your `.Rmd` file to find any files you need to draw in, like data sets or script files. This proved to be a pain for me because I keep all my `.R` and `.Rmd` files in a `scripts/` folder and data files in a separate folder. You cannot use setwd() with knitr, so the canonical way to do this is to include an initial code chunk:

<pre class="brush: r; title: ; notranslate" title="">```{r "setup", include=FALSE}
require("knitr")
opts_knit$set(root.dir = "~/gits/project/")
```
</pre>

This creates an R chunk called `setup` which isn't included in the knitted file. Knitr package is loaded, and `root.dir` is set to my the `gits/project/` folder in my user area (&#8216;`~/`&#8216;). Knitr will now look for all files from this root folder rather than the folder it is stored in.
