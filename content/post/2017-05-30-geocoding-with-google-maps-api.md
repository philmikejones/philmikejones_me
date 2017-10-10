---
title: Geocoding with Google Maps API
author: ~
date: '2017-05-30'
slug: geocoding-with-google-maps-api
categories: []
tags: []
---

You need to build a URL to query the Google Places API, one URL per place. Judging by the Places API guide you need to:

 1. [Get an API key](https://developers.google.com/places/web-service/get-api-key)
 2. Obtain a `placeid` from a places search, then
 3. Use this `placeid` to get information from the Place Details API.

The base URL is:

    https://maps.googleapis.com/maps/api/place/nearbysearch/output?parameters

`JSON` is the recommended output format, and we need to specify the following [parameters](https://developers.google.com/places/web-service/search):

 1. `key`: your API key
 2. `location`: lat/long (NOT long/lat!) coordinates of the centre of
    your search area
 3. `radius`: the radius to search in metres
 4. `keyword` or `name`: keywords or name of the place to search

So build this up in R:

    places_key = "Your key goes here"
    url = paste0("https://maps.googleapis.com/maps/api/place/",
                 "nearbysearch/json?key=", places_key,
                 "&location=41.699042,-72.864847",
                 "&radius=5000",  # max = 50,000
                 "&name=ebm-papst")

Query the URL with

    install.packages("jsonlite")  # if not already installed
    result <- jsonlite::fromJSON(url)

The `placeid`(s) is/are then in `result$results$placeid`.

Plug this `placeid` into a Google Places Details API query:

    details_id  <- result$results$placeid

If there is more than one `placeid` you can specify which one you want with `result$results$placeid[1]`, for example for the first `placeid`

    details_url <- paste0("https://maps.googleapis.com/maps/api/place/",
                          "details/json?",
                          "key=", places_key,
                          "&placeid=", details_id)

    details <- jsonlite::fromJSON(details_url)
