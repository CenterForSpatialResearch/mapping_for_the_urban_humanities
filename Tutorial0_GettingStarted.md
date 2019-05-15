## Tutorial 0: Getting Started
#### Premise & Objectives
The purpose of this tutorial is to introduce you to the QGIS interface, exploring a environment and a handful of its options. In doing this, we will set up the layers needed for the first tutorial (Tutorial 1), exploring the QGIS environment and a handful of its options. In the process, we will
- start and save a map project,
- add vector- and raster-based spatial data to the map project,
- access the Attribute Table of a vector layer,
- change the symbology of a vector layer using qualitative attributes, and
- learn the basics of working with map projections.

#### Prep
Download the GitHub repository for this course. After following [this link](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities_2019), click on the green button on the right side that reads `Clone or Download`, and select `Download ZIP`. Save and decompress the downloaded folder to your preferred working location. (We highly recommend establishing a single folder or directory for all of the work and tutorials associated with the workshop.) The Class_Data folder will then have most of the datasets needed for tutorials.

Additional datasets required for the tutorials (those larger than certain upload limits allow) can be found in [this public google drive folder](https://drive.google.com/drive/u/1/folders/1yJlnKJy1WxAXuox4nmBxrs6xlwPK1HLb), including the georectified scanned map image included later in this tutorial. Download, save, and decompress this folder to the same directory as the GitHub repository you saved.

### Setting up QGIS

**Launch** QGIS. Your new blank map project will look like this:
![blank]
<div style="page-break-after: always;"></div>

Begin to familiarize yourself with the interface. Yours may not exactly resemble the layout shown above. For instance, most toolbars and panels are movable, allowing you to set up your workspace as you like. You can always add or remove these elements of the workspace by clicking through `View > Panels or Toolboars` (from the main menu bar). For more information, refer to this [brief description](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Resources/QGIS_InterfaceDescription.md) of the elements of the interface.

**Important Note:** Like all GIS software, QGIS provides an environment in which we work with spatial data (whether vector- or raster-based). Datasets are not stored within QGIS. Rather, layers stored elsewhere are assembled within a **map project** where we can visualize, compare, manipulate, and analyze them together. Within the map project, we can also compose and export a map. Storing your data outside of the project allows you to include a particular data layer in several map projects without having to produce multiple copies of it, but it carries two important implications: (1) Maintaining clear file organization is important. The data layers associated with your map projects are **linked** to each project from their stored location. If those files are moved or reorganized, then their links will break and you will need to re-establish their linkage. (2) GIS software is continuously reading the path to each data layer, accessing the information stored within your datasets. To enable this reading smoothly, we highly recommend a policy of **no spaces in your path or file names**.

**Save** your (currently empty) map project in your working folder by clicking through `Project > Save As...` on the main menu. Name the project file Tutorial0_GettingStarted. (The .qgz extension for QGIS project files will be added to your file name automatically.)

If your interface defaults to a list of Recent Projects, double-click the newly created project file name to access and open it.

You should notice your project added to the Brower Panel, in a folder collection named Project Home.

![ProjectHome]


#### Adding Layers

In the next tutorial, we will create a global map of population by country. Here, we will add a few different data layers to our map project, some which we will ultimately use in our new map and another for comparison, as a means of learning to navigate the interface.  

There are several ways to add data to a map project. We will begin by using the `Add Vector Layer` button located on the Manage Layers Toolbar. If this toolbar is not present, remember you can access it by clicking through `View > Toolbars > Manage Layers Toolbar` from the main menu. (In the screenshot below, the Add Vector Layer button is the first.) Hover your cursor over each option to note their range.

![AddVectorLayer]

**Click** the Add Vector Layer button to open the Data Source Manager dialogue box and access the Vector options. There, you can **navigate** to the `Tutorial0_ClassData/Shape/` folder, which contains the vector shapefile layer we will use for this project, by clicking the Browse `...` button highlighted in red below. (Alternatively, you an always use the Browse option to navigate through your files.)

![DataSourceManager]


![FileBrowsingSHP]

There are a number of different file extensions here that may be unfamiliar. Shapefiles are collections are separate files that describe different information or perform specific roles. The primary component files are as follows:

* .shp - The main file that stores the feature geometry (required).
* .shx - The index file that stores the index of the feature geometry (required).
* .dbf - The dBASE table that stores the attribute information of features (required).
* .sbn and .sbx - The files that store the spatial index of features.
* .prj - The file that stores the coordinate system information.
* For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).

**Important Note:** The files associated with a shapefile must stay together in the same folder, otherwise QGIS will not be able to load the layer (for the required files) or may not read it properly.

We will add the admin_0_countries shapefile (`admin_0_countries.shp`). Select the file and click Open.

Confirm that the appropriate file is named in the Vector Dataset(s) path in the Data Source Manager dialogue box and **click Add.**

![CRSSelector]

The Coordinate Reference System Selector dialogue box will appear asking that you confirm (or specify) the coordinate system of the dataset you are adding to your map project. This layer is projected with the Mollweide *projection* based on the World Geodetic System of 1984 (WGS1984) *datum*. Read through the information in the dialogue box confirming this.

**Click OK** in the Coordinate Reference System Selector dialogue box to add the layer to your map project.

**Click Close** in the Data Source Manager dialogue box to exit it.

The layer should appear in your map project as shown below. Note that the colors associated with each polygon feature (in this case depicting national boundaries) is the same for all features in the layer, and the color assigned is arbitrary.

**Save** your map project.

![Admin0Added]

The layer name appears listed in the Layers Panel, along with a swatch of its symbol. You can **toggle** layers on and off by clicking the check-mark next to their name, allowing you to choose which are visible when multiple layers are added to a project. Further, you can arrange the order in which the layers are rendered by reordering the list (simply click and drag to reorder).


### Attributes

#### Open the Attribute Table
To access the *Attribute Table* of associated with a vector feature class (and thus inspect the attributes of each feature), **right-click** on the layer name in the Layers panel and **select** Open Attribute Table.

![OpenAttributeTable]

The layer's Attribute Table will appear, allowing you to inspect the information contained in the shapefile per feature. In the case of this basic administrative boundary layer, it contains information commonly used to identify countries. In the screenshot below, the table is sorted by the Name *field* (click on the field *header* to sort). The first feature is *selected* (click on the row label -- in this case, "1"). The corresponding polygon feature is also selected within the map project's *data frame*.

![AttributeTableBasic]

The attributes of this country-level dataset include the short and long-form names of each country in two separate *text* or *string* fields. Two additional text fields describe the global region and subregions (here, determined by the UN) to which each country belongs. Lastly, there are two separate fields denoting the ISO three-digit country code. The ISO_N3 field indeed includes three digits (with placeholder zeros where needed) and the Cnt_Code field does not. In this case, the ISO_N3 field contains text and the Cnt_Code field is numeric. Thus, while the ISO_N3 field appears to contain numeric information, the software does not interpret it as such and would be unable to perform mathematical operations on that field. (Remember that all information contained within a field is of a single data type.)

To **deselect** any selected features, click the Deselect All button on the Attribute Table's toolbar (or on the Attributes Toolbar).

![Deselect]

#### On your own: Interactively Selecting and Inspecting Features and Attributes

Interactively select features in the Attribute Table to highlight the corresponding polygon in the data frame.

Of course, the relationship between the geometry and attributes of a feature works in the opposite direction as well. Using the Selection Tool from the Attributes Toolbar (chosen in the screenshot below), you can also interactively select polygons and highlight them in the Attribute Table. Further, you can isolate selected features from the table: choose Show Selected Features from the the Attribute Table's filter drop-down menu.

![InteractiveSelection]

Notice in the screenshot above that Indonesia is selected. From the Attribute Table we can see that the many polygons representing the area of Indonesia collectively represent only one feature in the dataset. This is an example of a *multipart polygon*.

While exploring, you can zoom and pan across the map's data frame with the tools included in the Map Navigation Toolbar (below) or by scrolling (to zoom) and holding (to pan) your middle mouse button.

![NavigationToolbar]

**Deselect** any selected features. Return your map to its full extents by **clicking the Zoom Full button**. **Save** your QGIS map project.


### Intro to Symbology
We will discuss map *symbology* and cartography more completely later in the workshop, but for now, we will learn to make a few simple changes to the appearance of the national boundaries layer. First, we will change the default *symbol* used to visualize the data layer. Second, we will assign colors to each polygon based on a qualitative field in its attribute table (in this case, the subregion designation).

There are a few short-cut options in the QGIS interface for quickly changing a layer's symbols. We will walk through the Layer Properties dialogue box, which includes these and many more options and functions per layer.

#### Accessing Symbology Properties
To access the Layer Properties dialogue box, **right-click** on the layer name (`admin_0_countries`) in the Layers Panel and choose **Properties**.

From the lelf-hand menu, choose the **Symbology** menu. You should notice that the layer is currently symbolized with a "Single Symbol" system and a "simple fill." **Highlight** "Simple Fill" from the panel at the top of the dialogue box to access the symbol options.

![SimpleFill]

#### Changing a Single Symbol
Take a moment to read through the various options and to experiment with an alternative symbol. **Note** that these options are tailored to a polygon feature class. (Polyline layers, for example, would not have "fill" options.) You can specify the color and style of the polygon fill and the color and width of the polygon stroke (outline).

**Click** Apply to apply your changes. When you are satisfied with your decisions, **click** OK to save them and close the Properties dialogue box. In the example below, the features have a transparent fill and a heavy, red stroke.

![SingleSymbolChanged]

#### Qualitative or Categorical Symbology
We can also use the layer's attributes to organize or categorize the map's symbology. To do this, access the Layer Properties (Symbology menu) dialogue box again and specify **Categorized** symbols from the drop-down menu at the top of the dialogue.

![CategoricalSymbol]

The symbology options will change, and from here we can quickly assign separate symbols to each feature within unique groups described in the Attribute Table. In this case, we will effectively color-code our polygons based on their subregion.

1. From the Column drop-down menu, **select** the SUBREGION field. **Note** that this menu includes each of the different fields included in the layer's attribute table.
2. **Confirm** that the Color Ramp option is set to Random Colors. (If it is not, you can select it by clicking the drop-down menu.)
3. Next, **click** the Classify button toward the bottom of the dialogue box to populate the panel with each unique value from the SUBREGION field. The Symbol list should automatically include each of the subregions listed in our dataset, with unique (randomly generated) color values.
4. **Click Apply** to apply your symbology changes.

![Subregions]

**Note** some of the options here. Each of the category symbols can be individually altered by double-clicking the color symbol swatch in the list. Categories can be toggled on or off (rendering features with those attribute values visible/invisible) or removed from the list altogether.

When you are satisfied with your categorical symbology strategy, **click OK** to exit the Layer Properties dialogue box.

**Save** your QGIS project.


### Finishing Up
Thus far, we have been interacting with a Mollweide map projection. Before finishing this tutorial, we will reproject the map data frame to match the original projection of a scanned, *georectified* global population map.

The georectified map (below) we will add to our project is from the [David Rumsey Historical Map Collection] (https://www.davidrumsey.com/luna/servlet/detail/RUMSEY~8~1~225244~5505992;JSESSIONID=fa751117-cbd7-452b-b867-46dac48ea52f#). The map is drawn in the Winkel Tripel projection, which is now commonly used in global atlases for its minimal distortion in distance, area, and direction.

![Bartholomew1958]

#### Assigning a new projection
When assigning a new projection to the data frame, **note** that we are not assigning a new projection or coordinate reference system to our original data layer. Rather, we are using the coordinate reference information contained within each spatial dataset to re-positioning those coordinates according to the rules of a different projection.

To change the the Coordinate Reference System of the map project, access the Project Properties dialogue box by clicking the Coordinate Reference System button on the bottom-right of the interface (in the screenshot below) or by clicking through Project > Properties from the Main Menu.

![CRSbutton]

In the CRS panel of the Project Properties dialogue box, **notice** the list of pre-installed coordinate systems. (The list is long, detailed, and varied. Almost all projections and datums can be quickly searched online for more information.)

Because we know the projection we need, we can use the Filter option to search for it. In the Filter text box at the top of the dialogue, **type "Winkel"** to isolate the reference systems that include Oswald Winkel's name (highlighted in blue in the screenshot below).

![Winkel]

In the resulting list of Coordinate Reference Systems, **highlight** the World_Winkel_Tripel_NGS option under Winkel Tripel (red box).

Notice (green box) that the coordinate reference system information includes more than the projection itself, but its origin,the datum to which it is applied (WGS84), and its linear unit (meters).

**Click OK** to change the projection of the map project's data frame. You should notice a quick transformation.

**Save** your map project.

#### Adding a raster layer
Lastly, **add** a new layer to your map project by, once again, accessing the Data Source Manager dialogue box. (You can click the Add Raster button from the toolbar or simply navigate to the Raster panel if you chose a different option.)

Just as when we added the original vector polygon layer, **navigate** to your data using the browse (`...`) button. **Add** the GeoTIFF file called DensityRec.tif located in the Tutorial0_ClassData\raster\ folder. (This dataset is provided in the auxiliary download for large files. You can find it directly [here](https://drive.google.com/drive/u/1/folders/1yJlnKJy1WxAXuox4nmBxrs6xlwPK1HLb). The cropped and georectified map should align fairly well with the national boundaries layer in your map project.

To finish, **arrange** your data layers (click and drag in the Layers panel), placing the current national boundaries over the 1958 map, and **change the national boundary symbols** such that they are transparent.

![WithRaster]

**Save** your QGIS project.

______________________________________________________________________________________________________________
Tutorial written by Leah Meisterlin, for *Mapping for the Urban Humanities*, a intensive workshop for Columbia University faculty taught in Summer 2019 by the [Center for Spatial Research](http://c4sr.columbia.edu). More information about the course is available [here](http://c4sr.columbia.edu/courses/mapping-urban-humanities-summer-bootcamp).

[blank]: Images/2019/Tutorial0_interface_blank.png
[ProjectHome]: Images/2019/Tutorial0_ProjectHome.png
[DataSourceToolbar]: Images/2019/Tutorial0_DataSourceManagerToolbar.png
[AddVectorLayer]: Images/2019/Tutorial0_AddVectorLayer.png
[FileBrowsingSHP]: Images/2019/Tutorial0_FileBrowsingShp.png
[DataSourceManager]: Images/2019/Tutorial0_DataSourceManager.png
[CRSSelector]: Images/2019/Tutorial0_CoordinateReferenceSystemSelector.png
[Admin0Added]: Images/2019/Tutorial0_Admin0Added.png
[OpenAttributeTable]: Images/2019/Tutorial0_OpenAttributeTable.png
[AttributeTableBasic]: Images/2019/Tutorial0_AttributeTableBasic.png
[Deselect]: Images/2019/Tutorial0_Deselect.png
[InteractiveSelection]: Images/2019/Tutorial0_InteractiveSelection.png
[NavigationToolbar]: Images/2019/Tutorial0_NavigationToolbar.png
[SingleSymbolChanged]: Images/2019/Tutorial0_SingleSymbolChanged.png
[CategoricalSymbol]: Images/2019/Tutorial0_CategoricalSymbol.png
[SimpleFill]: Images/2019/Tutorial0_SimpleFill.png
[Subregions]: Images/2019/Tutorial0_Subregions.png
[Bartholomew1958]: Images/2019/Tutorial0_Bartholomew1958.png
[CRSbutton]: Images/2019/Tutorial0_CRSbutton.png
[Winkel]: Images/2019/Tutorial0_Winkel.png
[WithRaster]: Images/2019/Tutorial0_WithRaster.png
