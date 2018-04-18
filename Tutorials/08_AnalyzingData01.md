## Analyzing Data

Through this exercise you will learn key tools of analysis using QGIS. After completing these exercises you will able to…

* Use proximity based measures
* Understand the principles and applications of boolean operations
* Conduct spatial joins
* Explain and perform proportional split population estimates
* Create a basic density map (and understand the potential pitfalls of this type of visualization)
* Perform basic raster math operations
* Develop a raster based decision mapping methodology to answer a specific question
* Adapt a raster dataset to your own research needs through raster re-classification

### Analyzing Data 01: Libraries, Education, and Language

#### Premise
We are interested in looking at libraries in the Bronx as a public resource. We will use proximity based measures to the zones of impact (and potential impact) of libraries on Bronx residents from a number of different perspectives. First we want to evaluate which library branches are located within areas that have a high number of Spanish speaking residents. Then we will evaluate which libraries serve the greatest number of school children.  

#### Research questions:
* Where are Bronx Library branches?
* Which Library branch locations are within areas with a high number of Spanish speaking residents?
* How many public schools are located within 1/4 mile of a library?
* Which five libraries serve the most students? 
* What is the nearest library to each school?
* How many people do these libraries serve?

#### The Strategy
To evaluate the confluence of Spanish speakers and branch libraries, we will first select using an expression and then select by area to identify which libraries fall in census tracts with a high percentage of Spanish speakers. 

Then to evaluate which libraries serve the greatest number of school children we will first create a buffer around each library location of ½ mile (which we will be able to export as its own layer to display on our map). We will then use a spatial join in order to count the number of schools within ½ mile of a library and to determine the number of students enrolled in those schools.

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

#### Let’s Begin

**Launch** QGIS. 

Select the `add vector data` button and navigate to the MappingfortheUrbanHumanities\Class_Data\AnalyzingData\Shape folder and add the following three Layers: 
* Bronx_Tracts_2014.shp
* Bronx_Schools.shp
* Bronx_Libraries.shp

![qgis dataframe](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_01.png)

**TROUBLESHOOTING**

If the map looks a little skewed, make sure the layers and the project are projected in the same CRS. Open the Bronx_Tracts_2014 Properties menu, navigate to General, and then notice which CRS it is projected in. If that **does not** match the project CRS (shown in the lower right hand corner), change the project CRS.
Click on the number in the lower right corner and search for the appropriate CRS. 

For this tutorial, all layers and the proejct should be projected in `NAD_1983_StatePlane_New_York_East_FIPS_3101_Feet EPSG:102715`

**END TROUBLESHOOTING**

First **open** the attribute tables of each data layer and inspect its contents. 

The field names for `Bronx_Tracts_2014` are: 
* `STATEFP’: the State FIPS code
* `COUNTYFP`: the county FIPS code
* `TRACTCE`: the FIPS code for the census tract
* `GEOID`: the unique FIPS code that combines the state, county, and tract code for each tract. 
* `NAMESLAD`: the name of the census tract 
* `ALAND`: the area of the census tract that is land
* `AWATER`: the area of the census tract that is water
* `INTPTLAT`: the latitude coordinate of the locator of the census tract
* ‘INTPTLON`: the longitude coordinate of the locators of the census tract
* `Pop2014`: the population of the census tract in 2014 according to the [American Community Survey 2014 5 Year Estimates]( http://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?pid=ACS_14_5YR_B01003&prodType=table)
* `PopOver5`: Population over 5 Years old 
* `Pct_OnlyEn`: the percent of the population over 5 years old within the census tract that speaks only English
* `Pct_Other`: the percent of the population over 5 years old within the census tract that speaks another language in addition to (or instead of) English
* `Pct_Spanis`=h`: the percent of the percent of the population over 5 years old within the census tract that speaks Spanish

The field names for `Bronx_Libraries` are: 
* `facname`: the name of the facility
* `borough`: the borough of the library – in this case they are all in the Bronx
* `ft_decode`: the type of library it is, Branch or Central
* `facaddress`: the address of the library
* `zipcode`: the zipcode of the library
* `ForRaster`: ignore this for now – it was created for an operation we will perform on the dataset in a later exercise. 

The field names for `Bronx_Schools` are: 
* `BORO`: a code for the name of the borough the school is within
* `BORONUM`: a numeric code for the borough the school is within
* `SCHOOLNAME`: the name of the school
* `SCH_TYPE`: the type of school, Elementary, K-8 etc
* `ADDRESS`: the school’s address
* `ZIP`: the school’s zipcode
* `GRADES`: the grades within the school
* `Emrollment`: the number of students enrolled in the school
* `Raster`: again ignore this field for now
**Save** your map project as `AnalyzingData01` within the MappingfortheUrbanHumanities\Tutorials\Exercises section.

#### Finding libraries near concentrations of Spanish speakers

Now, we want to determine which libraries are located within census tracts where more than 65% of the population speaks Spanish. We are interested in determining which libraries might be well suited to receive additional resources to go towards multilingual programs.

* **Open** the attribute table of the Bronx_Tracts_2014 layer and choose the `select using an expression` tool. Select census tracts where more than 65 percent of the population over 5 years old speaks Spanish. Your expression should read:

`Pct_Spanish > 65` 

Click `Select`. You should see that 56 features were selected. Close the attribute table. The tracts where greater than 65% of the population speaks Spanish should be highlighted in yellow.

![select by expression](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_02.png)

* Now we will determine which libraries lie within these census tracts by using the select by location tool. **navigate** to the `Vector` > `Research Tools`>`Select by Location` in the menu bar. 

![menu bar](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_03.png)

Then make the following selections:

Select features in: `Bronx_Libraries`
that intersect features in: `Bronx_Tracts_2014`

* Include input features that intersect the selection features
* Only selected features
From the dropdown menu:
* creating new selection

![select features](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_04.png)

* Open `Bronx_Libraries` layer Attribute Table. Use the Move selection to top button to note which libraries were selected. Four libraries were selected, what are their names? 

![selected features](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_05.png)

This analysis give us a very rough sense of which libraries might already serve a large number of Spanish speakers however we have only selected libraries which are located exactly within census tracts with a large proportion of Spanish speakers. What is there is a library in an adjacent census tract? Our analysis will not have picked up on this. 

Deselect all features from all layers.

![deselect features](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_07.png)

**Save** your map project

#### Schools and Libraries 
Now we will depart from questions about language and instead ask a series of questions about the relationship between schools and libraries in the Bronx. Specifically we will ask: 
* How many schools are within 1/4 mile of Bronx libraries? 
* How many students are enrolled in schools that are within ¼ mile of a Bronx library? 
* What is the nearest library to each school? 

To answer the first question, we will create a 1/4 mile buffer around the libraries.

We will be creating a number of new layers, to stay organized, we want to save all of the layers produced in the process of our analysis in a new folder named `Process`, within the MappingfortheUrbanHumanities/Class_Data/3_AnalyzingData folder. Save all new layers created during this exercise in this folder. 

##### Creating Buffers
* On your menu bar navigate to `Vector`>`Geoprocessing Tools` > `Buffer(s)`.

![buffer](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_06.png)

  * Choose Bronx_Libraries as your input vector layer. 

  * Set the buffer distance to 1320. Note: the values in this field have the same units as the projection of your input datalayer and map project. Our map is projected in the NAD83 New York State Plane (Long Island)- a projection system whose units are in feet. To confirm this, you can open the layer properties and inspect the coordinate reference system for the layer. Thus we chose 1320 feet to represent 1/4 mile. 

  * Browse in order to save the Output shapefile as ‘BX_Library_QuarterMiBuffer` within your 3_AnalyzingData\Process folder. 

  * Click `OK`. Then Click `Close`. Your map should look something like the following: 

![selected features](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_08.png)

* Next we will use the select by location tool to determine which schools fall within ¼ mile of a library. Navigate to `Vector`>`Research Tools`>`Select By Location`

Select features in:  `Bronx_Schools` 
that intersect features in: `BX_Library_QuarterMiBuffer`
* Include input features that intersect the selection features
* Only selected features
From the dropdown menu:
* creating new selection

  * Select OK, and then close. 

  * Open the attribute table of `Bronx_Schools` and notice that 90 schools were selected. Thus there are 90 schools in the Bronx that are within ¼ mile of a library.

*  Now we want to answer our second question:  Which five libraries serve the greatest number of school children? To answer this, we will perform a *spatial join*. 

  * A spatial join is a new tool for us which allows us to summarize the attributes from one layer within the attribute table of another based on the spatial relationship between them. 

  * On your menu navigate to `Vector`>`Data Management`>`Join attributes by location`. 

Make the selections:

Target vector layer:  `BX_Library_QuarterMiBuffer` 

that intersect features in: `Bronx_Schools`

* Take summary of intersecting features
	* Sum
	
* Keep all records (including non-matching target records)

Select `OK`.

A warning box will appear letting you know that a new layer has been created as a result of this spatial join. Click `OK`. Then close the `Join attributes by location` dialogue box.

![spatial join](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_09.png)

**Details**
  * QGIS only calculates the first **real number** that it encounters. So, if another real number appears before the one you are interested in, it will not calculate properly. You can check this in the Properties Menu, navigate to `Fields`, and under `Type name`, check for Real Numbers.
  
  ![real numbers](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_11.png)
  
  * Just like with a table join, the `Target vector layer` is the layer to which we want to join new information to and the `Join vector layer` is the layer we are joining to the target layer. 
  * Because there are many ways to tabulate data, we need to tell QGIS how we would like to summarize the attributes from the Bronx Schools layer when they are joined to the buffer around the libraries. We can tell QGIS to take the values of the attribute fields for the first school it finds or to compute a summary (either Mean, Min, Max, Sum, or Median) of the values of all features in the schools layer which lie within the target features.
  * Save the output shapefile within Class_Data/3_AnalyzingData/Process as ‘Library_QuartMiBuffer_SchoolsJoin`
  * We selected Keep all records (including non-matching target records) to ensure that even buffers that do not contain a school are kept in our dataset.  

**End Details**

**Open** the attribute table for this layer. Notice the new field `SUMEnrollment` that has been added on. This field contains the sum of the enrollments for all of the schools within the buffer. 

Now we want to know which five libraries serve the greatest number of enrolled school children. Sort the attribute table by SUMEnrollment and identify the top five libraries. 

![attribute table](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_10.png)

**Save** your map project

##### Using a Distance Matrix

*  Now we will move on to answer our third question: which is the nearest library to each public school? 
  *  To answer this question we will again introduce a new tool of analysis, `DistanceMatrix` tool. This tool takes two point layers and computes the linear distance between each feature in both layers.
  *  Navigate on your menu bar to `Vector`>`Analysis Tools`>`DistanceMatrix`
![location](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_13.png)

Make the following selections:

Input point layer: `Bronx_Schools`

Input unique ID field: `SCHOOLNAME`

Target point layer: `Bronx_Libraries`

Target unique ID field: `facname`

Output matrix type: `Linear (N*kx3) distance matrix` 
- select `Use only the nearest (k) target points` and leave this at 1.

`Browse` to save your output distance matrix as `BX_SchoolsNearestLibraries` in the 3_AnalyzingData\Process folder.  

Select `Okay`. Then select `Close`
  
![distance matrix](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_12.png)

  * In a finder window navigate to the BX_SchoolsNearestLibraries.csv file within your 3_AnalyzingData\Process folder and open it. It should open in Excel. 

  * You will see that we have generated a table where each school is matched with its nearest library and QGIS has computed the distance between them in feet. 

![location](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_14.png)

##### Making Estimates 

We now have gathered information about how many schools are within ¼ mile of each library, as well as the total number of children enrolled in those schools. We have also computed the nearest library to each school. Now we want to determine more generally how many people live near libraries in the Bronx – i.e. how many people do Bronx libraries serve? 

To answer this question, we will need to estimate the total population near libraries in the Bronx. We will first use a coarse method of estimation and then we will refine our estimate using a more advanced technique. 

First, how many people live in the census tracts that intersect a ¼ mile buffer around our libraries?

* We will use the select by location tool to select all of the census tracts that intersect with one of our ¼ mile library buffers.

* Navigate to `Vector`>`Research Tools`>`Select by location`. And make the following selections: 

Select features in: Bronx_Tracts_2014

that intersect features in: BX_Library_QuarterMiBuffer

* Include input features that intersect the selection features
* Include input features that overlap/cross the selection features

in the dropdown box:
creating new selection


![select features](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_15.png)

* Select ‘OK’ and then `Close`. 
* Your selections should look something like this: 
![output](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_16.png)

* We can already tell that this is a very coarse way to estimate the population served by each of the Bronx libraries because some census tracts which intersect our buffers are very large and portions of the tract are very far away from any library. 

* Despite this, we want to add up the total population within the selected census tracts. We will use the `Basic statistics` tool. Navigate to  `Vector`>`Analysis Tools`>`Basic Statistics`. Make the following selections:
Input vector layer: Bronx_Tracts_2014
* Use only selected features*=
Target Field: Pop2014

Click `OK`. 

![basic stats](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_17.png)

* We see that the total population of all of the census tracts that intersect a ¼ mile buffer around a Bronx library is 983,821. Make a note of this total we will compare it to the result we get in the next portion of the exercise. 

**Proportional Split Estimation**

Now we will refine our estimate of the population near libraries using a method called *proportional split estimation*. A proportional split is a way to estimate the proportion of a quantitative attribute that falls within a portion of a polygon’s area. A proportional split is calculated in a few fairly simple steps. 

1. We calculate the area of each polygon unit 
2. Clip the polygons to the boundary of the study area (in our case the ¼ mile buffers)
3. Calculate the area of the polygons after clipping them to the study area
4. Divide the area of the polygons within the study area by their original area to determine the proportion of the original area that falls within the study area
5. Multiply the attributes (for us, population in 2014) we wish to estimate by the proportion in order to estimate the proportion of the attribute that falls within the study area. 

Note: proportional split estimation assumes that the attribute you are estimating is evenly distributed through out the polygon. In reality the population within each census tract is not evenly distributed. However, this is a common method of estimation.


**Calculating the area of the census tracts**

Open the Bronx_Tracts_2014 layer attribute table and select the field calculator.
* Create a new field
Output field name: `Area`

Output field type: `Decimal number (real)`

Output field width:`10` 

Precision: `2`

Open the Geometry menu and double click on `$area`

Click `OK`

![new field](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_18.png)


* Scroll to the right in the attribute table for the Bronx census tracts and see the new field that you have added. Now select the `Toggle editing mode` button to exit the editing mode. You will be asked if you want to save your changes, say `yes`. 
* Note: census tracts extend into the water so the area we are calculating here includes both land area and area of the tract that might be in the water. This introduces some error into our proportional split estimation. One way to be even more precise in our estimate is to clip the census tract polygons by the shoreline **befor** starting this analysis. 

**Clipping the census tracts to the ¼ mile buffers**
* Next we will use the `clip` tool to clip the Bronx census tracts with the ¼ mile buffers around the Bronx libraries. 
* Navigate to `Vector`>`Geoprocessing Tools`>`Clip`
Make the selections:

Input vector layer: Bronx_Tracts_2014

Clip layer: BX_Library_QuarterMiBuffer

Add result to canvas

Save the Output shapefile within the 3_AnalyzingData/Process folder as `BXTracts_LibraryQuartMiClip`. 

Click `OK` and then `Close`

![clip](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_19.png)


A new layer containing the census tracts clipped to the ¼ mile buffers around the libraries was added to your map. 

Toggle the visibility of all of of the layers on your map off except for `BXTracts_LibraryQuartMiClip`.
 ![clip](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_20.png)

**Calculating the area of the clipped census tracts**

Now we will calculate the area of these new polygons. Open the attribute table for the clipped Bronx census tracts layer: `BXTracts_LibraryQuartMiClip`, and select the field calculator.
* Create a new field
Output field name: `AreaClip`

Output field type: `Decimal number (real)`

Output field width:`10` 

Precision: `2`

Open the Geometry menu and double click on `$area`

Click `OK`
Open the field calculator and again create a new field to calculate the new area of each polygon. 

* Notice the new field that has been added to the far right of the attribute table called `AreaClip`

![clip](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_21.png)

**Dividing the the area of the clipped census tracts by their original area**

* Again open the field calculator and create a new field
Output field name: `Proportion`

Output field type: `Decimal number (real)`

Output field width:`10` 

Precision: `2`

Calculate `”AreaClip” / “Area”` -- i.e. the proportion of the original area that remained after the clip

Click `OK`

![clip](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata08_22.png)

**Multiplying the population by the proportion** 

Now we will calculate one final field where we’ll multiply the attributes (for us, population in 2014) we wish to estimate by the proportion in order to estimate the proportion of the attribute that falls within the study area. 

* Again open the field calculator and create a new field
Output field name: `Pop2014_est`

Output field type: `Decimal number (real)`

Output field width:`10` 

Precision: `2`

Calculate `"Proportion" * "Pop2014"`

Click `OK`

End the edit session and say yes to saving the changes. 


Now we will compare the total estimated population within the buffers to the original rough population estimate we made at the beginning of this exercise using the select by location tool. 

* Navigate to `Vector`>`Analysis`>`Basic Statistics`.
* Select Pop2014_es as the Target field and note the Sum: 371,042.94 
* Repeat for the population field for the entire census tract Pop2014 and note the difference: 983,821

______________________________________________________________________________________________________________

Tutorial written by Dare Brawley, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2018 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

