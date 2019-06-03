
# Introduction to GIS {#introGIS}



## What is a GIS?

A Geographic Information System is a multi-component environment used to create, manage, visualize and analyze data and its spatial counterpart. It's important to note that most datasets you will encounter in your lifetime can all be assigned a spatial location whether on the earth's surface or within some arbitrary coordinate system (such as a soccer field or a gridded petri dish). So in essence, any dataset can be represented in a GIS: the question then becomes "does it need to be analyzed in a GIS environment?" The answer to this question depends on the purpose of the analysis. If, for example, we are interested in identifying the ten African countries with the highest conflict index scores for the 1966-78 period, a simple table listing those scores by country is all that is needed. 


Table: (\#tab:01-Africa-conflict)Index of total African conflict for the 1966-78 period [@Anselin1992a].

Country         Conflicts  Country                     Conflicts
-------------  ----------  -------------------------  ----------
EGYPT                5246  LIBERIA                           980
SUDAN                4751  SENEGAL                           933
UGANDA               3134  CHAD                              895
ZAIRE                3087  TOGO                              848
TANZANIA             2881  GABON                             824
LIBYA                2355  MAURITANIA                        811
KENYA                2273  ZIMBABWE                          795
SOMALIA              2122  MOZAMBIQUE                        792
ETHIOPIA             1878  IVORY COAST                       758
SOUTH AFRICA         1875  MALAWI                            629
MOROCCO              1861  CENTRAL AFRICAN REPUBLIC          618
ZAMBIA               1554  CAMEROON                          604
ANGOLA               1528  BURUNDI                           604
ALGERIA              1421  RWANDA                            487
TUNISIA              1363  SIERRA LEONE                      423
BOTSWANA             1266  LESOTHO                           363
CONGO                1142  NIGER                             358
NIGERIA              1130  BURKINA FASO                      347
GHANA                1090  MALI                              299
GUINEA               1015  THE GAMBIA                        241
BENIN                 998  SWAZILAND                         147

*Data source: Anselin, L. and John O'Loughlin. 1992. Geography of international conflict and cooperation: spatial dependence and regional context in Africa. In The New Geopolitics, ed. M. Ward, pp. 39-75.*


A simple sort on the Conflict column reveals that EGYPT, SUDAN, UGANDA, ZAIRE, TANZANIA, LIBYA, KENYA, SOMALIA, ETHIOPIA, SOUTH AFRICA are the top ten countries.

What if we are interested in knowing whether countries with a high conflict index score are geographically clustered, does the above table provide us with enough information to help answer this question? The answer, of course, is no. We need additional data pertaining to the geographic location and shape of each country. A map of the countries would be helpful.

<div class="figure">
<img src="img/Africa_conflicts.png" alt="Choropleth representation of African conflict index scores. Countries for which a score was not available are not mapped." width="638" />
<p class="caption">(\#fig:map-africa)Choropleth representation of African conflict index scores. Countries for which a score was not available are not mapped.</p>
</div>


Maps are ubiquitous: available online and in various print medium. But we seldom ask how the boundaries of the map features are encoded in a computing environment? After all, if we expect software to assist us in the analysis, the spatial elements of our data should be readily accessible in a digital form. Spending a few minutes thinking through this question will make you realize that simple tables or spreadsheets are not up to this task. A more complex data storage mechanism is required. This is the core of a GIS environment: a spatial database that facilitates the storage and retrieval of data that define the spatial boundaries, lines or points of the entities we are studying. This may seem trivial, but without a spatial database, most spatial data exploration and analysis would not be possible!

### GIS software

Many GIS software applications are available--both commercial and open source. Two popular applications are **ArcGIS** and **QGIS**.

#### ArcGIS

A popular commercial GIS software is [**ArcGIS**](http://desktop.arcgis.com/en/) developed by ESRI ([ESRI](https://en.wikipedia.org/wiki/Esri), pronounced *ez-ree*),was once a small land-use consulting firm which did not start developing GIS software until the mid 1970s. The ArcGIS desktop environment encompasses a suite of applications which include ArcMap, ArcCatalog, ArcScene and ArcGlobe. ArcGIS comes in three different license levels (basic, standard and advanced) and can be purchased with additional *add-on* packages. As such, a single license can range from a few thousand dollars to well over ten thousand dollars. In addition to software licensing costs, ArcGIS is only available for Windows operating systems; so if your workplace is a Mac only environment, the purchase of a Windows PC would add to the expense.

### QGIS 

A very capable open source (free) GIS software is [**QGIS**](http://qgis.org). It encompasses most of the functionality included in ArcGIS. If you are looking for a GIS application for your Mac or Linux environment, QGIS is a wonderful choice given its multi-platform support. Built into the current versions of QGIS are functions from another open source software: **GRASS**. GRASS has been around since the 1980's and has many advanced GIS data manipulation functions however, its use is not as intuitive as that of QGIS or ArcGIS (hence the preferred QGIS alternative).

## What is Spatial Analysis?

A distinction is made in this course between GIS and spatial analysis.
In the context of mainstream GIS software, the term *analysis*
refers to data manipulation and data querying. In the context
of **spatial analysis**, the *analysis* focuses on the *statistical analysis* of
patterns and underlying processes or more generally, spatial analysis
addresses the question “what could have been the genesis of the
observed spatial pattern?” It’s an **exploratory process** whereby we
attempt to quantify the observed pattern then explore the processes
that may have generated the pattern.

For example, you record the location of each tree in a well defined
study area. You then map the location of each tree (a GIS task).
At this point, you might be inclined to make inferences about the
observed pattern. Are the trees clustered or dispersed? Is the tree
density constant across the study area? Could soil type or slope have
led to the observed pattern? Those are questions that are addressed
in spatial analysis using quantitative and statistical techniques.


<div class="figure">
<img src="01-intro_files/figure-html/f01-ppp-1.png" alt="Distribution of Maple trees in a 1,000 x 1,000 ft study area." width="192" />
<p class="caption">(\#fig:f01-ppp)Distribution of Maple trees in a 1,000 x 1,000 ft study area.</p>
</div>

What you will learn in this course is that popular GIS software like ArcGIS are great tools to create and manipulate spatial data, but if one wishes to go beyond the data manipulation and analyze patterns and processes that may have led to these patterns, other quantitative tools are needed. One such tool we will use in this class is **R**: an open source (freeware) data analysis environment. 

R has one, if not the *richest* set of spatial data analysis and statistics tools available today. Learning the R programming environment will prove to be quite beneficial given that many of the operations learnt are transferable across many other (non-spatial) quantitative analysis projects.

[R](http://www.r-project.org/) can be installed on both Windows and Mac operating systems. Another related piece of software that you might find useful is [RStudio](https://www.rstudio.com/products/rstudio/download/) which offers a nice interface to R. To learn more about data analysis in R, visit the [ES218 course website](http://mgimond.github.io/ES218/).

## What's in an Acronym?

GIS is a ubiquitous technology. Many of you are taking this course in part because you have seen GIS listed as a "desirable"" or "required" skill in job postings. Many of you will think of GIS as a “map making” environment as do many ancillary users of GIS in the workforce. While "visualizing" data is an important feature of a GIS, one must not lose sight of *what* data is being visualized and for what purpose. O'Sullivan and Unwin [@Unwin1] use the term **accidental geographer** to refer to those *"whose understanding of geographic science is based on the operations made possible by GIS software"*. We can expand on this idea and define **accidental data analyst** as one whose understanding of data and its analysis is limited to the point-and-click environment of popular pieces of software such as spreadsheet environments, statistical packages and GIS software. The aggressive marketing of GIS technology has the undesirable effect of placing the *technology* before *purpose* and *theory*. This is not unique to GIS, however. Such concerns were shared decades ago when personal computers made it easier for researchers and employees to graph non-spatial data as well as perform many statistical procedures. 

The different purposes of mapping spatial data have strong parallels to that of graphing (or plotting) non-spatial data. **John Tukey** [@Tukey1972] offers three broad classes of the latter:

 * "*Graphs from which numbers are to be read off- substitutes for tables.*
 *  *Graphs intended to show the reader what has already been learned (by some other technique)--these we shall sometimes impolitely call propaganda graphs.*
 *  *Graphs intended to let us see what may be happening over and above what we have already described- these are the analytical graphs that are our main topic.*"

A *GIS world* analogy is proposed here:

 * **Reference maps** (USGS maps, hiking maps, road maps). Such maps are used to navigate landscapes or identify locations of points-of-interest.
 * **Presentation maps** presented in the press such as the NY Times and the Wall Street Journal, but also maps presented in journals. Such maps are designed to convey a very specific narrative of the author's choosing. (Here we'll avoid Tukey's harsh description of such visual displays, but the idea that maps can be used as *propaganda* is not farfetched).
 * **Statistical maps** whose purpose it is to manipulate the raw data in such a way to tease out patterns otherwise not discernable in its original form. This usually requires multiple data manipulation operations and visualization and can sometimes benefit from being explored outside of a spatial context.
 
This course will focus on the last two spatial data visualization purposes with a strong emphasis on the latter (*Statistical maps*).




