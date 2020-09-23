# (PART) Appendix {-}



# Reading and writing spatial data in R{-#app1_1}

## Sample files for this exercise{-#app1_2}

First, you will need to download some sample files from the github repository.  Make sure to set your R session folder to the directory where you will want to save the sample files before running the following code chunks.



```r
download.file("http://github.com/mgimond/Spatial/raw/master/Data/Income_schooling.zip", 
              destfile = "Income_schooling.zip" , mode='wb')
unzip("Income_schooling.zip", exdir = ".")
file.remove("Income_schooling.zip")
```



```r
download.file("http://github.com/mgimond/Spatial/raw/master/Data/rail_inters.gpkg", 
              destfile = "./rail_inters.gpkg", mode='wb')
```


```r
download.file("http://github.com/mgimond/Spatial/raw/master/Data/elev.img",  
              destfile = "./elev.img", mode='wb')               
```

## Introduction {-#app1_3}

There are several different R spatial formats to choose from. Your choice of format will largely be dictated by the package(s) and or function(s) used in your workflow. A breakdown of formats and intended use are listed below.


<table class="table table-striped table-hover table-condensed" style="width: auto !important; ">
 <thead>
  <tr>
   <th style="text-align:right;color: white !important;background-color: #6E6E6E !important;text-align: center;"> Data format </th>
   <th style="text-align:center;color: white !important;background-color: #6E6E6E !important;text-align: center;"> Used with... </th>
   <th style="text-align:center;color: white !important;background-color: #6E6E6E !important;text-align: center;"> Used in package... </th>
   <th style="text-align:left;color: white !important;background-color: #6E6E6E !important;text-align: center;"> Used for... </th>
   <th style="text-align:left;color: white !important;background-color: #6E6E6E !important;text-align: center;"> Comment </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> `sf` </td>
   <td style="text-align:center;"> vector </td>
   <td style="text-align:center;"> `sf`, others </td>
   <td style="text-align:left;"> visualizing, manipulating, querying </td>
   <td style="text-align:left;"> This is likely to become the new spatial standard in R. Will also read from spatially enabled databases such as postgresSQL. </td>
  </tr>
  <tr>
   <td style="text-align:right;"> `raster` </td>
   <td style="text-align:center;"> raster </td>
   <td style="text-align:center;"> `raster`, others </td>
   <td style="text-align:left;"> visualizing, manipulating, spatial statistics </td>
   <td style="text-align:left;"> This is the most versatile raster format </td>
  </tr>
  <tr>
   <td style="text-align:right;"> `SpatialPoints*` 
 `SpatialPolygons*` 
 `SpatialLines*` 
 `SpatialGrid*` </td>
   <td style="text-align:center;"> vector and raster </td>
   <td style="text-align:center;"> `sp`, `spdep` </td>
   <td style="text-align:left;"> Visualizing, spatial statistics </td>
   <td style="text-align:left;"> May be superseded by `sf` in the future </td>
  </tr>
  <tr>
   <td style="text-align:right;"> `ppp` `owin` </td>
   <td style="text-align:center;"> vector </td>
   <td style="text-align:center;"> `spatstat` </td>
   <td style="text-align:left;"> Point pattern analysis/statistics </td>
   <td style="text-align:left;"> NA </td>
  </tr>
  <tr>
   <td style="text-align:right;"> `im` </td>
   <td style="text-align:center;"> raster </td>
   <td style="text-align:center;"> `spatstat` </td>
   <td style="text-align:left;"> Point pattern analysis/statistics </td>
   <td style="text-align:left;"> NA </td>
  </tr>
</tbody>
<tfoot><tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>1</sup> The `spatial*` format includes SpatialPointsDataFrame, SpatialPolygonsDataFrame, SpatialLinesDataFrame, etc...</td></tr></tfoot>
</table>


There is an attempt at standardizing the spatial format in the R ecosystem by adopting a well established set of spatial standards known as [simple features](https://en.wikipedia.org/wiki/Simple_Features). This effort results in a recently developed package called   [`sf`](https://r-spatial.github.io/sf/). It is therefore recommended that you work in an `sf` framework  when possible. As of this writing, most of the _basic_ data manipulation and visualization operations can be successfully conducted using `sf` spatial objects. 

Some packages such as `spdep` and `spatstat` require specialized data object types. This tutorial will highlight some useful conversion functions for this purpose.



## Creating spatial objects {-#app1_4}

The following sections demonstrate different spatial data object creation strategies.

### Reading a shapefile {-#app1_4_1}

Shapefiles consist of many files sharing the same core filename and different suffixes (i.e. file extensions). For example, the sample shapefile used in this exercise consists of the following files:


```
[1] "Income_schooling.dbf" "Income_schooling.prj" "Income_schooling.sbn" "Income_schooling.sbx"
[5] "Income_schooling.shp" "Income_schooling.shx"
```

Note that the number of files associated with a shapefile can vary. `sf` only needs to be given the `*.shp` name. It will then know which other files to read into R such as projection information and attribute table.


```r
library(sf)
s.sf <- st_read("Income_schooling.shp")
```

Let's view the first few records in the spatial data object. 


```r
head(s.sf, n=4)  # List spatial object and the first 4 attribute records
```

```
Simple feature collection with 4 features and 5 fields
geometry type:  MULTIPOLYGON
dimension:      XY
bbox:           xmin: 379071.8 ymin: 4936182 xmax: 596500.1 ymax: 5255569
projected CRS:  NAD83 / UTM zone 19N
         NAME Income   NoSchool NoSchoolSE IncomeSE                       geometry
1   Aroostook  21024 0.01338720 0.00140696  250.909 MULTIPOLYGON (((513821.1 51...
2    Somerset  21025 0.00521153 0.00115002  390.909 MULTIPOLYGON (((379071.8 50...
3 Piscataquis  21292 0.00633830 0.00212896  724.242 MULTIPOLYGON (((445039.5 51...
4   Penobscot  23307 0.00684534 0.00102545  242.424 MULTIPOLYGON (((472271.3 49...
```

Note that the `sf` object stores not only the geometry but the coordinate system information and attribute data as well. These will be explored later in this exercise.

### Reading a GeoPackage {-#app1_4_2}

A geopackage can store more than one layer. To list the layers available in the geopackage, type:


```r
st_layers("rail_inters.gpkg")
```

```
Driver: GPKG 
Available layers:
  layer_name     geometry_type features fields
1 Interstate Multi Line String       35      1
2       Rail Multi Line String      730      3
```

In this example, we have two separate layers: `Interstate` and `Rail`. We can extract each layer separately via the `layer=` parameter.


```r
inter.sf <- st_read("rail_inters.gpkg", layer="Interstate")
rail.sf  <- st_read("rail_inters.gpkg", layer="Rail")
```

### Reading a raster {-#app1_4_3}

The `raster` package will read many different raster file formats such as geoTiff, Imagine and HDF5 just to name a few. To see a list of supported raster file formats simply run `rgdal::gdalDrivers()` at a command prompt. The `rgdal` package is normally installed with your installation of `raster`.

In the following example, an _Imagine_ raster file is read into R.


```r
library(raster)
elev.r <- raster("elev.img")
```

What sets a `raster` object apart from other R data file objects is its storage. By default, data files are loaded into memory but `raster` objects are not. This can be convenient when working with raster files too large for memory. But this comes at a performance cost. If your RAM is large enough to handle your raster file, it's best to load the entire dataset into memory.

To check if the `elev.r` object is loaded into memory, run:


```r
inMemory(elev.r)
```

```
[1] FALSE
```

To force the raster into memory use `readAll()`:


```r
elev.r <- readAll(raster("elev.img"))
```

Let's check that the raster is indeed loaded into memory:


```r
inMemory(elev.r)
```

```
[1] TRUE
```

Now let's look at the raster's properties:


```r
elev.r
```

```
class      : RasterLayer 
dimensions : 994, 652, 648088  (nrow, ncol, ncell)
resolution : 500, 500  (x, y)
extent     : 336630.3, 662630.3, 4759303, 5256303  (xmin, xmax, ymin, ymax)
crs        : +proj=utm +zone=19 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs 
source     : memory
names      : elev 
values     : 0, 1546  (min, max)
```

The raster object returns its grid dimensions (number of rows and columns), pixel size/resolution (in the layer's coordinate system units), geographic extent, native coordinate system (UTM NAD83 Zone 19 with units of meters) and min/max raster values.

### Creating a spatial object from a data frame {-#app1_4_5}

Geographic point data locations recorded in a spreadsheet can be converted to a spatial point object. Note that it's important that you specify the coordinate system used to record the coordinate pairs since such information is not stored in a data frame. In the following example, the coordinate values are recorded in a WGS 1984 geographic coordinate system (`crs = 4326`).


```r
# Create a simple dataframe with lat/long values
df <- data.frame(lon = c(-68.783, -69.6458, -69.7653),
                 lat = c(44.8109, 44.5521, 44.3235),
                 Name= c("Bangor", "Waterville", "Augusta"))

# Convert the dataframe to a spatial object. Note that the
# crs= 4326 parameter assigns a WGS84 coordinate system to the 
# spatial object
p.sf <- st_as_sf(df, coords = c("lon", "lat"), crs = 4326) 
p.sf  
```

```
Simple feature collection with 3 features and 1 field
geometry type:  POINT
dimension:      XY
bbox:           xmin: -69.7653 ymin: 44.3235 xmax: -68.783 ymax: 44.8109
geographic CRS: WGS 84
        Name                 geometry
1     Bangor  POINT (-68.783 44.8109)
2 Waterville POINT (-69.6458 44.5521)
3    Augusta POINT (-69.7653 44.3235)
```

### Geocoding street addresses {-#app1_4_6}

The `ggmap` package offers a geocoding function called `mutate_geocode` which will take a table with physical addresses and create a new table with latitude and longitude values for those addresses. However, as of Spring 2019, `ggmap` will only access Google's API  which requires that a key be created on the Google Cloud (the latter will also require that a paid account be created with Google Cloud). The Data Science Toolkit, a previously free API alternative, has (as of May 2019) terminated its mapping services.

The Google API option will not be covered here, instead, the reader is encouraged to read the detailed instructions on `ggmap`'s [Github page](https://github.com/dkahle/ggmap).

For a free (but manual) alternative, you can use the US Census Bureau's [geocoding service](https://geocoding.geo.census.gov/geocoder/locations/addressbatch?form) for creating lat/lon values from US street addresses. This needs to be completed via their web interface and the resulting data table (a CSV file) would then need to be loaded into R as a data frame.

## Converting from an `sf` object {-#app1_5}

Packages such as `spdep` and `spatsat` currently do not support `sf` objects. The following sections demonstrate methods to convert from `sf` to other formats.

### Converting an `sf` object to a `Spatial*` object (`spdep`/`sp`) {-#app1_5_1}

The following code will convert point, polyline or polygon features to a `spatial*` object. In this example, an `sf` polygon feature is converted to a `SpatialPolygonsDataFrame` object.


```r
s.sp <- as(s.sf, "Spatial")
class(s.sp)
```

```
[1] "SpatialPolygonsDataFrame"
attr(,"package")
[1] "sp"
```

Note that if you wish to create a `Spatial*` object directly from a shapefile (and bypass the `sf` object creation), you could run the `maptools` function `readShapeSpatial("Income_schooling.shp")`. However, this approach _strips_ the coordinate system information from the spatial object.

### Converting an `sf` polygon object to an `owin` object {-#app1_5_2}

The `spatstat` package is normally used to analyze point patterns however, in most cases, the study extent needs to be explicitly defined by a polygon object. The polygon should be of class `owin`. Conversion from `sf` to `owin` requires the use of the `maptools` package.

Note that the attribute table gets stripped from the polygon data. This is usually fine given that the only reason for converting a polygon to an `owin` format is for delineating the study boundary.


```r
library(maptools)
s.owin <- as(s.sp, "owin")
class(s.owin)
```

```
[1] "owin"
```

### Converting an `sf` point object to a `ppp` object {-#app1_5_3}

As of this writing, it seems that you need to first convert the `sf` object to a `SpatialPoints*` before creating a `ppp` object as shown in the following code chunk. Note that the `maptools` package is required for this step.


```r
p.sp  <- as(p.sf, "Spatial")  # Create Spatial* object
p.ppp <- as(p.sp, "ppp")      # Create ppp object
```

```
Error in as.ppp.SpatialPointsDataFrame(from): Only projected coordinates may be converted to spatstat class objects
```


A `ppp` object is associated with the `spatstat` package which is designed to work off of a projected (cartesian) coordinate system. The error message reminds us that a geographic coordinate system (i.e. one that uses angular measurements such as latitude/longitude) cannot be used with this package. If you encounter this error, you will need to project the `p.sp` or `ps.f` layer to a projected coordinate system.

In this example, we'll project the `p.sf` object to a UTM coordinate system (`epsg=32619`). Coordinate systems in R are treated in a separate appendix. 


```r
p.sf.utm <- st_transform(p.sf, 32619) # project from geographic to UTM
p.sp  <- as(p.sf.utm, "Spatial")      # Create Spatial* object
p.ppp <- as(p.sp, "ppp")              # Create ppp object
class(p.ppp)
```

```
[1] "ppp"
```

Note that if the point layer has an attribute table, its attributes will be converted to `ppp` _marks_.

### Converting a `raster` object to an `im` object (`spatstat`) {-#app1_5_4}

The `maptools` package will readily convert a `raster` object to an `im` object using the `as.im.RasterLayer()` function.


```r
elev.im <- as.im.RasterLayer(elev.r) # From the maptools package
class(elev.im)
```

```
[1] "im"
```

## Converting to an `sf` object {-#app1_6}

All aforementioned spatial formats, except `owin`, can be coerced to an `sf` object via the `st_as_sf` function. for example:


```r
st_as_sf(p.ppp)  # For converting a ppp object to an sf object
st_as_sf(s.sp)   # For converting a Spatial* object to an sf object
```

## Dissecting the `sf` file object {-#app1_7}


```r
head(s.sf,3)
```

```
Simple feature collection with 3 features and 5 fields
geometry type:  MULTIPOLYGON
dimension:      XY
bbox:           xmin: 379071.8 ymin: 4936182 xmax: 596500.1 ymax: 5255569
projected CRS:  NAD83 / UTM zone 19N
         NAME Income   NoSchool NoSchoolSE IncomeSE                       geometry
1   Aroostook  21024 0.01338720 0.00140696  250.909 MULTIPOLYGON (((513821.1 51...
2    Somerset  21025 0.00521153 0.00115002  390.909 MULTIPOLYGON (((379071.8 50...
3 Piscataquis  21292 0.00633830 0.00212896  724.242 MULTIPOLYGON (((445039.5 51...
```

The first line of output gives us the geometry type, `MULTIPOLYGON`,  a multi-polygon data type. This is also referred to as a multipart polygon. A single-part `sf` polygon object will adopt the `POLYGON` geometry.

The next few lines of output give us the layer's bounding extent in the layer's native coordinate system units. You can extract the extent via the `extent()` function as in `extent(s.sf)`.

The next lines indicate the coordinate system used to define the polygon feature locations. It's offered in two formats: **epsg** code (when available) and **PROJ4** string format. You can extract the coordinate system information from an `sf` object via:


```r
st_crs(s.sf)
```

```
Coordinate Reference System:
  User input: NAD83 / UTM zone 19N 
  wkt:
PROJCRS["NAD83 / UTM zone 19N",
    BASEGEOGCRS["NAD83",
        DATUM["North American Datum 1983",
            ELLIPSOID["GRS 1980",6378137,298.257222101,
                LENGTHUNIT["metre",1]]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["degree",0.0174532925199433]],
        ID["EPSG",4269]],
    CONVERSION["UTM zone 19N",
        METHOD["Transverse Mercator",
            ID["EPSG",9807]],
        PARAMETER["Latitude of natural origin",0,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8801]],
        PARAMETER["Longitude of natural origin",-69,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8802]],
        PARAMETER["Scale factor at natural origin",0.9996,
            SCALEUNIT["unity",1],
            ID["EPSG",8805]],
        PARAMETER["False easting",500000,
            LENGTHUNIT["metre",1],
            ID["EPSG",8806]],
        PARAMETER["False northing",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8807]]],
    CS[Cartesian,2],
        AXIS["(E)",east,
            ORDER[1],
            LENGTHUNIT["metre",1]],
        AXIS["(N)",north,
            ORDER[2],
            LENGTHUNIT["metre",1]],
    ID["EPSG",26919]]
```

The output of this call is an object of class `crs`. Extracting the reference system from a spatial object can prove useful in certain workflows.

What remains of the `sf` summary output is the first few records of the attribute table. You can extract the object's table to a dedicated data frame via:


```r
s.df <- data.frame(s.sf)
class(s.df)
```

```
[1] "data.frame"
```

```r
head(s.df, 5)
```

```
         NAME Income   NoSchool  NoSchoolSE IncomeSE                       geometry
1   Aroostook  21024 0.01338720 0.001406960  250.909 MULTIPOLYGON (((513821.1 51...
2    Somerset  21025 0.00521153 0.001150020  390.909 MULTIPOLYGON (((379071.8 50...
3 Piscataquis  21292 0.00633830 0.002128960  724.242 MULTIPOLYGON (((445039.5 51...
4   Penobscot  23307 0.00684534 0.001025450  242.424 MULTIPOLYGON (((472271.3 49...
5  Washington  20015 0.00478188 0.000966036  327.273 MULTIPOLYGON (((645446.5 49...
```

The above chunk will also create a geometry column. This column is somewhat unique in that it stores its contents as a **list** of geometry coordinate pairs (polygon vertex coordinate values in this example).


```r
str(s.df)
```

```
'data.frame':	16 obs. of  6 variables:
 $ NAME      : chr  "Aroostook" "Somerset" "Piscataquis" "Penobscot" ...
 $ Income    : int  21024 21025 21292 23307 20015 21744 21885 23020 25652 24268 ...
 $ NoSchool  : num  0.01339 0.00521 0.00634 0.00685 0.00478 ...
 $ NoSchoolSE: num  0.001407 0.00115 0.002129 0.001025 0.000966 ...
 $ IncomeSE  : num  251 391 724 242 327 ...
 $ geometry  :sfc_MULTIPOLYGON of length 16; first list element: List of 1
  ..$ :List of 1
  .. ..$ : num [1:32, 1:2] 513821 513806 445039 422284 424687 ...
  ..- attr(*, "class")= chr [1:3] "XY" "MULTIPOLYGON" "sfg"
```

You can also opt to remove this column prior to creating the dataframe as follows:


```r
s.nogeom.df <- st_set_geometry(s.sf, NULL) 
class(s.nogeom.df)
```

```
[1] "data.frame"
```

```r
head(s.nogeom.df, 5)
```

```
         NAME Income   NoSchool  NoSchoolSE IncomeSE
1   Aroostook  21024 0.01338720 0.001406960  250.909
2    Somerset  21025 0.00521153 0.001150020  390.909
3 Piscataquis  21292 0.00633830 0.002128960  724.242
4   Penobscot  23307 0.00684534 0.001025450  242.424
5  Washington  20015 0.00478188 0.000966036  327.273
```

## Exporting to different data file formats {-#app1_8}

You can export an `sf` object to many different spatial file formats such as a shapefile or a geopackage.


```r
st_write(s.sf, "shapefile_out.shp", driver="ESRI Shapefile")  # create to a shapefile 
st_write(s.sf, " s.gpkg", driver="GPKG")  # Create a geopackage file
```

You can see a list of writable vector formats via a call to `subset(rgdal::ogrDrivers(), write == TRUE)`. Only as subset of the output is shown in the following example. Note that supported file formats will differ from platform to platform.


```
             name                       long_name write  copy isVector
18 ESRI Shapefile                  ESRI Shapefile  TRUE FALSE     TRUE
20     Geoconcept                      Geoconcept  TRUE FALSE     TRUE
21        GeoJSON                         GeoJSON  TRUE FALSE     TRUE
22     GeoJSONSeq                GeoJSON Sequence  TRUE FALSE     TRUE
24         GeoRSS                          GeoRSS  TRUE FALSE     TRUE
25            GFT            Google Fusion Tables  TRUE FALSE     TRUE
26            GML Geography Markup Language (GML)  TRUE FALSE     TRUE
```


The value in the `name` column is the driver name used in the `st_write()` function.

To export a raster to a data file, use `writeRaster()` from the `raster` package.


```r
writeRaster(elev.r, "elev_out.tif", format="GTiff" ) # Create a geoTiff file
writeRaster(elev.r, "elev_out.img", format="HFA" )  # Create an Imagine raster file
```

You can see a list of writable raster formats via a call to `subset(rgdal::gdalDrivers(), create == TRUE)`. 


```
        name                            long_name create  copy isRaster
40      FITS      Flexible Image Transport System   TRUE FALSE     TRUE
46      GPKG                           GeoPackage   TRUE  TRUE     TRUE
49     GS7BG Golden Software 7 Binary Grid (.grd)   TRUE  TRUE     TRUE
51      GSBG   Golden Software Binary Grid (.grd)   TRUE  TRUE     TRUE
53     GTiff                              GeoTIFF   TRUE  TRUE     TRUE
54       GTX             NOAA Vertical Datum .GTX   TRUE FALSE     TRUE
57 HDF4Image                         HDF4 Dataset   TRUE FALSE     TRUE
```

The value in the `name` column is the format parameter name used in the `writeRaster()` function.

