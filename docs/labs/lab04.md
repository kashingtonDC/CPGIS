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

QGIS and ArcGIS each have slighlty different methods for adding and removing tools. The relevant information to each program is described below.

=== "QGIS"

    1. In QGIS, only the Browser and Layers Panel are shown by default. 

    2. Add the Layer Styling Panel and Processing Toolbox Panel by navigating to View -> Panels in the menubar and clicking the name of those two panels.

    3. Similarly, you can add **Toolbars** by navigating to View -> Toolbars in the menu bar

    4. You can move panels around by clicking and dragging their label to undock them and redock them in a different location

=== "ArcGIS"

    1. In ArcGIS, the Contents and Catalog panes are shown by default.
    
    2. ArcGIS will add panels automatically as you take actions like modifying symbology or using processing tools from the toolbox.

    3. If you accidentally close a pane it can be confusing to get it back, simply seach for the name of the pane in the command search to add back a missing pane. 

    4. You can snap panes by clicking and dragging the label to cock them in different places on your workspace.

--- 

## Task 1: Creating Tree Points

You won't always be able to find spatial data for your GIS projects, either because it hasn't been published publicly or because it has never been made. In this activity, you will learn to create your trees layer for an area of Cal Poly's Campus. 

=== "QGIS"

    1. Add the **ESRI Satellite** basemap to your project using the NextGIS QuickMapServices plugin [Installing QuickMapServices](../getting-started/software-setup.md#installing-qgis-plugins)

    2. Zoom to Cal Poly by either finding Cal Poly visually in the basemap or by typing "> Cal Poly" into the Search Bar in the bottom left

    3. Click New Geopackage Layer in the toolbar to create the points layer to store our tree points

    4. Click the three dots to Set the save location to your lab 4 folder and name the file **CalPolyTrees**

    5. Set the Geometry Type to Point and keep the CRS as the Default (EPSG:4326 - WGS 84)

    4. Create a Text(string) field to input the tree species 

    5. Click **OK** to create the new layer

=== "ArcGIS"


After making the geopackage or Feature Layer for your GIS software, we will use the digitizing tools in GIS to create points for the trees that are in the Satellite imagery. As you create trees, use the prompt to add a species classification to each tree.

=== "QGIS" 

    1. We will use the Digitizing Toolbar to create point features, if you don't have the Digitizing Toolbar add it to your workspace by navigating to View -> Toolbars -> Digitizing Toolbar in the menubar

    2. With the CalPolyTrees Layer active in the layer panel, toggle editing with the pencil icon in the toolbar.

    3. With editing enabled, you can add features with the Add Point Feature tool.

    4. With the tool active, scroll on your mousewheel or trackpad to zoom in or out on your map canvas.

    5. Click the location of a tree to create a tree point. 

    6. A popup will appear prompting you to fill in the fields, add a species category to the Species field such as Palm, Pine, or Deciduous, and leave **fid** as *Autogenerate*. (make a best guess of what species they are)

    7. Repeat step 6 until you have 10 trees. If you need to pan around your canvas, **hold the spacebar** or c**lick in on the mouse wheel** and **move your mouse** to temporarily activate the Pan tool.

Now that you have created points for trees, let's add symbology to make a map that can show the species of the trees you mapped

=== "QGIS"

    1. With the CalPolyTrees layer active use the layer styling Panel to switch the symbology to Categorized based on the Species Value.

    2. Click Classify

    3. Change the Color of the points by double clicking the symbol preview 

    4. Take a screenshot of your QGIS window to show the trees you mapped

!!! Question "Task 1 Question"

    Add a screenshot of the trees you mapped with symbology to show the species.


---

## Task 2: Creating GreenSpace Polygons

Now that you have learned to create a point layer, this task will guide you through creating a polygon layer

=== "QGIS"

    1. Just like you did with the points layer, to create a polygon layer, use the New GeoPackage Layer Tool in the Toolbar