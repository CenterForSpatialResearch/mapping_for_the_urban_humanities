### Tutorial 5: tools for thought


#### Why do we make maps? Over the past few days, maps have mainly been tools to represent data. In this tutorial, you will learn some of the key methods for formal geospatial *analysis*,* including how to:

- Dissolve geographies and data into larger spatial units
- Calculate areas of geographies
- Calculate the sums, means and other summary statistics on the data aggregated into larger geographies.
- Join information based on location ("spatial joins")
- Perform summary statistics inside a spatial join.
- Build a buffer around a feature
- Select features by location - in this case proximity to a line.

*As scholars of the humanities, you know better than we do that analysis can occur in multiple ways!


### Dissolve: scale up and look at speakers by neighborhood

Describing library policy by tract doesn’t make sense; libraries serve neighborhoods. In lieu of figuring out the geographies of library catchment areas (likely overlapping!), we can use the neighborhood-tract-area (NTA) as a stand-in. These areas overlap roughly with the ‘named’ neighborhoods of New York City, as well as with the community board (and city council representative) areas. We'll start off at the end of Tutorial 4: with our map of Russian speakers and institutions. ![endof4]

#### Step 1: Aggregate the tracts into neighborhoods

GIS allows users to m----erge spatial divisions. One common method is to add up all of the spatial attributes that are inside of a bigger area - in our case tracts into neighborhoods. 

In the ‘toolbox’ ![gear] or `processing: toolbox` , search for ‘dissolve’. The basic QGIS function only changes the geography, so we’ll use the accessory GDAL tool ![gdal]. Double-click, and then in the window that opens, 
- Select the input layer of census tracts with the language information attached. 
- Select ‘NTACode’ from the drop-down menu for `Dissolve Field` - NTA is the geography that we want to scale up to.
- Tick the box for `Compute max/min/sum/mean` and then select `Russian` in the drop-down menu right below. This action will make sure that we keep the number we need - the total number of Russian speakers over space. You can specify that it save to a new file, but it’s fine to save as a temporary layer (it will show up as *dissolve* on your layer bar), and then after checking for errors you can export as a shape file. 
![dissolve]

#### *Troubleshooting*
In some cases, there’s a [documented glitch](https://gis.stackexchange.com/questions/276853/gdal-scripts-not-found-in-qgis-3-on-osx) inside Q that results in an error message after any attempt to use the GDAL dissolve function. To fix, go to Q’s `Settings:Options:System:Environment, then Enable `Use Custom Variables`. Select "Prepend" and then, under variable, enter *PATH*, and under value enter
*/Library/Frameworks/GDAL.framework/Programs:/Library/Frameworks/Python.framework/Versions/3.6/bin:* 


#### Step 2: But not all the neighborhoods are the same size: calculate the area of the polygons in square kilometers. 

Our file - and most that have geography - already has a column `AREA`. The information there, and the default, is always square meters. This is precise, but hard to read and not often used to compare large areas. 

Calculating a new column for area is straight-forward: open the attribute table, and click on `new field`. Then type in $AREA *.000001. (this number is to convert the square meters into square kilometers; there are a million square meters in a square kilometer).
![areakm]

#### Step 3: Calculate density of Russian speakers by square kilometer

What if a critical factor to support language maintanence is the actual proximity to other speakers. To be more honest, density might as a weak proxy for the likelihood that Russian speakers will bump into each other and chat; access and distance are not the same!

To calculate this, simply open the attribute field of our new layer and open the calculator ![fieldcalc], and select `make new field`. Name the field, then type in or select the variable for the number of Russian speakers and divide by area:  `10Russian`/ `AREA_KM2` . Check by opening the attribute table.

![calculatedensity]

- Sort by high to low : what do you notice? Does the geography make sense? 
- How do you (and will you!) navigate using numbers that are true, but might be misleading in your own work?

To complete this analysis, navigate to your new variable showing density of speakers, and depict on the map using a graduated symbology. 
- Does it show anything unexpected? 
- *Side note: Notice that the size, placement and shape of relatively arbitrary administrative divisions often translates into greater or lower visibility. But many of the neighborhood divisions also have a basis in some structural spatial factors; e.g. natural or human barriers such as highways and creeks, or geological hardnesses of soils, or discriminatory lending maps - in other words, they often aren't arbitrary at all, but it takes work to unpack.*

### Task 2: Calculate institutional density: spatial join and points-to-polygon

We could count each of our mapped spaces where Russian is spoken and then add them up by neighborhood. Or we could choose to show as-is, as points. But what about single buildings (or neighboring buildings) that house multiple meaningful places of language maintanence, such as a church with weekly services that rents their basement out to a Pushkin poetry group? Or a library with a literature group as well as a story hour and a monthly radio show (true!). These wouldn't communicate as points; only one would be visible. To show density, we want to add them up by neighborhood. *This is also useful for larger datasets, obviously!*

The #### spatial join 
is one of the most powerful tools that GIS can deliver - it can identify what parts of your information are related somehow *in space* and not by any other characteristic. The tool itself is straight-forward. 
- Open the processing toolbox ![gear] and either navigate to `vector general` and then #### `join attributes by location`
-or just search for "location". There are two options: we want the one with (summary): it will calculate contents of columns being brought in.
- Select your dissolved layer as the `input layer`- that's what we want to bring the points into. 
- Then select Russian spaces of language use as the `join layer`.
- Doing the spatial join with summary means we can ask for information on the NTA-level data of our institutions. We don't have too many variables to choose from, but the one we want for sure is #### the number of institutions in the NTA = > `count`
- For fun, you can also add `mean` and the indexes calculated for scale, intensity and frequency. Note to calculate summaries, text variables won't work. 
![spatialjoin]
![spatialjoin2]

#### Compare the areas with high density of institutions versus those with high density of residents. Don't forget the visual component of the argument - is side to side more effective, or a layered single map?
![compare_density]

#### Task 3: Test the 'subway line' hypothesis : buffers
An imaginary prominent academic writes that enclave dispersal over generations in New York follows subway lines; if this is true, we could expect to see a line connecting the cluster of institutions to the cluster of current residents. 

- #### First, build a simple buffer around the D line. 
For simplicity, imagine that the perception of being near the D line - not just a station - is important, and that a 1 kilometer distance away is meaningful. 
- Add the shape file `D_train_may2016.shp` from your folder onto your map.
- Go to the processing toolbox and navigate to `vector geometry: buffer`. Double-click.
- Select the D train layer as your input file, and select a 1.0 km for your buffer area, on both sides.
![buffer]
![buffer2]
#### Spatial query: How many institutions are within a kilometer of the D line? 
Because we have a small dataset, it's fairly easy to see that a handful of institutions intersect with the buffer. You could also calculate this precisely with a spatial query: 
- Open `select by location` , inside of the processing toolbox, under `vector selection`.![vectorselection]
- Select the features from the institutions (`Russian`), where they intersect  by comparing them to  the `buffer` layer generated in the previous step.
![selectlocation]
![selectlocation2]
The institutions that are within 1 km of the D line should be highlighted on your map. You can right-click on the layer and `save selection as` to make them their own layer. You did it! Spurious arguments in analytical maps aren't hard to make: now it's time to apply these tools to your own research and teaching agendas!

[endof4]: Images/2019/Tutorial5_endof4.png

[gear]: Images/2019/Tutorial5_gear.png

[gdal]: Images/2019/Tutorial5_gdal.png

[areakm]: Images/2019/Tutorial5_areakm.png

[dissolve]: Images/2019/Tutorial5_dissolve.png

[dissolve2]: Images/2019/Tutorial5_dissolve2.png

[fieldcalc]: Images/2019/Tutorial5_fieldcalc.png

[calculatedensity]: Images/2019/Tutorial5_calculatedensity.png

[spatialjoin]: Images/2019/Tutorial5_spatialjoin.png

[spatialjoin2]: Images/2019/Tutorial5_spatialjoin2.png

[compare_density]: Images/2019/Tutorial5_compare_density.png

[buffer]: Images/2019/Tutorial5_buffer.png

[Dline]: Images/2019/Tutorial5_buffer2.png

[vectorselection]: Images/2019/Tutorial5_vectorselection.png

[selectlocation]: Images/2019/Tutorial5_selectlocation.png

[selectlocation2]: Images/2019/Tutorial5_selectlocation2.png

