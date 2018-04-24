## Making Data 

### Making Data 01: Geocoding historic data

#### Premise
In this tutorial, we are going to make a map of newspapers in the United States before and after the invention of the rotary printing press in 1843. We want to visualize how newspapers both exploded in urban areas and began to spread to smaller areas (if you want to take this to the next level, you could combine this project with the )

One of the primary hurdles that researchers encounter is finding appropriate datasets. This problem is compounded when working with historic data as it may not necessarily have spatial data attached or it may only have place names attached that may or may not represent modern place names. Ultimately, finding data and transforming data are separate issues. As far as finding data is concerned, the library, the Census, NHGIS, or XXXXX may have everything that you need. If not, you may need to turn to repositories on the Internet. 

Sometimes the library may have data available, or you may find it through a web search. Assuming that you are not able to find shapefiles, you will want your data to be in a format that QGIS can parse. This includes .csv (comma separated values), .txt (plain text), or some form of database. Formats such as .pdf may pose insurmountable problems. 

We will go through the process of turning data that we find through an internet search into data we can use in a mapping project. This is not the only way to get data, and at Columbia, the librarians can be immensely helpful in this regard.  

By the end of this tutorial, you will be able to:
- search the internet for datasets
- transform data you find in a table into a csv file that can be used in QGIS
- align that data to geographic locations using a gazetteer
- query the data you collected to answer a research question

### Making the Data

We are going to use data from [Readex](https://www.readex.com/who-we-are-what-we-do), a company that sells primary source collections to institutions. We only want the names of the newspapers, the location of publication, and the year it was established. We are not interested in reading the papers right now. Readex offers these lists in a variety of organizations: by region, decade, or era. We will use the 'By Era' breakdown, and look at the pre- and post-1842 eras. 

Open a web browser (Google Chrome, Firefox, or Safari are OK, please do not use Internet Explorer), and navigate to [www.readex.com](www.readex.com). Hover over the 'Collections' link in the Navigation bar and click on 'By Era'. Then select the `Jacksonian Era, Parts 1 and 2, 1823-1842` > `Title List` it will open in a new tab.

Also open the `Antebellum Period, Parts 1 and 2, 1843-1860` > `Title List`

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_01.png)

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_02.png)

Looking at this website, we can see that it is a table. This is very fortunate because whenever data is in a table (as it often is on a website), we can use a simple tool in Google Drive to format the table nicely for our use. If the data was not in a table, we may be able to get it through Webscraping (i.e., with a webscraping script or a plugin to our browser. Both of those techniques are far beyond the scope of this tutorial,)

ADD THE REST HERE

### Geocoding 

We are first going to use a table join method to align our newspapers data to the spatial coordinates. 

First add the Newspapers layers

Now add the cities points layer using the `Delimited Text Layer` button, and make the following selections:
- csv
- point coordinates
	- X field: 'lng'
	- Y Field: 'lat'

![readex](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2018/blob/master/Images/mappingdata06_03.png)





	
	