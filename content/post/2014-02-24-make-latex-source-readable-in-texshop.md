---
title: Make LaTeX source readable in TeXShop
date: 2014-02-24
author: philmikejones
categories:
  - Code
---

[TeXShop](http://pages.uoregon.edu/koch/texshop/texshop.html) for the Mac is my source editor of choice for LaTeX files because it comes with the [MacTex](http://tug.org/mactex/) binary and can compile your document straight from the editor. With a dark background though &#8211; as I prefer when writing source files &#8211; the default colours for syntax highlighting are woefully unreadable because they're designed for a lighter background.<figure id="attachment_1016" class="thumbnail wp-caption aligncenter" style="width: 759px">

[<img class="size-full wp-image-1016" src="https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-not-optimised.png?fit=648%2C294" alt="TeX source unoptimised" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-not-optimised.png?w=749 749w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-not-optimised.png?resize=300%2C136 300w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-not-optimised.png?resize=660%2C300 660w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" />](https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-not-optimised.png)<figcaption class="caption wp-caption-text">TeX source with dark background without optimised colours</figcaption></figure> 

Having said that I like size 16 font, so maybe it's just my eyes. In case it isn't just me though, it's a doddle to change the syntax colours. In Mac Terminal, run the following commands (copy all lines and paste in to terminal, then press enter just the once):

<pre class="brush: bash; title: ; notranslate" title="">defaults write TeXShop commentblue 0.6
defaults write TeXShop commentred 0.6
defaults write TeXShop commentgreen 0.6
defaults write TeXShop markergreen 0.8
defaults write TeXShop markerblue 0.8
defaults write TeXShop markerred 0.3
defaults write TeXShop commandred 1.0
defaults write TeXShop commandgreen 0.5
defaults write TeXShop commandblue 0.2</pre>

As you can see, there are three types of syntax that are highlighted:

- Comments
- Markers
- Commands

I've modified that colours so that comments are a light grey, markers a light green, and commands orange so that they stand out more clearly against the black background.<figure id="attachment_1017" class="thumbnail wp-caption aligncenter" style="width: 759px">

[<img class="size-full wp-image-1017" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-optimised.png?fit=648%2C292" alt="TeX source optimised" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-optimised.png?w=749 749w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-optimised.png?resize=300%2C135 300w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-optimised.png?resize=660%2C298 660w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" />](https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/02/tex-source-optimised.png)<figcaption class="caption wp-caption-text">TeX source with dark background with higher contrast syntax highlighting</figcaption></figure> 

If you prefer different colours, each syntax type has three options to specify, each corresponding to a line of code:

- Blue
- Green
- Red

They are like traditional rgb, except you specify them as a fraction between 0 and 1.0, where 1.0 is equivalent to 255 in traditional notation. You can therefore control the rgb parameters for each syntax type, using the codes above as a template, and make source editing with a dark background much easier to read.