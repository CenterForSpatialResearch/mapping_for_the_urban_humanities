## Tutorial 3: Digitizing Features from a georeferenced map

#### Premise

In this exercise, you will *create your own dataset* by outlining the trees that were represented in the "1902 map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" that we previously georeferenced. Making new data from historic maps is a fairly common, if laborious, practice. In many cases, the data we are interested in is not digitized, so we have to translate it ourselves. This process can be compared to digitizing books handwritten in script by typing them. It is time-intensitve, but sometimes, it is the only way to get the data we need in a format a computer can read.

Through this tutorial, you will explore some of the on-screen hand digitizing tools available in QGIS and use them to digitize trees, paths and other features from a georeferenced map. In essence, you will be converting raster spatial data into vector-based features.

#### Notes on the data:

The map you will be using for this exercise is the map sheet from "Map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" that you georeferenced in the previous exercise. If you have not already done so, please complete [Tutorial 2: Georeferencing](https://github.com/CenterForSpatialResearch/mapping_for_the_urban_humanities/blob/master/Tutorial2_Georeferencing.md) exercise.

### Digitizing Exercise

Open a **new project** in QGIS.

Since we already georeferenced our map, you only need to load the georeferenced tiff file. In the process of georeferencing it, we aligned the image with spatial information that QGIS can understand. It is now similar to the raster file for the gridded population of the world that we used in Part I. This is important because we can now combine other datasets such as historic or current population data, maps showing development in the intervening years, or other datasets. We can also use the data that was drawn onto this map and combine it with other datasets once we translate it from the scanned version into a digitized version.

Let's start with our map.

Click on the Data Source Manager button ![Data Source] choose raster and navigate to the georeferenced image you made in the [Tutorial 2: Georeferencing](https://github.com/CenterForSpatialResearch/mapping_for_the_urban_humanities/blob/master/Tutorial2_Georeferencing.md) exercise.  Click Add:

![Add Map]

Since you verified its accuracy already, you will not need any basemap data for this exercise, so your project will look like this:

![Map Sheet]

This map is part of a very large-scale plan and the Bronx park area, which contains the then-new botanical garden and zoo, is particularly detailed. Every structure, road, walking path, and tree is mapped. We would like to be able to use this data in another setting, so we will digitize some of the features. We will start by digitizing trees. For the trees, we will use point geometry, so this will be a particularly simple dataset.

Zoom into the southwest corner of Bronx Park, where the Conservatory garden and library are (labeled "museum" on the map):

![zoomed map]

We will create a New Shapefile layer consisting of points. Navigate to Layer >> Create Layer >> New Shapefile Layer:

![New Shapefile]

In top of the New Shapefile Layer dialog box, save the new file in the same directory with your map, and name it "BronxParkTrees". Choose geometry type “Point”. Assign the same EPSG:3857 Pseudo-Mercator projection you used for the map in the previous exercise.  

Every point will have its own unique ID that you will have to enter.  If you want to attach more data, you can create additional attribute fields for your dataset. It is best practice to separate all of the data types into different attributes (i.e., if you had data about the age of the tree, you would make another attribute field for "Age," etc.). When making data, having additional specific categories is always preferable to having a smaller table.

In the "New Field" Name box, enter the Name, "Type," to create a new attribute (We might fill this attribute with values such as "Maple," "Walnut," or "London Plane.").  Choose attribute type "Text Data" and click ![Add to Fields List] then click `OK`:

![New Layer Settings]

The layer will now appear in the Layers panel:

![Layers List]

Now click on the BronxParksTrees Layer to activate it and turn on editing by clicking on the Toggle Editing Tool ![Toggle editing]

![Editing Mode]

Now the `Add Features` ![Add features] tool should be available. Click on the ![Add features] to begin digitizing trees.  This tool gives us a crosshair cursor. For every tree (or other data point) we want to add, all we have to do is click on it. An attribute dialog appears where we can type in attribute information for the feature we just created:

![Attribute entry]

There is no information on the map in regards to the type of tree; however, I happen to know that the trees in front of the library are a stand of stately tulips, so we can enter that information now. We will give each tree a unique id so that we can reference them later (unfortunately, QGIS does not do this automatically, and doing this manually is prone to errors. However, it is still worth doing as it is much easier to work with data where the rows have unique identifiers). It is generally best practice to make these identifiers simple and uniform. For example, while "3rd tree on the left after the museum" is unique and probably refers to one and only one tree, this naming system would be difficult to make consistent in our dataset. This is obviously a silly example, but the issue becomes much more relevant if we think about buildings, names, or even states (i.e., New York is unique, but NY is a better identifier — simpler, but also because other states also begin with "New"). For our trees example, I'm just going to use sequential numbers.

Click `OK` when finished.

Continue to digitize trees in this corner of the park:

![More trees]

We can move or edit the point features with the Vertex Tool, click ![vertex tool] and then click on the desired point to select it:

![select point]

 You can manually move a selected point with the mouse or delete it with the delete key on the keyboard:

 ![move point]

  It is a good idea to regularly use the “save for all layers” function, under the Current Edits menu ![current edits], to save your work as you digitize:

![Save Feature]

When finished, depress the toggle editing tool ![Toggle editing] to close the editing session and save your changes to the layer.

We are also interested in where the park pathways were situated. However, in order to do this, we will need to create another new shapefile layer. The reason for this is that the pathways will be made with lines, while the trees were made points. It is best practice to keep different types of shapes (points, lines, and polygons) separate (luckily, QGIS won't let us make them all as the same file anyhow). This is a general principle to keep in mind when making data. When working with datasets, the more uniform the dataset is, the better, and the less information per bin, the better. So, whether it is breaking up different data types, or separating each datum into its own bin, we want to organize our data by categories rather than human-readable things like words.

So let's get started with digitizing the park pathways. Create another new shapefile layer as above (Layer >> Create Layer >> New Shapefile Layer). This time, use `BronxParkPaths` as the name. Select "Line" as the vector type. Again assign the same EPSG:3857 Pseudo-Mercator projection.  I'm going to include the "Path Type" attribute to keep track of if the path is for a "major" or "minor" path. The only thing I will type into this box is "major" or "minor" (in all lowercase). If I wanted to make a sub-type of either of these categories, I would have to add another attribute.

![New Line Layer]

Now when you toggle on editing and select the add features tool ![Add Line features]. You will be digitizing line features. As you click with the add features tool you can continue to add as many vertices to the line as you wish. To complete the line segment, use the right mouse button.

Line features are more complex than the point features, so we need to consider a few more dimensions (pun intended :) ). Since these streets are so detailed, we could potentially digitize everything from the path outlines to the curbs; this is more detail than we need. For our analysis, we are less concerned with the outline of the paths (the space they take up) and more concerned with where the paths were situated. Therefore, we are going to digitize the "centerline," using a single line feature to represent the center of the path feature.

We also must decide where to begin and end the individual line features. A common practice is to create individual features between every intersection, ending each feature at the next intersection. This is advantageous because we can represent the connectivity of the features, essentially modeling a network. But doing it this way means that we must make sure that the connecting features are exactly coincident. QGIS has a handy feature to help with this: snapping tolerances. Snapping tools will automatically adjust the digitizing tools and "snap" them to specified features as the cursor gets sufficiently close.

To activate and customize the snapping tools, navigate to Settings >> Options:

![Settings Options]

In the Options dialog, choose the Digitizing tabs and navigate to the snapping options:

![Digitizing options]

Set the snapping options for the current layer to be within 10 map units of a vertex (our map units are meters, based on the projection we are working in):

Check on `Enable snapping by default`

Default snap mode: `Vertex`

Default snapping tolerance: `10.00000` `map units`

![Digitizing settings]

Click `OK`

Now the `Add feature` tool will automatically snap to another feature’s vertex whenever the cursor comes within 10 meters.

Activate `Editing Mode` and select the add features tool ![Add Line features]. Be careful to keep each vertex as close to the center of the street as possible. The more vertices you add, the smoother the street can be. Right click at the middle of the first intersection. This ends a line.

The attributes box will appear. I was digitizing a "major" path, so I entered:

id: `1`

Path Type: `major`

![Create Line]

Begin the next feature at the endpoint of the first. Make sure the first point "snaps" to the last vertex. In QGIS the cursor will highlight when you get within the snapping tolerance.

Continue to digitize until the next intersection.

**TROUBLESHOOTING**

If you can't make a second line, your snapping tool may have small, easily resolved bug. Go back to Settings >> Snapping Options, and change the Tolerance from 10 map units to 10 pixels. This is a much smaller distance, but will solve the problem. Continue digitizing the paths.

**END TROUBLEHSHOOTING**

![All paths]

You can make the line bigger by clicking on the layer and navigating to Properties >> Style and change the line width - though this is not necessary.

Be sure to save your work regularly.

When you are completed, you will have two new datasets that you can use to study the evolution of the park's vegetation and paths. The features you encoded (i.e., tree type or path type) are permanently attached to the geometries you just traced as well. You will also be able to import these new datasets into any other QGIS project.

If you would like to see several detailed GIS datasets made from this map, you can find several layers in [Geodata@Columbia](https://geodata.library.columbia.edu/catalog?f%5Bdct_provenance_s%5D%5B%5D=Columbia&q=1902+bronx&bbox=-73.973419%2040.704275%20-73.73378%2040.953663) available for public use.

______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2019 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

[Data Source]: Images/2019/Digitize1.png
[Add Map]: Images/2019/Digitize2.PNG
[Map Sheet]: Images/2019/Digitize3.png
[zoomed map]: Images/2019/Digitize4.png
[New Shapefile]: Images/2019/Digitize5.png
[Add to Fields List]: Images/2019/Digitize6.png
[New Layer Settings]: Images/2019/Digitize7.png
[Layers List]: Images/2019/Digitize8.png
[Toggle editing]: Images/2019/Digitize9.png
[Editing Mode]: Images/2019/Digitize10.png
[Add features]: Images/2019/Digitize11.png
[Attribute entry]: Images/2019/Digitize12.png
[More trees]: Images/2019/Digitize13.png
[vertex tool]: Images/2019/Digitize14.png
[select point]: Images/2019/Digitize15.png
[move point]: Images/2019/Digitize16.png
[current edits]: Images/2019//Digitize17.png
[Save Feature]: Images/2019/Digitize18.png
[New Line Layer]: Images/2019/Digitize19.png
[Add Line features]: Images/2019/Digitize20.png
[Settings Options]: Images/2019/Digitize21.png
[Digitizing options]: Images/2019/Digitize22.png
[Digitizing settings]: Images/2019/Digitize23.png
[Create Line]: Images/2019/Digitize24.png
[All paths]: Images/2019/Digitize25.png
