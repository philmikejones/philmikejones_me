---
title: Regression Diagnostics with R
date: 2014-05-12
author: philmikejones
categories:
  - Code
  - rstats
tags:
  - diagnostics
  - r
  - regression
  - statistics
---

The [R statistical software](http://en.wikipedia.org/wiki/R_(programming_language)) is my preferred statistical package for many reasons. It's mature, well-supported by communities such as [Stack Overflow](http://stackoverflow.com/questions/tagged/r), has programming abilities built right in, and, most-importantly, is completely free ([in both senses](http://en.wikipedia.org/wiki/Gratis_versus_libre)) so that anyone can reproduce and check your analyses.

R is extremely comprehensive in terms of available statistical analyses, which can be easily expanded using additional packages that are free and easily installed. When there isn't a readily-available built-in function, for example I don't know of a function to calculate the standard error, R's support for programming functions means it's a doddle to write your own.

That said, I've found performing regression diagnostics quite difficult in R. I've tried numerous methods and each had their flaws, until I finally found a method I like and have settled on. I think my way (actually a combination of other methods by different authors) is relatively easy, almost fool-proof, and less prone to errors. I'll run you through it step-by-step, including running a simple, example, linear regression; explaining the assumptions and how to test them; and what you're looking for to accept &#8211; or reject &#8211; a regression model.

## Setup

The [UK Data Service](http://ukdataservice.ac.uk/) provide a small number of [teaching datasets](http://ukdataservice.ac.uk/get-data/open-access.aspx) that are perfect for our use. I've chosen to use the [Living Costs and Food Survey, 2010: Unrestricted Access Teaching Dataset](http://discover.ukdataservice.ac.uk/catalogue/?sn=7216) as an example because it contains two continuous variables, which we'll need for regression.

[<img class="alignleft wp-image-1077 size-full" src="https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/05/github-mark-32px.png?fit=32%2C32" alt="Github" data-recalc-dims="1" />](https://github.com/philmikejones/regdiag)You can download the file and set up a working directory in R yourself, or I've set up a project folder on github called &#8216;[regdiag](https://github.com/philmikejones/regdiag)&#8216; with the necessary data file, R code, and .Rproj file for easy set up.

  1. [Download the regdiag github project](https://github.com/philmikejones/regdiag/archive/master.zip) and extract the zip to a folder of your choice (or use github to clone the project if you know what you're doing).
  2. Open the `regdiag.Rproj` file in R Studio, and it will configure a workspace for you.
  3. Open the `regdiag.R` file and run lines 39 &#8211; 48. These install and configure the required package `sjPlot` (to use SPSS files) and then loads the data file.

I'm using the sjPlot rather then foreign package (although both open SPSS files adequately) because of the sjPlot function to view the variable names and value labels, `sji.viewSPSS()`. Try this now by typing:

<pre class="brush: r; title: ; notranslate" title="">sji.viewSPSS(lcfs)</pre>

You can also view the dataframe with:

<pre class="brush: r; title: ; notranslate" title="">View(lcfs)</pre>

## Regression: A Simple Example

There isn't an awful lot of choice of variables to use as we need continuous variables for simple (or multiple) regression. From the information about the variables and value labels I've chosen:

- Gross normal weekly household income (P344pr), and;
- Total expenditure (P550tpr).

I expect income will affect how much a household spends, so run the following to check:

<pre class="brush: r; title: ; notranslate" title="">m1 &lt;- lm(lcfs$P550tpr ~ lcfs$P344pr)
summary(m1)</pre>

This is running a linear model (lm) using expenditure as the outcome (dependent) variable and income as the predictor (independent) variable. From the results we can see this is a pretty good model! The r-squared value is approximately 0.50, suggesting about half of the variability in expenditure is predicted by income! The model is also highly statistically significant, as the p-value is much less than 0.01, so we can be very confident this isn't just a random anomaly we're seeing and this is, in fact, a real relationship. Since it's such a good model, I've included a gratuitous scatter graph:<figure id="attachment_1072" class="thumbnail wp-caption aligncenter" style="width: 610px">

[<img class="size-full wp-image-1072" src="https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/05/m1-scatter-small.png?fit=600%2C424" alt="Scatter plot of linear model" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/05/m1-scatter-small.png?w=600 600w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/05/m1-scatter-small.png?resize=300%2C212 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/05/m1-scatter-small.png)<figcaption class="caption wp-caption-text">Scatter plot of linear model, &#8216;m1'</figcaption></figure> 

While the relationship is strong this isn't exactly ground-breaking and unlikely to get us a peer-reviewed journal article, but it does mean we have a good model that we can perform regression diagnostics on. Diagnostics are important because all regression models rely on a number of assumptions. If these assumptions are met, the model can be used with confidence. If the assumptions are violated, the model should probably be discarded because you cannot confidently assume that the relationships seen in the model are mirrored in the population. Diagnostics allow us to test the assumptions.

## Assumptions

The are four assumptions of simple linear regression:

  1. Linear relationship between the two variables.
  2. Residuals are independent (can't be tested statistically, so ignored for now).
  3. The residuals of the model are normally distributed.
  4. The variance of the residuals isn't affected by the predicted value (homoscedasticity).

In addition to testing these assumptions, we also need to investigate any outliers, if any. So as well as the assumptions, we'll check the:

  1. Cook's distance
  2. Leverage (hat) values

If you want to know what these terms _mean_ then I recommend a textbook like Andy Field's [_Discovering Statistics Using R_](http://www.uk.sagepub.com/booksProdDesc.nav?prodId=Book236067). I'm just going to concentrate on _how_ you test and interpret them.

### Linear Relationship(s)

For simple linear regression with two variables, simply check a scatter plot of your two variables (don't forget to put independent variable on the _x_ axis, and dependent variable on the _y_ axis; this forever trips me up!).

We can tell from our beautiful scatterplot above that there is, in fact, a linear relationship between the two variables so this assumption is met in our example.

If you're performing multiple regression (i.e. you have more than one independent variable) you need a plot of the predicted values against the standardized residuals to test for linearity. This is easy to plot, assuming m1 is what you've called your linear model:

<pre class="brush: r; title: ; notranslate" title="">plot(m1, which = 1)</pre>

This might produce a scatter plot a bit like the following:

[<img class="aligncenter size-full wp-image-1049" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/04/mr-linear.png?fit=600%2C442" alt="Scatter plot of predicted vs standardized residuals for testing linear relationship in multiple regression" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/04/mr-linear.png?w=600 600w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/04/mr-linear.png?resize=300%2C221 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/04/mr-linear.png)A scatter plot that looks fairly random like this suggests the relationships between the variables are linear, which is what we want. If the relationship wasn't linear the pattern of the points would be curved rather than random.

### Residuals are Independent

Since this can't be tested statistically &#8211; it depends on the design of the research &#8211; I'll be ignoring this here.

### Residuals Normally Distributed

The residuals of the model can be plotted as a density plot or Q-Q plot to see if they're normally distributed:

<pre class="brush: r; title: ; notranslate" title="">ggplot() + geom_density(aes(residuals(m1)))  # density plot
qqPlot(m1)  # qq plot, requires the car library</pre>

The density plot and QQ plot are below:

[<img class="aligncenter size-full wp-image-1054" src="https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/04/density-res.png?fit=600%2C462" alt="Density plot of model residuals" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/04/density-res.png?w=600 600w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/04/density-res.png?resize=300%2C231 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />](https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/04/density-res.png)[<img class="aligncenter wp-image-1055" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/04/qqres.png?resize=600%2C462" alt="QQ plot of model residuals" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/04/qqres.png?w=600 600w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2014/04/qqres.png?resize=300%2C231 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/04/qqres.png)Both charts suggest the same thing: there are deviations from normal shown by the kink in the density plot, and the deviation from the red line in the QQ plot. This might be a spanner in the works for our model, and if this were a real analysis I would definitely look in to this further.

### Homoscedasticity

This is testing that the variance of residuals doesn't vary by predictable amounts, i.e. they are random. This can easily be checked by plotting fitted values against residuals:

<pre class="brush: r; title: ; notranslate" title="">spreadLevelPlot(m1)</pre>

For our example data this results in the following plot:<figure id="attachment_1080" class="thumbnail wp-caption aligncenter" style="width: 610px">

[<img class="wp-image-1080 size-full" src="https://i2.wp.com/philmikejones.me/wp-content/uploads/2014/05/homoscedasticity.png?fit=600%2C424" alt="Homoscedasticity" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/05/homoscedasticity.png?w=600 600w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2014/05/homoscedasticity.png?resize=300%2C212 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />](http://philmikejones.me/wp-content/uploads/2014/05/homoscedasticity.pdf)<figcaption class="caption wp-caption-text">Plot testing homoscedasticity</figcaption></figure> 

For all fitted values (i.e. along the _x_ axis) you should expect to see variation in the residuals that is random, that is no pattern should be apparent. For our graph, the left side of the graph looks pretty good as the points are pretty randomly distributed. Towards the right of the graph, though, the residuals start to show a pattern. This might be evidence of heteroscedasticity, that is the assumption might be violated, and should be investigated further.

## Outliers

As well as checking our assumptions, we should also investigate any outliers. This can easily be checked with two statistics, Cook's distance and leverage (hat) values.

### Cook's Distance

This can easily be checked with the following plot:

<pre class="brush: r; title: ; notranslate" title="">plot(org1, which = 4)</pre>

This plots the observation number against its respective Cook's distance, and handily labels the largest Cook's distances for you. The rule of thumb often quoted is you're looking for Cook's distances to be less than 1.0, with no Cook's distance &#8216;significantly' larger than the rest (although there's no rule of thumb as far as I know for what significantly means in this instance).

In our example, no observation has a Cook's distance greater than 1.0 (good), and although three observations have higher Cook's distances than the rest, I've decided they're not significantly different. If, instead, there was a Cook's distance of greater than 1.0 or significantly large you would need to investigate the observation to see what's going on and, if it's an error, consider removing it.

### Leverage (Hat) Values

Finally, leverage &#8211; sometimes called hat values &#8211; should be checked. To plot the leverage values and inspect them visually, run:

<pre class="brush: r; title: ; notranslate" title="">lev &lt;- hatvalues(m1)
plot(lev)</pre>

In our example there are not large leverage values (notice the tiny scale on the y axis), so we need do nothing further. If you notice large leverage values you can run the following lines of code to identify observations:

<pre class="brush: r; title: ; notranslate" title="">out &lt;- identify(lev)
View(lcfs[out, ])</pre>

After running the first line, simply click on the offending observations, then press Escape. This stores the observations numbers in a variable which is used to subset the dataframe and the second line shows you just the identified observations for analysis. Neat, huh?

## Conclusions

So there you have it, a whistle-stop tour of regression diagnostics in R. I haven't explained any of the functions, so a good textbook like Andy Field's _Discovering Statistics with [R/SPSS]_ is recommended if you need to understand the terms or how to properly interpret them. Also, these methods only really allow you to check the assumptions visually. This is usually effective enough but is subjective. But, the point is that hopefully for most purposes these tools will allow you to check a regression model and know with some confidence if you can use it or if you should treat it with suspicion.