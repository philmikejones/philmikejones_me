---
title: Layout figures for comparison
author: Phil Mike Jones
date: '2017-05-19'
slug: layout-figures-review
categories: [python, code]
tags: [python, pillow, visualisation, image-manipulation]
---

I recently had to review figures from nearly 50 countries for a project I'm working on.
Each country had three figures that needed comparing.
Anyone who knows me will know that I had had enough after loading figures for just the first few countries.
Apart from being tedious it was also error--prone; double--click the wrong file by mistake and it's not immediately obvious you've got the wrong figure.

Instead of doing it manually and risking making mistakes I wrote the following small python script using the `pillow` library.
The script creates a blank canvas, then loads the images, places them together on a blank canvas, and saves the output for review.
My images were called `mort_ABC.png`, which was a Lexis surface plot which fills the top half of each image (approx. 420mm x 148mm).
The `cohort_ABC.png` images are HAPC plots for females and males, which each take up a space about A5 in size.
I placed these together in the bottom half of the canvas.

Anyway, here's the code:

```{python, eval=FALSE, include=TRUE}
## Pastes Lexis surface diagrams and HAPC plots together

import os
import glob
from subprocess import call
from PIL import Image, ImageDraw, ImageFont

# Get country code list
countries = glob.glob("mort_*.png")
countries = sorted(countries)

## http://stackoverflow.com/questions/3136689/find-and-replace-string-values-in-python-list
## Get the country codes
countries = [countries.replace("mort_", "") for countries in countries]
countries = [countries.replace(".png", "") for countries in countries]

# Set output canvas size
dpi = 300
width  = int((42.0 / 2.54) * dpi)
height = int((29.7 / 2.54) * dpi)

for i in countries:
    # Create blank canvas
    canvas = Image.new("RGBA", (width, height), color = (255, 255, 255))
    
    # Open Lexis surface plot, trim whitespace, paste into canvas
    lexis = Image.open("mort_" + i + ".png")
    canvas.paste(lexis)
    
    # Lexis plots place females on left; males on right
    # Copy this layout for HAPC plots
    
    # Paste in HAPC female plot
    pastex = 0
    pastey = int(height / 2)
    hapc_female = Image.open("cohort_" + i + "_female.png")
    canvas.paste(hapc_female, box = (pastex, pastey))
    
    # Paste in HAPC male plot
    pastex = int(width / 2)
    hapc_male = Image.open("cohort_" + i + "_male.png")
    canvas.paste(hapc_male, box = (pastex, pastey))
    
    # Add annotations
    draw = ImageDraw.Draw(canvas)
    font = ImageFont.truetype("FreeMono.ttf", 100)
    draw.text((20, 20), "Country: " + i, 
    fill = (0, 0, 0, 255), font = font)
    
    # Save
    filename = "country_" + i + ".png"
    canvas.save(filename)

# Needs a load of memory
call("./convert_multipage_pdf.sh")
```

The final `call()` calls a simple `bash` shell file which combines the individual single--page images into one mutliple--page pdf so I can print double--sided.

```{bash, eval=FALSE}
#! /bin/bash

countries=$(find . -name "country_*.png" | sort)
convert $countries countries.pdf
```
