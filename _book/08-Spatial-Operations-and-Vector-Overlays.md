

# Spatial Operations and Vector Overlays


## Selection by Attribute

Features in a GIS layer can be selected graphically or by querying attribute values. For example, if a GIS layer represents land parcels, one could use the *Area* field to select all parcels having an area greater than 2.0 acres. 

**Set algebra** is used to define conditions that are to be satisfied while **Boolean algebra** is used to combine a *set* of conditions. 

### Set Algebra

Set algebra consists of four basic operators: 

 * less than (`<`), 
 * greater than (`>`), 
 * equal to (`=`)
 * not equal to (`<>`).

> In some programming environments (such as R and Python), the equality condition is presented as **two** equal signs, `==`, and not one. In such an environment `x = 3` is interpreted as "*pass the value 3 to x*" and `x == 3` is interpreted as "*is x equal to 3?*.


If you have a GIS layer of major cities and you want to identify all census tracts having a population count greater than 50000, you would write the expression as `"POP" > 50000` (of course, this assumes that the attribute field name for population count is `POP`).

<div class="figure">
<img src="img/Select_attribute_1.jpg" alt="An example of *selection by attributes* tool in ArcMap  where it is accessed from the *Selection* pull-down menu." width="358" />
<p class="caption">(\#fig:f08-sel1)An example of *selection by attributes* tool in ArcMap  where it is accessed from the *Selection* pull-down menu.</p>
</div>


<div class="figure">
<img src="img/Select_cities.svg" alt="Selected cities meeting the criterion are shown in cyan color."  />
<p class="caption">(\#fig:f08-sel1-result)Selected cities meeting the criterion are shown in cyan color.</p>
</div>


The result of this operation is a selected subset of the Cities point layer. Note that in most GIS applications the selection process *does not* create a new layer.

### Boolean Algebra

You can combine conditions from set algebra operations using the following Boolean algebra operators: 

 * `or` (two conditions *can* be met), 
 * `and` (two conditions *must* be met), 
 * `not` (condition *must not* be met).
 
Following up with the last example, let's now select cities having a population greater than 50000 and that are in the US (and not Canada or Mexico). Assuming that the country field is labeled `FIPS_CNTRY` we could setup the expression as `"POP" > 50000 AND "FIPS_CNTRY" = US`. Note that a value need not be numeric. In this example we are asking that an attribute value equal a specific string value (i.e. that it equal the string `'US'`).


<div class="figure">
<img src="img/Select_cities_2.svg" alt="Selected cities meeting `POP &gt; 50000` AND `FIPS_CNTRY == US` criteria are shown in cyan color."  />
<p class="caption">(\#fig:f08-sel2)Selected cities meeting `POP > 50000` AND `FIPS_CNTRY == US` criteria are shown in cyan color.</p>
</div>

## Selection by location

We can also select features from *one* GIS layer based on their spatial association with *another* GIS layer. This type of spatial association can be broken down into four categories: **adjacency** (whether features from one layer *share* a boundary with features of another), **containment** (whether features from one layer are *inside* features of another), **intersection** (whether features of one layer *intersect* features of another), and **distance** (whether one feature is within a certain *distance* from another).

Continuing with our working example, we might be interested in cities that are within 100 miles of recent earthquakes. The earthquake points are from another GIS layer called `Earthquakes (Sep 2013)`. 

<div class="figure">
<img src="img/Select_location_1.jpg" alt="An example of a *selection by location* tool in ArcMap  where it is accessed from the *Selection* pull-down menu." width="420" />
<p class="caption">(\#fig:f08-loc1)An example of a *selection by location* tool in ArcMap  where it is accessed from the *Selection* pull-down menu.</p>
</div>


<div class="figure">
<img src="img/Cities_earthquakes.svg" alt="Selected cities meeting the criterion are shown in cyan color." width="300" />
<p class="caption">(\#fig:f08-loc1-map)Selected cities meeting the criterion are shown in cyan color.</p>
</div>


You can, of course, combine multiple selection criteria (both by attribute and location), but be careful when selecting from an existing selection in ArcMap: in both the *Selection by Location* window and the *Selection by Attribute* window, you must explicitly set the option to *select from an existing selection*.
 
<img src="img/Select_from_selection.jpg" width="399" />

## Vector Overlay

<aside>
The concept of *vector overlay* is not new and goes back many decades--even before GIS became ubiquitous. It was once referred to as **sieve mapping** by land use planners who combined different layers--each mapped onto separate transparencies--to isolate or eliminate areas that did or did not meet a set of criteria.
</aside>

Map overlay refers to a group of procedures and techniques used in combining information from different data layers. This is an important capability of most GIS environments. Map overlays involve at least two input layers and result in at least one new output layer. A basic set of overlay tools include **clipping**, **intersecting** and **unioning**.

### Clip

**Clipping** takes one GIS layer (the *clip* feature) and another GIS layer (the to-be-clipped input feature). The output is a clipped version of the original input layer. The output attributes table is a subset of the original attributes table where only records for the clipped polygons are preserved.

![](img/Clip.svg)<!-- -->

### Intersect

**Intersecting** takes both layers as inputs then outputs the features from both layers that share the same spatial extent. Note that the output attribute table inherits attributes from *both* input layers (this differs from *clipping* where attributes from just one layer are carried through).

![](img/Intersect.svg)<!-- -->

### Union

**Unioning** overlays both input layers and outputs *all* features from the two layers. Features that overlap are intersected creating new polygons. This overlay usually produces more polygons than are present in both input layers combined. The output attributes table contains attribute values from *both* input features (note that only a *subset* of the output attributes table is shown in the following figure).

![](img/Union.svg)<!-- -->


