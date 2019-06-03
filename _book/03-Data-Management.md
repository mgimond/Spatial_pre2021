
# GIS Data Management


## GIS File Data Formats

In the GIS world, you will encounter many different GIS file formats. Some file formats are unique to specific GIS applications, others are universal. For this course, we will focus on a subset of spatial data file formats: **shapefiles** for vector data, **imagine** and **GeoTiff** files for rasters and **file geodatabases** for both vector and raster data.

### Vector Data File Formats

#### Shapefile

A **shapefile** is a file-based data format native to ArcView 3.x software (a much older version of ArcMap). Conceptually, a shapefile is a feature class--it stores a collection of features that have the same geometry type (point, line, or polygon), the same attributes, and a common spatial extent. 

Despite what its name may imply, a "single" shapefile is actually composed of at least three files, and as many as eight. Each file that makes up a "shapefile" has a common filename but different extension type. 

The list of files that define a "shapefile" are shown in the following table. Note that each file has a specific role in defining a shapefile. 

File extension |	Content
---------------|------------
.dbf |	Attribute information
.shp |	Feature geometry
.shx |	Feature geometry index
.aih |	Attribute index
.ain |	Attribute index
.prj |	Coordinate system information
.sbn |	Spatial index file
.sbx |	Spatial index file


#### File Geodatabase

A **file geodatabase** is a relational database storage format. It's a far more complex data structure than the shapefile and consists of a **.gdb** folder housing dozens of files. Its complexity renders it more versatile allowing it to store multiple feature classes and enabling topological definitions (i.e. allowing the user to define rules that govern the way different feature classes relate to one another). An example of the contents of a geodatabase is shown in the following figure.

<div class="figure">
<img src="img/geodatabase.jpg" alt="Sample content of an ArcGIS file geodatabase." width="500" />
<p class="caption">(\#fig:f02-gdb)Sample content of an ArcGIS file geodatabase.</p>
</div>

#### GeoPackage

This is a relatively new data format that follows [open format standards](https://en.wikipedia.org/wiki/Open_format) (i.e. it is non-proprietary). It's built on top of SQLite (a self-contained relational database). Its one big advantage over many other vector formats is its compactness--coordinate value, metadata, attribute table, projection information, etc..., are all stored in a *single* file which facilitates portability. Its filename usually ends in `.gpkg`. Applications such as QGIS (2.12 and up), R and ArcGIS will recognize this format (ArcGIS version 10.2.2 and above will read the file from ArcCatalog but requires a script to create a GeoPackage).


### Raster Data File Formats

Rasters are in part defined by their pixel depth. Pixel depth defines the range of distinct values the raster can store. For example, a 1-bit raster can only store 2 distinct values: 0 and 1.

<img src="03-Data-Management_files/figure-html/unnamed-chunk-2-1.png" width="288" />

There is a wide range of raster file formats used in the GIS world. Some of the most popular ones are listed below.

#### Imagine

The **Imagine** file format was originally created by an image processing software company called ERDAS. This file format consists of a single **.img** file. This is a simpler file format than the shapefile. It is sometimes accompanied by an .xml file which usually stores metadata information about the raster layer.

#### GeoTiff

A popular public domain raster data format is the **GeoTIFF** format. If maximum portability and platform independence is important, this file format may be a good choice.

#### File Geodatabase

A raster file can also be stored in a file geodatabase alongside vector files. Geodatabases have the benefit of defining image mosaic structures thus allowing the user to create “stitched” images from multiple image files stored in the geodatabase. Also, processing very large raster files can be computationally more efficient when stored in a file geodatabase as opposed to an Imagine or GeoTiff file format.

## Managing GIS Files

Unless you are intimately familiar with the file structure of a GIS file, it is best to copy/move/delete GIS files from within the software environment. **ArcCatalog** (part of the ArcGIS suite) acts like a Windows file management environment with the added benefit that it recognizes GIS files. 

<div class="figure">
<img src="img/ArcCatalog.jpg" alt="Windows Explorer view vs. ArcCatalog view. Note how the many files that make up the Parks shapefile (as viewed in a Windows Explorer environment) appears as a single entry in the ArcCatalog view. This makes it easier to rename the shapefile since it needs to be done only for a single entry in ArcCatalog (as opposed to renaming the Parks files seven times in the Windows Explorer environment)." width="300" />
<p class="caption">(\#fig:f02-catalog)Windows Explorer view vs. ArcCatalog view. Note how the many files that make up the Parks shapefile (as viewed in a Windows Explorer environment) appears as a single entry in the ArcCatalog view. This makes it easier to rename the shapefile since it needs to be done only for a single entry in ArcCatalog (as opposed to renaming the Parks files seven times in the Windows Explorer environment).</p>
</div>


## Managing a Map Project in ArcGIS

Unlike many other software environments such as word processors and spreadsheets, a GIS map project is not self-contained in a single file. A GIS map consists of many files: ArcMap's **.mxd** file and the various vector and/or raster files used in the map project. The .mxd file only stores information about how the different layers are to be symbolized and the GIS file locations these layers point to.

Because of the complex data structure associated with GIS maps, it's usually best to store the .mxd and all associated GIS files under a single project directory. Then, when you are ready to share your map project with someone else, just pass along that project folder as is or compressed in a zip or tar file.

Because .mxd map files read data from GIS files, it must know where to find these files on your computer or across the network. There are two ways in which a map document can store the location to the GIS files: as a **relative pathname** or a **full pathname**. 

A *relative pathname* defines the location of the GIS files relative to the location of the .mxd file on your computer. For example, let's say that you created a project folder called HW05 under D:/Username/. In that folder, you have a map document, Map.mxd, that displays two layers stored in the GIS files Roads.shp and Cities.shp. In this scenario, the .mxd document and shapefiles are in the same project folder. If you set the **Pathnames** parameter to **"Store relative pathnames to data sources"** (accessed from ArcMap's **File >> Map Document Properties menu**) ArcMap will not need to know the entire directory structure above the HW05/ folder to find the two shapefiles as illustrated below. 


![](img/Directory_relative.svg)<!-- -->

If the **"Store relative pathnames to data sources"** is not checked in the map's document properties, then ArcMap will need to know the *entire* directory structure leading to the HW05/ folder as illustrated below.

![](img/Directory_full.svg)<!-- -->

Your choice of full vs relative pathnames matters if you find yourself having to move or copy your project folder to another directory structure. For example, if you share you HW05/ project folder with another user and that user places the project folder under a different directory structure such as C:/User/Jdoe/GIS/, ArcMap will not find the shapefiles if the pathnames is set to full (i.e. the _Store relative pathnames_ option is not checked). This will result in **exclamation marks** in your map document TOC. This problem can be avoided by making sure that the map document is set to use relative pathnames and by placing all GIS files (raster and vector) in a common project folder.

<div class="warning">
<p>NOTE: Exclamation marks in your map document indicate that the GIS files are missing or that the directory structure has changed.</p>
</div>

<img src="img/Exclamation_marks.jpg" width="100" />


