---
title: Installing RGDAL in R on Linux
date: 2014-07-14
author: philmikejones
categories:
  - Code
---

The RGDAL package is used by R and RStudio to plot maps. Under Linux you may encounter one or two errors when trying to install the package:

<pre class="brush: r; title: ; notranslate" title="">Error: gdal-config not found.
The gdal-config script distributed with GDAL could not be found.
</pre>

Or:

<pre class="brush: r; title: ; notranslate" title="">configure: error: proj_api.h not found in standard or given locations.
ERROR: configuration failed for package 'rgdal'
</pre>

You experience these errors because R in Linux installs the packages from source (rather than a ready-compiled binary) and you need additional libraries to compile RGDAL. Essentially, the packages <var>libgdal-dev</var> and <var>libproj-dev</var> are required and may be missing. To install them on an Ubuntu system open a terminal (CTRL+ALT+T) and type (or copy and paste):

<pre class="brush: r; title: ; notranslate" title="">sudo apt-get update && sudo apt-get install libgdal-dev libproj-dev
</pre>

To ensure you package lists are up to date and then installs the required packages. Once these are installed on your system you can install the RGDAL package by running the following code inside R:

<pre class="brush: r; title: ; notranslate" title="">install.packages("rgdal"); library(rgdal)
</pre>

Job done.

## Sources:

<http://stackoverflow.com/questions/12141422/error-gdal-config-not-found> <http://stackoverflow.com/questions/15248815/rgdal-package-installation>