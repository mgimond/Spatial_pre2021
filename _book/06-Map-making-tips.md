# Good Map Making Tips



## Elements of a map

A map can be composed of many different map elements. They may include: Main map body, legend, title, scale indicator, orientation indicator, inset map and source and ancillary information.

Not all elements need to be present in a map. In fact, in some cases they may not be appropriate at all. A scale bar, for instance, may not be appropriate if the coordinate system used does not preserve distance across the map's extent. 

Knowing why and for whom a map is being made will dictate its layout. If it's to be included in a paper as a figure, then parsimony should be the guiding principle. If it's intended to be a standalone map, then additional map elements may be required. 

Knowing the intended audience should also dictate what you will convey and how. If it's a general audience with little technical expertise then a simpler presentation may be in order. If the audience is well versed in the topic, then the map may be more complex. 

<div class="figure">
<img src="img/Map_elements.png" alt="Map elements. Note that not all elements are needed, nor are they appropriate in some cases. Can you identify at least one element that does not belong in the map (hint, note the orientation of the longitudinal lines; are they parallel to one another? What implication does this have on the North direction and the placement of the North arrow?)"  />
<p class="caption">(\#fig:f06-map)Map elements. Note that not all elements are needed, nor are they appropriate in some cases. Can you identify at least one element that does not belong in the map (hint, note the orientation of the longitudinal lines; are they parallel to one another? What implication does this have on the North direction and the placement of the North arrow?)</p>
</div>



## How to create a *good* map

Here's an example of a map layout that showcases several bad practices.

<div class="figure">
<img src="img/Bad_map.jpg" alt="Example of a *bad* map. Can you identify the problematic elements in this map? " width="528" />
<p class="caption">(\#fig:Bad-map)Example of a *bad* map. Can you identify the problematic elements in this map? </p>
</div>

+ A good map establishes a **visual hierarchy** that ensures that the most important elements are at the top of this hierarchy and the least important are at the bottom. Typically, the top elements should consist of the main map body, the title (if this is a standalone map) and a legend (when appropriate).

+ When showcasing Choropleth maps, it's best to limit the **color swatches** to less than a dozen--it becomes difficult for the viewer to tie too many different colors in a map to a color swatch element in the legend. Also, classification breaks should not be chosen at random but should be chosen carefully; for example adopting a quantile classifications scheme to maximize the inclusion of the different color swatches in the map; or a classification system designed based on logical breaks (or easy to interpret breaks) when dictated by theory or cultural predisposition.

+ **Scale bars** and **north arrows** should be used judiciously and need *not* be present in *every* map. These elements are used to measure orientation and distances. Such elements are critical in reference maps such as USGS Topo maps and navigation maps but serve little purpose in a thematic map where the goal is to highlight *differences* between aerial units. If, however, these elements are to be placed in a thematic map, reduce their visual prominence (see Figure \@ref(fig:ScaleBar) for examples of scale bars). The same principle applies to the selection of an orientation indicator (north arrow) element. Use a small north arrow design if it is to be placed low in the hierarchy, larger if it is to be used as a reference (such as a nautical chart).


<div class="figure" style="text-align: center">
<img src="img/ScaleBar.svg" alt="Scale bar designs from simplest (top) to more complex (bottom). Use the simpler design if it's to be placed low in the visual hierarchy."  />
<p class="caption">(\#fig:ScaleBar)Scale bar designs from simplest (top) to more complex (bottom). Use the simpler design if it's to be placed low in the visual hierarchy.</p>
</div>

+ **Title** and other **text elements** should be concise and to the point. If the map is to be embedded in a write-up such as a journal article, book or web page, title and text(s) elements should be omitted in favor of figure captions and written description in the accompanying text.

Following the aforementioned guidelines can go a long way in producing a *good* map. Here, a divergent color scheme is chosen whereby the two hues converge to the median income value. A coordinate system that minimizes distance error measurements and that preserves "north" orientation across the main map's extent is chosen since a scale bar and north arrow are present in the map. The inset map (lower left map body) is placed lower in the visual hierarchy and could be omitted if the intended audience was familiar with the New England area. A unique (and unconventional) legend orders the color swatches in the order in which they appear in the map (i.e. following a strong north-south income gradient).


<div class="figure">
<img src="img/Good_map.jpg" alt="Example of an *improved* map." width="528" />
<p class="caption">(\#fig:Good-map)Example of an *improved* map.</p>
</div>

## Typefaces and Fonts

Maps may include text elements such as labels and ancillary text blocks. The choice of typeface (font family) and font (size, weight and style of a typeface) can impact the legibility of the map. A rule of thumb is to limit the number of fonts to two: a **serif** and a **sans serif** font.

<div class="figure">
<img src="img/Fonts.svg" alt="Serif fonts are characterized by brush strokes at the letter tips (circled in red in the figure). Sans Serif fonts are devoid of brush strokes."  />
<p class="caption">(\#fig:f06-serif)Serif fonts are characterized by brush strokes at the letter tips (circled in red in the figure). Sans Serif fonts are devoid of brush strokes.</p>
</div>


Serif fonts are generally used to label natural features such as mountain ridges and water body names. Sans serif fonts are usually used to label anthropogenic features such as roads, cities and countries.

Varying the typeset size across the map should be avoided unless a visual hierarchy of labels is desired. You also may want to stick with a single font color across the map unless the differences in categories need to be emphasized. In the following example, a snapshot of a map before (left) and after (right) highlight how manipulating typeset colors and styles (i.e. italic, bold) can have a desirable effect **if done properly**.

<div class="figure">
<img src="img/labels.svg" alt="The lack of typeset differences makes the map on the left difficult to differentiate county names from lake/river names. The judicious use of font colors and style on the right facilitate the separation of features." width="600" />
<p class="caption">(\#fig:f06-typeset)The lack of typeset differences makes the map on the left difficult to differentiate county names from lake/river names. The judicious use of font colors and style on the right facilitate the separation of features.</p>
</div>
