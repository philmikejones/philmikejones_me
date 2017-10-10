---
title: rakeR v0.1.1 released on CRAN
date: 2016-09-19
author: philmikejones
categories:
  - Code
  - rstats
  - Works
tags:
  - CRAN
  - ipf
  - raking
  - rstats
  - spatial microsimulation
---

I'm proud to announce the [initial release of rakeR](https://cran.r-project.org/package=rakeR), v0.1.1, has been published on CRAN! It's licensed under the GPLv3 so you can use it for any projects you wish.

## Purpose

The goal behind rakeR is to make performing spatial microsimulation in R as easy as possible. R is a succinct and expressive language, but previously performing spatial microsimulation required multiple stages, including weighting, integerising, expanding, and subsetting. This doesn't even include testing inputs and outputs, and validation of the results. To make matters worse, each stage of the microsimulation required the input data to be in a slightly different format, adding to the workload of the analyst and the complexity of the task, introducing multiple opportunities for errors to creep in.

rakeR reduces this complexity, risk and time needed by:

- Performing the data re-formatting for each stage silently and automatically: no manual processing of data between stages.
- Accepting standardised arguments. The core functions accept either: two data frames and a character vector of variables to constrain over; or a table of weights.
- Robust error checking. The core functions are designed to be strict and not to try to correct any inputs. This means getting the inputs in the right format can sometimes be tricky, but because of this you can be confident in the results. There are also functions to help you check your inputs to make this as pain-free as possible.

## Installation

Install the stable version from CRAN:

<pre>i<span class="pl-c">nstall.packages("rakeR")</span></pre>

Alternatively install the development version with `devtools`:

<div class="highlight highlight-source-r">
  <pre><span class="pl-c"># Obtain devtools if you don't already have it installed</span>
<span class="pl-c"># install.packages("devtools")</span>

<span class="pl-c"># Install rakeR development version from GitHub</span>
<span class="pl-e">devtools</span><span class="pl-k">::</span>install_github(<span class="pl-s"><span class="pl-pds">"</span>philmikejones/rakeR<span class="pl-pds">"</span></span>)</pre>
</div>

Load the package with:

<div class="highlight highlight-source-r">
  <pre>library(<span class="pl-s"><span class="pl-pds">"</span>rakeR<span class="pl-pds">"</span></span>)
<span class="pl-c">#&gt; </span>
<span class="pl-c">#&gt; Attaching package: 'rakeR'</span>
<span class="pl-c">#&gt; The following object is masked from 'package:stats':</span>
<span class="pl-c">#&gt; </span>
<span class="pl-c">#&gt;     simulate</span></pre>
</div>

## Usage

To perform the raking you should supply two data frames, one with the constraint information with counts per category for each zone (e.g. census counts) and one with individual&#8211;level data (i.e. one row per individual). In addition supply a character vector with constraint variable names.

<div class="highlight highlight-source-r">
  <pre><span class="pl-smi">cons</span> <span class="pl-k">&lt;-</span> <span class="pl-k">data.frame</span>(
  <span class="pl-s"><span class="pl-pds">"</span>zone<span class="pl-pds">"</span></span>   <span class="pl-k">=</span> <span class="pl-c1">letters</span>[<span class="pl-c1">1</span><span class="pl-k">:</span><span class="pl-c1">3</span>],
  <span class="pl-s"><span class="pl-pds">"</span>a0_49<span class="pl-pds">"</span></span>  <span class="pl-k">=</span> c(<span class="pl-c1">8</span>, <span class="pl-c1">2</span>, <span class="pl-c1">7</span>),
  <span class="pl-s"><span class="pl-pds">"</span>a_gt50<span class="pl-pds">"</span></span> <span class="pl-k">=</span> c(<span class="pl-c1">4</span>, <span class="pl-c1">8</span>, <span class="pl-c1">4</span>),
  <span class="pl-s"><span class="pl-pds">"</span>f<span class="pl-pds">"</span></span>      <span class="pl-k">=</span> c(<span class="pl-c1">6</span>, <span class="pl-c1">6</span>, <span class="pl-c1">8</span>),
  <span class="pl-s"><span class="pl-pds">"</span>m<span class="pl-pds">"</span></span>      <span class="pl-k">=</span> c(<span class="pl-c1">6</span>, <span class="pl-c1">4</span>, <span class="pl-c1">3</span>)
)

<span class="pl-smi">inds</span> <span class="pl-k">&lt;-</span> <span class="pl-k">data.frame</span>(
  <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span>     <span class="pl-k">=</span> <span class="pl-c1">LETTERS</span>[<span class="pl-c1">1</span><span class="pl-k">:</span><span class="pl-c1">5</span>],
  <span class="pl-s"><span class="pl-pds">"</span>age<span class="pl-pds">"</span></span>    <span class="pl-k">=</span> c(<span class="pl-s"><span class="pl-pds">"</span>a_gt50<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>a_gt50<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>a0_49<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>a_gt50<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>a0_49<span class="pl-pds">"</span></span>),
  <span class="pl-s"><span class="pl-pds">"</span>sex<span class="pl-pds">"</span></span>    <span class="pl-k">=</span> c(<span class="pl-s"><span class="pl-pds">"</span>m<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>m<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>m<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>f<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>f<span class="pl-pds">"</span></span>),
  <span class="pl-s"><span class="pl-pds">"</span>income<span class="pl-pds">"</span></span> <span class="pl-k">=</span> c(<span class="pl-c1">2868</span>, <span class="pl-c1">2474</span>, <span class="pl-c1">2231</span>, <span class="pl-c1">3152</span>, <span class="pl-c1">2473</span>),
  <span class="pl-v">stringsAsFactors</span> <span class="pl-k">=</span> <span class="pl-c1">FALSE</span>
)

<span class="pl-smi">vars</span> <span class="pl-k">&lt;-</span> c(<span class="pl-s"><span class="pl-pds">"</span>age<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>sex<span class="pl-pds">"</span></span>)</pre>
</div>

- (Re-)weighting is done with `weight()` which returns a data frame of fractional weights.
- Integerisation is performed with `integerise()` which returns a data frame of integerised weights.
- `simulate()` takes care of creating the final microsimulated data and returns a data frame of simulated cases in zones.

These functions can be combined with pipes:

<div class="highlight highlight-source-r">
  <pre><span class="pl-c"># obtain magrittr if not already installed</span>
<span class="pl-c"># install.packages("magrittr")</span>
library(<span class="pl-s"><span class="pl-pds">"</span>magrittr<span class="pl-pds">"</span></span>)

<span class="pl-smi">sim_df</span> <span class="pl-k">&lt;-</span> weight(<span class="pl-smi">cons</span>, <span class="pl-smi">inds</span>, <span class="pl-smi">vars</span>) %<span class="pl-k">&gt;</span>% integerise() %<span class="pl-k">&gt;</span>% simulate(<span class="pl-v">inds</span> <span class="pl-k">=</span> <span class="pl-smi">inds</span>)
head(<span class="pl-smi">sim_df</span>)
<span class="pl-c">#&gt;     id    age sex income zone</span>
<span class="pl-c">#&gt; 1    A a_gt50   m   2868    a</span>
<span class="pl-c">#&gt; 2    B a_gt50   m   2474    a</span>
<span class="pl-c">#&gt; 3    C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.1  C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.2  C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.3  C  a0_49   m   2231    a</span></pre>
</div>

Alternatively use the `rake()` function, which is a wrapper for `weight() %>% integerise() %>% simulate()`:

<div class="highlight highlight-source-r">
  <pre><span class="pl-smi">sim_df</span> <span class="pl-k">&lt;-</span> rake(<span class="pl-smi">cons</span>, <span class="pl-smi">inds</span>, <span class="pl-smi">vars</span>)
head(<span class="pl-smi">sim_df</span>)
<span class="pl-c">#&gt;     id    age sex income zone</span>
<span class="pl-c">#&gt; 1    A a_gt50   m   2868    a</span>
<span class="pl-c">#&gt; 2    B a_gt50   m   2474    a</span>
<span class="pl-c">#&gt; 3    C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.1  C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.2  C  a0_49   m   2231    a</span>
<span class="pl-c">#&gt; 3.3  C  a0_49   m   2231    a</span></pre>
</div>

## Contributing

All software is a work in progress, and rakeR is no exception. Feedback, comments, and suggestions are very welcome, as are [bug/issue reports](https://github.com/philmikejones/rakeR/issues), and pull requests.

Please note that this project is released with a [Contributor Code of Conduct](https://github.com/philmikejones/rakeR/blob/master/CONDUCT.md). By participating in this project you agree to abide by its terms.

## Acknowledgements

Many of the functions in this package are based on code written by [Robin Lovelace](https://github.com/Robinlovelace) and [Morgane Dumont](https://github.com/modumont) for their book [_Spatial Microsimulation with R_ (2016), Chapman and Hall/CRC Press](https://www.crcpress.com/Spatial-Microsimulation-with-R/Lovelace-Dumont/p/book/9781498711548), licensed under the terms below:

Copyright (c) 2014 Robin Lovelace

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the &#8220;Software&#8221;), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED &#8220;AS IS&#8221;, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Their book is also an excellent resource for learning about spatial microsimulation and understanding what's going on under the hood of this package.

The rewighting (ipfp) algorithm itself is [written by Andrew Blocker](https://github.com/awblocker/ipfp) and is written in `C` for maximum speed and efficiency.

Thanks to [Tom Broomhead](http://mhs.group.shef.ac.uk/members/tom-broomhead/) for his feedback on error handling and suggestions on function naming.