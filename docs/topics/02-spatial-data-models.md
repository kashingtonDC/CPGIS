# Topic 2: Spatial Data Models and Formats

## Overview

Now that you understand what GIS is, it's time to learn how spatial information is represented and stored in a GIS. This is fundamental to everything else you'll do with GIS!

---

## Learning Objectives

By the end of this topic, you should be able to:

- Distinguish between vector and raster data models
- Understand when to use discrete vs. continuous representations
- Identify the three vector geometry types: points, lines, and polygons
- Explain what attribute tables are and how they link to spatial features
- Recognize common spatial data formats and their uses

---

## Two Fundamental Data Models

GIS represents the real world using two primary data models:

<div class="grid cards" markdown>

-   **🔷 Vector Data**

    ---
    
    Discrete features with defined boundaries
    
    - Exact locations and shapes
    - Good for distinct objects
    - Examples: buildings, roads, boundaries
    
-   **🟦 Raster Data**

    ---
    
    Continuous surfaces as a grid of cells
    
    - Each cell has a value
    - Good for phenomena that vary continuously
    - Examples: elevation, temperature, rainfall

</div>

Think of it this way:
- **Vector** = Drawing with pens (crisp lines and points)
- **Raster** = Painting with pixels (grid of colors)

---

## Vector Data Model

Vector data represents geographic features using **geometric primitives**: points, lines, and polygons.

### The Three Geometry Types

#### 1. Points 📍
Represent discrete locations with X, Y (and sometimes Z) coordinates.

**Use Cases:**
- Cities and towns
- Sampling locations
- GPS waypoints
- Trees in an inventory
- Fire hydrants
- Weather stations

!!! example "Real World Point Data"
    A dataset of coffee shops where each point has:
    
    - **Geometry**: Latitude/Longitude coordinates
    - **Attributes**: Shop name, hours, rating, price level

---

#### 2. Lines (Polylines) 📏
Sequences of connected points forming paths or linear features.

**Use Cases:**
- Roads and highways
- Rivers and streams
- Power lines
- Trails
- Flight paths
- Political boundaries (when shown as lines)

!!! example "Real World Line Data"
    A roads dataset where each line has:
    
    - **Geometry**: Series of coordinate pairs forming the road centerline
    - **Attributes**: Road name, speed limit, number of lanes, surface type

---

#### 3. Polygons 📐
Closed shapes representing areas, defined by connected lines.

**Use Cases:**
- Parcel boundaries
- Lakes and water bodies
- Forest stands
- Zip codes
- Land use zones
- Building footprints
- Political boundaries (when shown as areas)

!!! example "Real World Polygon Data"
    A land parcels dataset where each polygon has:
    
    - **Geometry**: Coordinates defining the property boundary
    - **Attributes**: Parcel ID, owner, area, zoning, assessed value

---

### Topology: Spatial Relationships

Vector data can encode **topology** - the spatial relationships between features:

**Key Topological Concepts:**

- **Connectivity**: Which features are connected?
  <br>*Example: Which roads intersect at this junction?*

- **Adjacency**: Which features are next to each other?
  <br>*Example: Which parcels share a boundary?*

- **Containment**: Which features are inside others?
  <br>*Example: Which points fall within this polygon?*

!!! warning "Topology Errors"
    Common topology problems to avoid:
    
    - **Gaps**: Unwanted space between polygons
    - **Overlaps**: Polygons covering the same area
    - **Slivers**: Thin polygons from imperfect digitizing
    - **Dangles**: Lines that don't connect properly

---

## Raster Data Model

Raster data divides space into a regular **grid of cells (pixels)**, where each cell contains a value.

### Key Raster Concepts

**Cell Size (Spatial Resolution)**
<br>The ground area covered by one pixel
<br>*Examples: 30m (Landsat), 10m (Sentinel), 1m (lidar)*

**Extent**
<br>The geographic area covered by the entire grid

**Value/DN (Digital Number)**
<br>The data stored in each cell
<br>*Could represent elevation, temperature, reflectance, land cover class, etc.*

### Raster Data Types

| Type | Description | Example |
|------|-------------|---------|
| **Integer** | Whole numbers only | Land cover classes (1=forest, 2=water, etc.) |
| **Float** | Decimal numbers | Elevation (1456.23 meters) |
| **Binary** | 0 or 1 only | Burned area (0=unburned, 1=burned) |

### Continuous vs. Discrete Rasters

**Continuous Rasters** 🌊
<br>Values change gradually across space

- Elevation
- Temperature
- Rainfall
- Slope
- Soil pH

**Discrete (Categorical) Rasters** 📊
<br>Values represent distinct classes

- Land cover types
- Soil types
- Zones
- Boolean (yes/no) masks

---

## Vector vs. Raster: When to Use Each?

<table>
<tr>
<th>Aspect</th>
<th>Vector</th>
<th>Raster</th>
</tr>
<tr>
<td><strong>Best For</strong></td>
<td>Discrete features with clear boundaries</td>
<td>Continuous phenomena and surfaces</td>
</tr>
<tr>
<td><strong>Precision</strong></td>
<td>Exact locations and shapes</td>
<td>Limited by cell size</td>
</tr>
<tr>
<td><strong>File Size</strong></td>
<td>Generally smaller (for simple features)</td>
<td>Can be very large (high resolution)</td>
</tr>
<tr>
<td><strong>Analysis</strong></td>
<td>Better for topology and networks</td>
<td>Better for surface analysis and modeling</td>
</tr>
<tr>
<td><strong>Examples</strong></td>
<td>Roads, parcels, administrative boundaries</td>
<td>Elevation, satellite imagery, climate surfaces</td>
</tr>
<tr>
<td><strong>Editing</strong></td>
<td>Individual features easily edited</td>
<td>Must edit cell by cell</td>
</tr>
</table>

!!! tip "You Can Convert Between Models"
    - **Vector → Raster**: "Rasterizing" - assigns cell values based on vector attributes
    - **Raster → Vector**: "Vectorizing" - creates features from cell patterns
    
    Each conversion involves trade-offs!

---

## Attribute Tables

Both vector and raster data can have associated **attribute data** - information about each feature beyond just location.

### Vector Attribute Tables

Each row = one feature (point, line, or polygon)
<br>Each column = one attribute

**Example: City Points Attribute Table**

| OBJECTID | CITY_NAME | STATE | POPULATION | MEDIAN_INCOME |
|----------|-----------|-------|------------|---------------|
| 1 | San Luis Obispo | CA | 47,063 | $71,317 |
| 2 | Santa Barbara | CA | 91,364 | $76,917 |
| 3 | Monterey | CA | 28,575 | $68,456 |

### Common Field (Column) Types

| Data Type | Description | Example Values |
|-----------|-------------|----------------|
| **Text/String** | Letters and characters | "Oak Street", "Residential" |
| **Integer** | Whole numbers | 42, -17, 1000 |
| **Float/Double** | Decimal numbers | 3.14159, -122.4567 |
| **Date** | Date/time values | 2025-03-15, 14:30:00 |
| **Boolean** | True/False | True, False, 1, 0 |

### Raster Attribute Tables (RATs)

For **categorical rasters**, each unique value can have attributes:

| VALUE | LAND_COVER | DESCRIPTION | COLOR |
|-------|------------|-------------|-------|
| 1 | Forest | Evergreen forest | Dark green |
| 2 | Grassland | Open grassland | Light green |
| 3 | Urban | Developed areas | Gray |
| 4 | Water | Water bodies | Blue |

---

## Common Spatial Data Formats

### Vector Formats

| Format | Extension | Description | When to Use |
|--------|-----------|-------------|-------------|
| **Shapefile** | .shp (+ .shx, .dbf, .prj) | ESRI's legacy format | Widely compatible, but limited |
| **GeoJSON** | .geojson | JSON-based, human-readable | Web mapping, lightweight |
| **GeoPackage** | .gpkg | Modern SQLite-based format | Replace shapefiles! Single file. |
| **KML/KMZ** | .kml, .kmz | Google Earth format | Sharing on Google Earth/Maps |
| **File Geodatabase** | .gdb | ESRI's modern format | Complex datasets, topologies |

!!! danger "Shapefile Limitations"
    Shapefiles are old (1990s) and have major limitations:
    
    - Field names limited to 10 characters
    - No fields > 255 characters
    - No date+time (just date)
    - Multiple files (.shp, .shx, .dbf, .prj, etc.)
    - File size limit: 2GB
    
    **Use GeoPackage (.gpkg) instead!**

### Raster Formats

| Format | Extension | Description | When to Use |
|--------|-----------|-------------|-------------|
| **GeoTIFF** | .tif, .tiff | TIFF with georeferencing | Industry standard, preserves all info |
| **ERDAS Imagine** | .img | Common remote sensing format | Satellite/aerial imagery |
| **NetCDF** | .nc | Multi-dimensional arrays | Climate data, ocean data |
| **HDF** | .hdf | Hierarchical Data Format | NASA satellite products |
| **JPEG2000** | .jp2 | Compressed imagery | When file size matters |

!!! warning "Avoid Regular JPEG and PNG"
    Standard .jpg and .png images lose georeferencing! Always use GeoTIFF for spatial rasters.

---

## Data Storage Concepts

### Single File vs. Multiple Files

**Single File Formats** ✅
- GeoPackage (.gpkg)
- GeoTIFF (.tif)
- GeoJSON (.geojson)
- File Geodatabase (.gdb folder)

**Multiple File Formats** ⚠️
- Shapefile (requires .shp, .shx, .dbf, .prj minimum)
- ERDAS Imagine (.img + .ige auxiliary)

!!! tip "Best Practice"
    Always use formats that keep everything together! It's much easier to share, back up, and manage.

### Compression

Raster data can be **compressed** to reduce file size:

- **Lossless**: Perfect quality preserved (LZW, Deflate)
- **Lossy**: Some quality lost (JPEG, JPEG2000)

For analysis, always use lossless compression!

---

## Metadata: Data About Data

**Metadata** describes your spatial data:

- **What**: Content description
- **When**: Creation/modification dates
- **Who**: Author/organization
- **Where**: Geographic extent
- **Why**: Purpose and use
- **How**: Collection methods, accuracy

Good metadata is essential for:
- Understanding data limitations
- Proper use of data
- Reproducibility
- Sharing with others

---

## Discrete vs. Continuous Phenomena

Understanding whether your data represents **discrete** or **continuous** phenomena helps you choose the right model:

### Discrete Phenomena
**Definition**: Features with defined boundaries and distinct identities

**Examples:**
- Buildings
- Roads
- Political boundaries
- Soil types (categorical)

**Best Model**: Usually **vector**

### Continuous Phenomena
**Definition**: Features that vary smoothly across space without clear boundaries

**Examples:**
- Elevation
- Temperature
- Air pollution
- Rainfall

**Best Model**: Usually **raster**

### The Gray Area
Some phenomena can be represented either way:

- **Population density**: Raster surface OR census polygons with density values
- **Vegetation**: Categorical raster OR vegetation polygon types
- **Temperature**: Point measurements (vector) OR interpolated surface (raster)

!!! tip "Choice Depends On..."
    - Your analysis goals
    - Available data
    - Required precision
    - Computational resources

---

## Layers: Organizing Spatial Data

In GIS software, different datasets are managed as **layers** that can be turned on/off and reordered:

```
Map Document
├── Roads (vector lines)
├── Buildings (vector polygons)
├── Tree points (vector points)
├── Elevation (raster)
└── Satellite imagery (raster)
```

**Layer Order Matters!**
<br>Top layers draw over bottom layers (like sheets of paper)

---

## Visual Example: Vector vs. Raster

![Vector vs Raster Comparison](../images/vector-vs-raster.png)
*Left: Vector representation with crisp boundaries. Right: Raster representation as a grid.*

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Two data models**: Vector (discrete features) and Raster (grid cells)
2. **Three vector types**: Points, lines, polygons - each suited for different features
3. **Attribute tables link** descriptive data to spatial features
4. **Choose the right format**: GeoPackage for vector, GeoTIFF for raster
5. **Avoid shapefiles**: Use modern formats like GeoPackage
6. **Discrete vs. continuous**: Helps you pick the right data model

</div>

---

## Further Reading

- [QGIS Documentation: Vector Data](https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html)
- [QGIS Documentation: Raster Data](https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/raster_data.html)
- ESRI: [Vector vs Raster Data](https://www.esri.com/arcgis-blog/products/product/imagery/raster-data-vs-vector-data-in-gis/)

---

## Lab Exercise

!!! lab "Lab 2: Exploring Vector Data and Attribute Tables"
    In [Lab 2](../labs/lab02.md), you'll:
    
    - Load different types of vector data (points, lines, polygons)
    - Explore attribute tables
    - Perform basic feature selection and queries
    - Add and edit attribute fields
    - Experiment with symbology based on attributes
    
    **Time Required**: 2-3 hours
    
    [:octicons-arrow-right-24: Go to Lab 2](../labs/lab02.md)

---

## Next Topic

Now that you understand spatial data models, let's explore how we reference locations on Earth:

[:octicons-arrow-right-24: Topic 3: Coordinate Systems & Projections](03-coordinate-systems.md)
