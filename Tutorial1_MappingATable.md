## Tutorial 1: Mapping a Table

#### Premise & Objectives
The purpose of this tutorial is to produce and export global map of population by country. For this we will use the national administrative boundaries layer in the previous tutorial, combining it with population data contained in a table. In the process, we will
- learn more about the QGIS interface, 
- add a csv table to a map project,
- perform a table join,
- change the symbology of a vector layer using quantitative attributes,
- layout and compose a map, and
- export a finished map.


### Setting up in QGIS
**Launch** QGIS and **open** the Tutorial0_GettingStarted project file. When the project loads, immediately **Save As** Tutorial1_MappingATable.qgz.

We will not be using the raster layer (the scanned and georectified 1958 population density map) to make our global population map. Thus, you can **turn off** the layer (by unchecking it in the Layers Panel) or **remove** the layer from your project by right-clicking on the layer name and selecting "Remove Layer."

#### Adding a Delimited Table
For this tutorial, we will make a map based on global population estimates from 2010. The country-level population data used for this tutorial was published by the [United Nations Population Division](http://esa.un.org/unpd/wpp/Download/Standard/Population/) in 2010. All figures are reported in thousands -- i.e., a value of "7,000" indicates a population of seven million. We have provided a cleaned version of the dataset but the original can be downloaded [here](http://esa.un.org/unpd/wpp/Download/Standard/Population/). 

These have been compiled into a simple CSV table (a delimited text file) located in the ClassData\Tutorial1_ClassData\tables folder. The file, called TotalPopulation_Countries.csv, can be opened and inspected in any software that reads tables and spreadsheets (such as Microsoft Excel or Google Sheets). We will add it to our QGIS project, as we added the vector and raster layers in the previous tutorial, and inspect its contents there.

To add a delimited text file, **click** the Add Delimited Text Layer button on the Manage Layers toolbar, which will open the Data Source Manager dialogue box to the Delimited Text panel. 

![AddTable]

In the File Name field, **click** the Browse (`...`) button to navigate to the TotalPopulation_Countries.csv file. Once you have selected the appropriate file, we will walk through some of the various options of the dialogue box individually below. You can **expand** or **collapse** the different option panels as needed. Some of the options are pre-populated by default. Others we will need to specify or change. **Notice** the preview of our data table under Sample Data at the bottom of the dialogue box.

![csvOptions1]

**File Format**: By default, the file format is read as a CSV (comma separated values) because of the file extension.

**Record and Fields Options**: Here, you can specify how your table is imported. Because the first row of our table includes *field headers* we **specify** that the "First record has field names." Similarly, we want the software to "Detect field types" which means QGIS will interpret fields that "seem" to include numbers as numeric. 

Take a moment to read through the other options, which are often useful. For example, if numeric values include commas as the decimal separator (rather than field separators) or if your table includes empty fields. 

![csvOptions2]

**Geometry Definition**: Here, we have three options for adding a table to our map project. Two will auto-generate location-based geometric features corresponding to the data in the table. (If you click each choice, you will see the options corresponding to them. When you have latitude and longitude coordinates, which is often the case, the Point Coordinates option is quite useful.) For our purposes, we will add our table with **No geometry (attribute only table)**. (In the next step we will use the geometry of the national boundaries to map the population data in this table.)

When the options are set, **click Add** to add the table as a layer in your map project. **Click Close** to close the Data Source Manager dialogue box. You should see the name of the TotalPopulation_Countries table layer in the Layers Panel.

**Save** your QGIS project.

#### Open the Population Table
The table layer performs the same as the Attribute Table of a vector layer. To open it, **right-click** on the layer name in the Layers panel and **choose** Open Attribute Table. 

**Open** the Attribute Table of the admin_0_countries layer in the same manner, in order to compare the two.

![TwoTables]

The total number of features (as well as the number filtered and selected) is listed at the top of each attribute table. Notice that our population table does not include as many countries as those listed in the polygon dataset. Notice also that they appear to have at least two fields in common: They both have a numeric field with the ISO country code, and they both have a Name field. 

**Close** your Attribute Tables.


### Performing a Table Join
A *table join* is the process of *appending data from one table to another based on unique values within a common field.* Table joins are almost always one-to-one processes. In this case, we would like to join the population data to the administrative boundary layer, in order to then visualize the global map based on the population values associated with each country. 

It appears that we have two fields that might serve as the basis of the join (two fields with unique values within each table, but shared in common between the two tables): the country code field and the country name field. We will use the numeric country code fields for our join. The values in the join fields must be identical in order to match features when performing the join. Because text fields may have spelling errors or errant spaces, the numeric fields are preferable for this matching process. 

**Helpful Note:** You will always initiate a join process on the Layer you are joining *to*. This is known as the *Target Layer*.

To assign a joined table to the admin_0_countries layer, **access** its Layer Properties dialogue box by right-clicking on the layer name and clicking Properties.

In the "Joins" panel, click the Add Join button (highlighted in red in the screenshot below) to access the Add Vector Join dialogue box. We will list the options of the Add Vector Join dialogue below.

![Join1]

**Join Layer**: Specify the Attribute Layer you would like to *join to* this layer. In this case, we would like to join the TotalPopulation_Countries table to the this (the administrative boundaries) layer.

**Join Field**: The Join Field is the particular field in the Join Layer that will facilitate the join.

**Target Field**: The Target Field is the field in the Target Layer that will facilitate the join. It must be of the same data type as the Join Field (e.g., numeric, text, etc.). 

The Join Field and Target Field do not need to have the same field header (name), but they must be of the same data type (e.g., numeric, text, etc). Further, you should know before joining that they include unique values in order to ensure a proper one-to-one join. (Imagine if we accidentally joined the population data corresponding to one country to the boundaries of another. Now imagine if we did that across the dataset, and mapped the results!)

Take a moment to read through the other options in this dialogue box. We will change only one of the defaults: the **Joined Fields** options under Dynamic Form. 

**Select** both the Dynamic Form option and the Joined Fields option. In the expanded Joined Fields option, notice that all the fields in the Join Layer (the population table) are listed. Here you can specify which of the Join Layer's fields should be appended to the Target Layer's (the administrative boundaries) attribute table. Three fields is not cumbersome, but for very large tables this is a useful option. Here, **choose** to join the Country_Code and Pop_2010 fields. We need the latter to map population by country. We will use the former to quickly see the results of our join.

When you are ready, **click** OK in the Add Vector Join dialogue box and return to the Layer Properties.

![Join2]

In the Layer Properties Joins panel, you should now see the details of the new join associated with the administrative boundary layer. **Click** OK to close the Layer Properties dialogue box. 

**Save** your map project.

**Open** the admin_0_countries layer Attribute Table to see the results of your join. 

![Join3]

**Notice** the two new fields appended to the end of our layer's original attribute table, based on shared values in the two country code fields. You should notice that features without a corresponding entry in the population table will have *NULL* values in the joined table (such as Antarctica in the screenshot above). 

**IMPORTANT NOTE**: Table joins are not permanent changes to a dataset. Instead, they are temporary associations made between datasets within the context of the specific map project. In other words, if you added the admin_0_countries layer to a new map project, it would not include the data from the population table. (Again, this is extremely uesful because we can associate several different types of data with such a layer.)

### Exporting a new shapefile
Because Table Joins are temporary, it is often useful to create a new shapefile (vector feature class) with the joined data permanently included in the layer. To do this, we will export a new shapefile from the results of the table join. 

To export a new feature layer from the admin_0_countries layer, **right-click** on the layer name in the Layers panel and click through Export > Save Features As... to open the Save Vector Layer as... dialogue box.

![Export1]

We will move through the options in the In the Save Vector Layer as... dialogue, from top to bottom. 

![Export2]

**Format**: First, specify the output format as an ESRI Shapefile using the drop-down menu.

**File name**: Navigate to the Tutorial1_ClassData folder (click the Browse `...` button) and create a new folder called "shape," where you can store the shapefile. Name the new file "admin_0_Pop2010."

**CRS**: You have a few options for specifying the Coordinate Reference System of the new shapefile. By default, an exported shapefile will be assigned the same CRS as the layer from which it is being created. In the screenshot above, this option has been changed to match the Winkel Tripel CRS of the map project file. 

We will maintain the default options for the remainder of the dialogue box, but a few are worth mentioning. Maintain the default option to **Add the saved file to map** so we can use our results without needing to add the layer to our map project. 

![Export3]

Under the **Select fields to export and their export options** you can choose to export only a subset of the fields included in the original layer (and any joined information). For our purposes, we will keep all options. 

Take a moment to expand the other options for your reference. When you are ready, **click OK** to export a new vector layer with the joined population data in the attribute table.

**Note**: If prompted to confirm the CRS of the new layer, do so and click OK.

When the new layer is added to your map project, **turn off** the previous admin_0_countries layer by unchecking it in the Layers panel. **Open** the Attribute Table of the new admin_0_Pop2010 layer to inspect its Attribute Table. 

![Export4]

**Congratulations!** You should see the two joined fields from the population table now included in the attributes of the new vector feature layer. 

#### The Attribute Field Properties: Field Alias

You probably also noticed an artifact of the join in the field headers of the last two fields in the new table. They are truncated versions of the population table's name, given the naming options chosen when we performed the table join and the ten-character limit on field headers in shapefile tables. Though we cannot change a field's name (without creating a new field and deleting the old), we can create an alias for these fields in order to make their contents more legible.

(**Note**: In the future, you can avoid this step by specifying or removing the **Custom Field Name Prefix** in the Join options earlier. That said, it is very useful to know where to access your layers' Field Properties.)

To create an alias for each field, we must access the layer's Attributes Form properties in its Layer Properties dialogue box.

![FieldAlias]

Once again, **open** the Layer Properties for the admin_0_Pop2010 layer by right-clicking on its name in the Layers panel. Reading the options from left to right:
1. Access the Attributes Form panel,
2. Select the TotalPop_1 Field from the Available Widgets options. 
3. In the General options section, specify "Pop2010" as the Alias for the TotalPop_1 field. 
4. Click Apply to save your changes.
Repeat these steps for the "TotalPopul" field, assigning it the Alias "Country_Code."

When you are finished, the new layer's attribute table should read cleanly.

**Save** your map project.


### Intro to Quantitative Symbols
We will further discuss quantitative map symbology (and classification) in a later tutorial. For now, let's make a map of this newly joined population data!

We will create a *graduated color* map from the numeric values in the Pop2010 field of the admin_0_Pop2010 attribute table. A when a graduated color symbology system is applied to a contiguous polgyon layer, the resulting map is called a *choropleth*.

**Access** the symbology options for graduated symbols (as we did for the other symbol options in the previous tutorial) in the admin_0_Pop2010 layer:
1. Open the Layer Properties dialogue box.
2. Access the Symbology panel.
3. From the first option, choose a "Graduated" system.

The options for graduated quantitative symbology are very similar to those of the categorical system we have seen before, save for color-assignment based on a range of numeric values within the attribute table instead of unique categories. We will read through the options and populate the dialogue box with our choices.

![Choropleth1]

**Column**: Select the field (column) in the attribute table containing the values you want to map. In our case, we want to map the population field, which is called "TotalPop_1."

**Symbol**: The default symbol here assigns a simple fill to each feature based on the options we choose below. Maintain this default option.

**Legend format**: The default option describes a range of values, depicted as integers. (The `%` symbol here is a coded placeholder for the appropriate values per range.) Maintain this default option.

**Method**: The only available option here is "Color" because we chose a simple fill symbol above. (A variety of other options are available through a combination of manipulating both the Symbol and Method choices.) Maintain this default option.

**Color Ramp**: You can use a preset, default color ramp or design your own by clicking the drop-down menu here. (Suggestion: Leave this decision for last.)

Under the Classes and Histogram tabs, find the **Mode** drop-down options. We will discuss these options in detail later. For now, choose a Quantile classication method. Notice that there are five **Classes** specified (to the right of the dialogue box). Together, these options ensure that the color-coding of our features will group all the features (country polygons) into five *classes* according to their population values and each class will contain the same number of features (countries). In other words, we will organize the population data into *quintiles*, grouping the top 20% most populous countries together (then the next 20%, and so on).

**Click Classify** to load your symbology settings into the dialogue. Click **Apply** to see your settings applied to the map's data frame.

Explore the other symbology and rendering options. When you are ready to save your changes and return to your map project, **click OK**.

![Choropleth2]

**Save** your map project.


### Creating a Map Layout
When you are satisfied with your symbology choices and are ready to export a map document from QGIS, you will need to create a New Print Layout. To do this, either **click** the New Print Layout button on the Project Toolbar or **click through** Project > New Print Layout on the main menu.

When prompted, you can choose to title your layout or let QGIS assign a default title for you.

Take a moment to familiarize yourself with the Map Composer interface. You can **change** the page dimensions and orientation, for example, by clicking through Layout > Page Setup.

To **add a map** from your project to the Composer, click the Add Map button or click through Add Item > Add Map from the main menu. (Both are highlighted in red in the screenshot below.) Notice also the other options one can add to a map composition.

![Layout1]

With the Add Map tool selected, click and draw a rectangle within the page to establish the frame of your map. The visible layers of your map project will be visible in the map you add to your Layout.

Next, we will add a legend to the Layout. From the toolbar or the Add Item menu, **click Add Legend**. Again, draw a rectangle to specify the legend's location and approximate size.

**Notice** the options in the Item Properties panel to the right of the Layout interface. Take a moment to scroll through the various options, including which layers to include in your legend as well as fonts and other graphic considerations. 

**Uncheck** the "Auto Update" option for the Legend's Item properties to unlock various editing opportunties. These include changing the layer's name to a more descriptive and meaningful phrase for your readers. (See the red highlights in the screenshot below.)

![Layout2]

**On Your Own:** Experiment and explore the layout options (remembering to Save along the way). **Add** a scale bar, sufficient descriptive text for a general audience, and a reference for your data source. **Specify** the various Item properties to control the map's layout. (The screenshot below is not intended as a final product, but as an indication of the fairly quick edits one can make with the Properties options.)

![Layout3]

Finally, you can **export** your layout as an Image, SVG, or PDF by either clicking through Layout > Export as... in the main menu or by clicking their corresponding buttons on the Layout Toolbar. (Alternatively, if you have experience with other graphic and illustration software, you can assempble the map elements within the layout and export for graphic editing in another software.)

![Layout4]

**Congratulations! You have a map!**

When you are finished, **Save** your Layout and Map project. 


[AddTable]: Images/2019/Tutorial1_AddTable.png
[csvOptions1]: Images/2019/Tutorial1_csvOptions1.png
[csvOptions2]: Images/2019/Tutorial1_csvOptions2.png
[TwoTables]: Images/2019/Tutorial1_TwoTables.png
[Join1]: Images/2019/Tutorial1_Join1.png
[Join2]: Images/2019/Tutorial1_Join2.png
[Join3]: Images/2019/Tutorial1_Join3.png
[Export1]: Images/2019/Tutorial1_Export1.png
[Export2]: Images/2019/Tutorial1_Export2.png
[Export3]: Images/2019/Tutorial1_Export3.png
[Export4]: Images/2019/Tutorial1_Export4.png
[FieldAlias]: Images/2019/Tutorial1_FieldAlias.png
[Choropleth1]: Images/2019/Tutorial1_Choropleth1.png
[Choropleth2]: Images/2019/Tutorial1_Choropleth2.png
[Layout1]: Images/2019/Tutorial1_Layout1.png
[Layout2]: Images/2019/Tutorial1_Layout2.png
[Layout3]: Images/2019/Tutorial1_Layout3.png
[Layout4]: Images/2019/Tutorial1_Layout4.png
