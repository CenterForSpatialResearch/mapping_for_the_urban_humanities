### Tutorial 3B: Geocoding historic data

#### Premise
In this tutorial, we are going to make a map of newspapers in the United States before and after the invention of the rotary printing press in 1843. We want to visualize the effect of this technological change on the access to communication across the United States.

By the end of this tutorial, you will be able to:
- identify types of data that can be used in GIS applications
- transform data you find in a table into a csv file that can be used in QGIS
- align that data to geographic locations using a gazetteer
- query the data you collected to answer a research question

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials.

### Data

One of the primary hurdles that researchers encounter is finding appropriate datasets (for QGIS and otherwise). For more on this, see the [Finding Spatial Data](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Resources/FindingSpatialData.md) page in the Resources.  

This problem is compounded when working with historic data as it may not necessarily have spatial data attached, or it may only have place names attached that may or may not represent modern place names. Ultimately, finding data and transforming data are separate issues. As far as finding data is concerned, Columbia Libraries keep a list of [GIS and spatial data resources](https://guides.library.columbia.edu/GIS) as well as the libraries' own spatial data portal [Geodata@Ciolumbia](https://geodata.library.columbia.edu/). Other good places to start include [Lehman Library's Map Collection](http://library.columbia.edu/locations/maps.html) and [CIESIN](http://sedac.ciesin.columbia.edu/data/sets/browse), the [NYPL Maps Division](https://www.nypl.org/about/divisions/map-division) the [US Census](https://www.census.gov/data.html), [NHGIS](https://www.nhgis.org/), or the [AAG Databases](http://www.aag.org/cs/projects_and_programs/historical_gis_clearinghouse/hgis_databases). This list is not comprehensive, but illustrative that data is in a lot of places. If none of these have the data you are looking for, you may need to turn to less-straightforward repositories on the Internet.

Sometimes the library may have data available, or you may find it through a web search. Assuming that you are not able to find shapefiles, you will want your data to be in a format that QGIS can parse. This includes .csv (comma separated values), .txt (plain text), or some form of database. Formats such as .pdf may pose insurmountable problems.

In this tutorial, we will go through the process of turning data that we find through an internet search into data we can use in a mapping project. This is not the only way to get data, and often not the best way. At Columbia, the librarians may be more helpful than the internet in locating data sources. But learning these techniques will also help you start to think about less-than-obvious places data can be found.

### Making the Data

We are going to use data from [Readex](https://www.readex.com/who-we-are-what-we-do), a company that sells primary source collections to institutions. We want the names of newspapers, the location of publication, and the year they were established. We are not interested in reading the papers right now. Readex offers these lists in a variety of organizations: by region, decade, or era. We will use the 'By Era' breakdown, and look at the pre- and post-1842 eras.

Open a web browser (Google Chrome, Firefox, or Safari are OK, please do not use Internet Explorer), and navigate to [www.readex.com](www.readex.com). Hover over the 'Collections' link in the Navigation bar and under the "Early American Newspapers" list, click on 'By Era'. Then select `Jacksonian Era, Parts 1 and 2, 1823-1842` > `Title List`, opening it in a new tab.

Also open the `Antebellum Period, Parts 1 and 2, 1843-1860` > `Title List`

![readex1]


![readex2]

Looking at this website, we suspect that the data is organized as a table because there are columns, column headers, and all the data in each column lines up nicely.

![readex3]

This is fortunate because whenever data is in an organized format, there are a host of simple tools to help us translate that data. Today, we are going to use Google Drive to format the table nicely for our use.

#### Making Tables into CSVs

Go to Google Drive and log in to your account. You actually don't need to save anything to your account, but you do need to log in. <!--If you do not have a Google Account and do not wish to create one, please skip this section.--> <!--columbia webmail is google, and has google drive, so everyone in the course has a google account-->

(Note: If you have any trouble with this step, the data is already included in the `Class Data` folder. You can find it there and continue with the rest of the tutorial. If you are familiar with webscraping, you can also get the You can also gather this data through webscraping, but that is far beyond the scope of this tutorial.)

In Google Drive, click on the `New` button in the upper left hand corner, and select `Sheet`. This will take you to an empty Google Sheet.

In the first cell (cell A1), type the following formula and hit 'Enter':

`=IMPORTHTML("https://www.readex.com/titlelists/jacksonian-era-parts-1-and-2-1823-1842", "table", 1)`

![google sheet options]


Let's break that expression down. Google Sheets has a function, `IMPORT HTML`, which imports and parses content found on websites. For this function to work in our Sheet, anything that is words has to be enclosed in quotes because we  want the Sheet to just match the words, not *evaluate* them<!--will see if there is link to explain strings versus values-->. First, we tell it which website we want it to read by giving it the exact url (first, for the Readex Jacksonian Era), then tell the function if it should look for a "table" or a "list"; we want a "table". Those are the only types this particular function can work with, but that's enough for us. Finally, which table (or list) it should look for (the first, second, etc.). Once we hit 'Enter', it goes out and reads the website, sees if there is a table where we told it to look and then pulls in the data.

For more on this function, click on the 'Learn More about IMPORTHTML' link at the bottom of the dialogue box. Google sheets also has IMPORT XML (for structured data online), FEED (for RSS feeds), DATA (for data hosted online), or RANGE (for portions of other Google Sheets) for different types of data.

![google sheet help]

Now we will save our sheet as a csv. Navigate to File >> Download as >> Comma-separated values (.csv, current sheet). Save it in the Class_Data/Tutorial3B_Geocoding Folder

![save csv]

Now add another sheet at the bottom of the page (or overwrite the one we just made) and do the same for the newspapers listed on the Antebellum Era website.


#### Cities Data

We now need to find a list of cities so we can geolocate these places. The list we are using is from [www.data.gov](https://catalog.data.gov/dataset/place-national), it has already been downloaded for you as a csv (and modified in the way that we need), and is in the Class_Data/Tutorial3B_Geocoding folder, `uscities.csv`. This is a modern list of US cities, and as such, there may be some discrepancies, as some place names may have changed since the mid-19th century (luckily, none of these will impact our project). We also know that the biggest changes between then and now are the shape of the counties more than the names of the cities. Columbia University Libraries keeps a [collection of historical place names](http://www.columbiagazetteer.org/static/using_gazetteer) with geographic information for just this purpose, many of which reference ancient times as well as modern.

Let's take a look at our cities data by opening it in any program that can read a csv (e.g., LibreOffice, Excel, Google Sheets, Sublime Text, etc.). We see that there are two "unique" identifiers: `city_state`, and the last column, `id`. I made that `city_state` column — data rarely arrives with a column that is both redundant and complicated (i.e., it has 2 pieces of information). However, for the geocoding step, we need a column that contains both the city and state information.

This column will also allow us to do a lookup with our newspapers data, serving as a sort of dictionary of places, and will allow us to match the place names.

#### Make an Address Field

For the Geocoding, we will need one field that contains ALL of the address data. We want to make that *before* we start our project. To make this field, we need to CONCATENATE the city and state columns. There are instructions here for Excel and Google Drive users. You can also do this in LibreOffice, the process is similar, though there are no images here.

**EXCEL**

Open one of your newspapers files in Excel (it does not matter which one, you will have to do this for both files anyhow).

Insert a column between the \*State\* and \*Start Date\* columns by clicking on the 'Column D' box to highlight the whole column, then right click and select 'Insert'. A new column will appear.

![insert]

In the first cell of that column, type `city_state` with no space between the words - use an underscore instead (this is just good naming convention). In the next cell (D2), type the following formula: `=CONCATENATE(B2, ", ", C2)` and hit 'Enter'. The new field should appear.


![formula]

Hover over the little square in the bottom right hand corner of the cell and your cursor should turn into a black hatch mark. Once it does, click and drag this cell down to populate all of the rows.

![excel]

Your file should look like this now:

![paper]

Save your file as a .csv. You will get a warning message, select 'Continue'

![warning]

Repeat this process for the other newspaper file.

**GOOGLE DRIVE**

If you saved your file to your Google Drive, open it from there. Otherwise, import it by clicking on the `New` button in the upper left corner, and the `File Upload`, and select the newspaper you want to start with. Once you upload it, open it in Google Drive, and then click on `Open in Google Sheets` at the top of the window.

Insert a column between the \*State\* and \*Start Date\* columns by clicking on the 'Column D' box to highlight the whole column, then right click and select 'Insert 1 left'. A new column will appear.

![insert2]

In the first cell of that column, type `city_state` with no space between the words - use an underscore instead (this is just good naming convention). In the next cell (D2), type the following formula: `=CONCATENATE(B2, ", ", C2)` and hit 'Enter'. The new field should appear.

![formula2]

Hover over the little square in the bottom right hand corner of the cell and your cursor should turn into a black hatch mark. Once it does, click and drag this cell down to populate all of the rows.

![excel2]

Your file should look like this now:

![papers]

Download your sheet as a csv file the same way we did before. Move it to the Class_Data/Tutorial3B_Geocoding folder. You can (and should) rename these files.

Repeat this process for the other newspaper file.


### Set Up

Open a new QGIS project.


In their original form, the newspapers files we just downloaded do not have any geographic information attached to them, so we will have to add it. But before we get started, we would like a basemap, so first, add the counties file from the Mapping Data tutorial.  

**Click** on the `Add Data Source Manager` button, select the `Vector` tab and open the `US_county_1850_Albers.shp` file from the Class_Data/Tutorial3B_Geocoding folder.

If the map of the US comes out very stretched at the top, change the *project* projection by clicking on the number in the bottom right corner. Change the projection to `USA_Contiguous_Albers_Equal_Area_Conic` or EPSG: 102003, this is the projection of the counties file.

![projection]

Now add the `uscities.csv layer` by using the  `Add Data Source Manager` button, and selecting `Delimited Text`. Use options:
- csv
- point coordinates
	- X field: 'lng'
	- Y Field: 'lat'

![view csv]

The uscities layer will be essential for matching the cities in our newspapers files with geolocated places.

**TROUBLESHOOTING**

If you only get one point in the middle of the US when you add your cities layer, right click on the cities layer, navigate to Properties >> General. change the Coordinate reference system to `Default CRS WGS 84` EPSG: 4326

![Layer properties]

**END TROUBLESHOOTING**

Finally, add **both** of the Newspapers layers you just created using the `Add Data Source Manager` button, and make the following selections:
- csv
- No geometry (attribute only table)

![Add csv]

Finally, we will need another plugin - actually a group of plugins. Install the MMQGIS plugin. Navigate to Plugins >> Manage and Install Plugins

![mmqgis]

Search for MMQGIS and Select `Install Plugin`

![mmqgis2]

SAVE your project in the Tutorials/Exercises folder.

### Geocoding

Now that we have all of our data loaded into QGIS, we need to align the place names in our newspapers with geographic data. I am going to start with the Antebellum file, you will do the same set of steps for the Jacksonian files. HINT: we will have to fix our Antebellum file and reimport it. The problem will exist in the Jacksonian file, too... You may want to fix the problem *before* doing all of these steps.

Generally, there are two ways to go about geocoding. The first is to do a table join, matching records 1:1. If we had tabulated data, this would be our strategy. For example, if we had a list of how many newspapers were in each city, and each city only appeared once. We did this in the Mapping Data tutorial. However, if we have multiple records for the same city, we cannot do a table join, since there is no unique identifier. This is our situations, so we will have to make our own *geocoder* from a *gazetteer*

Table Join **will** work for this data:

![tablejoin]

Table Join will **NOT** work for this data:

![tablejoin2]

The uscities layer will become our gazeteer. A gazetteer is essentially a "lookup" file, kind of a geographic dictionary. Rather than matching columns 1:1, QGIS goes through every item in our newspapers file and matches it with an item in the uscities file. For this to work, though, there must be one column in both files that is formatted the exact same way. We already made this: it's our cities_states column.

Let's get started with the Antebellum Newspapers

Navigate to MMQGIS >> Geocode >> Street Address Join

![Address join]

Make the following selections:

- Input CSV File: AntebellumNewspapers.csv
- CSV File Address Field: city_state
- Shape Layer: uscities
- Shape Layer Address Field: city_state
- Output Shapefile: Tutorial3B_Geocoding/AntebellumStreetAddressJoin
- Not Found CSV Output List: Tutorial3B_Geocoding/AntebellumNotFound

![Address join2]

Click `OK` and wait... This is a long process.

Once it is complete, a new layer will appear in your layers pane. Open the Attribute table for this layer. Each row should have both the geographic information and the newspaper information.

![geocode table]

Now let's go check our 'not found layer and see what problems arose. In not found, we have three categories of problems:

Washington, DC was formatted in a strange way, and some cities did not appear.

![Not found]

Since this is a relatively small dataset, we will fix these problems in the original dataset (this is why we saved a set of files in the `Originals` Folder) and then re-do the geocoding.

First, let's fix the Washington, DC problem. Open the `uscities Attribute Table`, and sort by `city` to find how Washington, DC is formatted in the `city_state column`. Now open the **AntebellumNewspapers.csv** file (in either Excel or Google Sheets). Find and Replace 'Washington (DC)' with 'Washington'. Save this file.

In Excel:
![excel replace]

In Google Sheets:
![sheets replace]

Now on to the other problems. I did a web search for each place to get more information about where it is located and other names it may be called. This works because our dataset is small. Your data management strategy always depends on your project.

**May's Landing** is an unincorporated community and census-designated place located within Hamilton Township. In the AntebellumNewspapers file, change the city_state column to say 'Hamilton, NJ'. However,  keep May's Landing in the city column, because we don't want to lose that information. This column now has unique information in it.

**Sing-Sing** likely refers to the prison (which did have a printing press in the mid-1800's). Sing Sing Correctional Facility is in the village of Ossining, NY. We will fix this entry in the AntebellumNewspapers file the same way we fixed May's Landing.

**Rondout** was originally a maritime village serving the nearby city of Kingston, NY, Rondout merged with Kingston in 1872. We will fix this entry in the AntebellumNewspapers file the same way we fixed May's Landing.

That is all of the problems. Save this file (or Download, if using Google Sheets).

Return to QGIS. Remove the AntebellumNewspapers layer (both the delimited text file and the points layer). Right-click and select `Remove`. Upload your corrected AntebellumNewspapers.csv file as a `Delimited Text Layer` with no geometry, and complete the geocoding steps again.

Navigate to MMQGIS >> Geocode >> Street Address Join
Make the following selections (overwrite the files you made before):

- Input CSV File: AntebellumNewspapers.csv
- CSV File Address Field: city_state
- Shape Layer: uscities
- Shape Layer Address Field: city_state
- Output Shapefile: Tutorial3B_Geocoding/AntebellumStreetAddressJoin
- Not Found CSV Output List: Tutorial3B_Geocoding/AntebellumNotFound

![Address Join2]

Click `OK`.

Once it finishes loading, check the AntebellumNotFound.csv file one last time to make sure everything is ok.

Follow the same steps for the JacksonianNewspapers file. Start with the corrections you know are problems before running it for the first time.

Once the Antebellum layer loads, remove and upload the new JacksonianNewspapers.csv file and geocode it using the same steps.

Once that completes, open the JacksonianNotFound file and make the necessary changes to the JacksonianNewspapers.csv (you may have to cross reference with the uscities file and internet searches to understand what is going on, and there may be some issues with alternative spellings).

Geocode the JacksonianNewspapers.csv file again.


#### Cleaning the results

We want to remove some of the layers either because they are redundant or because they do not align to our time period.

Open the Attribute table for the AntebellumStreetAddressJoin layer.

Click on the `Edit` button, and select the `Delete Field` button. Then, delete the following fields:

- county_fip  (because the historic county names are different from these modern county names)
- county_nam
- \*State\* (because this field is redundant. Note that \*City\* is not redundant)
- city_stat2

![Delete fields]


Save your changes.

Do the same for the JacksonianStreetAddressJoin layer.

### Visualizing the results

Turn off the uscities layer if it is still on. We will style the points so they are a bit easier to see, and make the county boundaries slightly less obtrusive.

First select properties of the US_county_1850 layer. Select the `Style` tab on the left. Click on the `Simple Line`, and change the color to a dark grey and/or change the line width to .200 or smaller if you like. *Note*: It may have defaulted to `Simple Fill` rather than `Simple Line`; that's fine, you can still change the line weight by adjusting `Outline Width`.

![Line symbol]

Now click on the Jacksonian points layer, and select Properties >> Style

Click on `Marker`, and change the color to something brighter (I've used pink), and the size to something larger (I've used 3.00 mm).

Repeat with the Antebellum layer.

Process to use the print composer (as we did in the Mapping Data Tutorials) to make two maps:
- one of the Jacksonian Era Newspapers (1823-1842, before the expansion of the railroads and the invention of the rotary printing press)
- one of the Antebellum Era Newspapers (1843-1860, before the expansion of the railroads and after the invention of the rotary printing press).

Note: These maps are not very good: it's almost impossible to tell how many newspapers exist in the northeast, but it is a good first pass.

![Jacksonian Map]

![Antebellum Map]


______________________________________________________________________________________________________________

Tutorial written by Michelle McSweeney, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2018 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

[readex1]: Images/2019/Geocoding_01.png
[readex2]: Images/2019/Geocoding_02.png
[view csv]: Images/2019/Geocoding_03.png
[readex3]: Images/2019/Geocoding_04.png
[google sheet options]: Images/2019/Geocoding_06.png
[google sheet help]: Images/2019/Geocoding_07.png
[save csv]: Images/2019/Geocoding_08.png
[Add csv]: Images/2019/Geocoding_09.png
[projection]: Images/2019/Geocoding_10.png
[insert]: Images/2019/Geocoding_12.png
[formula]: Images/2019/Geocoding_13.png
[excel]: Images/2019/Geocoding_14.png
[paper]: Images/2019/Geocoding_15.png
[insert2]: Images/2019/Geocoding_16.png
[formula2]: Images/2019/Geocoding_17.png
[excel2]: Images/2019/Geocoding_18.png
[papers]: Images/2019/Geocoding_19.png
[warning]: Images/2019/Geocoding_20.png
[Layer properties]: Images/2019/Geocoding_21.png
[tablejoin]: Images/2019/Geocoding_22.png
[tablejoin2]: Images/2019/Geocoding_23.png
[mmqgis]: Images/2019/Geocoding_24.png
[mmqgis2]: Images/2019/Geocoding_25.png
[Address join]: Images/2019/Geocoding_26.png
[Address join2]: Images/2019/Geocoding_27.png
[geocode table]: Images/2019/Geocoding_28.png
[Delete fields]: Images/2019/Geocoding_29.png
[Not found]: Images/2019/Geocoding_30.png
[excel replace]: Images/2019/Geocoding_32.png
[sheets replace]: Images/2019/Geocoding_33.png
[Line symbol]: Images/2019/Geocoding_35.png
[Jacksonian Map]: Images/2019/Geocoding_37.png
[Antebellum Map]: Images/2019/Geocoding_38.png
