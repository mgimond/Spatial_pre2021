
--- 
title: "Intro to GIS and Spatial Analysis"
author: "Manuel Gimond"
date: "Last edited on 2019-04-24"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib, journal.bib]
biblio-style: apalike
link-citations: yes
github-repo: mgimond/spatial
description: "This is a compilation of lecture notes that accompany my Intro to GIS and Spatial Analysis course."
---

# Preface {-}

These pages are a compilation of lecture notes for my Introduction to GIS and Spatial Analysis course (ES214). They are ordered in such a way to follow the course outline, but most pages can be read in any desirable order. The course (and this book) is split into two parts: data manipulation & visualization and exploratory spatial data analysis. The first part of this book is usually conducted using [ArcGIS Desktop](http://desktop.arcgis.com) whereas the latter part of the book is conducted in [R](https://www.r-project.org/). ArcGIS was chosen as the GIS data manipulation environment because of its "desirability" in job applications for undergraduates in the Unites States. But other GIS software environments, such as the open source software [QGIS](http://qgis.org), could easily be adopted in lieu of ArcGIS--even R can be used to perform many spatial data manipulations such as clipping, buffering and projecting. Even though some of the chapters of this book make direct reference to ArcGIS techniques, most chapters can be studied without access to the software.

The latter part of this book (and the course) make heavy use of R because of a) its broad appeal in the world of data analysis b) its rich (if not richest) array of spatial analysis and spatial statistics packages c) its scripting environment (which facilitates reproducibility) d) and its very cheap cost (it's completely free and open source!). But R can be used for many traditional "GIS" application that involve most data manipulation operations--the only benefit in using a full-blown GIS environment like ArcGIS or QGIS is in creating/editing spatial data, rendering complex maps and manipulating spatial data.

The Appendix covers various aspects of spatial data manipulation and analysis using R. The course only focuses on point pattern analysis and spatial autocorrelation using R, but I've added other R resources for students wishing to expand their GIS skills using R.




<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.
