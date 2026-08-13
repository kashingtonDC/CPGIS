# Lab 2: Exploring Vector Data and Attribute Tables

!!! info "Lab Overview"
    **Topic**: Vector Data and Attributes
    **Time Required**: 2-3 hours
    **Software**: QGIS or ArcGIS Pro

---

## Lab Preparation


1. This lab doesn't require a data download.
2. Create a folder for this lab in your One Drive folder called GIS_Course/Labs/Lab-04.
4. Create a new map project in QGIS or ArcGIS and save it to your Lab-04 folder.

---

## Introduction

In this lab you will learn how to create your own vector data in GIS. You will use the **Digitizing tools** in your GIS software to create points for trees on campus and polygons of greenspaces on campus. You will also learn how to **create and modify attributes** using the **field calculator**.


!!! note "Learning Objectives"
    - Creating vector features 
    - Editing attributes 
    - Field calculator basics  
    - Basic topology and avoiding topological issues (e.g. gaps, overlaps, slivers) 

---

## Toolbars and Panels

Both QGIS and ArcGIS have toolbars, panels, panes and ribbons in their interfaces. As you work with GIS, you may occasionally want add, remove, or rearrange panels or toolbars to fit your needs.

QGIS and ArcGIS each have slightly different methods for adding and removing tools. The relevant information to each program is described below.

=== "QGIS"

    1. In QGIS, only the **Browser and Layers Panel** are shown by default. 
    ![Task 0 Step 1 Image](../images/lab-images/lab-04/00-Q-01.png)

    2. Add the **Layer Styling Panel and Processing Toolbox Panel** by navigating to View -> Panels in the menubar and clicking the name of those two panels.
    ![Task 0 Step 2 Image](../images/lab-images/lab-04/00-Q-02.png)

    3. Similarly, you can add **Toolbars** by navigating to **View -> Toolbars** in the menu bar

    4. You can move panels around by **clicking and dragging** their label to undock them and redock them in a different location
    ![Task 0 Step 4 Image](../images/lab-images/lab-04/00-Q-04.png)

=== "ArcGIS"

    1. In ArcGIS, the Contents and Catalog panes are shown by default.
    
    2. ArcGIS will add panels automatically as you take actions like modifying symbology or using processing tools from the toolbox.

    3. If you accidentally close a pane it can be confusing to get it back, simply search for the name of the pane in the command search to add back a missing pane. 

    4. You can snap panes by clicking and dragging the label to cock them in different places on your workspace.

--- 

## Task 1: Creating Tree Points and adding symbology

You won't always be able to find spatial data for your GIS projects, either because it hasn't been published publicly or because it has never been made. In this activity, you will learn to create your trees layer for an area of Cal Poly's Campus. 

### Creating a new Geopackage

=== "QGIS"

    1. Add the **Google Hybrid** basemap to your project using the NextGIS **QuickMapServices** plugin [Installing QuickMapServices](../getting-started/software-setup.md#installing-qgis-plugins)
    ![Task 1 Step 1 Image](../images/lab-images/lab-04/01-Q-01.png)

    2. Zoom to *Cal Poly* by either finding Cal Poly visually in the basemap or by typing "**> Cal Poly**" into the **Search Bar** in the bottom left
    ![Task 1 Step 2 Image](../images/lab-images/lab-04/01-Q-02.png)

    3. Click **New Geopackage Layer** in the *toolbar* to create the points layer to store our tree points.
    ![Task 1 Step 3 Image](../images/lab-images/lab-04/01-Q-03.png)

    4. Click the three dots to Set the save location to your lab 4 folder and name the file **CalPolyTrees**.
    ![Task 1 Step 4 Image](../images/lab-images/lab-04/01-Q-04.png)

    5. Set the **Geometry Type** to *Point* and keep the **CRS** as the *Default (EPSG:4326 - WGS 84)*

    6. Create a **Text(string)** field called *Species* and leave the *maximum length blank*.
    ![Task 1 Step 6 Image](../images/lab-images/lab-04/01-Q-06.png)

    7. Click **OK** to create the new layer.

=== "ArcGIS"

### Creating Tree Points

After making the geopackage or Feature Layer for your GIS software, we will use the digitizing tools in GIS to create points for the trees that are in the Satellite imagery. As you create trees, use the prompt to add a species classification to each tree.

=== "QGIS" 

    8. We will use the **Digitizing Toolbar** to create point features, if you don't have the Digitizing Toolbar add it to your workspace by navigating to View -> Toolbars -> Digitizing Toolbar in the menubar

    9. With the **CalPolyTrees** Layer active in the layer panel, **toggle editing** with the *pencil icon in the toolbar*.
    ![Task 1 Step 9 Image](../images/lab-images/lab-04/01-Q-9.png)

    10. With editing enabled, you can add features with the **Add Point Feature tool**.
    ![Task 1 Step 10 Image](../images/lab-images/lab-04/01-Q-10.png)

    11. With the tool active, *scroll on your mousewheel or trackpad* to zoom in to **Dexter Lawn** on your map Canvas.

    12. **Click** the location of a tree to *create a tree point*, A popup will appear prompting you to fill in the fields

    13. Add a species category to the **Species field** such as *Palm, Pine, or Deciduous*, and leave **fid** as *Autogenerate*. (make a best guess of what species they are)
    ![Task 1 Step 13 Image](../images/lab-images/lab-04/01-Q-13.png)

    14. **Repeat steps 5 and 6** until you have *10 trees*. If you need to pan around your canvas, **hold the spacebar** or **click in on the mouse wheel** and **move your mouse** to temporarily activate the Pan tool.

    15. Click the *pencil icon* to **toggle editing** and save the new points you added
    ![Task 1 Step 15 Image](../images/lab-images/lab-04/01-Q-15.png)


### Symbolizing by Species

Now that you have created points for trees, let's add symbology to make a map that can show the species of the trees you mapped

=== "QGIS"

    16. With the CalPolyTrees layer active use the **Layer Styling Panel** to switch the symbology to **Categorized** based on the *Species* **Value**.
    ![Task 1 Step 16 Image](../images/lab-images/lab-04/01-Q-16.png)

    17. Click **Classify**

    18. **Change the color or shape** of the tree markers for each category by **double clicking** the *symbol preview.* 
    ![Task 1 Step 18 Image](../images/lab-images/lab-04/01-Q-18.png)

    19. Take a screenshot of your QGIS window to show the trees you mapped.
    ![Task 1 Step 19 Image](../images/lab-images/lab-04/01-Q-19.png)

!!! Question "Task 1 Question"

    Add a screenshot of the trees you mapped including the symbology you used to show the species.


---

## Task 2: Creating GreenSpace Polygons and adding labels

Now that you have learned to create a point layer, this task will guide you through creating a polygon layer

### Creating a Polygon Layer

=== "QGIS"

    1. Just like you did with the points layer, to create a polygon layer, use the New GeoPackage Layer Tool in the Toolbar
    ![Task 2 Step 1 Image](../images/lab-images/lab-04/02-Q-01.png)

    2. Click the three dots to set the save location to your lab-04 folder and name the GeoPackage **CalPolyGreenSpaces**
    ![Task 2 Step 2 Image](../images/lab-images/lab-04/02-Q-02.png)

    3. Set the **Geometry Type** to *Polygon*, Change the **Coordinate Reference System** to *California Zone 5 (EPSG: 2874)* and add a **Text(string)** field called *Name*
    ![Task 2 Step 3 Image](../images/lab-images/lab-04/02-Q-03.png)
    
    4. Toggle Editing on the **CalPolyGreenSpaces** layer and switch to the **Add Polygon Feature** tool
    ![Task 2 Step 4 Image](../images/lab-images/lab-04/02-Q-04.png)

    5. Create a polygon for Dexter Lawn by **clicking the corners** and **right clicking** to complete the shape.
    ![Task 2 Step 5 Image](../images/lab-images/lab-04/02-Q-05.png)

    6. Input Dexter Lawn into the Name field and repeat with 4 more lawns or plazas for a total of 5 polygons. 
    ![Task 2 Step 6 Image](../images/lab-images/lab-04/02-Q-06.png)

    7. If you make a mistake while drawing a polygon, you can use the Vertex Tool to move or add points to refine the shape.
    ![Task 2 Step 7 Image](../images/lab-images/lab-04/02-Q-07.png)

    8. You can also use command/ctl Z to undo or shift-command/ctl Z to redo changes
    ![Task 2 Step 8 Image](../images/lab-images/lab-04/02-Q-08.png)

    9. Toggle Editing and save your changes
    ![Task 2 Step 9 Image](../images/lab-images/lab-04/02-Q-09)

Now that we have made some polygons, let's make our map better by adjusting the symbology of the Green Spaces layer by making it green and adding labels

### Adding Labels

=== "QGIS"

    10. With the CalPolyGreenSpaces layer active change the symbology to a green fill.
    ![Task 2 Step 10 Image](../images/lab-images/lab-04/02-Q-10.png)

    11. Now switch to the Labels Tab in the layer Styling Panel.

    12. Change the label rule to Single Labels based on the Name Value that we added while creating the polygons.
    ![Task 2 Step 12 Image](../images/lab-images/lab-04/02-Q-12.png)

    13. Change the font and size to your liking and add a Buffer to the text to make it more readable.
    ![Task 2 Step 13 Image](../images/lab-images/lab-04/02-Q-13.png)

    14. There are a multitude of other settings in the Label Properties, that you can explore in the [QGIS Documentation](https://docs.qgis.org/3.44/en/docs/user_manual/style_library/label_settings.html) or in other online tutorials.

    15. For this activity, let's reduce the duplicate labels for Dexter Lawn by Navigating to the Placement Tab in the Label Properties and checking the **Avoid Duplicate Labels** Setting.
    ![Task 2 Step 15 Image](../images/lab-images/lab-04/02-Q-15.png)

!!! Question "Task 1 Question"

    Add a screenshot of the Green Spaces that you mapped and added name labels to.

---

## Task 3: Editing Attributes

When working with vector data you may need to edit attributes or add fields to your data. In this activity you will learn how to edit attributes and add another field to your trees layer to rate the shade of each of the trees you mapped.

### Adding a Shade Rating to Trees

=== "QGIS"

    1. Open the Attribute Table for the Cal Poly Trees Layer by right clicking and selecting Open Attribute Table.
    ![Task 3 Step 15 Image](../images/lab-images/lab-04/03-Q-01.png)

    2. Dock the Attribute Table with the Dock Attribute Table Button
    ![Task 3 Step 2 Image](../images/lab-images/lab-04/03-Q-02.png)

    3. To add a new field, you must enable editing for the layer by using one of the toggle editing buttons or by right clicking and choosing toggle editing
    ![Task 3 Step 3 Image](../images/lab-images/lab-04/03-Q-03.png)
    
    5. Click the New Field button to add a new field for the Shade Rating. 
    ![Task 3 Step 5 Image](../images/lab-images/lab-04/03-Q-05.png)

    6. The shade rating will be on a 1-5 scale, so it is probably best to use the integer data type, but the decimal number data type is also a good choice since it would allow partial star ratings.
    ![Task 3 Step 6 Image](../images/lab-images/lab-04/03-Q-06.png)

    7. Create the Shade Rating Field with your chosen data type
    ![Task 3 Step 7 Image](../images/lab-images/lab-04/03-Q-06.png)

    8. Now use the Select Features by area tool to select each tree and then input a shade rating into the attribute table by double clicking and typing a number
    ![Task 3 Step 8 Image](../images/lab-images/lab-04/03-Q-08.png)

    9. You can highlight your selected features in the attribute table by toggling the Move selection to top setting in the Attribute Table.
    ![Task 3 Step 9 Image](../images/lab-images/lab-04/03-Q-09.png)

    10. Add a shade rating to all 10 of the trees you created earlier, either from your personal knowledge or based on the species category or imagery
    ![Task 3 Step 10 Image](../images/lab-images/lab-04/03-Q-10.png)

    11. Toggle editing to save your edits.

### Sizing tree Points by Shade Rating

It is possible to show numerical data in GIS by apply a field to the size variable of a layer's symbology. We will set the Shade Rating to the size of the tree markers to show which trees have a higher or lower shade cast.

=== "QGIS"

    12. Select the CalPolyTrees layer and Open the Layer Styling Panel.
    ![Task 3 Step 12 Image](../images/lab-images/lab-04/03-Q-12.png)

    13. Select the Symbol icon to change the symbol size for all the points
    ![Task 3 Step 13 Image](../images/lab-images/lab-04/03-Q-13.png)

    14. You can set the size manually by adjusting the size category. All of the tree markers should change size together
    ![Task 3 Step 14 Image](../images/lab-images/lab-04/03-Q-14.png)

    15. If only one species of tree changed size, go back and ensure that none of the species are selected on the main page.
    ![Task 3 Step 15 Image](../images/lab-images/lab-04/03-Q-15.png)

    16. To apply the Shade rating to the tree marker size, click the **Data Define Override** button, navigate the **Field type: int, double, string** and select the *Shade Rating* Field.
    ![Task 3 Step 16 Image](../images/lab-images/lab-04/03-Q-16.png)

    17. The size of the tree marker is now determined by the shade rating of the tree.
    ![Task 3 Step 17 Image](../images/lab-images/lab-04/03-Q-17.png)


!!! Question "Question 3"

    Take a screenshot of your map canvas with the CalPolyTrees layer displaying the species and shade rating of the trees you mapped. 

    What method did you choose to make your shade and species determinations. If you had more time to work on a tree layer like this, what would you need to improve the data or make it easier to map the species and shade more accurately? 

---

## Task 4: Field Calculator Basics

Manipulating the Attribute table and symbology vector layers, allows a GIS technician to show data in uniques ways. Up until now, you have modified the attribute table of your layers manually, but what if your project has a layer with 100's or 1000's of features?

The field calculator tool allows you to modify attribute tables and creating data fields using expressions and code. In this activity, you will learn how to add an area field to your CalPolyGreenSpaces layer.

### Calculating Area

=== "QGIS"

    1. Prepare for using the field calculator by making the CalPolyGreenSpaces layer visible and opening and docking the Attribute Table
    ![Task 4 Step 1 Image](../images/lab-images/lab-04/03-Q-01.png)

    2. Open the Field Calculator for the CalPolyGreenSpaces layer by clicking the Open Field Calculator Button.
    ![Task 4 Step 2 Image](../images/lab-images/lab-04/03-Q-02.png)

    4. Leave Create virtual Field setting off, set the **Output field name** to *Area (sqm)* and set the data type to Decimal (double) to retain decimal area calculations.
    ![Task 4 Step 4 Image](../images/lab-images/lab-04/03-Q-04.png)

    5. We will use the "**$Area**" function, either type this function into the Expression area or search it in the expression dictionary.
    ![Task 4 Step 5 Image](../images/lab-images/lab-04/03-Q-05.png)

    6. You will see a preview of the calculation result in the bottom left, and if everything looks good, press ok to apply the calculation.
    ![Task 4 Step 6 Image](../images/lab-images/lab-04/03-Q-06.png)

    7. Now that the areas have been calculated, it is not immediately obvious what units the areas are in, with value that range from ~400 to ~6,000.
    ![Task 4 Step 7 Image](../images/lab-images/lab-04/03-Q-07.png)

    8. QGIS default areas are measured in square meters, but you can check what your QGIS is set to by navigating to Project -> Properties in the menubar and looking at the measurements section. 
    ![Task 4 Step 8 Image](../images/lab-images/lab-04/03-Q-08.png)

    9. Change the area measurement to Acres and repeat steps 4 and 5 to create a new Area (Acres) field.
    ![Task 4 Step 9 Image](../images/lab-images/lab-04/03-Q-09.png)

=== "ArcGIS"

