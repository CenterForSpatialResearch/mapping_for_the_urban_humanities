## Making Webmaps with Leaflet.js

With this exercise you will learn how to create a basic web-based map using the javascript library leaflet.js. This is necessarily not an introduction to javascript, but rather intends to provide familiarity with the components and requirements of publishing maps online. Upon completing this tutorial you should ....

1. Understand how to export GeoJSON files from QGIS
2. Understand the structure of a basic webpage
3. Be able to import a historical map to be shown on the web
4. Create interactive vector features with embedded photos and annotations
5. Experiment with layer styles and map composition
6. Access the NYPL Map Warper archive  

#### The Premise

With this exercise our goal is to create a simple interactive online map that shows the New York Botanical Garden just after it was initially constructed and annotates several important buildings and roads at the NYBG. We will use the 1902 Bronx map (that we georeferenced in the previous exercise) as well as some of the features we digitized adding additional annotations. 

For context lets take a look at what this final map will look like. It is visible [here](https://centerforspatialresearch.github.io/MappingForTheUrbanHumanities_2017/Class_Data/3_Webmaps/)

To accomplish this we will be using Leaflet.js, an incredibly well documented javascript library with many online easily accessible examples to learn from. Review the [Docs](http://leafletjs.com/reference-1.0.3.html) page for explanations of all of the functions in the leaflet library. 

Leaflet.js is one of many many ways to create webmaps. Others include: 
* OpenLayers
* Neatline (a plugin for Omeka) 
* Mapbox
* Carto
* TileMill
* GeoServer

Should you look into creating webmaps further you'll fine that many of these tools are used together, or build upon each other. 

### To Begin

We have provided the basic folder structure that you will need to create your webmap, in the `Class_Data/3_Webmaps` folder downloaded with this repository. Lets review the structure before we proceed. It contains three folders and one file: 

* `css`
* `data`
* `img`
* index.html
* `js`

In the broadest terms web development can be understood in the following way: HTML is the structure of a website, CSS is the style, and JavaScript is the functionality or the interaction. Each of these are contained in text files which we have organized into the above folder structure. When you are creating a webpage you are creating a series of linked text files that your browser reads. 

In addition there are folders for images: `img` and `data`. These two folders will contain any images you will use, and the data for the vector annotations as well as the georeferenced historical map. 

#### Preparing your data
For the purposes of this tutorial we have already prepared all of the data for you. However the following steps outline how you would go about exporting data from QGIS to include in an online map if you were starting from scratch. 

**Exporting and Formatting a Georeferenced Historical Map**
1. *Find the latitude and longitude* coordinates of your image. We will need these later on when we import the historical map into our web map. Enable the `Lat Lon Tools` plugin in QGIS. Then use it to select the top left and bottom right corners of your raster and copy these to your notes. One thing that is important to note, you must choose the corners of your raster dataset (i.e. the corners of the black rectangle around your rotated map).
![img](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/05_LatLonTools.png).
2. *Set No Data Value.* Open the `Properties ` menu for the georeferenced historical map. In the Transparency tab enter 0 in the `Additional no data value` field. Click **Apply**. You should notice that the black border around the outside of your image disappears. 
![instructions image](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/01_NoData.png)
3. *Export Historical Map as a GeoTiff.* Right click on the georeferenced map in the layers panel and select Save as. Then in the save as dialog box select `Rendered image` as the output mode. Select `GTiff` as the format. Name  your image and save it in the appropriate directory. (You must select `Rendered image` in order to export a version of your map without the black border)
![instructions image](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/01_MapExport.png)
4. *Reducing the File Size of the Map Image*. To make it more manageable to load in the browser open the GeoTiff file we just created in the photo editor of your choice, adjust the image size to something more manageable and then export as a **.png**. Save this file in the `data` folder of your webmap directory. 

**Exporting Vector Layers as GeoJSON**
Our webmap will rely on a different data format for our spatial data. Up until now we have been working with shapefiles. When we upload our annotations to the web we will be using a data format called GeoJSON. It is a different way to structure spatial and tabular information and it preserves all of the information we have come to expect from shapefiles. 

1. *Export as GeoJSON*. Right click on the layer you want to export in the layers panel. Select Save as. Select `geoJSON` as the file format. Select `WGS 84` (a geographic coordinate reference system) as the CSR. Name  your file and save it in the appropriate directory.
![instructions image](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/03_ExportGeoJSON.png)

#### Building a Webmap

Lets begin to make our webmap. 
First you need to make sure you have Python installed. Check if you have Python installed and which version it is. We will be using Python to run a local server.

### (Mac) Check which Python version you have (if any)

1. Open a Terminal Window 
2. Type `$ python -V` hit 'Return'
4. Make a note of which Python version you have, you will need it later.

### (Windows) Check which Python version you have (if any)
1. open Command Prompt
2. type python --version hit 'Return'
	* if python is installed something like this will appear
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/pythontest.png)
	* if it isn't then a message stating that will appear
	* if Python is installed make note of which version you have installed, you will need it later
3. if python is not installed then go to [python.org](python.org) to download python. We recommend installing version 2.7. 
4. After downloading the installer, double-click to open it and follow the installation prompts, selecting the default settings until you get to the page that reads "Customize Python 2.7.XX" 
	* Scroll to the bottom of options, and click the drop-down selection that reads "Add python.exe to Path" (it should have a red "X" by default)
	* Select the option that reads "Entire feature will be installed on local hard drive"
5. Follow the prompts on the rest of the setup, allow the installation to finish. When it's done, it will tell you, and python is now installed on your computer and available to use.
6. To test that python was installed, open the Command Prompt application, and enter `python --version`. It should read `Python 2.12.XX`.

### (Mac) Set up a local server

We will run a local server from our computers. The details of this are far beyond this tutorial, for more on  the technical details, visit the [Mozilla Developer site](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Set_up_a_basic_working_environment). For more on how the web works the difference between a local and remote server, [read this](https://devdojo.com/blog/technology/local-vs-remote-servers).

1. In a Terminal window, navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Documents > MappingForTheUrbanHumanities_2017 > Class_Data >3_Webmaps. To navigate there, I type the following commands (don't type the $, that just indicates that you are in the Terminal):

	* `$ cd Documents`
	* `$ cd MappingForTheUrbanHumanities_2017` 
	* `$ cd Class_Data`
	* `$ cd 3_Webmaps`
	
2. If you have Python 3, type:

	* `$  python -m http.server`  
	
2. If you have Python 2, type:

	* `$ python -m SimpleHTTPServer`
	
3. Return to your browser window (Chrome, Firefox, or Safari) and type `localhost` in the navigation bar. You should see an empty webpage. 

### (Windows) Set up a local server
1. Open Command Prompt. Then navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Documents > MappingForTheUrbanHumanities_2017 > Class_Data >3_Webmaps. To navigate there, I type the following commands:

	* cd Documents
	* cd MappingForTheUrbanHumanities_2017
	* cd Class_Data
	* cd 3_Webmaps

2. If you have python 2 type:

	* python -m SimpleHTTPServer

3. If you have python 3 type: 

	* python -m http.server

	It will look something like this:
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/localhost.png)

3. Return to your browser window (Chrome, Firefox, or Safari) and type `http:\\localhost` in the navigation bar. You should see an empty webpage.

### Deconstructing The Webmap

We will break down the example map provided in the `index.html` file line by line. The full code for the example is also provided at the end of this tutorial.

1. *open* the index.html file in the text editor of your choice.

#### Overall Structure

HTML documents are constructed through using what are called tags that are denoted like this `<html> content </html>. All HTML documents follow a basic structure with a series of nested elements labeled with tags. 

```html
<html>
<head>
	//this is a comment
	//all of your header information goes in the header, 
	//such as the leaflet library and the title of your webpage
	<style>
		//style tags are a way to embed simple CSS styles within your html document, 
		//that specify how certain elements on the page should look
	</style>

</head>

<body>
	//all of the content of your webpage is contained within the body tags
	//Think of tags as a set of parentheses that we must both open and then close. 
	//Closing tags look like this: </body>
</body>
</html>
```

#### Writing the Header

As mentioned above we are using the Leaflet.js javascript library to create a webmap. Javascript is a language, like HTML and CSS, that all modern web browsers understand naturally. 

Leaflet is a set of commands built with javascript that allow us to make webmaps relativley easily. 

We will also use another library called jQuery.js that will allow us to import the points and road outlines data. 

It is helpful to think of these libraries as sets of commands that our program can draw on. 

Because Leaflet and jQuery are both libraries we need to include them in our html document so that they can be referenced by our program when it runs in the browser. These libraries are really just also sets of text files, contained in javascript and css file types. 

We include them in the header section: `<head>`

1. *Download required libraries.* We have already done this step for you. But for reference we downloaded the Leaflet.js library from [here](http://leafletjs.com/download.html). And we downloaded the jQuery library from [here](http://jquery.com/download/).  
2. *Name your map.* The `<title>` tag contains the name of your map that will appear at the top of the browser window.
3. *Import Leaflet's CSS.* Leaflet comes with its own CSS styles that specify how certain elements, like the zoom buttons, should look. We have placed this css file in the `css` folder and now need to tell our index.html document where to find it.
	`<link rel="stylesheet"  href="css/leaflet.css"/>`
4. *Import Javascript libraries.* Now we need to import the Leaflet and jQuery javascript libraries. We have likewise saved these in the `js` folder in our webmaps directory. 
	`<script src="js/leaflet.js"></script>`

	`<script src="js/jquery-2.1.1.min.js">  </script>`
5. *Set the size of your map.* Using CSS syntax we will set the size of the map to fill a full browser window: 
	`<style> #map{position: absolute; top:0; bottom:0; left:0; width: 100%;} </style>`
6. *Close the <header> tag.*

#### Writing the Body

Now we will move on to building the content of our map. 
Please note: `//` in front of a line means that the code is "commented out" and will not be read by the browser. As we go along, uncomment the code section by section. 

1. *Open the <body> section.* `<body>`
2. *Make a section for the map.* Make a `<div>` for the map, and call it map.
3. *Start a javascript command.* Write `<script>` to start writing in javascript within our index.html file.
4. *Initialize the map* by creating a map variable. 
`var map = L.map('map').setView([40.87,-73.87], 15);`
	* Javascript requires that all variables be labeled with 'var'.
	* We are going to create a map var and use leaflet to initialize it. We need to give out map two parameters. First, the latitude/longitude for the center of our map, and the zoom level. 
	1. set `var map =`
	2. When we call leaflet (i.e. access the leaflet library's set of commands), we use capital L  `L.map` to call Leaflet's map property.
	*. Javascript (and therefore Leaflet) uses both dot notation and bracket notation, whenever there's a period between things in js, it's called dot notation, and you are "accessing the properties" of an "object" don't worry too much about this - it just means you are looking inside of that object to find a particular property.
	4. '.setView([40.87,-73.87], 15)': We set the view of the map by specifying the center point in latitude and longitude `[40.87,-73.87]`, as well as the zoom level: `15`.

**Add Map Tiles**

5. *Add background tile layers.* We are going to be using background tiles from [Open Street Map](http://wiki.openstreetmap.org/wiki/Tiles#cite_note-1) that have been styled by [Stamen Design](http://maps.stamen.com/#terrain/12/37.7706/-122.3782). There are a number of open source map tile providers out there and Stamen has some great versions. 

1. *Call the tileLayer property* from Leaflet, and pass it the webaddress of the map tiles we are using. `L.tileLayer('http://tile.stamen.com/toner-lite/{z}/{x}/{y}.png'`
	* We could try switching to a different tile provider `'https://maps.wikimedia.org/osm-intl/{z}/{x}/{y}.png'`
2. *Pass the tileLayer some properties.* 
	1. Inside curly brackets after the address for the map tiles we will set the attribution (which is displayed in the bottom right corner). `attribution: 'Tiles from <a href="http://www.openstreetmap.org/">OSM style by Stamen Design</a>',`
	2. We will also set the minimum and maximum zoom levels. `maxZoom: 19,
		minZoom: 1`
3. *Add the tileLayer to the map.* Pass the .addTo property, and give it the map variable. `.addTo(map);`

```javascript
`L.tileLayer('http://tile.stamen.com/toner-lite/{z}/{x}/{y}.png',
		{
			attribution: 'Tiles from <a href="http://www.openstreetmap.org/">OSM style by Stamen Design</a>',
		maxZoom: 19,
		minZoom: 1
		}).addTo(map);
```
4. *Save* your index.html document. Open your browser and refresh the `localhost:8000` page. You should see the following: 
![img](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/04_MapTiles.png)

**Add GeoreferencedHistorical Map**
We will now embed the "Map or plan of that part of the Borough of the Bronx, City of New York, lying easterly of the Bronx River" published in 1902 that we georeferenced in the previous exercise. 

1. *Create a variable* that contains the url of the image, in this case the path to where is it stored in the directory for our webmap. 
`var imageUrl = 'data/BronxMap.png';`
2. *Create another variable* where you define the area that the image covers using two pairs of latitude and longitude coordinates for the top left and bottom right corners of your image. We found these coordinates using the `lat lon tools` plugin for QGIS when we were preparing the historical map raster earlier. 
`var imageBounds = [[40.8846829955, -73.8978315922], [40.8290586719, -73.8201512858]];`
3. *Call Leaflet's .imageOverlay()* method pass it the two variable we just created, set the opacity of the map layer and add it to the map. 
`L.imageOverlay(imageUrl, imageBounds, {opacity: 0.8}).addTo(map);`
4. *Save and then refresh your browser* and the 1902 map should appear. 

**Add Digitized Road Outlines (or any geojson file)**
Now we will add the road outlines that we digitized. 

1. *Use the jQuery command, getJSON.* Use $ to call the jQuery library, just like Leaflet is **called** with L., jQuery is **called** with $.
2. *Tell jQuery where your file is located,* and give the function a name (I'm going to use 'roadsData'). 
3. *Set the color,* line weight, and opacity of your lines. 
4. *Comment out* `//onEachFeature: road_annon` we will use this in the next step.
5. *Add the lines to the map*
6. *Save and then refresh your browser,* the road lines should be visible.

```javascript
$.getJSON('data/RoadLines.geojson',function(roadsData){
	    L.geoJson(roadsData, {
	    	color: "#ff7800",
	    	weight: 3.5,
	    	opacity: 0.65,
	    	//onEachFeature: road_annon
	    }).addTo(map);
	    }); 
```
**Add Interactivity to Road Outlines (or any geojson file)**
We will now add popups for each of our road lines. 

1. *Create a variable* lets call it `road_annon`
2. *Call the leaflet function* `onEachFeature`. This must be defined for two parameters:  `feature` and `layer`. Whatever information we include in this function will be called once for each feature (basically each row) in our GeoJSON file. 
3. *Define the action* we want called for each feature: 
	* If the RoadLines.geojson file has properties (attribute information) and has a column named `Descr` 
	* Then create a variable called `roadsPopup`. 
	* Inside that variable store the value of the `Descr` column in the RoadLines.geojson file. 
	* Use the `.bindPopup()` leaflet method to attach the content of the roadsPopup to each element in the RoadsData layer
4. *Call the onEachFeature function we just defined.* Return to the block of code above where we added the data and uncomment `onEachFeature: road_annon`

Your code should now look like the following.

```javascript
//load GeoJSON file containing roads, and style lines
  	$.getJSON('data/RoadLines.geojson',function(roadsData){
	    L.geoJson(roadsData, {
	    	color: "#ff7800",
	    	weight: 3.5,
	    	opacity: 0.65,
	    	onEachFeature: road_annon
	    }).addTo(map);
	    });  

//define popup content for road annotations
 	var road_annon = function onEachFeature(feature, layer) {
	    if (feature.properties && feature.properties.Descr) {
	    	var roadsPopup = feature.properties.Descr;
	        layer.bindPopup(roadsPopup);
	    }
	}
```
**Add GeoJSON file containing Points**
We will now add the GeoJSON file that contains the points we want to highlight with annotations on our map. 

This follows largely the same process as above.

The main difference here is that we have added some extra formatting to the popup windows for the points. 

1. *Use the jQuery command, getJSON.* Use $ to call the jQuery library, just like Leaflet is **called** with L., jQuery is **called** with $.
2. *Tell jQuery where your file is located,* and give the function a name (I'm going to use 'bldg'). 
4. *Call the onEachFeature function* we will define below. `onEachFeature: point_annon`
5. *Add the points to the map*
6. *Create a variable* lets call it `point_annon`
7. *Call the leaflet function* `onEachFeature`. As above, this must be defined for two parameters:  `feature` and `layer`. Whatever information we include in this function will be called once for each feature (basically each row) in our GeoJSON file. 
8. *Define the action* we want called for each feature: 
	* If the PointAnnotations.geojson file has properties (attribute information) and has a column named `Descr`
	* Then create a variable called `pointsPopup`. 
	* Inside that variable store the value of the `Name` column in the RoadLines.geojson file, the `ImgURL` column, and the `Descr` colum. 
	* Then use html tags to format these elements, creating line breaks `<br/>` between each and setting the size of the image `'" width ="300px"/>'`. 
	* Use the `.bindPopup()` leaflet method to attach the content of the pointsPopup to each element in the bldg layer

```javascript
//load GeoJSON file containing points
	$.getJSON('data/PointAnnotations.geojson',function(bldg){
		L.geoJson(bldg,{
			onEachFeature: point_annon
	    }).addTo(map);
	});

//define popup content for point annotations
	var point_annon = function onEachFeature(feature, layer) {
	    if (feature.properties && feature.properties.Descr) {
	    	var pointsPopup = feature.properties.Name + '<br/> <img src="'+ feature.properties.ImgURL + '" width ="300px"/> <br/>' + feature.properties.Descr;
	        layer.bindPopup(pointsPopup);
	    }
	}
```
9. *Save your file and refresh* your browser. 
![img](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2017/blob/master/Tutorials/Images/Webmaps/06_ImagePopup.png)

**Add NYPL Map Warper Raster Tiles**
As we reviewed yesterday the New York Public Library's Map Warper site is a tremendous resource for historical maps that are in the public domain, and many of which are already georeferenced. 

In addition the NYPL has make it possible to access these historical maps directly from within a webpage. On the [Export page](http://maps.nypl.org/warper/maps/18631#Export_tab) for each georeferenced map within the NYPL Map Warper collection has a link to the map's information in the "Tiles (Google/OSM scheme)." This link allows us to add any of these maps to our webpage in the same way we added the Open Street Map tileLayer. 

1. *Call the .tileLayer method* `L.tileLayer('http://maps.nypl.org/warper/maps/tile/27688/{z}/{x}/{y}.png').addTo(map);`

Explore the NYPL Map Warper collection and experiment with pulling in additional maps. 


The full completed code for this example is available here: 

```html


<html>
<head>
	<title>GeoreferencedWebmaps</title>

	<link rel="stylesheet"  href="css/leaflet.css"/> 

	<script src="js/leaflet.js"></script>

	<script src="js/jquery-2.1.1.min.js">  </script>

	<style>
	#map{position:absolute; top:0; bottom:0; left:0; width: 100%;}
	</style>


</head>
<body>
	
	<div id="map"></div>

	<script>
//initializing the map
	var map = L.map('map').setView([40.87,-73.87], 15);

//add background tile layers
	L.tileLayer('http://tile.stamen.com/toner-lite/{z}/{x}/{y}.png',
		{
			attribution: 'Tiles from <a href="http://www.openstreetmap.org/">OSM by Stamen Design</a>',
		maxZoom: 19,
		minZoom: 1
		}).addTo(map);

	
//link to the historical map image 
	var imageUrl = 'data/BronxMap.png';

//define the area that image covers
	var imageBounds = [[40.8846829955, -73.8978315922], [40.8290586719, -73.8201512858]]; 

//add georeferenced historical map
	L.imageOverlay(imageUrl, imageBounds, {opacity: 0.8}).addTo(map);


//load GeoJSON file containing roads, and style lines
  	$.getJSON('data/RoadLines.geojson',function(roadsData){
	    L.geoJson(roadsData, {
	    	color: "#ff7800",
	    	weight: 3.5,
	    	opacity: 0.65,
	    	onEachFeature: road_annon
	    }).addTo(map);
	    });  

//define popup content for road annotations
 	var road_annon = function onEachFeature(feature, layer) {
	    if (feature.properties && feature.properties.Descr) {
	    	var roadsPopup = feature.properties.Descr;
	        layer.bindPopup(roadsPopup);
	    }
	}

//load GeoJSON file containing points
	$.getJSON('data/PointAnnotations.geojson',function(bldg){
		L.geoJson(bldg,{
			onEachFeature: point_annon
	    }).addTo(map);
	});

//define popup content for point annotations
	var point_annon = function onEachFeature(feature, layer) {
	    if (feature.properties && feature.properties.Descr) {
	    	var pointsPopup = feature.properties.Name + '<br/> <img src="'+ feature.properties.ImgURL + '" width ="300px"/> <br/>' + feature.properties.Descr;
	        layer.bindPopup(pointsPopup);
	    }
	}
	
	  
//add NYLP Map Warper maps
	L.tileLayer('http://maps.nypl.org/warper/maps/tile/27688/{z}/{x}/{y}.png').addTo(map);
	
//add NYLP Map Warper maps
	L.tileLayer('http://maps.nypl.org/warper/maps/tile/17090/{z}/{x}/{y}.png').addTo(map);


	</script>
</body>
</html>
```






______________________________________________________________________________________________________________

Tutorial written by Dare Brawley, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2017 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp). It is based on the tutorial prepared by Michelle McSweeney for the Spring 2017 course, *Conflict Urbanism: Language Justice* offered at Columbia Univeristy through the Center for Spatial Research. 