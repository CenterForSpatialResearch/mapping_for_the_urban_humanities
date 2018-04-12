## Analyzing Data

### Analyzing Data 04: Schools, Libraries and Density Mapping
#### Premise

In this exercise we are interested in answering two questions: which areas of New York City have the highest concentration of libraries? And which areas have the highest concentration of schools?

We will create a density map to do this – this is a very common type of map that is often used to construct persuasive arguments but it can also be incredibly misleading. 

The density map will help us to see whether there are clear concentrations of schools and libraries, at the same time we will create several maps using different parameters in order to explore how subjective these maps are and how many different narratives can come from them.

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

##### Adding the Data Layers

**Launch** QGIS

Select the `add vector layer` button and navigate to MappingfortheUrbanHumanities/Class_Data/3_AnalyzingData and open: 
* NYC_Libraries.shp
* NYC_Schools.shp
* NYC_Tracts_2014.shp (this is just to provide us with some context).
* if you would like you can download a shapefile containing the water bodies and rivers for New York [here](http://gis.ny.gov/gisdata/inventories/details.cfm?DSID=928) which will help give greater context to our map. 

![layers]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/01_Layers.png)

In order to create heatmaps of schools and libraries in New York City we will first need to install a plugin. **Navigate** to the Plugins tab in the top menu bar and select Manage and Install Plugins. In the Plugins window that opens select the `All` tab on the left and then search for `Heatmap`. If it is not already installed, install it. Otherwise make sure that the check box next to its name is checked. 

![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/02_Heat.png)

Once the heatmap plugin is installed you will be able to find it under the Raster tab in your menu bar.

First we will make two density maps: first of libraries and then of schools. These will point out where there are concentrations of these public facilities within New York City. Save all new layers created during this exercise in the **MappingfortheUrbanHumanities/Class_Data/3_AnalyzingData/Process** folder.

* On the menu bar **navigate** to `Raster`>`Heatmap`. 
  * The heatmap plugin allows us to calculate a **kernel density** of all of the point features in your layer. 
  * This tool can only be used for point features. 

  * In order to compute the density of the point features the plugin fits a smooth curved surface over
each point – the highest value of the surface is exactly above the point and then the values diminish outwards in all directions from there until it reaches a set radial distance at which point all values go to null. The options in the heatmap dialogue box allow us to manipulate the rate at which the values decrease, the distance of the search radius, whether the points are weighted by a value in their attribute table. 

* A few things to note about this dialogue box: 
  * Radius:  the radius specifies the distance around a point at which the influence of the point will be felt. This is also sometimes called the kernel bandwidth. If you choose a small radius then the radius of the raster layer around each point will be smaller and will show a great deal of variation, if you choose a larger radius the impact of the individual points will likely overlap with one another and thus create a smoother surface. 
  * Cell size: this value determines the cell size of the output raster – the size in map units of each individual raster cell. 
  * Kernel shape: this controls the way that the influence of a point decrease as you move away from the point’s location. 
  * Use radius from field: you can determine the radius of the heatmap from a field in the dataset
  * Use weight from field: allows you to give greater significance to certain features based on their value in the attribute table (we will use this later in the exercise).
  * Decay ratio: when using Triangular kernels this can be used to determine how the values of the kernel density map decrease as you move away from a point feature, (we will not be using this today however more information is available here.  
  * Output values: either raw or scaled by kernel size.  

* Save your file as `NYC_Libraries-Heat.tif` and make the following selections:

![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/03_library.png)

* Click `OK`. The result should look somewhat like this:

![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/04_result.png)

* What narratives about libraries in New York can this map aid you to create? What does it say about the distribution of libraries throughout the five boroughs? 


Next repeat these steps and use the same parameters but produce a heat map of New York City public schools. 

* On the menu bar **navigate** to `Raster`>`Heatmap`. 
* Save your file as `NYC_Schools-Heat.tif` and make the same selections as we did for libraries. 
![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/05.png)
* Click `OK`. The result will look like the following: 
![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/06.png)

* What narratives about public schools in New York can this map aid you to create? What does it say about the distribution of schools throughout the five boroughs? Are there clear large clusters? Areas without many schools?

In the next portion of the exercise we will create several additional density maps of schools in New York, each with different parameters, and observe the impact of changing these parameters on the maps we can produce and on the observations which each supports. 

We will first modify our original density map of schools by weighting schools by their levels of enrollment.
* On the menu bar **navigate** to `Raster`>`Heatmap`. 
![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/07.png)

* Save your file as `NYC_Schools-Heat_Enrollment_4000-200.tif`. Note we have encoded the radius and cell size into the file name so we can keep track of them for each layer in order to make comparisons. 

* We will choose the same radius and cell size that we used previously, but this time we will click the check-box next to `use weight from field` and we will select `Enrollment` as the field. Our density map will now be weighted by the values in this field.  

* Click `OK`. The result should look like this: 

![heatmap]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData04/08.png)

Toggle the visibility of the `NYC_Schools-Heat_Enrollment_4000-200.tif` layer on and off to see the differences between the weighted density map of schools and the un-weighted one. 

What narratives about public schools in New York can this map aid you to create? What does it say about the distribution of schools throughout the five boroughs? 

Now we will repeat these same steps but will test several combinations of radius distances and cell sizes.

1.	Create a new density map of schools with a larger search radius, 8000 feet, but the same cell size, 200 feet. Name this ` NYC_Schools-Heat_Enrollment_8000-200.tif`
2.	Create a new density map of schools with a larger search radius, 8000 feet, and a larger cell size, 1200 feet. Name this ` NYC_Schools-Heat_Enrollment_8000-1200.tif`
3.	Create a new density map of schools with a smaller search radius, 2002 feet, but the same cell size, 200 feet. Name this ` NYC_Schools-Heat_Enrollment_2000-200.tif`
4.	Create a new density map of schools with a smaller search radius, 2000 feet, and a larger cell size, 1200 feet. Name this ` NYC_Schools-Heat_Enrollment_2000-1200.tif`

What are the key differences between each of these density maps? What conclusions would each lead you to make about the spatial patterns of schools in New York City?  


______________________________________________________________________________________________________________

Tutorial written by Dare Brawley, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2017 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).
