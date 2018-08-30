---
title: "Pandoc error parsing BibTeX file"
author: "Phil Mike Jones"
date: 2017-06-15
categories: ["tutorials"]
tags: ["latex", "bibtex", "pandoc"]
---

I get the following error so often (and I always forget how to solve it) that I thought I'd post a solution.

```latex
pandoc-citeproc: "stdin" (line 2421, column 2):
unexpected "m"
expecting "c", "C", "p", "P", "s" or "S"
pandoc: Error running filter /usr/lib/rstudio/bin/pandoc/pandoc-citeproc
Filter returned error status 1
Error: pandoc document conversion failed with error 83
```

<!--more-->

The problem is that there's an entry in my bibliography BibTeX file without a trailing comma:

```bibtex
@article{
  author = {Somebody}
  year   = {Somewhen}
}
```

Fixing the error is just a matter of putting the comma in:

```bibtex
@article{
  author = {Somebody},
  year   = {Somewhen}
}
```
