## Mapping Data 

With this exercise, you will learn introductory skills involved in using QGIS to map existing spatial datasets. After the completion of this set of three Mapping Data exercises, you should have…

1. become familiar with the QGIS user interface 
2. learned the components of shapefiles 
3. created a clear and effective map composition 
4. critically considered symbology and classification and the differences between mapping qualitative and quantitative information 
5. created and calculated new fields in an attribute table 
6. performed a table join to combine additional data to an existing shapefile’s attribute table 
7. queried a GIS dataset, using both tabular queries and spatial queries 
8. worked with projections and examined the impacts of projection transformations on spatial analysis

#### Part 00
Download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

### Mapping Data 00: Mapping World Population(s)
#### Premise
We are interested in creating a map of world countries and cities (and at the same time exploring the QGIS interface). We have a point file for the locations of populated places around the world as well as a polygon file for country boundaries. This map will serve as a basemap to which we can add additional information and layers in order to examine multiple measures of population and the differences between them.

#### Setting up QGIS

**Launch** QGIS. Your new blank map project will look like this:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/01_OpenQGIS.png)

Begin to familiarize yourself with the interface. You can also refer to this [brief description](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Resources/QGIS_InterfaceDescription.md) of the elements of the interface for more information. 

#### Adding Layers

In order to construct our map within QGIS we will need to add our data layers to the map project. There are several ways to accomplish this however we will begin by using the `Add Vector Layer` button. 

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)

**Navigate** to the MappingData\Shape\ folder. You'll notice a number of different file extensions that are likely unfamiliar. The files outlined in blue are all components of the admin_0_countries shapefile, and the ones outlined in magenta are all elements of the populated_places shapefile. It is very important that all of these files stay together in the same folder otherwise QGIS will not be able to load the layer.

* .shp - The main file that stores the feature geometry (required).
* .shx - The index file that stores the index of the feature geometry (required).
* .dbf - The dBASE table that stores the attribute information of features (required).
* .sbn and .sbx - The files that store the spatial index of features (these might get corrupted, see note at the end of this tutorial).
* .prj - The file that stores the coordinate system information.
* For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_ElementsofSHP.png)

Add the `populated_places.shp` and `admin_0_countries.shp` files. Even though we will just be adding these files to the map QGIS still references the other files associated with each layer (.shx,.dbf,.sbn,.prj). 
Note you can select multiple shapefiles by holding down Command (on Mac) or Ctrl (on Windows) while individually clicking the file names. 
The selected layers will be added in default colors. 
![layers](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/04_LayerOrder.png)
The cities layer is represented by points and the countries layer is represented by polygons. The order of the layers can be controlled with the `Layers panel` to the left of the Data Frame. 

**Click** and drag the admin_0_countries layer on top of the populated_places layer. The cities points are no longer visible because they are behind the countries polygons (or only visible at the borders of the countries and the oceans). 

![order](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/03_Adding_Layers.png)

We can change this by removing the fill color of the country polygons, leaving only the outline of their boundaries. To do this, we must change the style of the data layer. That is, we will change the way the data is styled or symbolized on the map. The simplest style for any dataset is to apply a single symbol to every feature within the layer. 

We will display the countries as just borders. To access the `Style Menu` **double-click** on the layer name in the Layers panel, or **right-click** on the layer name and select `Properties.`  There are many different ways to symbolize data on a map through QGIS. For now, we will just use one style for all of the features in the layer. 

![properties](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/05_Properties.png)

Once inside the Layer Properties Menu **select** the `Style` tab. **Select** `Simple Fill` and then in the `Symbol layer type` menu **select** Outline: Single line. 

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/05_Style.png)

When your style settings are finished, **click** `OK` to exit the properties menu. You should now be able to see each of the populated places points through the empty country polygons.

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/06_PopulatedPlaces.png)

**Save** your QGIS project by selecting `Project` > `Save`. Name your project MappingData_Population.qgs and save it in the Tutorials/Exercises folder. QGIS projects are saved as .qgs files. It is important to note that the data layers are not saved with it the map project but are rather linked to the project.


______________________________________________________________________________________________________________

Tutorial written by Dare Brawley, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2017 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).






