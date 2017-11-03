
# (PART) Spatial Analysis {-} 
 
# Point Pattern Analysis

## Centrography

A very basic form of point pattern analysis involves summary statistics such as the **mean center**, **standard distance** and **standard deviational ellipse**.

![](img/centrography.svg)<!-- -->

These point pattern analysis techniques were popular before computers were  ubiquitous since hand calculations are not too involved, but these summary statistics are too concise and hide far more valuable information about the observed pattern. More powerful analysis methods can be used to explore point patterns. These methods can be classified into two groups: **density based** approach and **distance based** approach.

## Density based analysis


<div class="note">
<p>A <em>first order</em> property of a pattern concerns itself with the variation of the observations' density across a study area. For example, the distribution of oaks will vary across a landscape based on underlying soil characteristics (resulting in areas having dense clusters of oaks and other areas not).</p>
</div>


Density based techniques characterize the pattern in terms of its distribution *vis-a-vis* the study area--a **first-order** property of the pattern. Here, we make a distinction between the **intensity** of a spatial process and the observed **density** of a pattern under study (which is often used to estimate the process' intensity). A point pattern can be thought of as a "realization" of an underlying process whose intensity $\lambda$ is estimated from the observed point pattern's density (which is sometimes denoted as $\widehat{\lambda}$ where the caret $\verb!^!$  is referring to the fact that the observed density is an *estimate* of the underlying process' intensity) . 


### Global density

A basic measure of a pattern's density $\widehat{\lambda}$ is its overall, or **global**, density. This is simply the ratio of observed number of points, $n$, to the study region's surface area, $a$, or:

$$
\begin{equation}
\widehat{\lambda} = \frac{n}{a}
\label{eq:global-density}
\end{equation}
$$

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-gobal-dens-1.png" alt="An example of a point pattern where n = 20 and the study area (defined by a square boundary) is 10 units squared. The point density is thus 20/100 = 0.2 points per unit area." width="240" />
<p class="caption">(\#fig:f11-gobal-dens)An example of a point pattern where n = 20 and the study area (defined by a square boundary) is 10 units squared. The point density is thus 20/100 = 0.2 points per unit area.</p>
</div>

### Local density

A point pattern's density can be measured at different locations within the study area. Such an approach helps us assess if the density--and, by extension, the underlying process' local intensity $\widehat{\lambda}_i$--is constant across the study area. This can be an important property of the data since it may need to be mitigated for when using distance based analysis tools. Several techniques to measure local density are available, here we will focus on two such methods: *quadrat density* and *kernel density*.

#### Quadrat density

This technique requires that the study area be divided into sub-regions (aka *quadrats*). Then, the point density is computed for each quadrat by dividing the number of points in each quadrat by the quadrat's area. Quadrats can take on many different shapes such as hexagons and triangles, here we use square shaped quadrats to demonstrate the procedure.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-quad01-1.png" alt="An example of a quadrat count where the study area is divided into four equally sized quadrats whose area is 25 square units each. The density in each quadrat can be computed by dividing the number of points in each quadrat by that quadrat's area." width="211.2" />
<p class="caption">(\#fig:f11-quad01)An example of a quadrat count where the study area is divided into four equally sized quadrats whose area is 25 square units each. The density in each quadrat can be computed by dividing the number of points in each quadrat by that quadrat's area.</p>
</div>



The choice of quadrat numbers and quadrat shape can influence the measure of local density and must be chosen with care. If very small quadrat sizes are used you risk having many quadrats with no points which may prove uninformative. If very large quadrat sizes are used, you risk missing subtle changes in spatial density distributions such as the east-west gradient in density values in the above example.

Quadrat regions do not have to take on a uniform pattern across the study area, they can also be defined based on a **covariate**. For example, if it's believed that the underlying point pattern process is driven by elevation, quadrats can be defined by sub-regions such as different ranges of elevation values (labeled 1 through 4 on the right-hand plot in the following example). This can result in quadrats having non-uniform shape and area.

<div class="note">
<p>Converting a continuous field into discretized areas is sometimes referred to as <strong>tesselation</strong>. The end product is a <strong>tesselated surface</strong>.</p>
</div>

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-quad02-1.png" alt="Example of a covariate. Figure on the left shows the elevation map. Figure on the right shows elevation broken down into four sub-regions for which a local density will be computed." width="576" />
<p class="caption">(\#fig:f11-quad02)Example of a covariate. Figure on the left shows the elevation map. Figure on the right shows elevation broken down into four sub-regions for which a local density will be computed.</p>
</div>


If the local intensity changes across all regions of the tessellated covariate as a function of the covariate, then there is evidence of a dependence between the process that generated the point pattern and the covariate. In our example, sub-regions 1 through 4 have surface areas of 17.08, 50.45, 26.76, 5.71 respectively. To compute these regions' point densities, we simply divide the number of points by the area.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-quad03-1.png" alt="Figure on the left displays the number of points in each elevation sub-region (sub-regions are coded as values ranging from 1 to 4). Figure on the right shows the density of points (number of points divided by area of sub-region)." width="576" />
<p class="caption">(\#fig:f11-quad03)Figure on the left displays the number of points in each elevation sub-region (sub-regions are coded as values ranging from 1 to 4). Figure on the right shows the density of points (number of points divided by area of sub-region).</p>
</div>

We can plot the relationship between point density and elevation regions to help assess any dependence between the variables.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-quad04-1.png" alt="Plot of point density vs elevation regions." width="672" />
<p class="caption">(\#fig:f11-quad04)Plot of point density vs elevation regions.</p>
</div>

Though there is a steep increase in density at the highest elevation range, this increase is not monotonic across all ranges of increasing elevation suggesting that density may not be explained by elevation alone.

Note that how one chooses to tessellate a surface can have an influence on the resulting density values. For example, dividing the elevation into *equal area* sub-regions produces different density values.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-quad05-1.png" alt="Same analysis as last figure using different sub-regions. Note the difference in density values." width="576" />
<p class="caption">(\#fig:f11-quad05)Same analysis as last figure using different sub-regions. Note the difference in density values.</p>
</div>



#### Kernel density

The kernel density approach is an extension of the quadrat method: Like the quadrat density, the kernel approach computes a localized density for subsets of the study area, but unlike its quadrat density counterpart, the sub-regions overlap one another providing a *moving* sub-region window. This moving window is defined by a **kernel**. Unlike its quadrat density counterpart, the kernel density approach generates a grid of density values whose cell size is smaller than that of the kernel window. Each cell is assigned the density value computed for the kernel window centered on that cell. Many software applications will usually generate a raster output to store the density values. 

A kernel not only defines the shape and size of the window, but it can also *weight* the points following a well defined kernel function. The simplest of functions is a **basic kernel** where each point in the kernel window is assigned equal weight.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-kernel01-1.png" alt="An example of a basic 3x3 kernel density map (ArcGIS calls this a point density map) where each point is assigned an equal weight. For example, the second cell from the top and left (i.e. centered at location x=1.5 and y =8.5) has one point within a 3x3 unit (pixel) region and thus has a local density of 1/9 = 0.11." width="672" />
<p class="caption">(\#fig:f11-kernel01)An example of a basic 3x3 kernel density map (ArcGIS calls this a point density map) where each point is assigned an equal weight. For example, the second cell from the top and left (i.e. centered at location x=1.5 and y =8.5) has one point within a 3x3 unit (pixel) region and thus has a local density of 1/9 = 0.11.</p>
</div>

Some of the most popular **kernel functions** assign weights to points that are inversely proportional to their distances to the kernel window center. A few such kernel functions follow a *gaussian* or *quartic* like distribution function. These functions tend to produce a smoother density map.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-kernel02-1.png" alt="An example of a kernel function is the 3x3 quartic kernel function where each point in the kernel window is weighted based on its proximity to the kernel's center cell (typically, closer points are weighted more heavily). Kernel functions, like the quartic, tend to generate smoother surfaces." width="672" />
<p class="caption">(\#fig:f11-kernel02)An example of a kernel function is the 3x3 quartic kernel function where each point in the kernel window is weighted based on its proximity to the kernel's center cell (typically, closer points are weighted more heavily). Kernel functions, like the quartic, tend to generate smoother surfaces.</p>
</div>


#### Kernel Density Adjusted for Covariate

In the previous section, we learned that we could use a covariate, like elevation, to define the sub-regions (quadrats) within which densities were computed. In essence a form of *normalization* was applied to the density calculations whereby each sub-region was assumed to represent a unique underlying process (if this were the case, then the density values would have been the same across each sub-region). The idea of *normalizing* the data to some underlying covariate can be extended to kernel density analysis. Here, instead of *dividing* the study region into discrete sub-regions (as was done with quadrat analysis), we normalize the computed density (from our observed point pattern) to a *measure* of density expected from the underlying covariate. This normalized density, which we'll denote as $\rho$, can be estimated in one of three different ways-- by *ratio*, *re-weight* and *transform* methods. We will not delve into the differences between these methods, but note that there is more than one way to estimate $\rho$.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-kernel03-1.png" alt="An estimate of $\rho$ using the ratio method. The figure on the left shows the estimated $\rho$ as a function of elevation. The envelope shows the 95% confidence interval. The figure on the right shows the spatial distribution of $\rho$." width="480" />
<p class="caption">(\#fig:f11-kernel03)An estimate of $\rho$ using the ratio method. The figure on the left shows the estimated $\rho$ as a function of elevation. The envelope shows the 95% confidence interval. The figure on the right shows the spatial distribution of $\rho$.</p>
</div>

If the density, $\rho$, can be explained by the elevation, we would expect a constant $\rho$ value across all elevation values (figure on the left) and across the spatial extent (figure on the right). This appears to be the case with our working example except near the upper right-hand corner of the spatial extent where the elevation values are the highest. This can be explained by the small area covered by these high elevation locations which result in fewer observed points and thus higher uncertainty for that corner of the study extent. This is very apparent in the left figure where the 95% confidence interval envelope widens at higher elevation values (indicating the greater uncertainty in our estimated $\rho$ value at the higher elevation).

### Modeling intensity as a function of a covariate

So far, we have learned techniques that *describe* the distribution of points across a region of interest. But it is often more interesting to *model* the relationship between the distribution of points and some underlying covariate by defining that relationship mathematically. This can be done by exploring the *changes* in point density as a function of a covariate, however, unlike techniques explored thus far, this approach makes use of a statistical model. One such model is a *Poisson point process* model which can take on the form of:

$$
\begin{equation}
\lambda(i) = e^{\alpha + \beta Z(i)}
\label{eq:density-covariate}
\end{equation}
$$


where $\lambda(i)$ is the modeled intensity at location $i$, $e^{\alpha}$ (the exponent of $\alpha$) is the base intensity when the covariate is *zero* and $e^{\beta}$ is the multiplier by which the intensity increases (or decreases) for each 1 unit increase in the covariate. This is a form of the *logistic regression* model--popular in the field of statistics. This equation implies that the relationship between the process that lead to the observed point pattern is a **loglinear** function of the underlying covariate (i.e. one where the process' intensity is exponentially increasing or decreasing as a function of the covariate). Note that taking the log of both sides of the equation yields the more familiar linear regression model where $\alpha + \beta Z(i)$ is the *linear predictor*.

<div class="note">
<p>Note: The left-hand side of a logisitic regression model is often presented as the <em>probability</em>, <span class="math inline"><em>P</em></span>, of occurance and is related to <span class="math inline"><em>λ</em></span> as $\lambda=P/(1-P)$ which is the <em>ratio of probability of occurence</em>. Solving for <span class="math inline"><em>P</em></span> gives us $P = \lambda/(1 + \lambda)$ which yields the following equation: <br /><span class="math display">$$
P(i) = \frac{e^{\alpha + \beta Z(i)}}{1 + e^{\alpha + \beta Z(i)}}
$$</span><br /></p>
</div>

Let's work with the point distribution of Starbucks cafes in the state of Massachusetts. The point pattern clearly exhibits a non-random distribution. It might be helpful to compare this distribution to some underlying covariate such as the population density distribution.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-starbucks-1.png" alt="Location of Starbucks relative to population density. Note that the classification scheme follows a log scale to more easily differentiate population density values." width="672" />
<p class="caption">(\#fig:f11-starbucks)Location of Starbucks relative to population density. Note that the classification scheme follows a log scale to more easily differentiate population density values.</p>
</div>

We can fit a poisson point process model to these data where the modeled intensity takes on the form:

$$
\begin{equation}
Starbucks\ density(i) = e^{\alpha + \beta\ population(i)}
\label{eq:walmart-model}
\end{equation}
$$


The parameters $\alpha$ and $\beta$ are estimated from a method called *maximum likelihood*. Its implementation is not covered here but is widely covered in many statistics text books. And the term $(i)$ serves as a reminder that the point density and the population distribution both can vary as a function of location $i$.



The estimated value for $\alpha$ is -18.966. This is interpreted as stating that given a population density of *zero*, the base intensity of the point process is e^-18.966^ or 5.79657e-09 stores per square meter (the units are derived from the point's reference system)--a number close to zero (as one would expect). The estimated value for $\beta$ is 0.00017. This is interpretated as stating that for every unit increase in the population density derived from the raster, the intensity of the point process increases by e^0.00017^ or 1.00017.

If one were to plot the relationship between density and population, we would get:

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-pppm01-1.png" alt="Poisson point process model fitted to the relationship between Starbucks store locations and population density. The model assumes a loglinear relationship. Note that the density is reported in number of stores per map unit area (the map units are in meters)." width="288" />
<p class="caption">(\#fig:f11-pppm01)Poisson point process model fitted to the relationship between Starbucks store locations and population density. The model assumes a loglinear relationship. Note that the density is reported in number of stores per map unit area (the map units are in meters).</p>
</div>



## Distance based analysis

<div class="note">
<p>A <em>second order</em> property of a pattern concerns itself with the observations' influence on one another. For example, the distribution of oaks will be influenced by the location of parent trees: where parent oaks are present we would expect dense clusters of oaks to emerge.</p>
</div>

An alternative to density based methods is **distance based methods** for pattern analysis where the interest lies in how the points are distributed relative to one another--a second-order property of the pattern. 

### Average Nearest Neighbor

An average nearest neighbor (ANN) analysis measures the average distance from each point in the study area to its nearest point. In the following example, the average nearest neighbor for all points is 1.52 units.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-ppp-dist-1.png" alt="Distance between each point and its closest point. For example, the point closest to point 1 is point 9 which is 2.32 units away." width="480" />
<p class="caption">(\#fig:f11-ppp-dist)Distance between each point and its closest point. For example, the point closest to point 1 is point 9 which is 2.32 units away.</p>
</div>

An extension of this idea is to plot the ANN values for different order neighbors, that is for the first closest point, then the second closest point, and so forth.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-ANN-plot-1.png" alt="ANN values for different neighbor order numbers. For example, the ANN for the first closest neighbor is 1.52 units; the ANN for the 2nd closest neighbor is 2.14  units; and so forth." width="240" />
<p class="caption">(\#fig:f11-ANN-plot)ANN values for different neighbor order numbers. For example, the ANN for the first closest neighbor is 1.52 units; the ANN for the 2nd closest neighbor is 2.14  units; and so forth.</p>
</div>

The shape of the ANN curve as a function of neighbor order can provide insight into the spatial arrangement of points relative to one another. In the following example, three different point patterns of 20 points are presented.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-diff-patterns-1.png" alt="Three different point patterns: a single cluster, a dual cluster and a randomly scattered pattern." width="432" />
<p class="caption">(\#fig:f11-diff-patterns)Three different point patterns: a single cluster, a dual cluster and a randomly scattered pattern.</p>
</div>

Each point pattern offers different ANN vs. neighbor order plots.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-diff-ANN-plots-1.png" alt="Three different ANN vs. neighbor order plots. The black ANN line is for the first point pattern (single cluster); the blue line is for the second point pattern (double cluster) and the red line is for the third point pattern." width="384" />
<p class="caption">(\#fig:f11-diff-ANN-plots)Three different ANN vs. neighbor order plots. The black ANN line is for the first point pattern (single cluster); the blue line is for the second point pattern (double cluster) and the red line is for the third point pattern.</p>
</div>

The bottom line (black line) indicates that the cluster (left plot) is tight and that the distances between a point and all other points is very short. This is in stark contrast with the top line (red line) which indicates that the distances between points is much greater. Note that the way we describe these patterns is heavily influenced by the size and shape of the study region. If the region was defined as the smallest rectangle encompassing the cluster of points, the cluster of points would no longer look clustered.

<div class="figure">
<img src="11-Point-Patterns_files/figure-html/f11-diff-ppp02-1.png" alt="The same point pattern presented with two different study areas. How differently would you describe the point pattern in both cases?" width="384" />
<p class="caption">(\#fig:f11-diff-ppp02)The same point pattern presented with two different study areas. How differently would you describe the point pattern in both cases?</p>
</div>


### K and L functions

#### K function

The average nearest neighbor (ANN) statistic is one of many point pattern analysis statistics. Another statistic is the K-function which summarizes the distance between points for *all* distances. The calculation of K is fairly simple: it consists of dividing the mean sum of the number of points at different distance lags for each point by the area event density. For example, for point $S1$ we draw circles, each of varying radius $d$, centered on that point. We then count the number of points (events) inside each circle. We repeat this for point $S2$ and all other points $Si$. Next, we compute the average number of points in each circle then divide that number by the overall point density $\hat{\lambda}$ (i.e. total number of events per study area).

<table>


<td style="width:30%;">
<img src="img/K_bands.png" width=300> </img>
</td>

<td style="width:350px !important">
 <table style="width:75%;">
 <tr>
 <th>Distance <br>band <br>(km) </th><th>	# events <br>from S~1~</th><th>	# events <br> from S~2~ </th><th>	# events<br> from S~i~ </th><th> K </th>
 </tr>
 <tr>
 <td>10 </td><td>	0	</td><td> 1  </td><td>	... </td><td>	0.012 </td>
 </tr><tr>
 <td>20 </td><td>	3 </td><td>	5	 </td><td> ...	</td><td> 0.067 </td>
 </tr><tr>
 <td>30 </td><td>	9 </td><td>	14 </td><td> ... </td><td> 0.153 </td>
 </tr><tr>
 <td>40 </td><td>	17 </td><td> 17 </td><td> ... </td><td>	0.269 </td>
 </tr><tr>
 <td>50 </td><td> 25 </td><td> 23 </td><td> ... </td><td> 0.419 </td>
 </tr>
 </table>
</td>

</table><br>


We can then plot K and compare that plot to a plot we would expect to get if an IRP/CSR process was at play (K~expected~).

<div class="note">
<p>K-function calculated from the Walmart stores point distribution in MA (shown in black) compared to<span class="math inline"><em>K</em><sub><em>e</em><em>x</em><em>p</em><em>e</em><em>c</em><em>t</em><em>e</em><em>d</em></sub></span> under the IRP/CSR assumption (shown in red).</p>
</div>

K values greater than $K_{expected}$ indicates a greater number of points at that distance (more clustered); K values less than $K_{expected}$ indicates fewer number of points at that distance (more dispersed).

Note that like the ANN analysis, the $K$-function assumes stationarity in the underlying point process (i.e. that there is no overall drift or trend in the  process' intensity). 

#### L function

One problem with the $K_{expected}$ is that the shape of the function tends to curve upward making it difficult to see small differences between K and $K_{expected}$. A work-around is to transform the values in such a way that the expected values, $K_{expected}$, lie horizontal. The transformation is calculated as follows:

$$
\begin{equation}
L=\sqrt{\dfrac{K(d)}{\pi}}-d
\label{eq:L-function}
\end{equation}
$$


The above $\hat{K}$ is transformed to the following plot (note how the $K_{expecetd}$ red line is now perfectly horizontal)


<div class="figure">
<img src="img/L_function.svg" alt="L-function (a simple transformation of the K-function). This graph makes it easier to compare K with K~expected~ at lower distance values. It appears that Walmart locations are more clustered than expected under CSR/IRP up to a distance of 12 km but more dispersed at distances greater than 12 km."  />
<p class="caption">(\#fig:f11-L)L-function (a simple transformation of the K-function). This graph makes it easier to compare K with K~expected~ at lower distance values. It appears that Walmart locations are more clustered than expected under CSR/IRP up to a distance of 12 km but more dispersed at distances greater than 12 km.</p>
</div>

### The Pair Correlation Function $g$

A shortcoming of the $K$ function (and by extension the $L$ function) is its cumulative nature which makes it difficult to know at exactly which distances a point pattern may stray from $K_{expected}$ since *all* points up to distance $r$ can contribute to $K(r)$. The **pair correlation function**, $g$, is a modified version of the $K$ function where instead of summing *all* points within a distance $r$, points falling within a narrow distance *band* are summed instead.  

<div class="figure">
<img src="img/K_vs_g_bands.png" alt="Difference in how the $K$ and $g$ functions aggregate points at distance $r$ ($r$ = 30 km in this example). *All* points *up to* $r$ contribute to $K$ whereas just the points in the *annulus band* at $r$ contribute to $g$." width="632" />
<p class="caption">(\#fig:f11-k-g)Difference in how the $K$ and $g$ functions aggregate points at distance $r$ ($r$ = 30 km in this example). *All* points *up to* $r$ contribute to $K$ whereas just the points in the *annulus band* at $r$ contribute to $g$.</p>
</div>

The plot and interpretation of the $g$ function differs from that of the $K$ and $L$ functions.

<div class="figure">
<img src="img/g_function.svg" alt="$g$-function of the Massachusets Walmart point data. Its interpretation is  similar to that of the $K$ and $L$ functions. Here, we observe distances between stores greater than expected under CSR up to about 5 km. Note that this cutoff is less than the 12 km cutoff observed with the $K$ function; this can be explained by the point pattern at the shorter $r$ distances contributing to the $K$ values at higher $r$ values--a problem avoided using the $g$-function." width="400" />
<p class="caption">(\#fig:f11-g)$g$-function of the Massachusets Walmart point data. Its interpretation is  similar to that of the $K$ and $L$ functions. Here, we observe distances between stores greater than expected under CSR up to about 5 km. Note that this cutoff is less than the 12 km cutoff observed with the $K$ function; this can be explained by the point pattern at the shorter $r$ distances contributing to the $K$ values at higher $r$ values--a problem avoided using the $g$-function.</p>
</div>

If $g(r)$ = 1, then the inter-point distances (at and around distance $r$) are consistant with CSR. If $g(r)$ > 1, then the points are more clustered than expected under CSR. If $g(r)$ < 1, then the points are more dispersed than expected under CSR. Note that $g$ can never be less than 0.

Like its $K$ counterpart, the $g$-function assumes stationarity in the underlying point process (i.e. that there is no overall drift or trend in the  process' intensity). 

## First and second order effects

The concept of 1^st^ order effects and 2^nd^ order effects is an important one. It underlies the basic principles of spatial analysis. 

<div class="figure">
<img src="img/1st_2nd_order_property.png" alt="Tree distribution can be influenced by 1^st^ order effects such as elevation gradient of spatial distribution of soil characteristics; this, in turn, changes the  tree density distribution across the study area. Tree distribution can also be influenced by 2^nd^ order effects such as seed dispersal processes where the process is independent of location and, instead, dependent on the presence of other trees." width="750" />
<p class="caption">(\#fig:f11-1st-2nd-effects)Tree distribution can be influenced by 1^st^ order effects such as elevation gradient of spatial distribution of soil characteristics; this, in turn, changes the  tree density distribution across the study area. Tree distribution can also be influenced by 2^nd^ order effects such as seed dispersal processes where the process is independent of location and, instead, dependent on the presence of other trees.</p>
</div>

Density based measurements such as kernel density estimations look at the *1^st^ order* property of the underlying process. Distance based measurements such as ANN and K-functions focus on the *2^nd^ order* property of the underlying process. 

It's important to note that it is seldom feasible to separate out the two effects when analyzing the data, thus the importance on relying on a priori knowledge of the phenomena being investigated before drawing any conclusions from the analyses results.

