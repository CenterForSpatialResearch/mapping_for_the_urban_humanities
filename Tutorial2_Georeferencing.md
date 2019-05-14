## Tutorial 2: Georeferencing a scanned paper map

#### Premise

In this exercise, we will create spatial data from a scanned paper map. As far as a computer program (such as QGIS) is concerned, a scanned map is an image, and the geographic information contained within it is largely incomprehensible to a computer. So, while an image is human-readable as a map, it is not "computer-readable," so to speak.

The first thing we need to do to transform a scanned paper map into a map that a computer can read is to *georeference* it. This means that we will match spots on the image with coordinates on a map. Though we will use a webmap for this (Open Street Maps), it could be done with any map that has coordinate information embedded in it.

In the second part of this tutorial, we will take this georeferenced map and digitize some of the features on it to make a new dataset that can then be used with this map or imported into other projects as a shapefile itself.

In this tutorial, we will explore some of the georeferencing tools available in QGIS and use them to georeference a 1902 map of the Bronx. You will learn how to use GIS tools to georeference raster datasets. You will use the georeferenced map for the next exercise where you will digitize vector features from the map information.

#### Notes on the data:

The map you will be using for this exercise is one sheet of six from "Map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" published in 1902.  This map is from the Columbia Map collection and is an exceptionally detailed, large scale (1:7,200) series made shortly after the area east of the Bronx River was annexed from Westchester to the Bronx, and the Bronx was consolidated into New York City and New York County. The library catalog record for the map can be found [here](https://clio.columbia.edu/catalog/9282162). If you would like to see the entire map, there is another copy (in a lower resolution) in the New York Public Libraries digital collections [here](http://digitalcollections.nypl.org/items/dc910ee0-4682-0131-4759-58d385a7bbd0)

You are going to use [OpenStreetMap](https://www.openstreetmap.org/about) (OSM)  as reference data for the georeferencing process. OSM provides a free, open-source map of the world from public domain and volunteered data.

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials.

#### Setting up QGIS

Open QGIS:

![open]

You are going to use OSM data as the reference data for the georeferencing process. You can view the OSM web basemap service directly through QGIS. One way to do this is to connect to OSM directly through the QGIS browser.  Expand "XYZ Tiles" in the QGIS browser listing and click on OpenStreetMap:

![XYZ Tiles]

Since you are working in a new QGIS project, the map should show the entire earth as the default:
![OSM]

Use the zoom-in tool ![zoom tool] and zoom into the Central Bronx in the area around The Botanical Garden:

![garden zoom]

Now you will access the georeferencing tools and match the scanned map to the OSM map.

Under the Raster menu,<!--Georeferencer was not automatically activated on my version. May have to manually activate on others.--> select Georeferencer..:

![georeferencer]

The Georeferencer screen will open:

![georeferencer window]

Click on the Add Raster button ![Add Raster] and navigate to the JPEG image "Bronx1902Sheet2_Edit.jpg" from the class files in the directory Class_Data/Tutorial2_Georeferencing.

It will appear in the georeferencer window:

![georeferencer window with map]

This map is one sheet of six of a map of the East Bronx in 1902.  This section represents the area around the New York Botanical Garden and the (then new) Bronx Zoo. Fordham University can be seen just to the southwest of the garden and the Norwood neighborhood is in the northeast corner. The area to the east of the Bronx Park area is still largely undeveloped at this point.

Historical maps can be difficult to georeference, and this sheet illustrates a number of the complications that can arise. The map projection is unclear and there are no ground control points or coordinates specified on the image itself. Because of this, you will georeference by matching physical features represented on the map with their current counterparts (and their known coordinates). However, most of the features in this map have changed or no longer exist (or were never actually built in the first place). Thus, you will need to be very careful to choose locations that you are confident match up well with their contemporary counterparts. Fortunately, there are a number of good candidates, particularly on the western half of the map where many streets and buildings still exist in the same location. You can use these landmarks to georeference the map.

The QGIS georeferencer does not allow you to view both the scanned map and the workspace at the same time, so you will have to inspect both maps in turn and choose carefully to select locations to add georeferencing control points.
One candidate is the Haupt Conservatory in the Botanical Garden which continues to exist largely its original configuration. Use the georeferencer zoom tools ![zoom tools] to zoom to the conservatory structure in the southwest corner of the park:

![Conservatory]

![Conservatory zoom]

Identify as precise a location as possible (a corner of the building will work nicely) and click on it in the georeferencing window using the add point tool ![Add Point] When you do so, the Enter map coordinates window appears:

![Enter Coords]

If you knew the coordinates of this location, you could now add them manually, but since you do not, you can select them from the OSM data in the main QGIS window. Click on the ![From map canvas] button to see the QGIS workspace.
You may want to zoom in very closely to the conservatory.

![osm conservatory]

Once you do so, you will need to reactivate the add point tool ![Add Point] by maximizing the georeferencing window and clicking the ![From map canvas] button again. Once you select the same location on the workspace window, you will automatically be brought back to the georeferencing window where the assigned coordinates will be imputed.

![Coordinates imputed]

At this point, if you are dissatisfied, you can move the assigned control points with the move GCP point tool ![Move Point] or delete it entirely and start over with the delete point tool ![Delete Point].
If satisfied, click the OK button and the point will be assigned and appear on the map.

A link table entry will be generated on the bottom of the window:

![Link Table]

To add a second point, repeat the same process. It is a good idea to choose another point in a different portion of the map. A street intersection or corner from the western portion of the map will work well for this as most of those streets continue to exist in the same configuration.

Here, I have zoomed in to the northwestern most potion of the map where I add a ground control point at the very center of the intersection of Gun Hill Road and Tryon Ave:

![Intersection]

Repeat the same steps to select the center of the same intersection from the OSM map and add the locations to the link table:

![Intersection link]

You must add a minimum of four points to complete the georeferencing (although more is generally better). Generate at least two more points on your own and add them to the link table.

Be careful to make sure that the control points you add match. This can be quite tricky as many of the features have changed or were not actually built as planned.

Normally it is a good idea to choose control points from throughout the map. However, in this case this will be difficult as there are few features in the eastern sections of the map that can be reliably associated with contemporary locations.

In this example, I selected six control points:

![Six points]

It is good practice to save the table of control points at this stage. Choose “Save GCP points as” under the file menu and save it in the .points format in the same location as the image. This will allow you to later recreate the work you have done:

![Save points]

Next, you will “transform” the image and create a georeferenced version of the scanned map image. In the georeferencer window, select transformation settings under the settings window:

![Transform]

Make the following selections:

Transformation type: `Polynomial 1`

Resampling Method: `Cubic` (usually used for images and photos)

Output Raster: *save this in the same folder you are working in*

Target SRS: `EPSG:3857` (*this is the pseudo Mercator projection used in the OSM data — you may have to manually add this*)

You should also opt to have the georeferenced layer "Load in QGIS when done":

![Transformation Settings]

Close the settings options and click on the start georeferencing button ![Start Referencing].

After the transformation finishes, you should see the map appear in the QGIS workspace:

![georeferenced map]

You can make the scanned map layer partially transparent in the layer properties.  Right click on the map in the layer panel and select properties:

![properties]

On the left panel in the properties dialog, select Transparency, here you can adjust the global transparency with a slider:

![transparency]

Compare the georeferenced map with the Open Street Map layer.  Make sure that features appear to match up closely:

![review]

In the next exercise you will be using the sheet you georeferenced here and digitize some of the features from it.


______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2019 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

[open]: Images/2019/GeoRef1.png
[XYZ Tiles]: Images/2019/GeoRef2.png
[OSM]: Images/2019/GeoRef3.png
[zoom tool]: Images/2019/GeoRef4.png
[garden zoom]: Images/2019/GeoRef5.png
[georeferencer]: Images/2019/GeoRef6.png
[georeferencer window]: Images/2019/GeoRef7.png
[Add Raster]: Images/2019/GeoRef8.png
[georeferencer window with map]: Images/2019/GeoRef9.png
[zoom tools]: Images/2019/GeoRef10.png
[Conservatory]: Images/2019/GeoRef11.png
[Conservatory zoom]: Images/2019/GeoRef12.png
[Add Point]: Images/2019/GeoRef13.png
[Enter Coords]: Images/2019/GeoRef14.png
[From map canvas]: Images/2019/GeoRef15.png
[osm conservatory]: Images/2019/GeoRef16.png
[Coordinates imputed]: Images/2019/GeoRef19.png
[Move Point]: Images/2019/GeoRef20.png
[Delete Point]: Images/2019/GeoRef21.png
[Link Table]: Images/2019/GeoRef22.png
[Intersection]: Images/2019/GeoRef23.png
[Intersection link]: Images/2019/GeoRef24.png
[Six points]: Images/2019/GeoRef25.png
[Save points]: Images/2019/GeoRef26.png
[Transform]: Images/2019/GeoRef27.png
[Transformation Settings]: Images/2019/GeoRef28.png
[Start Referencing]: Images/2019/GeoRef29.png
[georeferenced map]: Images/2019/GeoRef30.png
[properties]: Images/2019/GeoRef31.png
[transparency]: Images/2019/GeoRef32.png
[review]: Images/2019/GeoRef33.png
