---
title: Dissolve polygons in R
date: 2015-09-03
author: philmikejones
categories:
  - GIS
  - rstats
tags:
  - dissolve
  - gis
  - polygon
  - r
---

Dissolving polygons is another fairly elementary GIS task that I need to perform regularly. With R this is can be a bit involved, but once done is fully reproducible and the code can be re-used. This post is essentially a companion piece to [Clipping polygons in R](https://philmikejones.wordpress.com/2015/09/01/clipping-polygons-in-r/); I wrote both because I often forget how to complete these tasks in R.

## Getting started

Let's gather together everything we need to complete this example. We need a shapefile of small geographies to &#8216;dissolve', a lookup table to tell us which polygons dissolve into which, and we need a couple of R spatial packages to run everything. Let's get started.

<pre># The default behaviour of this script is to create a folder called 'dissolve-example'
# and download and run everything from here.
# You can change this by modifying the next two lines
dir.create("dissolve-example")
setwd("dissolve-example")

# Load a few packages. dplyr makes merges easier
require("rgdal")
require("rgeos")
require("dplyr")

# Set up shapefile to dissolve. I'm using English regions
download.file("http://census.edina.ac.uk/ukborders/easy_download/prebuilt/shape/England_gor_2011.zip",
              destfile = "lad-region-lookup.zip")
unzip("lad-region-lookup.zip", exdir = ".")
region &lt;- readOGR(".", "England_gor_2011")

# Check the shapefile has loaded correctly
plot(region)</pre><figure id="attachment_1725" class="thumbnail wp-caption aligncenter" style="width: 610px">

<img class="size-full wp-image-1725" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/09/region.png?fit=600%2C454" alt="Regions" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/09/region.png?w=600 600w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/09/region.png?resize=300%2C227 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" /><figcaption class="caption wp-caption-text">Regions</figcaption></figure> 

<pre># We're going to dissolve all regions in to one country (England!)
# For this we'll create a lookup table and merge with the spatial data
# Hopefully for your 'real' data you have a lookup table of all polygons and
# their larger geography already!
lu &lt;- data.frame()
lu &lt;- rbind(lu, region@data)
lu$CODE &lt;- as.character(lu$CODE)
lu$NAME &lt;- as.character(lu$NAME)
lu$country &lt;- NA
lu$country &lt;- "England"</pre>

## Merge

We now need to merge the lookup table into our spatial object data frame. We should end up with one row per zone to dissolve, each with a reference for the relevant larger geography. I think the trick is to make sure the row names match exactly, and if you can match the polygon IDs as well with <tt>spChFIDs()</tt>.

<pre># Merge lu (LookUp) into polygons,
region@data$CODE &lt;- as.character(region@data$CODE)
region@data &lt;- full_join(region@data, lu, by = "CODE")

# Tidy merged data
region@data &lt;- select(region@data, -NAME.x)
colnames(region@data) &lt;- c("code", "name", "country")

# Ensure shapefile row.names and polygon IDs are sensible
row.names(region) &lt;- row.names(region@data)
region &lt;- spChFIDs(region, row.names(region))</pre>

## Dissolve

Now we can do the dissolve. I use <tt>gUnaryUnion</tt> (and indeed I think <tt>unionSpatialPolygons</tt> in the maptools package uses this by default).

<pre># Now the dissolve
region &lt;- gUnaryUnion(region, id = region@data$country)</pre>

If you want to just plot this using base plot you can stop there. If you want to do anything with the data or plot using ggplot you need to recreate the data frame.

<pre># If you want to recreate an object with a data frame
# make sure row names match
row.names(region) &lt;- as.character(1:length(region))

# Extract the data you want (the larger geography)
lu &lt;- unique(lu$country)
lu &lt;- as.data.frame(lu)
colnames(lu) &lt;- "country"  # your data will probably have more than 1 row!

# And add the data back in
region &lt;- SpatialPolygonsDataFrame(region, lu)

# Check it's all worked
plot(region)</pre>

Your plot should look like this:<figure id="attachment_1722" class="thumbnail wp-caption aligncenter" style="width: 610px">

<img class="size-full wp-image-1722" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/09/dissolve-example.png?fit=600%2C454" alt="Dissolved polygons" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/09/dissolve-example.png?w=600 600w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/09/dissolve-example.png?resize=300%2C227 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" /><figcaption class="caption wp-caption-text">Example dissolved polygons</figcaption></figure> 

And your data frame should look like this:

<pre>region@data
##   country
## 1 England</pre>