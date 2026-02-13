# Lab 1: Creating Your First Map

!!! info "Lab Overview"
    **Topic**: Introduction to GIS Software
    <br>**Time Required**: 2-3 hours
    <br>**Software**: QGIS or ArcGIS Pro
    <br>**Due**: [See course schedule]

---

## Learning Objectives

By completing this lab, you will:

- Navigate GIS software interface (QGIS or ArcGIS Pro)
- Load and visualize spatial data
- Use basic map navigation tools (pan, zoom, identify)
- Change layer symbology and appearance
- Create a simple map layout
- Export a map as a PDF

---

## Prerequisites

- [ ] GIS software installed ([Setup Guide](../getting-started/software-setup.md))
- [ ] Basic computer file management skills
- [ ] Completed Topic 1: [What is GIS?](../topics/01-what-is-gis.md)

---

## Part 1: Getting Started with GIS Software

### QGIS Users

#### Launch QGIS

1. Open **QGIS Desktop** from your applications
2. You should see the QGIS interface with:
   - **Menu bar** at the top
   - **Toolbars** below the menu
   - **Browser panel** (left side)
   - **Layers panel** (left side, below browser)
   - **Map canvas** (center - the main viewing area)
   - **Status bar** (bottom)

![QGIS Interface](../images/qgis-interface.png)

#### Understanding the Interface

| Component | Purpose |
|-----------|---------|
| **Browser Panel** | Navigate your file system and database connections |
| **Layers Panel** | Shows all loaded layers and controls visibility |
| **Map Canvas** | Main viewing area where your map displays |
| **Toolbars** | Quick access to common tools |
| **Status Bar** | Shows coordinates, scale, coordinate system |

---

### ArcGIS Pro Users

#### Launch ArcGIS Pro

1. Open **ArcGIS Pro** from your applications
2. Click **Create a new project**
3. Choose **Map** template
4. Name your project: `Lab01_FirstMap`
5. Choose a location (your GIS_Course folder)
6. Click **OK**

You should see:
- **Ribbon** at the top (organized into tabs)
- **Contents pane** (left side) - shows layers
- **Catalog pane** (right side) - browse data
- **Map view** (center) - where your map displays

![ArcGIS Pro Interface](../images/arcgis-interface.png)

---

## Part 2: Loading Data

### Download Sample Data

Download the lab data package: [Lab01_Data.zip](link-to-data)

Contents:
- `california_counties.shp` - County boundaries (polygons)
- `california_cities.shp` - Major cities (points)
- `california_highways.shp` - Major highways (lines)

!!! tip
    Extract the ZIP file to: `GIS_Course/Labs/Lab01/Data/`

---

### Loading Vector Data

=== "QGIS"

    **Method 1: Drag and Drop**
    1. Open File Explorer/Finder
    2. Navigate to your Lab01/Data folder
    3. Drag `california_counties.shp` onto the map canvas
    
    **Method 2: Add Vector Layer**
    1. Click **Layer → Add Layer → Add Vector Layer**
    2. Click the **...** button next to "Vector Dataset(s)"
    3. Navigate to your data folder
    4. Select `california_counties.shp`
    5. Click **Open**, then **Add**
    
    Repeat for `california_cities.shp` and `california_highways.shp`

=== "ArcGIS Pro"

    **Method 1: Drag and Drop**
    1. In the **Catalog pane**, navigate to your Lab01/Data folder
    2. Drag `california_counties.shp` onto the map
    
    **Method 2: Add Data**
    1. On the **Map tab**, click **Add Data**
    2. Navigate to your Lab01/Data folder
    3. Select `california_counties.shp`
    4. Click **OK**
    
    Repeat for `california_cities.shp` and `california_highways.shp`

---

### Understanding What You Loaded

You should now see three layers in your Layers/Contents panel:

```
☑ california_highways
☑ california_cities
☑ california_counties
```

!!! question "Question 1"
    What geometry type is each layer?
    
    - Counties: ____________
    - Cities: ____________
    - Highways: ____________

---

## Part 3: Map Navigation

### Essential Navigation Tools

=== "QGIS"

    | Tool | Icon | Shortcut | Purpose |
    |------|------|----------|---------|
    | **Pan** | ✋ | Hold Spacebar | Move around the map |
    | **Zoom In** | 🔍+ | Ctrl/Cmd + Scroll | Zoom closer |
    | **Zoom Out** | 🔍- | Ctrl/Cmd + Scroll | Zoom farther |
    | **Zoom Full** | 🗺️ | Ctrl+Shift+F | View entire map extent |
    | **Zoom to Layer** | - | Right-click layer → Zoom to Layer | Zoom to specific layer |
    | **Identify** | ℹ️ | Ctrl+Shift+I | Click features to see attributes |

=== "ArcGIS Pro"

    | Tool | Icon | Shortcut | Purpose |
    |------|------|----------|---------|
    | **Explore** | ✋ | X | Pan and identify features |
    | **Fixed Zoom In** | 🔍+ | Z | Zoom in by fixed amount |
    | **Fixed Zoom Out** | 🔍- | Shift+Z | Zoom out by fixed amount |
    | **Zoom to Selection** | - | Ctrl+Shift+Z | Zoom to selected features |
    | **Full Extent** | 🗺️ | Ctrl+Shift+F | View entire map extent |

### Practice Navigation

**Exercise:**

1. Click **Zoom Full** to see all of California
2. Use the **Pan** tool to center the map on the San Francisco Bay Area
3. **Zoom in** until you can clearly see individual cities
4. Use **Identify** tool (QGIS) or **Explore** tool (Pro) to click on a city
5. Read the attributes that appear

!!! question "Question 2"
    Click on the city of San Luis Obispo. What is its population according to the attribute data?
    
    Population: ____________

---

## Part 4: Exploring Attribute Tables

Attribute tables store the descriptive data associated with spatial features.

=== "QGIS"

    1. Right-click on `california_cities` layer
    2. Select **Open Attribute Table**
    3. A table window opens showing all cities

=== "ArcGIS Pro"

    1. Right-click on `california_cities` layer
    2. Select **Attribute Table**
    3. A table view opens at the bottom

### Understanding the Attribute Table

Each row = one city
<br>Each column = one attribute (field)

!!! question "Question 3"
    Answer these questions using the attribute table:
    
    a) How many cities are in the dataset? ____________
    <br>b) What fields (columns) are in the table? ____________
    <br>c) Which city has the highest population? ____________

### Sorting Data

=== "QGIS"

    1. Click on the **POPULATION** column header
    2. Cities are now sorted by population

=== "ArcGIS Pro"

    1. Right-click the **POPULATION** column header
    2. Select **Sort Descending**

---

## Part 5: Changing Symbology

Currently, all features probably display with default colors. Let's make them more meaningful!

### Styling the Counties

=== "QGIS"

    1. Right-click `california_counties` → **Properties**
    2. Click the **Symbology** tab on the left
    3. At the top, change from "Single Symbol" to **"Categorized"**
    4. Set **Value** to a field like `NAME` or `COUNTY`
    5. Click **Classify** button at the bottom
    6. Click **OK**

=== "ArcGIS Pro"

    1. Select `california_counties` layer
    2. On the **Appearance** tab, click **Symbology**
    3. Change from "Single Symbol" to **"Unique Values"**
    4. Set **Field 1** to `NAME` or `COUNTY`
    5. Colors are automatically assigned

Each county now has a different color!

### Styling the Highways

=== "QGIS"

    1. Right-click `california_highways` → **Properties** → **Symbology**
    2. Click the colored line to open **Symbol Selector**
    3. Change color to red
    4. Change width to 1.5
    5. Click **OK**

=== "ArcGIS Pro"

    1. Select `california_highways`
    2. On **Appearance** tab, change color to red
    3. Change width to 2 pt

### Styling the Cities

Let's make cities different sizes based on population:

=== "QGIS"

    1. Right-click `california_cities` → **Properties** → **Symbology**
    2. Change to **"Graduated"**
    3. Set **Value** to `POPULATION`
    4. Choose a color ramp (e.g., yellow to red)
    5. Click **Classify**
    6. Click **OK**

=== "ArcGIS Pro"

    1. Select `california_cities`
    2. **Symbology** → **Graduated Symbols**
    3. Set **Field** to `POPULATION`
    4. Adjust symbol size range if needed
    5. Choose a color ramp

!!! tip "Pro Tip"
    Larger cities should appear with bigger symbols. This is called **proportional symbol mapping**.

---

## Part 6: Layer Order

Layers draw from bottom to top in the layer list. The top layer draws on top of everything else.

**Current order should be:**
```
☑ california_highways
☑ california_cities
☑ california_counties
```

This is correct because:
- Counties (polygons) should be on the bottom (fill the background)
- Highways (lines) draw on top of counties
- Cities (points) draw on top of everything

### Experiment with Layer Order

1. Drag `california_counties` to the top
2. Notice cities and highways disappear (covered by polygons!)
3. Drag counties back to the bottom

!!! question "Question 4"
    Why is layer order important? Explain in 1-2 sentences.

---

## Part 7: Creating a Map Layout

Now let's create a printable map with title, legend, scale bar, and north arrow.

=== "QGIS"

    1. Click **Project → New Print Layout**
    2. Enter a title: `Lab 1 Map`
    3. A blank layout window opens
    
    **Add Map:**
    4. Click **Add Item → Add Map**
    5. Drag a rectangle on the layout (leave room for title at top)
    6. Your map appears in the rectangle
    
    **Add Title:**
    7. Click **Add Item → Add Label**
    8. Drag a rectangle at the top
    9. In the **Item Properties** panel, change text to:
       <br>`California Counties, Cities, and Highways`
    10. Increase font size to 20-24
    11. Make it bold
    
    **Add Legend:**
    12. Click **Add Item → Add Legend**
    13. Drag a rectangle (usually in bottom right)
    14. Edit legend items in **Item Properties** if needed
    
    **Add Scale Bar:**
    15. Click **Add Item → Add Scale Bar**
    16. Drag below the map
    17. Adjust style in **Item Properties**
    
    **Add North Arrow:**
    18. Click **Add Item → Add North Arrow**
    19. Place in a corner
    20. Choose a simple north arrow style

=== "ArcGIS Pro"

    1. Click **Insert** tab → **New Layout**
    2. Choose a page size (Letter/A4 Landscape)
    3. A blank layout appears
    
    **Add Map:**
    4. **Insert** → **Map Frame** → Select your map
    5. Drag a rectangle on the layout
    
    **Add Title:**
    6. **Insert** → **Text**
    7. Type: `California Counties, Cities, and Highways`
    8. Format the text (make it larger and bold)
    9. Center it at the top
    
    **Add Legend:**
    10. **Insert** → **Legend**
    11. Place in a corner (usually lower right)
    12. Adjust legend items if needed
    
    **Add Scale Bar:**
    13. **Insert** → **Scale Bar**
    14. Choose a style
    15. Place below the map
    
    **Add North Arrow:**
    16. **Insert** → **North Arrow**
    17. Choose a simple style
    18. Place in a corner

---

## Part 8: Exporting Your Map

=== "QGIS"

    1. In the Print Layout, click **Layout → Export as PDF**
    2. Navigate to `GIS_Course/Labs/Lab01/`
    3. Name it: `Lab01_Map_YourName.pdf`
    4. Click **Save**

=== "ArcGIS Pro"

    1. In the Layout, click **Share** tab
    2. Click **Export Layout**
    3. Choose **PDF**
    4. Navigate to `GIS_Course/Labs/Lab01/`
    5. Name it: `Lab01_Map_YourName.pdf`
    6. Click **Export**

---

## Part 9: Saving Your Project

=== "QGIS"

    1. Go back to the main QGIS window
    2. **Project → Save As**
    3. Navigate to `GIS_Course/Labs/Lab01/`
    4. Name: `Lab01_YourName.qgz`
    5. Click **Save**

=== "ArcGIS Pro"

    1. Your project auto-saves to the location you chose at the start
    2. You can also click **Save** button on Quick Access Toolbar

---

## Lab Deliverables

Submit the following to Canvas/LMS:

1. **PDF Map** (`Lab01_Map_YourName.pdf`)
   - Should include: map, title, legend, scale bar, north arrow
   - Cities colored/sized by population
   - Clean and professional appearance

2. **Written Answers** (submit as separate document or text)
   - Answers to Questions 1-4 from this lab

---

## Grading Rubric

| Component | Points | Criteria |
|-----------|--------|----------|
| **Map Quality** | 20 | All required elements present and well-placed |
| **Symbology** | 15 | Counties categorized, cities graduated, highways styled |
| **Cartographic Design** | 10 | Good color choices, readable, balanced layout |
| **Written Answers** | 15 | Correct and complete responses |
| **Total** | **60** | |

---

## Common Issues & Solutions

!!! warning "I can't see my data"
    - Check that the layer is turned on (checkbox in Layers panel)
    - Right-click layer → Zoom to Layer
    - Check the coordinate system matches other layers

!!! warning "My map looks cluttered"
    - Reduce the number of visible layers
    - Adjust symbol sizes
    - Choose better colors
    - Increase map size in layout

!!! warning "Export is taking forever"
    - Simplify your symbology
    - Reduce data complexity
    - Lower export resolution

---

## Going Further (Optional)

Want to explore more? Try these challenges:

1. **Add a basemap** for context (satellite imagery or street map)
2. **Label the cities** with their names
3. **Select only cities above 100,000 population** and symbolize them differently
4. **Calculate a new field** in the attribute table
5. **Create a second layout** with a different map extent (zoom to your region)

---

## Next Steps

Congratulations! You've created your first GIS map! 🎉

In the next lab, you'll learn more about working with vector data and attribute queries.

[:octicons-arrow-right-24: Continue to Topic 2: Spatial Data Models](../topics/02-spatial-data-models.md)

[:octicons-arrow-right-24: Preview Lab 2: Exploring Vector Data](lab02.md)
