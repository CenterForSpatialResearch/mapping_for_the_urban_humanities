### Analyzing Data 03: Schools, Libraries and Raster Analysis

### Premise
You will return to the analysis of schools and libraries we were conducting in Part One of this exercise, however, you will now use raster analysis tools to answer similar questions through slightly different means and for the entirety of New York City. You want to know which parts of New York City have the greatest access to schools and libraries. You will answer this using a raster-based decision map.

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

#### Let's begin

Open QGIS:
![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze31.png)

With the Add Vector Layer tool ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze32.png), add the NYC_Libraries.shp and NYC_Schools.shp layers from the MappingForTheUrbanHumanities-master\Class_Data\3_AnalyzingData\Shape directory. 

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze33.png)

These point layers represent primary and secondary schools and public libraries throughout New York City. 
Since you will be conducting a raster based proximity analysis, you will first convert these point based features to a raster layer.  Under the raster layer, choose Conversion>Rasterize (Vector to Raster):

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze34.png)

The Rasterize (Vector to Raster) window opens:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze35.png)

This tool will convert the libraries to a raster format.  Choose NYC_Libraries as the input file. Choose the “raster” field as the attribute value.  Note, the "raster" variable in the library attribute table has a value of one for each feature, and works somewhat like a dummy variable for creating the binary raster that will be the output.  Save the output as NYCLibraryRaster.tif in the working directory for this exercise. You will have to choose a raster resolution for the output map.  Since the datasets are in state plane, with the units expressed in feet, it is intuitive to use the “raster resolution in map units per pixel” option.  Enter a resolution for 50 units (or feet) for both the horizontal and vertical options:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze36.png)

There is one more step that you need to address before running the tool. For raster analysis you need to define the processing extent for the output file.  In essence, you need to tell the software what area to run the calculation for.  Otherwise, the tool would continue to run for the entire Earth!  By default, the rasterize tool will use the extent of the input file (NYC_Libraries).  This is not a good choice for two reasons.  First, you will want to make sure that your analysis will run for the entire city, even if those areas are outside the library extents.  Second, you want to be sure that all the rasters that you are using for this exercise have the identical extent and resolution. Thus, you must specify the processing extent.
Unfortunately, there are no automated methods to specify the processing extent in this tool.  You will need to specify it directly into the GDAL command line, the text box in the bottom on the tool. Click on the edit ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze39.png)
button to edit the GDAL command line.  You can enter the processing extent in the line after “gdal_rasterize.”  You will use the “–te” statement to define the extent, this statement takes the form “-te xmin ymin xmax ymax” Enter the statement as follows: “-te 550000 600000 730000 770000”. Your window should look like this:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze37.png)

The raster will add to the map.  It may look like a solid field, this is fine.  Each library location will appear as a single raster with a value of one and they may be imperceptable at this extent.

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze38.png)

Run the rasterize tool again for the NYC_Schools Layer.  Choose NYC_Schools as the input file. Again, choose the “raster” field as the attribute value. Save the output as NYCSchoolRaster.tif in the working directory for this exercise. Once again choose the “raster resolution in map units per pixel” option and enter a resolution of 50 units for both the horizontal and vertical options.  Click on the edit![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze39.png) button to edit the GDAL command line and enter the statement “-te 550000 600000 730000 770000” after “gdal_rasterize”:

 ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze310.png) 
 
 Click OK:
 
![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze311.png)

Next, you will create proximity based raster layers representing the distances to libraries and schools. First, you will calculate distances to the nearest library.  Under the raster menu, click on Analysis>Proximity:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze312.png)

Use NYCLibraryRaster as the input file and save the output file as NYCLibraryDistance.tif in the working directory. Make sure to select “geo” for dist units:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze313.png)

You should not need to specify the extent or raster resolution this time as the tool will automatically use the extent and cell size of the input file.  Click OK.

The resultant raster will represent the distance in feet to the nearest library:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze314.png)

Next, you will calculate distances to the nearest school using the same process.  
Under the raster menu, click on Analysis>Proximity:

Use NYCSchoolRaster as the input file and save the output file as NYCSchoolDistance.tif in the working directory. Make sure to select “geo” for dist units:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze315.png)

Click OK: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze316.png)

Now you will generalize these proximity based rasters into discrete distance classes.  Specifically, you will classify the proximity based rasters into classes of 0-¼ mile, ¼-½, mile, ½ - ¾ mile and above ¾ mile distances.

Unfortunately, there are no simple to use tools for this in QGIS.  You will need to use one of the built in GRASS tools for this. Open the processing toolbar by choosing Toolbox under the processing menu:


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze317.png)

The processing toolbox should open on the right hand side of the screen: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze318.png)

Expand the GRASS commands in the processing toolbar and then expand the Raster command set.  Open the “r.reclass” command: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze319.png)

This tool requires that you build a reclass rules file in order to define the classes.  This needs to be a text file containing the needed ranges. Open a text editor (Notepad in Windows or TextEdit in MacOS will work for this) and type:

0 thru 1319.99 = 1

1320 thru 2639.99 = 2

2640 thru 3959.99 = 3

3960 thru 82000 = 4



![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze320.png)

Save the file as DistanceClassifications.txt in your work directory.

In the r.reclass tool menu, choose NYCLibraryDistance as the input file.  Add the DistanceClassifications.txt file you just made as the file containing reclass rules.  Choose 50 as your cellsize.  Save the “reclassified” output to your working directory as NYCLibraryDistanceReclass.tif:


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze321.png)

Click Run.  The result should add automatically to QGIS.  Note that you can now clearly see the reclassified “bands” of values:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze322.png)

Run the same r.reclass command for the NYCSchoolDistance raster.  Use the same settings and the same DistanceReclass.txt file.  Save the “Reclassified” Output as NYCSchoolDistanceReclass.tif:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze323.png)

Click Run. Again, the result should add automatically to QGIS: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze324.png)

Note that the r.reclass command in QGIS confusingly names all the output “Reclassified” making it difficult to determine which layer is being referenced.  However, you can change the names in the layer panel by right-clicking on the two “Reclassified” layers and choosing “rename.”  Rename the two layers “ReclassifiedLibrary” and “ReclassifiedSchools” respectively.  

Now you will combine these two reclassified distance rasters into one by adding the two values together.  This can be done in the raster calculator.  Under the raster menu, choose “raster calculator”:


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze325.png)

In the raster calculator, simply add the two layer together. The raster calculator expression should thus be: "ReclassifiedLibrary@1" + "ReclassifiedSchools@1"  Set the output layer as SchoolLibraryDistanceWeightEqual:


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze326.png)

Click OK.

The output file should add automatically to QGIS: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze327.png)

Note that the raster values now range from 2-8, giving an overall measure of proximity to both schools and libraries for all parts of the city.

The calculation above gives equal weight to both libraries and schools.  You can also run the same calculation but giving greater weight to the libraries. 
 
One way to do this is by using the raster calculator.  You can triple the influence of the library locations in this model by multipieng the orginal NYCLibraryDistanceReclass raster by three. Open the raster calculator and enter the equation "ReclassifiedLibrary@1" * 3.  Save the Output as ReclassifiedLibraryTimes3 in your working directory:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze333.png)

Click OK.

The new raster should add automatically to QGIS

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze334.png)

Note that this result looks identical to ReclassfiedLibrary only the values are from 3-12 as opposed to 1-4. 

Now you will use the raster calculator again to add this new raster to the rReclassifiedSchool raster.  Open the raster alculator in the raster menu.   Enter the equation "ReclassifiedSchools@1" + "ReclassifiedLibraryTimes3@1".  Save the file as DistanceLibraryWeight:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze335.png)

Click OK. 

The output should add automatically to QGIS: 

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze336.png)

Note that the raster values now range from 4-16, reflecting the higher weight to the library distances.


______________________________________________________________________________________________________________

Tutorial written by Eric Glass, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2016 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).


