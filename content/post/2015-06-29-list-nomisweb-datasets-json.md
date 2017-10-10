---
title: List Nomisweb Datasets with JSON
date: 2015-06-29
author: philmikejones
categories:
  - Code
tags:
  - API
  - curl
  - jq
  - json
  - nomisweb
---

The [Nomisweb API](https://www.nomisweb.co.uk/api/v01/help) can be used both to discover (list) datasets, and to obtain one or more datasets once these have been identified.

The API supports a variety of formats including html, xml and [JSON](https://en.wikipedia.org/wiki/JSON). I find the JSON preferable because it's less verbose than xml so typically is a smaller file.

To list all the available datasets I used a programme called <tt>jq</tt> (&#8216;Json Query' I assume). At the time of writing (June 2015) I strongly recommend you install the development version, rather than the existing binary versions, because the manual and tutorial oddly refer to filters and commands that are not yet available in the official released version. [Instructions to install the development version from git](http://stedolan.github.io/jq/download/) are available or download a pre-compiled binary from the drop down box on the homepage.

You will also need <tt>curl</tt> which on a Ubuntu machine is as easy as:

<pre class="brush: bash; title: ; notranslate" title="">sudo apt-get install curl
</pre>

I then used curl and jq to obtain the list of datasets and filter out everything, keeping only the ID, name, and description to easily find relevant datasets. The following script does this and saves the output to <tt>nomisweb-datasets.txt</tt>:

<div class="gist-oembed" data-gist="99580cdc638611c0060b.json">
</div>

- Line 1 specifies the relevant json file listing all the datasets, specified in the API documentation.
- Line 2 is a series of filters piped together. It essentially obtains everything; then filters out everything but <tt>keyfamilies</tt> at that level; then filters everything but <tt>keyfamily</tt> (it just so happens there's nothing to filter at that level); then obtains all datasets (&#8216;<tt>.[]</tt>&#8216;); before finally extracting the id, name, and description from each index.
- Line 3 saves this to the file rather than print it to the terminal window as is the default.