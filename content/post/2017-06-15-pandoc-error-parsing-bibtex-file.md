---
title: Pandoc error parsing BibTeX file
author: Phil Mike Jones
date: '2017-06-15'
slug: pandoc-error-parsing-bibtex-file
categories: [code]
tags: [code, latex, pandoc]
---

I get this error so often (and I always forget how to solve it) that I thought I'd post a solution.
Here's the error:

```
pandoc-citeproc: "stdin" (line 2421, column 2):
unexpected "m"
expecting "c", "C", "p", "P", "s" or "S"
pandoc: Error running filter /usr/lib/rstudio/bin/pandoc/pandoc-citeproc
Filter returned error status 1
Error: pandoc document conversion failed with error 83
```

The problem is that there's an entry in my bibliography BibTeX file without a trailing comma:

```
@article{
  author = {Somebody}
  year   = {Somewhen}
}
```

Fixing the error is just a matter of putting the comma in:

```
@article{
  author = {Somebody},
  year   = {Somewhen}
}
```
