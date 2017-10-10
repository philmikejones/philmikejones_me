---
title: Creating a globe in QGIS
date: 2016-07-14
author: philmikejones
categories:
  - Code
  - GIS
tags:
  - cartography
  - gis
  - globe
  - projection
  - QGIS
  - world
---

I love a good bit of map making and I have a bit of time on my hands at the moment, so I followed this tutorial by [Steven Bernard](https://www.youtube.com/channel/UCrBM8Ka8HhDAYvQY1VX2P0w) to create a globe from a world map in QGIS:



The steps are straightforward. The fiddly bit was getting the line endings and indentation correct which are essential in Python, so I copied the text out and created a gist with line endings preserved:



This can then be called by opening the Python console as per the video, and typing:

    import globe_projection_processing_qgis.py as circle
    circle.doClip(iface, x, y)

Replacing `x` and `y` with your latitude and longitude (NOT longitude and latitude, note the order) respectively.

The result is a beautiful globe when appropriately styled:<figure id="attachment_1945" class="thumbnail wp-caption aligncenter" style="width: 656px">

[<img src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?fit=646%2C646" alt="Globe" class="size-full wp-image-1945" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?w=942 942w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?resize=150%2C150 150w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?resize=300%2C300 300w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?resize=768%2C768 768w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png?resize=60%2C60 60w" sizes="(max-width: 646px) 100vw, 646px" data-recalc-dims="1" />](https://i0.wp.com/philmikejones.me/wp-content/uploads/2016/07/globe_square.png)<figcaption class="caption wp-caption-text">Globe</figcaption></figure>