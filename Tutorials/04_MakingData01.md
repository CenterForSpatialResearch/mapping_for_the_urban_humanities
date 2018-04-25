## Making Data 

### Making Data 01: Geocoding historic data

#### Premise
In this tutorial, we are going to make a map of newspapers in the United States before and after the invention of the rotary printing press in 1843. We want to visualize the effect of this technological change on the access to communication across the United States (if you want to take this to the next level, you could combine this project with the rairoads data from Tutorial [03_MappingData02](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Tutorials/03_MappingData02.md)).

By the end of this tutorial, you will be able to:
- identify the types of data that can be used
- transform data you find in a table into a csv file that can be used in QGIS
- align that data to geographic locations using a gazetteer
- query the data you collected to answer a research question

#### Before you begin
If you haven't already, download the GitHub repository for this course. Using the green button [here](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities), select `Download ZIP`. The Class_Data folder will then have all of the datasets needed for tutorials. 

### Data

One of the primary hurdles that researchers encounter is finding appropriate datasets (for QGIS and otherwise). This problem is compounded when working with historic data as it may not necessarily have spatial data attached or it may only have place names attached that may or may not represent modern place names. Ultimately, finding data and transforming data are separate issues. As far as finding data is concerned, Columbia keeps a list of [Spatial Data on the Internet](http://library.columbia.edu/locations/dssc/data/spatialdata.html), as well as [Lehman Library's Map Collection](http://library.columbia.edu/locations/maps.html) and [CIESIN](http://sedac.ciesin.columbia.edu/data/sets/browse), the [NYPL Maps Division](https://www.nypl.org/about/divisions/map-division) the [US Census](https://www.census.gov/data.html), [NHGIS](https://www.nhgis.org/), or the [AAG Databases](http://www.aag.org/cs/projects_and_programs/historical_gis_clearinghouse/hgis_databases) are a good place to start (this list is obviously not comprehensive, but illustrative that data is in a lot of places). If none of these have the data you are looking for, you may need to turn to repositories on the Internet. 

Sometimes the library may have data available, or you may find it through a web search. Assuming that you are not able to find shapefiles, you will want your data to be in a format that QGIS can parse. This includes .csv (comma separated values), .txt (plain text), or some form of database. Formats such as .pdf may pose insurmountable problems. 

We will go through the process of turning data that we find through an internet search into data we can use in a mapping project. This is not the only way to get data, and at Columbia, the librarians may be more helpful than the internet in this regard.  

### Making the Data

We are going to use data from [Readex](https://www.readex.com/who-we-are-what-we-do), a company that sells primary source collections to institutions. We want the names of newspapers, the location of publication, and the year they were established. We are not interested in reading the papers right now. Readex offers these lists in a variety of organizations: by region, decade, or era. We will use the 'By Era' breakdown, and look at the pre- and post-1842 eras. 

Open a web browser (Google Chrome, Firefox, or Safari are OK, please do not use Internet Explorer), and navigate to [www.readex.com](www.readex.com). Hover over the 'Collections' link in the Navigation bar and click on 'By Era'. Then select the `Jacksonian Era, Parts 1 and 2, 1823-1842` > `Title List` it will open in a new tab.

Also open the `Antebellum Period, Parts 1 and 2, 1843-1860` > `Title List`

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_01.png)


![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_02.png)

Looking at this website, we suspect that the data is organized as a table because there are columns, column headers, and all the data in each column lines up nicely. 

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_04.png)

This is fortunate because whenever data is in an organized format, there are a host of simple tools to help us translat that data. Today, we are going to use Google Drive to format the table nicely for our use. 

#### Making Tables into CSVs

Go to Google Drive and log in to your account. You actually don't need to save anything to your account, but you do need to log in. If you do not have a Google Account and do not wish to create one, please skip this section. You will use the same dataset that has already been downloaded for you in the class folder. You can also gather this data through webscraping, but that is far beyond the scope of this tutorial. 

In Google Drive, click on the `New` button in the upper left hand corner, and select `Sheet`. This will take you to an empty Google Sheet. 

In the first cell (cell A1), type the following formula and hit 'Enter':

`=IMPORTHTML("https://www.readex.com/titlelists/jacksonian-era-parts-1-and-2-1823-1842", "table", 1)`

![google sheet options](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_06.png)


Let's break that expression down. Google Sheets has a function, `IMPORT HTML`, which imports and parses content found on websites. For this function to work in our Sheet, anything that is words has to be enclosed in quotes because we  want the Sheet to just match the words, not *evaluate* them. First, we tell it which website we want it to read by giving it the exact url ( for the Readex Jacksonian Era), then tell the function if it should look for a "table" or a "list"; we want a "table". Those are the only types this particular function can work with, but that's enough for us. Finally, which table (or list) it should look for (the first, second, etc.). Once we hit 'Enter', it goes out and reads the website, sees if there is a table where we told it to look and then pulls in the data. 

For more on this function, click on the 'Learn More about IMPORTHTML' link at the bottom of the dialogue box. Google sheets also has IMPORT XML (for structured data online), FEED (for RSS feeds), DATA (for data hosted online), or RANGE (for portions of other Google Sheets) for different types of data.

![google sheet help](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_07.png)

Now we will save our sheet as a csv. Navigate to File >> Download as >> Comma-separated values (.csv, current sheet). Save it in the Class_Data/2_MakingData Folder

![save](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_08.png)

Now add another sheet at the bottom of the page (or overwrite the one we just made) and do the same for the newspapers listed on the Antebellum Era website.


#### Cities Data

We now need to find a list of cities so we can geolocate these places. The list we are using is from [www.data.gov](https://catalog.data.gov/dataset/place-national), it has already been downloaded for you as a csv (and modified in the way that we need), and is in the Class_Data/2_MakingData folder. This is a modern list of US cities, and we may find some discrepancies (although none that impact our project). We also know that the biggest changes between then and now are the shape of the counties more than the names of the cities. Columbia University Libraries keeps a [collection of historical place names](http://www.columbiagazetteer.org/static/using_gazetteer) with geographic information for just this purpose: many of which reference ancient times as well as modern.

Let's take a look at our cities data by opening it in any program that can read a csv (i.e., Excel, Google Sheets, Sublime, etc.). We see that there are two **UNIQUE** identifiers: `city_state`, and the `city_ID`. I made that 'city_state' column - data rarely arrives with a column that is both redundant and complicated (i.e., it has 2 pieces of information). It's actually not that good of an identifier since so many town have different spellings. However, for the geocoding step, we will need one column that contains the city and state. 

This column allows us to do a lookup with our newspapers data, it serves as a sort of dictionary of places, and will allow us to match the place names. 

#### Make an Address Field 

For the Geocoding, we will need one field that contains **ALL** of the address data. We want to make that BEFORE we start our project. To make this field, we need to CONCATENATE the city and state columns. There are instructions here for Excel and Google Drive users. If you do not use either of those programs, you can do this in Libre Office, for which the process is very similar. 

**EXCEL**

Open one of your newspapers files in Excel (it does not matter which one, you will have to do this for both files anyhow). 

Insert a column between the \*State\* and \*Start Date\* columns by clicking on the 'Column D' box to highlight the whole column, then right click and select 'Insert'. A new column will appear. 

![insert](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_12.png)

In the first cell of that column, type `city_state` with no space between the words - use an underscore instead (this is just good naming convention). In the next cell (D2), type the following formula: `=CONCATENATE(B2, ", ", C2)` and hit 'Enter'. The new field should appear. 


![formula](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_13.png)

Hover over the little square in the bottom right hand corner of the cell and your cursor should turn into a black hatch mark. Once it does, click and drag this cell down to populate all of the rows. 

![excel](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_14.png)

Your file should look like this now:

![paper](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_15.png)

Save your file as a .csv. You will get a warning message, select 'Continue'

![warning](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_20.png)

Repeat this process for the other newspaper file. 

**GOOGLE DRIVE** 

If you saved your file to your Google Drive, open it from there. Otherwise, import it by clicking on the `New` button in the upper left corner, and the `File Upload`, and select the newspaper you want to start with. Once you upload it, open it in Google Drive, and then click on `Open in Google Sheets` at the top of the window.

Insert a column between the \*State\* and \*Start Date\* columns by clicking on the 'Column D' box to highlight the whole column, then right click and select 'Insert 1 left'. A new column will appear.

![insert](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_16.png)

In the first cell of that column, type `city_state` with no space between the words - use an underscore instead (this is just good naming convention). In the next cell (D2), type the following formula: `=CONCATENATE(B2, ", ", C2)` and hit 'Enter'. The new field should appear. 

![formula](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_17.png)

Hover over the little square in the bottom right hand corner of the cell and your cursor should turn into a black hatch mark. Once it does, click and drag this cell down to populate all of the rows. 

![excel](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_18.png)

Your file should look like this now:

![papers](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_19.png)

Download your sheet as a csv file the same way we did before. Move it to the Class_Data/2_MakingData folder. You can (and should) rename these files.

Repeat this process for the other newspaper file. 


### Geocoding 

The newspapers files, as they are written actually do not have any geographic information attached to them. We would like a basemap to begin with, so **FIRST**, add the counties file from the Mapping Data tutorial.  

**Click** on the `Add Vector Layer` button, and open the `US_county_1850_Albers.shp` file from the Class_Data/1_MappingData/Shape Folder folder. If you like, you can add the file we joined the population data to `US_county_1850_Albers_PopJoin.shp` instead; we won't use it in this tutorial, but if you want to investigate the relationship with population on your own later, it will save you a step.

If the map of the US comes out very stretched at the top, change the projection by clicking on the number in the bottom right corner. Change the projection to `USA_Contiguous_Albers_Equal_Area_Conic` or EPSG: 102003, this is the projection of the counties file.

![projection](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_10.png)

Now add the `uscities.csv layer` using the `Delimited Text Layer` button, and make the following selections:
- csv
- point coordinates
	- X field: 'lng'
	- Y Field: 'lat'

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_03.png)

**TROUBLESHOOTING**

If you only get one point in the middle of the US when you add your cities layer, right click on the cities layer, navigate to Properties >> General. change the Coordinate reference system to `Default CRS WGS 84` EPSG: 4326

![qgis](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_21.png)

**END TROUBLESHOOTING**

Finally, add **both** of the Newspapers layers you just created using the `Delimited Text Layer` button, and make the following selections:
- csv
- No geometry (attribute only table)

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_09.png)

Now we have all of our data loaded into QGIS, we need to align the place names in our newspapers with geographic data. There are two ways to go about doing this. The first would be to do a table join, matching records 1:1. If we had tabulated data, this would be our strategy. For example, if we had a list of how many newspapers were in each city, this would be our strategy. We did this in the Mapping Data tutorial. However, if we have multiple records for the same city, we cannot do a table join, since there is no unique identifier. Instead, we will have to make our own *geocorder* from a *gazetteer*

Table Join **will** work for this data:

![tablejoin](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_22.png)

Table Join will **NOT** work for this data:

![geocodeme](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_23.png)

The uscities layer will become our gazeteer. Our gazetteer is essentially a "lookup" file. Rather than matching 1:1, QGIS goes through every item in our newspapers file and matches it with an item in the uscities file. For this to work, though, there must be one column in both files that is formatted the exact same way. We already made this: it's our cities_states column. We also need the MMQGIS plugin. 





	
	