## Making Data 

### Making Data 03: Digitizing Features from a georeferenced map

#### Premise

In this exercise, you will create your own dataset by outlining the trees that were represented in the "1902 map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" that we previously georectified. Making new data from historic maps is a fairly common, if laborious, practice. In many cases, the data we are interested in is not digitized, so we have to translate it ourselves. This process is similar to digitizing books handwritten in script by typing them. It is time-intensitve, but sometimes, it is the only way to get the data we need in a format a computer can reas. 

Through this tutorial, you will explore some of the on-screen hand digitizing tools available in QGIS and use them to digitize trees, paths and other features from a georeferenced map. In essence, you will be converting raster spatial data into vector based features.

#### Notes on the data: 

The map you will be using for this exercise is the map sheet from "Map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" that you georeferenced in the previous exercise. If you have not already done so, please complete the [Making Data 01](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Tutorials/04_MakingData01.md) exercise. 

### Digitizing Exercise

Open a **new project** in QGIS.

Since we already georectified our map, you only need to load the georectified tiff file. In the process of georectifying it, we aligned the image with spatial information that QGIS can understand. It is now similar to the raster file for the gridded population of the world that we used in Part I. This is important because we can now combine other datasets such as historic or current population data, maps showing development in the intervening years, or other datasets. We can also use the data that was drawn onto this map and combine it with other datasets once we translate it from the scanned version it currently exists as into a digitized version. 


Let's start with our map.

Click on the add raster button ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize2.png) and navigate to the georeferenced image you made in the [Making Data 01](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Tutorials/04_MakingData01.md) exercise. 

Since you verified its accuracy already, you will not need any basemap data for this exercise, so your project will look like this:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_01.png)

This map is part of a very large-scale plan and the Bronx park area, which contains the then-new botanical garden and zoo, is particularly detailed. Every structure, road, walking path, and tree is mapped. We would like to be able to use this data in another setting, so we will digitize some of the features. We will start by digitizing trees. For the trees, we will use point geometry, so this will be a particularly simple dataset.

Remove any transparency from the georeferenced map layer. Zoom into the southwest corner of Bronx Park, where the Conservatory garden and library (labeled ‘museum’ on the map) are:
![zoomed map](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_02.png)

We will create a New Shapefile layer consisting of points. Navigate to Layer >> Create Layer >> New Shape File:
![New Layer](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_03.png)

In the new vector dialog layer, choose type “Point”. Every point will have its own unique ID that you will have to enter. If you want to attach more data, you can create additional attribute fields for your dataset. In the 'New Field' Name box, I've entered the category, Tree to create a new attribute. I might fill this attribute with values such as 'Maple', 'Tulip', or 'London Plane'
It is best practice to separate all of the data types into different attributes (i.e., if you had data about the age of the tree, you would make another attribute for 'Age', etc.). When making data, more specific categories is always better than a smaller table.
Here, I have added a tree “type” attribute and made it a text field with a maximum length of 80. Select `Add to fields list``, the click `OK`:
![New Layer](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_04.png)

When prompted, save the new file in the same directory with your map, and name it BronxParkTrees.

The layer will now appear in the Layers panel:
![New Layer](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_05.png)

Now click on the BronxParksTrees Layer to activate it and turn on editing by clicking on the `Editing Tool` ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize9.png) 

Now the `Add Features` tool should be available. Click on the `Add Features` tool to begin digitizing trees.

![New Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_06.png)
	 
This tool gives us a circular cursor. For every tree (or other data point) we want to add, all we have to do is click on it. An attribute dialog appears where we can type in attribute information for the feature we just created:
![New Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_07.png)

There is no information on the map in regards to the type of tree; however, I know that the trees in front of the library are a stand of stately tulips, so I am entering that information now. I will give each tree a unique id so that I can reference them later (unfortunately, QGIS does not do this automatically, so it is prone to errors, but still worth doing as this it is much easier to work with data where the rows have unique identifiers). It is generally best practice to make these identifiers simple and uniform. For example, "3rd tree on the left after the museum" is unique and probably refers to one and only one tree, it is difficult to manage in our dataset. This is obviously a silly example for trees, but much more likely to crop up if we think about buildings, names, or even states (i.e., New York is unique, but NY is a better identifier). For our trees example, I'm just going to use sequential numbers.

Click `OK` when finished. 

Continue to digitize trees in this corner of the park:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize12.png)

We can move or edit the point features with the move feature tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize13.png) if you want to delete a tree, you can select it with the select features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize14.png) at use the delete key on the keyboard. It is a good idea to regularly use the “save for selected laters” function to save your work as you digitize: 
![New Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_08.png)

When finished, depress the toggle editing tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize16.png) to close the editing session and save your changes to the layer.

We are also interested in where the park pathways were situated. It is best practice to keep different types of shapes (points, lines, and polygons) separate (and actually QGIS won't let us make them all as the same file anyhow). This goes back to making data more broadly. When working with datasets, the more uniform the dataset is, the better, and the less information per bin, the better. So, whether it is breaking up different data types, or separating each datum into its own bin, we want to organize our data with categories rather than human-readable things like words. 

So let's get started with digitizing the park pathways. Create another new shapefile layer as above (Layer >> New Layer >> New Shapefile Layer). This time, select “Line” as the vector type. I'm going to include the 'Path Type' attribute to keep track of if the path is for a 'major' or 'minor' path. The only thing I will type into this box is 'major' or 'minor' (in all lowercase). If I wanted to make a sub type of either of these categories, I would have to add another attribute. 

Save it as `BronxParkPaths` when prompted. 

![New Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_09.png)


Now when you toggle on editing and select the add features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize19.png). You will be digitizing line features. As you click with the add features tool you can continue to add as many vertices to the line as you wish. To complete the line segment, use the right mouse button. 

Line features are more complex than the point features, so we need to consider a few more dimensions (pun intended :) ). Since these streets are so detailed we have the option of actually digitizing the curbs and path outlines. For our analysis, we are less concerned with the outline and more concerned with where the paths were situated. Therefore, we are going to digitize the ‘centerline,’ using a single line feature to represent the center of the path feature. 

We also must decide where to begin and end the individual line features. A common practice is to create individual features between every intersection, ending each feature at the next intersection. This is advantageous because we can represent the connectivity of the features, essentially modeling a network. But doing it this way means that we must make sure that the connecting features are exactly coincident. QGIS has a handy feature to help with this: snapping tolerances. Snapping tools will automatically adjust the digitizing tools and ‘snap’ them to specified features as the cursor gets sufficiently close. 

To activate and customize the snapping tools, navigate to Settings >> Snapping Options:

![Snapping Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_10.png)

Set the snapping options for the current layer to be within 10 map units of a vertex (our map units are meters, based on the projection we are working in):

Layer selection: `Current Layer`

Snap: `To vertex`

Tolerance: `10.00000` `map units`

Click `Apply` then `OK`

![Snapping Selections](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize21.png)

Now the `Add feature` tool will automatically snap to another feature’s vertex whenever the cursor comes within 10 meters.

Activate `Editing Mode` and select the add features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize22.png). Be careful to keep each vertex as close to the center of the street as possible. The more vertices you add, the smoother the street can be. Right click (or Control+Click) at the middle of the first intersection. This ends a line. 

The attributes box will appear. I was digitizing a 'major' path, so I entered:

id: `1`

Path Type: `major`

![New Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_13.png)

Begin the next feature at the endpoint of the first. Make sure the first point ‘snaps’ to the last vertex. In QGIS the cursor will highlight when you get within the snapping tolerance.

Continue to digitize until the next intersection. 

**TROUBLESHOOTING**

If you can't make a second line, your snapping tool may have small, easily resolved bug. Go back to Settings >> Snapping Options

and change the Tolerance from 10 map units to 10 pixels. This is a much smaller distance, but will solve the problem. Continue digitizing the paths. 

**END TROUBLEHSHOOTING**

![Next Feature](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata05_15.png)

You can make the line bigger by clicking on the layer and navigating to Properties >> Style and change the line width - though this is not necessary. 

Be sure to save your work regularly. 

When you are completed, you will have two new datasets that you can use to study the evolution of the park's vegetation and paths. The features you encoded (i.e., tree type or path type) are permanently attached to the geometries you just traced as well. You will be able to import these new datasets into any other QGIS project. 

______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2018 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

