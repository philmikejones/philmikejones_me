---
title: Downloading ONS geography lookups
date: 2015-12-21
author: philmikejones
categories:
  - GIS
tags:
  - curl
  - ons geoportal
---

I wasn't able to easily download ONS output area lookups from either their main site or the [geoportal](https://geoportal.statistics.gov.uk/geoportal/catalog/main/home.page). I kept getting errors that the download failed. I suspect on Linux the URLs are considered malformed; they might work on Windows.

Anyway, on Linux use links from the geoportal. They directly link to the .zip files (and the main site links to the geoportal, anyway).

I used cURL on the command line and escaped the brackets in the URL with :

<pre>curl -o ~/Downloads/oa-lookup.zip https://geoportal.statistics.gov.uk/Docs/Lookups/Output_areas_(2011)_to_lower_layer_super_output_areas_(2011)_to_middle_layer_super_output_areas_(2011)_to_local_authority_districts_(2011)_E+W_lookup.zip</pre>

Which worked a treat.