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

One of the primary hurdles that researchers encounter is finding appropriate datasets (for QGIS and otherwise). This problem is compounded when working with historic data as it may not necessarily have spatial data attached or it may only have place names attached that may or may not represent modern place names. Ultimately, finding data and transforming data are separate issues. As far as finding data is concerned, Columbia's [Lehman Library's Map Collection](http://library.columbia.edu/locations/maps.html) and [CIESIN](http://sedac.ciesin.columbia.edu/data/sets/browse), the [NYPL Maps Division](https://www.nypl.org/about/divisions/map-division) the [US Census](https://www.census.gov/data.html), [NHGIS](https://www.nhgis.org/), or the [AAG Databases](http://www.aag.org/cs/projects_and_programs/historical_gis_clearinghouse/hgis_databases) are a good place to start (this list is obviously not comprehensive, but illustrative that data is in a lot of places). If none of these have the data you are looking for, you may need to turn to repositories on the Internet. 

Sometimes the library may have data available, or you may find it through a web search. Assuming that you are not able to find shapefiles, you will want your data to be in a format that QGIS can parse. This includes .csv (comma separated values), .txt (plain text), or some form of database. Formats such as .pdf may pose insurmountable problems. 

We will go through the process of turning data that we find through an internet search into data we can use in a mapping project. This is not the only way to get data, and at Columbia, the librarians may be more helpful than the internet in this regard.  

### Making the Data

We are going to use data from [Readex](https://www.readex.com/who-we-are-what-we-do), a company that sells primary source collections to institutions. We want the names of newspapers, the location of publication, and the year they were established. We are not interested in reading the papers right now. Readex offers these lists in a variety of organizations: by region, decade, or era. We will use the 'By Era' breakdown, and look at the pre- and post-1842 eras. 

Open a web browser (Google Chrome, Firefox, or Safari are OK, please do not use Internet Explorer), and navigate to [www.readex.com](www.readex.com). Hover over the 'Collections' link in the Navigation bar and click on 'By Era'. Then select the `Jacksonian Era, Parts 1 and 2, 1823-1842` > `Title List` it will open in a new tab.

Also open the `Antebellum Period, Parts 1 and 2, 1843-1860` > `Title List`

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_01.png)

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_02.png)

Looking at this website, we suspect that the data is organized as a table. 

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_04.png)

This is fortunate because whenever data is in an organized format, there are a host of simple tools to help us translat that data. Today, we are going to use Google Drive to format the table nicely for our use. 

#### Making Tables into CSVs

Go to Google Drive and log in to your account. You actually don't need to save anything to your account, but you do need to log in. If you do not have a Google Account and do not wish to create one, please skip this section. You will use the same dataset that has already been downloaded for you in the class folder. You can also gather this data through webscraping, but that is far beyond the scope of this tutorial. 

In Google Drive, click on the `New` button in the upper left hand corner ![google drive new button](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_05.png), and select `Sheet`. This will take you to an empty Google Sheet. 

In the first cell (cell A1), type the following formula and hit 'Enter':

`=IMPORTHTML("https://www.readex.com/titlelists/jacksonian-era-parts-1-and-2-1823-1842", "table", 1)`

![google sheet options](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_06.png)


Let's break that down. Google Sheets has a function, `IMPORT HTML`, which imports and parses content found on websites. For this function to work in our Sheet, anything that is words has to be enclosed in quotes because we  want the Sheet to just match the words, not *evaluate* them. First, we tell it which website we want it to read by giving it the exact url ( for the Readex Jacksonian Era), then tell the function if it should look for a "table" or a "list"; we want a "table". Those are the only types this particular function can work with, but that's enough for us. Finally, which table (or list) it should look for (the first, second, etc.). Once we hit 'Enter', it goes out and reads the website, sees if there is a table where we told it to look and then pulls in the data. 

For more on this function, click on the 'Learn More about IMPORTHTML' link at the bottom of the dialogue box.

![google sheet help](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_07.png)

Now we will save our sheet as a csv. Navigate to File >> Download as >> Comma-separated values (.csv, current sheet). 

![ssve](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_08.png)

It also has IMPORT XML (for structured data online), FEED (for RSS feeds), DATA (for data hosted online), or RANGE (for portions of other Google Sheets). 


### Geocoding 

We are first going to use a table join method to align our newspapers data to the spatial coordinates. 

First add the Newspapers layers

Now add the cities points layer using the `Delimited Text Layer` button, and make the following selections:
- csv
- point coordinates
	- X field: 'lng'
	- Y Field: 'lat'

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_03.png)





	
	