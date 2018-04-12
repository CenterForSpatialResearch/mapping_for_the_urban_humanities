## Making Data 

### Making Data 02: Digitizing Features from a georeferenced map

#### Premise

In this exercise, you will explore some of the on-screen hand digitizing tools available in QGIS and use them to digitize trees, paths and other features from a georeferenced map.  In essence, you will be converting raster spatial data into vector based features.

#### Notes on the data: 

The map you will be using for this exercise is the map sheet from "Map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" that you georeferenced in the previous exercise. If you have not already done so please complete the [Making Data 01](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/04_MakingData01.md) exercise. 

### Digitizing Exercise

Open QGIS:

![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize1.png)

Click on the add raster button ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize2.png) and navigate to the georeferenced image you made in the [Making Data 01](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/04_MakingData01.md) exercise.  Since you verified its accuracy already, you will not need any basemap data for this exercise:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize3.png)

This map is part of a very large-scale plan and the Bronx park area, which contains the then-new botanical garden and zoo, is particularly detailed.  Every structure, road, walking path, and tree is mapped.  In the next part of this exercise, you will create new vector datasets, and hand-digitize some of the path and tree features.

First you will digitize some trees.  For the trees you will use point geometry, so this will be a particularly simple dataset.

Remove any transparency from the georeferenced map layer. Zoom into the southwest corner of Bronx Park, where the Conservatory garden and library (labeled ‘museum’ on the map) are:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize4.png)

Next you will create a new point layer.  Under the layer menu, choose create new layer and new shapefile layer:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize5.png)

 In the new vector dialog layer, choose type “Point”.  You can also create additional attribute fields for your dataset, if applicable.  Here, I have added a tree “type” attribute and made it a text field with a maximum length of 80.  Select OK:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize6.png)

Save the new file in the same directory with your map, and name it BronxParkTrees.
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize7.png)

 The layer will now appear in the Layers panel:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize8.png)

Now begin editing by depressing the toggle editing tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize9.png) while the trees layer is highlighted in the layers panel.  Now you can use the add feature tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize10.png) to start creating trees.  Click on one of the trees in the map.  An attribute dialog appears where you can type in attribute information for the feature you just created:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize11.png)

There is no information on the map in regards to the type of tree; however, I know that the trees in front of the library are a stand of stately tulips, so I am entering that information now.  Click OK when finished. 

Continue to digitize trees in this corner of the park:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize12.png)

If you want to move one of the point features you can use the move feature tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize13.png) if you want to delete a tree, you can select it with the select features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize14.png) at use the delete key on the keyboard.  It is a good idea to regularly use the “save for selected laters” function to save your work as you digitize:  
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize15.png)

When finished, depress the toggle editing tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize16.png) to close the editing session
Next you will digitize some of the park pathways.  Create another new shapefile layer as above, but this time choose “Line” as the vector type and BronxParkPaths as the file name:

![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize17.png)

![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize18.png)

Now when you toggle on editing and select the add features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize19.png).  You will be digitizing line features.  As you click with the add features tool you can continue to add as many vertices to the line as you wish.  To complete the line segment, use the right mouse button. 

Line features are more complex than the point features you made earlier and a few more considerations need to be made. One issue regards the shape of the streets and paths.  Since these streets are so detailed you have the option of actually digitizing the curbs or path outlines.  Instead, you are going to digitize the ‘centerline,’ using a single line feature to represent the center of the path feature.  

You also must decide where to begin and end the individual line features.  A common practice is to create individual features between every intersection, ending each feature at the next intersection.  In this way, you can represent the connectivity of the features, essentially modeling a network.  It is important then to make sure that the connecting features are exactly coincident.  You can make sure that you connect features while digitizing by taking advantage of snapping tolerances.  Snapping tools will automatically adjust the digitizing tools and ‘snap’ them to specified features as the cursor gets sufficiently close. 

To set snapping, select “snapping options” under the settings menu: 
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize20.png)

Set the snapping options for the current layer to be within 10 map units of a vertex:
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize21.png)

Now the add feature tool will automatically snap to another feature’s vertex whenever the cursor comes within 10 meters.

Digitize the first feature using the add features tool ![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize22.png). Be careful to keep each vertex as close to the center of the street as possible.  The more vertices you add the smoother the street can be. Right click at the middle of the first intersection. 
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize23.png)

Begin the next feature at the endpoint of the first.  Make sure the first point ‘snaps’ to the last vertex.  In QGIS the cursor will highlight when you get within the snapping tolerance.
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize24.png)

Continue to digitize until the next intersection. 
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize25.png)

Continue to add paths in this section of the map.  Remember to regularly save your work.
![DigitizingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/Digitize26.png)

______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2017 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

