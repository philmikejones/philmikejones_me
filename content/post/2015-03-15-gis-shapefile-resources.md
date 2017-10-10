---
title: GIS shapefile resources
date: 2015-03-15
author: philmikejones
categories:
  - GIS
tags:
  - gis
  - openstreetmap
  - shapefile
---

## UK

UK shapefiles for various administrative geographies can be easily obtained from [UK Data Service Census Support boundary data pages](http://census.ukdataservice.ac.uk/get-data/boundary-data.aspx), and most use the permissive [Open Government License](http://census.edina.ac.uk/licenses.html).

## Countries

[DIVA-GIS](http://www.diva-gis.org/gdata) is a pretty good source for country shapefiles, including administrative boundaries, natural features, and infrastructure. Thanks to Tom B for pointing this one out.

[Geofabrik](http://download.geofabrik.de/) provide OpenStreetMap data extracts in a convenient format.

## Country-specific coordinate reference systems (projections)

When viewing a map of the world it's common to use the WGS84 (World Geodetic System 1984) coordinate reference system (CRS), although others can be used. The CRS includes the projection used to map the (nearly) spherical Earth on to two dimensions, but is not just the projection.

When looking at regions &#8211; like countries, or within countries &#8211; it is common to use a more specific CRS designed to represent that region accurately. For example, the further away from the equator a region is, the more distorted it will appear when projected using WGS84. In the UK, for example, it is common to use the British National Grid.

To find the CRS for a specific region or country you can therefore search the [EPSG coordinate system database](http://epsg.io/). Each CRS will have an EPSG code which can then be used in GIS software like QGIS. For example, the British National Grid is EPSG:27700.

## GIS software

No list of GIS resources would be complete without [QGIS](http://www.qgis.org/en/site/), which is a free and open source GIS package, comparable to ArcGIS ([and in my opinion, superior](https://philmikejones.wordpress.com/2014/05/16/qgis-thematic-mapping-open-source/)).