## Tutorial 4 : Telling stories with maps

This tutorial outlines how to deploy basic tools in QGIS to tell stories across multiple layers. The goal in this session is to learn approaches to make your maps compelling visual arguments. The final products should make sense at first glance, and convey your desired narrative or analysis. 

### Topics to cover:  

- Quantitative symbology & classification

- Subsetting data layers

- Querying (about pulling out the highpoint of a particular attribute)

- Layout & exporting map

*Language and the city: where do we speak?*
We will use the skills listed above to examine second language speakers and institutions of practice in New York City. New York has an incredible number and variety of second language speakers, yet how and where they are used - in a spoken format - remains less charted, especially on a spatial level. 

The questions we will be probing include: are there spatial patterns to where speakers of certain languages live within the city? And, drawing on a unique dataset of institutions where a language other than English is expected or formalized, how do these formal and semi-formal spaces map spatially across the city? How do they intersect, if at all, with places of residence? In the next tutorial (5), geoprocessing tools will help formalize these analyses.


*Data:*

- ACS language groups
- language institutions
- dual language programs in NYC public schools (private too?)

One story about each - make three maps

### Where do speakers of non-English languages live in the city?


Data on people by census tract is usually easy to access in countries with public data and standardized census processes, such as Mexico and the US. (The quality and accuracy of this data, especially as it relates to immigrants, sits at the middle of current debate in the US [in and out of court](https://www.npr.org/2019/03/31/707899218/what-you-need-to-know-about-the-2020-census)). 

The [American Community Survey](https://www.census.gov/programs-surveys/acs/about.html) estimates households that speak [select non-English languages](https://www.census.gov/quickfacts/fact/note/US/POP815217) at home. We will connect this information to [tract-level geography](https://www2.census.gov/geo/pdfs/education/CensusTracts.pdf) at the five-borough level and then tweak ways of displaying and representing to find stories that relate to our spatial research questions outlined above.

#### Add regional-scale base + Census tract map
Open QGIS and add these shapefiles from the Tutorial 4 folder:
- *Water_tristate.shp* : nice regional map
- *NYC_tract2010_LangJoin.shp* : the tracts that we need

![adding file]


*Fade out background*
*The water map will probably load in technicolor; while lovely, we need to fade the background out to better show what we care about -- households speaking other languages.*

Double-click on the small square to the left of 'Water_Tristate' in the layer panel. Then click on the `Single Fill` box and change the color and lines to something suitable for background. 

![single fill box]

#### Add and join data on language spoke at home
- Add a table (called a 'delimited text' layer; click on the comma icon on your left-hand panel) from the table subfolder in your Tutorial4 folder : *2010LanguagesbyTract2010.csv*
-*Always confirm and skim your data!* Double-click and open the attribute table from the layer panel.
-Join the language data to the tract map. Right click on NYC_tract2010_LangJoin layer and navigate to properties. Click on the join menu (resembling a microphone) and then click on the unassuming green plus sign at the bottom of the menu that pops up.
![joining table]
Select the name of the table (2010Languages..) and then the field GISJOIN in both of the other menus. `Apply.`
![joining table continued]
-Then open the attribute table of the shape file and check to make sure that all of the new columns are there.

#### Troubleshooting
Data type consistency - e.g. a column of numbers with one missing field -  is the most common problem bedeviling `joins` to a new table of data. Check your data twice before trying to join. QGIS also has some particularities importing quantitative data; if glitches arise, chances are it's not you, it's the program (so answers can be found online!)

#### The fun part: finding and showing spatial stories with numbers on maps.

QGIS has an immense array of tools to quickly change how your maps look; this will consequently shift the messages they communicate - and the clarity with which they do so. 

Legibility obviously depends on context of [time and place](http://socks-studio.com/2014/03/02/the-three-mawangdui-maps-early-chinese-cartography/): how much do you anticipate that your audience knows and how are they accustomed to reading maps and visuals? (Not to mention how they perceive beauty!)

A general rule is to keep information in the map to a *minimum*: only show exactly what you need to say. At the most basic, this means (a) remove unnecessary elements and (b) make the background a boring color  - in mapper-speak, make sure you have a visual hierarchy that puts your main story at the top. 

If you have multiple points you want to make, break them up. Just like in writing! You can always make sequences of single-color maps, mixed in with videos or other visualizations to tell larger stories, such as the making visible of the spatial realities of [Rohinga camps](http://fingfx.thomsonreuters.com/gfx/rngs/MYANMAR-ROHINGYA/010051VB46G/index.html), the ['bussings out' of the homeless in the US](https://www.theguardian.com/us-news/ng-interactive/2017/dec/20/bussed-out-america-moves-homeless-people-country-study), or [street names in Germany](https://www.zeit.de/feature/streetdirectory-streetnames-origin-germany-infographic-english)

#### Start your own!
Right-click on the NYC_tract2010... file and navigate to `properties` and the symbology menu.

- Select `graduated` from the top menu, and then drop down to pick the variable (ideally language: in the example we use speakers of French Creole, one of the largest second-language groups in NYC). 

![graduated classification]

- Then: pick a color scheme and a mode by which to cluster your numbers. All of these can completely change how your data communicates to your audience. 


*Choices inside colors and classification modes*

#### Color ramps inside shapes, aka 'chloropleth maps'
- Grayscale or a single color range. Most useful when: you are preparing a map for a journal or in-text in a scholarly book and you want to show a range over a wide area, and care less about showing the differences in smaller categories. Many [effective maps](https://www.theguardian.com/news/datablog/2013/mar/15/john-snow-cholera-map) have only needed black and white or a [spectrum of a single color.](http://www.radicalcartography.net/index.html?trees) 

- Short spectrum: most frequently used to illustrate intensity and a sharp difference in a single variable, e.g. land plots with some royal ownership share or those without; or the [presence of slavery in the American South.](https://pudding.cool/2017/01/shape-of-slavery/)

- Multiple colors: usually only clear when there are obvious clusters to your categories, but increasingly legible through interactive online maps, like this one showing ['who owns England'.](http://map.whoownsengland.org/)

#### Number of classes
Only break your data into the number of clusters that make sense for your story. In our case, we arbitrarily picked 50 and 500 as numbers of speakers inside a given tract that we thought would be meaningful to show places with a light presence of French Creole speakers, and the tracts where around a quarter of residents speak French Creole at home.

#### Number or percentage?
Does it make sense to show speakers in absolute numbers or as a percentage of all residents inside a tract? Usually the answer with population data is that percentages are more meaningful, especially for comparisons (note that with tracts and other census geography this matters slightly less, as tracts have relatively similar numbers of residents.) For our question, the actual number of speakers made more sense - it's an easier way to convey how many folks there are to talk with in the immediate area.

#### [*Modes*](https://www.axismaps.com/guide/data/data-classification/) of classification and  clustering perhaps most radically change how the data visualizes. 
*Try making your map with each of the following.*
- *Equal interval* means that each group of tracts will be organized according to equivalent numeric ranges of the number of language speakers per tract (e.g. 1-150, 150-300 people). This works best when there are a good number of tracts that fall into each range - not for our language speaker data.
![equalinterval]
![equalinterval2]
- *Quantiles*  divides the number of total tracts in NYC into equal groups of the number you choose (defaulting to five) The 'breaks' in our data will be determined by the number of tracts -- so the intervals can be very different in size, e.g. the bottom three quintiles might be for 0-1 speakers, and the top quintile will cover tracts that have 50-1,000 speakers of French Creole.  
![quantiles]
- *'Natural' breaks, aka Jenks.* Minimizes variation inside each cluster, so generally falls along already-existing breaks in data. Often looks good, but harder to explain and the breaks may be at points with little meaning (e.g. a cluster with 21-39 speakers and another for 40-301 speakers).
![naturalbreaks]
![naturalbreaks_inverse]
- *'Pretty' breaks* slice along easy-to-remember numbers, e.g. 0-5, 5-25 speakers. 
-  *Custom*: you can define how many classes you want and where the breaks in your data are. This makes the most sense if you have a theory of something meaningful behind different levels- e.g. if we had a study suggesting that more than 700 speakers in a neighborhood is a threshold for children to retain more of their second language. 

#### Visual hygiene: cleaning out background noise
This tutorial referenced the importance of visual heirarchy and minimizing map elements. Sometimes Q maps even a single variable in a 'noisy' way; this is particularly true when our geographic unit is something that isn't particularly meaningful to our story (Who cares or knows about tracts, anyways?!). Some quick tidying can help using the basic display functions, e.g. for the common too-big background lines scenario, as below 
![cleanuplines1]
The fastest way is to click on the square to the left of the zero value in the layer panel -
![cleanuplines2]
- and then select the 'simple fill' and make the border thinner and/or more transparent or a color that will blend into the background.
![cleanuplines3]

Don't forget: at the end of the day, all of your choices are subjective and reflect what you think makes a better story while still maintaining methodological integrity. Bon voyage!

### Language institutions
We've mapped out where residents live who speak languages other than English at home. But language retention also depends significantly on speaking in spaces outside the home. Where are those spaces? The data for this section was hand-collected by research assistants for a Mellon-foundation-funded project in the summer of 2017 at the Center for Spatial Research. It is in no way complete or representative - there are many spaces where meaningful language exchanges regularly take place but that are too hard to map- and other places may be over-represented. What the dataset does do, however, is map the electronically 'visible' institutions where second language usage is publicized and where entry is relatively open to the public.

*Can we identify spatial relationships by mapping institutions for a given language over the areas where speakers live? 

### Add the data. 
Browse to the table `language_institutions_NYC` and add to the map. 

![importinstitutions]

When you are adding, designate the `latitude` (Y) and `longitude` (X) variables and select the option for WGS 1984 coordinate reference system (the points in this table are in a different system; QGIS will convert as long as you flag which one it's coming from!).
 
![84]

First, let's look at this layer by itself -as points- and see if anything strikes us, or if we can modify to visualize interesting clusters or relationships (or skewdnesses in our data!). Are all five boroughs covered? Why not? Do some spaces seem to be particular clusters of a single language? 

![languagepoints1]

#### Built a filter and subset
We could un-click each of the languages one by one. Or we can quickly build rules - to show 'Language' points only when they are entities with programming or events in Haitian Creole and French (assuming some overlap), for example. 

![FrenchORCreole]

Map this on top of your census plotting of where speakers of 'French Creole' live. What do you notice? Now take away the 'French' institutions from your rule-based filter. What do you notice now?

![FrenchHaitianMap]

To investigate what each point is, click on the 'information' button, and then click on a specific feature (e.g. point)

![infobutton-haitian]

####Map Russian speakers and institutions
Here's another way to select and play with a subset of your data.
Select by values where Language = Russian in the institutions layer.

![selectbyvalues]

![selectbyvalues2]

You can make selections a new shapefile - smaller and sometimes easier to work with. 

![saveselection]

![saveselection2]

The language dataset coded cultural + educational institutions by their 'scale' of reach; whether they operated mainly for a neighborhood, borough or city-wide audience. We'll use this to learn to show these points by scale, not just different colors.

![byscale2]

![russiandots1]

Now: imagine that the city council wants to help fund a new Russian storyhour program in certain libraries. Where are the tracts with the highest numbers of Russian-speaking households? In GIS you can query (and select) features by certain values, or characteristics. Navigate to the `select by expression` option, search for "Russian", double-click on the p_russian field (percentage) and then write greater than 0.3 (30 percent). It should read `"2010LanguagesbyTract2010_P_Russian">0.30`

The selected fields should appear highlighted in yellow on our map.

![querythreshold]

Using our eyes (and tomorrow we can calculate), where are the 'hotspots' of speakers that are furthest away from the cultural services we've mapped?


### Preparing the map to print

From the `project` menu, select `print layout`. ![printlayout]. Once that window opens, add your map through the drop-down menu `add:add map` or click on add map icon ![addmaplayout]. Draw a rectangle where you want to place your map. Play around with the size you want your map to be on the page, and the extent - e.g. do you want to focus just on South Brooklyn or the whole city?

- #### *Add a legend.* Click on the legend icon and draw a rectangle on top of your map - ideally somewhere without much going on.![addlegend]. The legend items almost always need cleaning - in this case, I went back into the map and edited the percentages so they'd be more readable. 

- #### *Add a title*
Click on the add text box, and draw a rectangle where you want your title. Write, then make the font bigger so that it's legible - probably between 18 - 32 - point.![addtitle]

- #### *Add source information*
Draw another text rectangle and write out the data source and any other notes.

- #### *Add a scale bar*  
It's always important to situate maps in space - most people know roughly where New York City is, and how big it is, but it's still important to flag!

- #### *Add north arrow*
Click on the add image icon on the left, and then navigate (on the right side) to the `item properties` tab. ![northarrow1] 

Click on `search directories` and preset options will open for different styles of north arrows (and other icons).

#### Export
From the top-left menu (`layout`), select `export as image`. Save in a place you can find. Open and admire your work! Also likely: open, see the changes you'd like to tweak, and return to the layout window to modify and beautify.
![exportimage]

Prepared by Bernadette Baird-Zars for *Mapping for the Urban Humanities*, an intensive summer 2019 workshop from the [Center for Spatial Research]:(http://c4sr.columbia.edu/) in the Graduate School of Architecture, Planning and Preservation at Columbia University. More information about the course is available [here]:(http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-institute).

...

[adding file]:Images/2019/Tutorial4_add.png

[single fill box]:Images/2019/Tutorial4_fade.png

[joining table]:Images/2019/Tutorial4_join1.png

[joining table continued]:Images/2019/Tutorial4_join2.png
 
[graduated classification]:Images/2019/Tutorial4_graduated.png

[equalinterval]:Images/2019/Tutorial4_equalinterval.png

[equalinterval2]:Images/2019/Tutorial4_equalinterval2.png

[quantiles]:Images/2019/Tutorial4_quantiles.png

[naturalbreaks]:Images/2019/Tutorial4_naturalbreaks.png

[naturalbreaks_inverse]:Images/2019/Tutorial4_naturalbreaks_inverse.png

[cleanuplines1]:Images/2019/Tutorial4_cleanuplines1.png

[cleanuplines2]:Images/2019/Tutorial4_cleanuplines2.png

[cleanuplines3]:Images/2019/Tutorial4_cleanuplines3.png

[importinstitutions]:Images/2019/Tutorial4_importinstitutions.png

[84]:Images/2019/Tutorial4_84.png

[languagepoints1]:Images/2019/Tutorial4_languagepoints1.png

[FrenchORCreole]:Images/2019/Tutorial4_FrenchORCreole.png

[FrenchHaitianMap]:Images/2019/Tutorial4_FrenchHaitianMap.png

[infobutton-haitian]:Images/2019/Tutorial4_infobutton-haitian.png

[selectbyvalues]: Images/2019/Tutorial4_selectbyvalues.png

[selectbyvalues2]: Images/2019/Tutorial4_selectbyvalues2.png

[saveselection]: Images/2019/Tutorial4_saveselection.png

[saveselection2]: Images/2019/Tutorial4_saveselection2.png

[byscale2]: Images/2019/Tutorial4_byscale2.png

[russiandots1]:Images/2019/Tutorial4_russiandots1.png

[querythreshold]:Images/2019/Tutorial4_querythreshold.png

[printlayout]:Images/2019/Tutorial4_printlayout.png

[addmaplayout]:Images/2019/Tutorial4_addmaplayout.png

[addlegend]:Images/2019/Tutorial4_addlegend.png

[addtitle]:Images/2019/Tutorial4_addtitle.png

[northarrow1]:Images/2019/Tutorial4_northarrow1.png

[exportimage]:Images/2019/Tutorial4_exportimage.png


