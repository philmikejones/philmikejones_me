---
title: Glossary and acronyms in LaTeX
date: 2015-02-27
author: philmikejones
categories:
  - Code
---

I couldn't find one comprehensive source to create a glossary and acronym list in LaTeX with LaTeXila on Ubuntu, so this post will get you started (or remind me when I need it).
  

I use LaTeX to write my PhD thesis. One of the things I love about it is that, for the most part, I don't have to think about formatting. There is no (easy) way to tinker with spacing, fonts, and presentation. What you get is compiled from simply writing marked-up plain text, and it looks beautiful.

This does mean that when you want to produce more complicated items like a table of contents or, in this case, a glossary for my thesis you need to use specific packages designed for the purpose. I want to use a formal glossary package because it allows me to define the term and its acronym in a file, then reference the item in my thesis. The first time the item is referred to the full label and acronym are displayed automatically:

<pre>Building Economies and Resilient Societies (BEARS)</pre>

All subsequent times I refer to the item just the acronym is shown:

<pre>BEARS</pre>

As I edit and chop and change the thesis structure I don't then have to worry about making sure the first listing is the full listing, and all subsequent references are just the acronym; this is done automatically.

Getting the acronyms and glossaries working is relatively easy. In the preamble of your document, place the following code _before_ usepackage{hyperref} to load the appropriate package:

<pre>usepackage{hyperref}
usepackage[toc]{glossaries}
  makeglossaries</pre>

toc places a listing for the glossary in the table of contents. makeglossaries builds the glossary list when you build the main file.

I place all my glossary items and acryonyms in a separate file (called, imaginatively, glossary.tex) so I refer to this using input where I want the glossary to be placed in the document (typically after the table of contents):

<pre>input{glossary.tex}
printglossaries</pre>

I use input{} rather than include{} so as not to force a page break.

In the glossaries.tex file I list all my glossary items and acronyms. The syntax for producing these is well documented in the [LaTeX Wikibook: http://en.wikibooks.org/wiki/LaTeX/Glossary](http://en.wikibooks.org/wiki/LaTeX/Glossary) so I won't reproduce that here. As an example, my glossary.tex includes:

<pre>newacronym{BEARS}{BEARS}{Building Economies and Resilient Societies}</pre>

Where the first {BEARS} is the label referred to later, the second {BEARS} is the acronym which is printed each time I reference it, and the Building Economies and Resilient Societies is the description used in the glossary and when referenced the first time.

In my main document I can then simply refer to this listing using:

<pre>gls{BEARS}</pre>

Which produces the following output the first time I call it:

<pre>Building Economies and Resilient Societies (BEARS)</pre>

And simply BEARS each subsequent time.

This generally worked fine, but I did struggle to produce the glossary list at the beginning of the document, despite no warnings or errors when I built the document. It traspired that there is an additional build step, like when building a bibliography:

  1. Build file.tex.
  2. Build glossary using makeglossary.
  3. Build file.tex again.
  4. (Maybe) build file.tex again.

It seems that in most LaTeX GUIs there isn't a build option for glossaries, so you can either build the glossary from the command line or create a build button. To build from the command line, first build your .tex file, then navigate to (or open your terminal at) the folder your .tex file is located in. Type:

<pre>makeglossary file</pre>

Replace file with your actual filename without an extension (mine is thesis for example). Then build your .tex file again (and maybe again).

If, like me, you can't be bothered to run this command every time your glossary items change, you can add a GUI button to most LaTeX GUIs. I use LaTeXila. If you too use LaTeXila, press:

<pre>Build &gt; Manage Build Tools</pre>

You should get this dialogue box:<figure id="attachment_1506" class="thumbnail wp-caption alignnone" style="width: 670px">

<img class="size-large wp-image-1506" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/02/build-tools-dialogue.png?fit=648%2C289" alt="Build Tools dialogue box" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2015/02/build-tools-dialogue.png?w=762 762w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2015/02/build-tools-dialogue.png?resize=300%2C134 300w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2015/02/build-tools-dialogue.png?resize=660%2C294 660w" sizes="(max-width: 648px) 100vw, 648px" data-recalc-dims="1" /><figcaption class="caption wp-caption-text">Build Tools dialogue box</figcaption></figure> 

Press + under &#8216;Personal build tools'. Enter the following details:

<table  class=" table table-hover" >
  <tr>
    <th>
      Label
    </th>
    
    <td>
      Run makeglossaries
    </td>
  </tr>
  
  <tr>
    <th>
      Description
    </th>
    
    <td>
      Optional: Make glossary and acronyms
    </td>
  </tr>
  
  <tr>
    <th>
      Extensions
    </th>
    
    <td>
      .tex
    </td>
  </tr>
  
  <tr>
    <th>
      Icon
    </th>
    
    <td>
      Execute
    </td>
  </tr>
  
  <tr>
    <th>
      Commands
    </th>
    
    <td>
      makeglossaries $shortname
    </td>
  </tr>
  
  <tr>
    <th>
      Post-processor
    </th>
    
    <td>
      all-output
    </td>
  </tr>
</table>

This adds a new button to the GUI called &#8216;Make glossary and acronyms'. Don't forget to build the .tex file, then the glossary, then the .tex file again (and maybe again). It's maybe a chore to set up, but at least you never have to worry about finding instances of a term or acronym again.