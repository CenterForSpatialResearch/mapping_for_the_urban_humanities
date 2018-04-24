## Making Data

### Making Data 01: Geocoding historic data

#### Premise
In this tutorial, we are going to make a map of newspapers in the United States before and after the invention of the rotary printing press in 1843. We want to visualize how newspapers both exploded in urban areas and began to spread to smaller areas (if you want to take this to the next level, you could combine this project with the )

<<<<<<< HEAD
One of the primary hurdles that researchers encounter is finding appropriate datasets. This problem is compounded when working with historic data as it may not necessarily have spatial data attached or it may only have place names attached that may or may not represent modern place names. Ultimately, finding data and transforming data are separate issues. As far as finding data is concerned, the library, the Census, NHGIS, or XXXXX may have everything that you need. If not, you may need to turn to repositories on the Internet. 

Sometimes the library may have data available, or you may find it through a web search. Assuming that you are not able to find shapefiles, you will want your data to be in a format that QGIS can parse. This includes .csv (comma separated values), .txt (plain text), or some form of database. Formats such as .pdf may pose insurmountable problems. 
=======
In this exercise, you will explore some of the georeferencing tools available in QGIS and use them to georeference a 1902 map of the Bronx. You will learn how to use GIS tools to georectify raster datasets. You will use the georeferenced map for the next exercise where you will digitize vector features from the map infomation.

#### Notes on the data:
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0

We will go through the process of turning data that we find through an internet search into data we can use in a mapping project. This is not the only way to get data, and at Columbia, the librarians can be immensely helpful in this regard.  

By the end of this tutorial, you will be able to:
- search the internet for datasets
- transform data you find in a table into a csv file that can be used in QGIS
- align that data to geographic locations using a gazetteer
- query the data you collected to answer a research question

<<<<<<< HEAD
### Making the Data
=======
#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials.
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0

We are going to use data from [Readex](https://www.readex.com/who-we-are-what-we-do), a company that sells primary source collections to institutions. We only want the names of the newspapers, the location of publication, and the year it was established. We are not interested in reading the papers right now. Readex offers these lists in a variety of organizations: by region, decade, or era. We will use the 'By Era' breakdown, and look at the pre- and post-1842 eras. 

Open a web browser (Google Chrome, Firefox, or Safari are OK, please do not use Internet Explorer), and navigate to [www.readex.com](www.readex.com). Hover over the 'Collections' link in the Navigation bar and click on 'By Era'. Then select the `Jacksonian Era, Parts 1 and 2, 1823-1842` > `Title List` it will open in a new tab.

Also open the `Antebellum Period, Parts 1 and 2, 1843-1860` > `Title List`

<<<<<<< HEAD
![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_01.png)
=======
You are going to use OSM data as the reference data for the georeferencing process. You can view the OSM basemap service is QGIS through the OpenLayers plugin.  This plugin does not come pre-installed with QGIS, so you will probably need to add it.  Under the plugins menu, select “Manage and Install Plugins…”
![option](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_02.png)
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_02.png)

<<<<<<< HEAD
Looking at this website, we can see that it is a table. This is very fortunate because whenever data is in a table (as it often is on a website), we can use a simple tool in Google Drive to format the table nicely for our use. If the data was not in a table, we may be able to get it through Webscraping (i.e., with a webscraping script or a plugin to our browser. Both of those techniques are far beyond the scope of this tutorial,)

ADD THE REST HERE
=======
![plugin dialogue](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_03.png)

It may take a few seconds to install.  Close the plugins menu when finished.  The OpenLayers tools should now appear under the Web menu:
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0

### Geocoding 

We are first going to use a table join method to align our newspapers data to the spatial coordinates. 

First add the Newspapers layers

<<<<<<< HEAD
Now add the cities points layer using the `Delimited Text Layer` button, and make the following selections:
- csv
- point coordinates
	- X field: 'lng'
	- Y Field: 'lat'
=======
Since you are working in a new QGIS project, the map should show the entire earth as the default:
![qgis osm ](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_06.png)
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_03.png)



<<<<<<< HEAD


	
	
=======
The Georeferencer screen will open:
![georeferencer window](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_09.png)

Click on the Add Raster button ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef10a.png) and navigate to the JPEG image "Bronx1902Sheet2_Edit.jpg" from the class files in the directory Class_Data/2_MakingData.  

It will appear in the georeferencer window:
![georeferencer window with map](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_10.png)

This map is one sheet of six of a map of the East Bronx in 1902.  This section represents the area around the New York Botanical Garden and the (then new) Bronx Zoo. Fordham University can be seen just to the southwest of the garden and the Norwood neighborhood is in the northeast corner.  The area to the east of the Bronx Park area is still largely undeveloped at this point.  

Historical maps can be difficult to georeference, and this sheet poses a number of complications.  The map projection is unclear and there are no ground control points or coordinates specified.  Because of this, you will georeference by matching physical features represented on the map with their current counterparts (and their known coordinates).  However, most of the features in this map have changed or no longer exist (or were never actually built in the first place).  Thus, you will need to be very careful to choose locations that you are confident match up well with their contemporary counterparts.   Fortunately, there are a number of good candidates, particularly on the western half of the map where many streets and buildings still exist in the same location.  You will use those to georeferenced the map.

The QGIS georeferencer does not allow you to view both the scanned map and the workspace at the same time, so you will have to inspect both maps in turn and choose carefully to select locations to add georeferencing control points.
One candidate is the Haupt Conservatory in the Botanical Garden which continues to exist largely its original configuration.  Use the georeferencer zoom tools ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef11.png) to zoom to the conservatory structure in the southwest corner of the park:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef12.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef13.png)

Identify as precise a location as possible (a corner of the building will work nicely) and click on it in the georeferencing window using the add point tool ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef17.png) When you do so, the Enter map coordinates window appears:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef14.png)

If you knew the coordinates of this location, you could now add them manually, but since you do not, you must select them from the OSM data in the main QGIS window.  Click on the ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef15.png) button to see the QGIS workspace.  
You may want to use the QGIS zoom tools to zoom in very closely to the conservatory.

![conservatory](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_11.png))

Once you do so, you will need to reactivate the add button tool ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef17.png) by maximizing the georeferencing window and clicking the ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef18.png) button again.  Once you select the same location on the workspace window, you will automatically be brought back to the georeferencing window where the assigned coordinates will be imputed.  
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef19.png)

At this point, if you are dissatisfied, you can move the assigned control points with the move GCP point tool ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef20.png) or delete it entirely and start over with the delete point tool ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef21.png)
If satisfied, click the OK button and the point will be assigned and appear on the map.  

A link table entry will be generated on the bottom of the window:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef22.png)

To add a second point, repeat the same process.  It is a good idea to choose another point in a different portion of the map.  A street intersection or corner from the western portion of the map will work well for this as most of those streets continue to exist in the same configuration.  

Here, I have zoomed in to the northwestern most potion of the map where I add a ground control point at the very center of the intersection of Gun Hill Road and Tryon Ave:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef23.png)

Repeat the same stepsto select the center of the same intersection from the OSM map and add the locations to the link table:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef24.png)

You must add a minimum of four points to complete the georeferencing (although more is generally better). Generate at least two more points on your own and add them to the link table.

Be careful to make sure that the control points you add match.  This can be quite tricky as many of the features have changed or were not actually built as planned.  

Normally it is a good idea to choose control points from throughout the map.  However, in this case this will be difficult as there are few features in the eastern sections of the map that can be reliably associated with contemporary locations.

In this example, I selected six control points:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef25.png)

It is good practice to save the table of control points at this stage. Choose “Save GCP points as” under the file menu and save it in the .points format in the same location as the image. This will allow you to later recreate the work you have done:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef26.png)

Next, you will “transform” the image and create a georeferenced version of the scanned map image. In the georeferencer window, select transformation settings under the settings window:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef27.png)

Make the following selections:

Transformation type: Polynomial 1

Resampling Method: Cubic (usually used for images and photos)

Output Raster: *save this in the same folder you are working in*

Spatial reference system: EPSG:3857 *the pseudo Mercator projection used in the OSM data.**  

You can also opt to have the georeferenced layer added to QGIS when finished:

![save as](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_12.png)

Close the settings options and click on the start georeferencing button ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef29.png).

After the transformation finishes, you should see the map appear in the QGIS workspace:
![georeferenced map](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_13.png)

You can make the scanned map layer partially transparent in the layer properties.  Right click on the map in the layer panel and select properties:
![properties](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_14.png)

On the left panel in the properties dialog, select Transparency, here you can adjust the global transparency with a slider:
![transparency](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_15.png)

Compare the georeferenced map with the Open Street Map layer.  Make sure that features appear to match up closely:
![review](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata04_16.png)

In the next exercise you will be using the sheet you georeferenced here and digitizing some of the features from it.


______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2018 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).
>>>>>>> 3ff8281185c9ded0affab02b30839f6b293dc3d0
