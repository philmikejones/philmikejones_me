---
title: Load SPSS in R
date: 2014-09-12
author: philmikejones
categories:
  - Code
---

While I prefer to use a text delimited file to enter data in to R, sometimes only an SPSS file is provided for some datasets. I like the `sjmisc` and `sjPlot` packages because of their handling of values and labels, and because they use `haven` by default to read the file, meaning it's fast.

Load SPSS `.sav` files with the `sjPlot` package:

<pre class="brush: r; title: ; notranslate" title=""># install the package
install.packages(c("sjPlot", "sjmisc"))
require("sjPlot")
require("sjmisc")

# Open the .sav file with:
df &lt;- read_spss("path/to/spss/file.sav",
                 autoAttachVarLabels = TRUE)

# View the variable names with:
view_spss(df)
</pre>

That's all there is to it. For more information check out the author's website: http://strengejacke.de/sjPlot/view_spss/