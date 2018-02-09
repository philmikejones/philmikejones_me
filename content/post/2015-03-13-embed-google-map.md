---
title: Embed a Google Map
date: 2015-03-13
author: philmikejones
categories:
  - Code
  - GIS
tags:
  - API
  - Embed
  - Google
  - Map
---

It's actually quite straightforward to embed a customised Google Map in a website. Here I'll deal with embedding in Google Sites for the benefit of the GEO358 class, but the process is pretty similar for WordPress.

## Basic embedding

The most straightforward way to embed a simple map in a Google Sites page is to open the page in edit mode, press Insert, and select Map from the list of Google products. This method isn't very flexible though, so I recommend a slightly different method.

A better and more flexible way is to use [Google Maps](https://www.google.co.uk/maps/) itself:

  1. Enter your location or directions of interest as normal.
  2. Press &#8216;Settings' (the cog icon).
  3. Press &#8216;Share or embed map'
  4. Press the &#8216;Embed map' tab.<figure id="attachment_1558" class="thumbnail wp-caption aligncenter" style="width: 310px">

[<img class="size-medium wp-image-1558" src="https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed-300x209.png?fit=300%2C209" alt="Embed Google Map" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed.png?w=913 913w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed.png?resize=300%2C209 300w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed.png?resize=768%2C535 768w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed.png?resize=660%2C460 660w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />](https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/03/simple-embed.png)<figcaption class="caption wp-caption-text">Simple method to embed Google Map</figcaption></figure> 

You can then choose a size for the map (medium by default). When you have the map the right size for your needs, copy the provided code (Ctrl+C, or ⌘+C on a Mac) to your clipboard. At this point open your Google Sites (or WordPress) page in edit mode, and edit the html source. In Google Sites, this is the final icon in the toolbar:<figure id="attachment_1562" class="thumbnail wp-caption aligncenter" style="width: 123px">

<img class="size-full wp-image-1562" src="https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/03/edit-html-source.png?fit=113%2C76" alt="Edit html source" data-recalc-dims="1" /><figcaption class="caption wp-caption-text">Edit HTML source icon</figcaption></figure> 

In WordPress, you should press the &#8216;HTML' or &#8216;Text' tab (top right, next to &#8216;Visual'):<figure id="attachment_1563" class="thumbnail wp-caption aligncenter" style="width: 359px">

<img class="size-full wp-image-1563" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/03/wp-html-tab.png?fit=349%2C107" alt="HTML tab" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/03/wp-html-tab.png?w=349 349w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/03/wp-html-tab.png?resize=300%2C92 300w" sizes="(max-width: 349px) 100vw, 349px" data-recalc-dims="1" /><figcaption class="caption wp-caption-text">WordPress HTML tab</figcaption></figure> 

Then, simply paste the code where you want the map to be displayed. The easiest way to do this is to find the paragraph immediately before where you want the map placed, and paste the map code immediately after the 

tag (on a new line is fine). In WordPress the html mode doesn't use p tags, so you can simply paste the map code after the paragraph. The resulting map is interactive, so give it a go.

<div class="googlemaps">
</div>

You can also use this for directions, instead of a single point:

<div class="googlemaps">
</div>

## Google Maps Embed API and JavaScript API

The [Google Maps Embed API](https://developers.google.com/maps/documentation/embed/guide) is an alternative way to embed a standard map in a webpage and can be used on a WordPress or Google Sites page. The [Google Maps JavaScript API](https://developers.google.com/maps/documentation/javascript/tutorial) allows even finer control (for example using [custom markers](https://developers.google.com/maps/documentation/javascript/examples/marker-symbol-custom)), but you need a self-hosted website ([WordPress will not implement the JavaScript API at all](https://en.support.wordpress.com/code/#javascript)) and a bit of knowledge of JavaScript to use it.

I don't intend to go in to massive amounts of detail in this post about how to use these APIs &#8211; ask me about it if you want to know more, and the documentation is pretty comprehensive. To use either API you will need an API key. The documentation is slightly out of date (as of March 2015), but the basic steps are the same:

  1. Open and log in to the [Google Developer's Console](https://console.developers.google.com/project)
  2. Create a new project
  3. Give your project a meaningful name and id (maybe your student number?)
  4. I suggest opening the advanced options and selecting the EU data centre. This will probably only have a negligible effect, but could improve performance when accessing from the EU.
  5. From your project's dashboard, select **APIs & auth** then **APIs**
  6. Under **Browse APIs**, search for &#8216;maps'
  7. Enable either the Google Maps Embed API or Google Maps JavaScript API v3 (press the OFF button under status to toggle to on). When activated, the APIs will be listed at the top of this page under **Enabled APIs**
  8. Now go to the **Credentials** page under **APIs and auth**.
  9. Create a new key under **Public API access** (NOT OAuth)
 10. Choose a **browser key**
 11. You only want your website to be able to use this key so it isn't abused, so you will need to enter a domain in the **<span class="p6n-form-label ng-scope ng-isolate-scope"><span class="ng-scope">Accept requests from these HTTP referers (web sites)</span></span>** box. This will depend on if you're using WordPress or Google Sites. 
      1. If you're using WordPress your website will be something like: https://mysite.wordpress.com. Enter this as **mysite.wordpress.com**; do not include the http:// or https:// because this will change.
      2. If you're using Google Sites, the format is a bit different and will depend on whether you've created your site using your Sheffield university credentials or a personal email address. Assuming you've used your Sheffield university details, your website will be something like: https://sites.google.com/a/sheffield.ac.uk/mysite/. If that's the case enter **sites.google.com/a/sheffield.ac.uk/mysite/**, again excluding the http(s)://.
 12. You will have a new key which you can copy and paste to use in your embedded maps, like the example below:

<div class="googlemaps">
</div>
