## Mapping Data 

With this exercise, you will learn introductory skills involved in using QGIS to map existing spatial datasets. By completing this set of three Mapping Data exercises, you will

1. be familiar with the QGIS user interface 
2. learn the components of shapefiles 
3. create a clear and effective map composition 
4. critically considere symbology and classification and the differences between mapping qualitative and quantitative information 
5. create and calculate new fields in an attribute table 
6. perform a table join to combine additional data to an existing shapefile’s attribute table 
7. query a GIS dataset, using both tabular queries and spatial queries 
8. work with projections and examine the impacts of projection transformations on spatial analysis

#### Part 00
Download the GitHub repository for this course. Click on the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

### Mapping Data 00: Mapping World Population(s)
#### Premise
We want to create a map of cities and countries and ask some questions about population and population distibution. We have a point file for the locations of populated places around the world and a polygon file for country boundaries. This map will serve as a basemap. We can add additional information and layers to examine multiple measures of population and the differences between them.

The data we are using is the [Gridded Population of the World (GPW)](http://sedac.ciesin.columbia.edu/data/collection/gpw-v4). It is derived from the 2010 round of the Population and Housing Censuses. It is compiled by the NASA Socioeconomic Data and Applicaitons Center (SEDAC), operated by Center for International Earth Science Information Network (CIESIN) at Columbia University. The stated purpose for this data is to provide "globally consistent and spatially explicit data for use in research, policy-making, and communications." 

#### Setting up QGIS

**Launch** QGIS. Your new blank map project will look like this:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_01.png)

Begin to familiarize yourself with the interface. For more information, refer to this [brief description](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Resources/QGIS_InterfaceDescription.md) of the elements of the interface. 

#### Adding Layers

In order to construct our map within QGIS we will need to add our data layers to the map project. There are several ways to accomplish this. We will begin by using the `Add Vector Layer` button. 

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_02.png)

**Navigate** to the MappingData\Shape\ folder. There are a number of different file extensions that may be unfamiliar. The files outlined in blue are components of the admin_0_countries shapefile, and the ones outlined in magenta are elements of the populated_places shapefile. It is very important that all of these files stay together in the same folder otherwise QGIS will not be able to load the layer.

* .shp - The main file that stores the feature geometry (required).
* .shx - The index file that stores the index of the feature geometry (required).
* .dbf - The dBASE table that stores the attribute information of features (required).
* .sbn and .sbx - The files that store the spatial index of features (these might get corrupted, see note at the end of this tutorial).
* .prj - The file that stores the coordinate system information.
* For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_ElementsofSHP.png)

Add the `populated_places.shp` and `admin_0_countries.shp` files. Even though we will only add these files to the map, QGIS still references the other files (.shx,.dbf,.sbn,.prj). The selected layers will be added in default colors. 

Note you can select multiple files by holding down Command (on Mac) or Ctrl (on Windows) while clicking the file names. 

![layers](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_03.png)

**TROUBLESHOOTING**

If you see a long line across the top or just one point appearing, it is probably an issue with the projection. To resolve: 

1. Change the project projection to World_Mollweide
	1.Click on the numbers in the bottom right hand corner.
	![projection](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_04.png)

	2. Select World_Mollweide
	![projection](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_05.png)

2. Change each layer's project
	1. Double click on the layer name 
	![layer](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_06.png)
	
	2. Select World_Mollweide
	![projection](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_07.png)


3. For the permanent solution, save the layer with the new projection and reimport the layer. We will cover this further when we discuss projections.
	
**END TROUBLESHOOTING**

The cities layer is represented by points and the countries layer is represented by polygons. The order of the layers can be controlled by dragging the layer names up and down in the `Layers panel` to the left of the Data Frame. 

**Click** and drag the admin_0_countries layer on top of the populated_places layer. The cities points are no longer visible because they are behind the countries polygons. 

![order](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_08.png)

We want to be able to see both, so we will remove the country's fill color by changing the style of the data layer. Changing the style changes the way the data is symbolized on the map. The simplest way to style any dataset is to apply a single symbol to every feature in the layer. 

We will display the countries as just borders. To access the `Style Menu` **double-click** on the layer name in the Layers panel, or **right-click** on the layer name and select `Properties.`  There are many different ways to symbolize data on a map through QGIS. For now, we will just use one style for all of the features in the layer. 

![properties](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_10.png)

Once inside the Layer Properties Menu **select** the `Style` tab. **Select** `Simple Fill` and then in the `Symbol layer type` menu **select** Outline: Single line. 

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_09.png)

When your style settings are finished, **click** `OK` to exit the properties menu. You should now be able to see each of the populated places points through the empty country polygons.

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_11.png)

**Save** your QGIS project by selecting `Project` > `Save`. Name your project MappingData_Population.qgs and save it in the Tutorials/Exercises folder. QGIS projects are saved as .qgs files. 

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata01_12.png)

**NOTE**

The data layers are not saved with the map project. They are linked to the project. So when you open this project again, the *project* references the data layers in the place they were saved when you made the project. So, if you move (reorganize) the data files, the project will not be able to find them (and therefore will not be able to use them to make this map again). 




______________________________________________________________________________________________________________

Tutorial written by Dare Brawley for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2018 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).
