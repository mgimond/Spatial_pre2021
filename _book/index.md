
--- 
title: "Intro to GIS and Spatial Analysis"
author: "Manuel Gimond"
date: "Last edited on 2016-07-26"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib, journal.bib]
biblio-style: apalike
link-citations: yes
github-repo: mgimond/private-test
description: "This is a compilation of lecture notes that accompany my Intro to GIS and Spatial Analysis course."
---

# Preface {-}

These pages are a compilation of lecture notes for my Introduction to GIS and Spatial Analysis course (ES214). They are ordered in a such a way to follow the course outline but most pages can be read in any desirable order. The course (and this  book) is split into two parts: data manipulation & visualization using GIS software and exploratory spatial data analysis. The first part of this book is usually conducted using [ArcGIS Desktop](http://desktop.arcgis.com) whereas the latter part of the book is conducted in an [R](https://www.r-project.org/) data analysis environment. ArcGIS was chosen as the GIS data manipulation environment because of its "desirability" in job applications for undergraduates in the Unites States (where this course is taught). But other GIS software environments, such as the open source software [QGIS](http://qgis.org), could easily be adopted in lieu of ArcGIS--even R can be used to perform many spatial data manipulations such as clipping, buffering and projecting. Even though some of the chapters of this book make direct reference to ArcGIS technique, most chapters can be studied without access to the software.

The latter part of this book (and the course) make heavy use of R because of a) its broad appeal in the world of data analysis b) its rich (if not richest) array of spatial analysis and spatial statistics  packages c) its scripting environment (which facilitates reproducibility) d) and its very cheap cost (it's completely free and open source!). But R can be used for many traditional "GIS" application that involve most data manipulation operations--the only benefit in using a full-blown GIS environment like ArcGIS or QGIS is in creating/editing spatial data, rendering complex maps and manipulating spatial data. In future iterations of this book it is my hope to include additional R tutorials to the data manipulation sections.


