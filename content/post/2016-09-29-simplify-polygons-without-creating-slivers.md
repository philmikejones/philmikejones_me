---
title: Simplify polygons without creating slivers
date: 2016-09-29
author: philmikejones
categories:
  - Code
  - GIS
  - rstats
tags:
  - geometry
  - gis
  - polygons
  - simplify
---

When simplifying polygons it's almost inevitable that you will generate some sliver polygons or gaps between the correct polygons. For example, the following image shows two adjoining complex polygons, representing two adjoining administrative areas. Note there are no gaps between the polygons; they are contiguous (the border is between Sheffield and Barnsley LADs, by the way).<figure id="attachment_1996" class="thumbnail wp-caption aligncenter" style="width: 658px">

[<img class="wp-image-1996 size-large" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified-1024x639.png?fit=648%2C404" alt="Unsimplified polygons" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png?resize=1024%2C639 1024w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png?resize=300%2C187 300w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png?resize=768%2C479 768w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png?w=1509 1509w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png?w=1296 1296w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" />](https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_unsimplified.png)<figcaption class="caption wp-caption-text">Original geometries without simplification</figcaption></figure> 

Now if we simplify these polygons to reduce their complexity using simplify geometries in QGIS, gaps appear between the original two polygons and they are no longer contiguous.<figure id="attachment_1997" class="thumbnail wp-caption aligncenter" style="width: 658px">

[<img class="wp-image-1997 size-large" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis-1024x639.png?fit=648%2C404" alt="Polygons simplified with QGIS with sliters visible" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png?resize=1024%2C639 1024w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png?resize=300%2C187 300w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png?resize=768%2C479 768w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png?w=1509 1509w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png?w=1296 1296w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" />](https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_qgis.png)<figcaption class="caption wp-caption-text">Geometries simplified with QGIS simplify geometries command</figcaption></figure> 

If you're just plotting a basic, low resolution thematic map this isn't necessarily a problem, but it becomes problematic when you try to use these polygons with other data or use the polygons for clipping. There are solutions but correcting them can be a pain, and don't always work as intended. But why correct them; why not simplify without creating sliver polygons in the first place? If you're an R user the `ms_simplify()` function in the `rmapshaper` package allows you to do exactly that.<figure id="attachment_2000" class="thumbnail wp-caption aligncenter" style="width: 658px">

[<img class="wp-image-2000 size-large" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper-1024x639.png?fit=648%2C404" alt="Polygons simplified with rmapshaper" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png?resize=1024%2C639 1024w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png?resize=300%2C187 300w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png?resize=768%2C479 768w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png?w=1509 1509w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png?w=1296 1296w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" />](https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/09/polygons_simplified_rmapshaper.png)<figcaption class="caption wp-caption-text">Simplified geometries using rmapshaper</figcaption></figure> 

QGIS's simplify geometries and rmapshaper::ms_simplify() use different arguments for thresholds, so I've matched the level of simplification as best I can to ensure a fair test. The QGIS simplified shapefile is 6.6MB, while the rmapshaper simplified shapefile is 5.7MB (so slightly smaller and still without errors introduced).

To use `rmapshaper::ms_simplify()` just install and load the library and run it on a `spatialPolygons*` object:

    install.packages("rmapshaper")
    
    library("rmapshaper")
    
    simplified_shape <- ms_simplify(unsimplified_shape)
