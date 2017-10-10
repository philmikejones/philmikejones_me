---
title: Spatial microsimulation 101
date: 2016-12-21
author: philmikejones
categories:
  - Code
  - GIS
  - rstats
tags:
  - Doncaster
  - ipf
  - rstats
  - spatial microsimulation
---

I recently gave a presentation for analysts and data modellers at the [Department for Work and Pensions (DWP)](https://www.gov.uk/government/organisations/department-for-work-pensions/about/statistics) introducing the spatial microsimulation technique (specifically the [IPF](https://en.wikipedia.org/wiki/Iterative_proportional_fitting) flavour), and below are the slides I used (use `spacebar` to navigate through the slides):

<iframe src="https://philmikejones.github.io/spatial-microsimulation-101/#/" width="720px" height="550px"></iframe>

Much of the content is based on material from _Spatial Microsimulation with R_ by Robin Lovelace and Morgane Dumont ([online content](http://robinlovelace.net/spatial-microsim-book/) | [physical book](https://www.crcpress.com/Spatial-Microsimulation-with-R/Lovelace-Dumont/p/book/9781498711548)) and my own [rakeR package](https://cran.r-project.org/package=rakeR) for R. 

For the presentation I also created a spatial model of tax credits claimants in Doncaster based on data I already had for Doncaster and survey responses from [Understanding Society](https://www.understandingsociety.ac.uk/). NB: don't use the model results in any analysis; they were created quickly to demonstrate the concept and as such haven't been tested or validated in any way.

The figure below shows the proportion of residents in each output area who claim tax credits, with darker areas indicating a higher proportion of claimants.

![Spatial microsimulation of tax credits in Doncaster](../../images/taxcredits_result.png)
