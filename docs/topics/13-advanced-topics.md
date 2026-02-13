# Topic 13: Advanced GIS Topics

## Overview

This topic introduces advanced GIS capabilities including 3D analysis, network analysis, geocoding, and integration with other tools like Microsoft Excel.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand 3D GIS and terrain visualization
- Perform basic network analysis
- Geocode addresses to create point data
- Integrate GIS with Excel and other tools
- Recognize advanced analysis capabilities
- Know when to apply specialized GIS tools

---

## 3D GIS and Visualization

### 3D Data Types

**3D Features**:
- Points with Z values (elevation)
- 3D lines (flight paths, utility lines)
- 3D polygons (building footprints with heights)
- 3D models (CityGML, textured meshes)

**Surface Models**:
- Digital Elevation Models (DEMs)
- Digital Surface Models (DSMs)
- TIN (Triangulated Irregular Networks)

---

### 3D Visualization

**Techniques**:

**Hillshade**: Simulate sun illumination
**Contours**: Show elevation lines
**Perspective views**: Oblique angles
**Draping**: Overlay imagery on terrain
**Extrusion**: Give height to 2D features

**Applications**:
- Urban planning (building heights)
- Viewshed analysis
- Line of sight
- Flood modeling
- Solar analysis

---

## Network Analysis

### What is Network Analysis?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Network analysis** solves problems on connected linear features (roads, rivers, utilities) like finding shortest paths or service areas.

</div>

### Common Network Problems

**Routing** 🚗:
- Find shortest/fastest path from A to B
- Delivery routes
- Emergency response paths

**Service Areas** 🚑:
- What area can be reached in X minutes?
- Hospital service coverage
- School catchment zones

**Closest Facility** 🏥:
- Which hospital is nearest?
- Assign customers to closest store

**Origin-Destination Matrix** 📊:
- Travel time between all pairs
- Commute analysis

---

### Network Requirements

**Network dataset needs**:
- Connected lines (no gaps!)
- Direction rules (one-way streets)
- Turn restrictions
- Speed limits or costs
- Barriers (road closures)

**Tools**:
- QGIS: Network Analysis toolbox, QNEAT3 plugin
- ArcGIS Pro: Network Analyst extension
- pgRouting (PostgreSQL/PostGIS)

---

## Geocoding

### What is Geocoding?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Geocoding** converts addresses into geographic coordinates (latitude/longitude), allowing them to be mapped.

</div>

### Geocoding Process

**Input**: Address text
```
"1 Grand Avenue, San Luis Obispo, CA 93407"
```

**Output**: Coordinates
```
35.2828° N, -120.6596° W
```

**How it works**:
1. Parse address into components
2. Match to reference data (street database)
3. Interpolate position along street segment
4. Return coordinates

---

### Geocoding Services

**Free**:
- Google Maps Geocoding API (limited free tier)
- Nominatim (OpenStreetMap)
- QGIS built-in geocoder

**Commercial**:
- ESRI World Geocoding Service
- HERE Geocoding
- Mapbox Geocoding

**Batch geocoding**: Process many addresses at once

---

## GIS and Microsoft Excel Integration

### Exporting GIS Data to Excel

**Use cases**:
- Create charts and graphs
- Statistical analysis
- Share with non-GIS users
- Pivot tables

**Workflow**:

=== "QGIS"

    1. Right-click layer → Export → Save Features As
    2. Format: CSV or XLSX
    3. Select fields to include
    4. Open in Excel

=== "ArcGIS Pro"

    1. Export Table tool
    2. Or: Right-click → Data → Export Table
    3. Format: .xlsx or .dbf
    4. Open in Excel

**What exports**:
- Attribute table data
- Calculated fields
- Statistics
- *Not* geometry (except as coordinates)

---

### Importing Excel to GIS

**Requirements**:
- Coordinate columns (Latitude/Longitude or X/Y)
- Clean, consistent data
- Header row

**Workflow**:

=== "QGIS"

    1. Layer → Add Layer → Add Delimited Text Layer
    2. Browse to CSV/Excel
    3. Select X field (Longitude)
    4. Select Y field (Latitude)
    5. Set CRS (usually WGS84)
    6. Add

=== "ArcGIS Pro"

    1. XY Table to Point
    2. Select coordinate fields
    3. Specify coordinate system
    4. Create points

---

### Excel for GIS Charts

**After exporting attribute data**:

**Create visualizations**:
- Bar charts (area by land cover class)
- Line graphs (population over time)
- Pie charts (percentage breakdown)
- Scatter plots (correlation analysis)

**Pivot tables**:
- Summarize by categories
- Cross-tabulate data
- Dynamic filtering

**Share results**:
- Embed charts in reports
- Present statistics
- Dashboard creation

---

## Python for GIS Automation

### Why Python?

**Automation**:
- Process 100s of files
- Repeat analyses
- Batch operations

**Customization**:
- Build custom tools
- Extend GIS functionality
- Create workflows

**Integration**:
- Connect to databases
- Web services
- Other software

---

### Python GIS Libraries

**PyQGIS**: QGIS Python API
**ArcPy**: ArcGIS Python library
**GeoPandas**: Like Pandas but for spatial data
**Shapely**: Geometric operations
**Rasterio**: Raster processing
**Folium**: Interactive web maps

**Example** (GeoPandas):
```python
import geopandas as gpd

# Read shapefile
gdf = gpd.read_file('counties.shp')

# Calculate area in sq km
gdf['area_km2'] = gdf.geometry.area / 1e6

# Filter
large_counties = gdf[gdf['area_km2'] > 1000]

# Save
large_counties.to_file('large_counties.gpkg')
```

---

## Model Builder / Graphical Modeler

### Visual Programming

**Benefits**:
- No coding required
- Document workflows visually
- Reusable models
- Share with team

**Components**:
- Input data (blue)
- Tools/processes (yellow)
- Outputs (green)
- Connections (arrows)

**Typical uses**:
- Multi-step analyses
- Batch processing
- Standardized workflows

---

## Advanced Analysis Techniques

### Terrain Analysis

**Viewshed**: What's visible from a point?
**Watershed**: Drainage basin delineation
**Solar radiation**: Sun exposure modeling
**Cut/Fill**: Earthwork calculations

---

### Spatial Statistics

**Hot spot analysis**: Statistically significant clusters
**Spatial autocorrelation**: Moran's I, Geary's C
**Point pattern analysis**: Cluster vs random vs dispersed
**Regression**: Geographic Weighted Regression (GWR)

---

### Time Series Analysis

**Temporal GIS**:
- Tracking changes over time
- Animation of spatial phenomena
- Time-enabled layers
- Space-time cubes

**Applications**:
- Disease spread
- Urban growth
- Wildlife migration
- Climate change

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **3D GIS adds vertical dimension** - Terrain, buildings, viewsheds
2. **Network analysis solves routing** - Shortest paths, service areas
3. **Geocoding creates points from addresses** - Enables mapping locations
4. **Excel integrates with GIS** - Export attributes for charts
5. **Python automates workflows** - Batch processing, custom tools
6. **Model Builder documents visually** - Reusable workflows
7. **Advanced analysis exists** - Spatial statistics, time series

</div>

---

## Further Reading

- [QGIS 3D Views](https://docs.qgis.org/latest/en/docs/user_manual/map_views/3d_map_view.html)
- [Network Analysis in QGIS](https://docs.qgis.org/latest/en/docs/user_manual/processing_algs/qgis/networkanalysis.html)
- [GeoPandas Documentation](https://geopandas.org/)
- [ArcGIS Pro Network Analyst](https://pro.arcgis.com/en/pro-app/latest/help/analysis/networks/what-is-network-analyst-.htm)

---

## Lab Exercise

!!! lab "Lab 13: Advanced Techniques"
    In [Lab 13](../labs/lab13.md), you'll:
    
    - Create 3D visualizations of terrain
    - Perform simple routing analysis
    - Geocode addresses to points
    - Export data to Excel and create charts
    - Build a processing model
    - Explore advanced analysis options
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 13](../labs/lab13.md)

---

## Next Topic

You've explored advanced tools! Now learn about modern web mapping:

[:octicons-arrow-right-24: Topic 14: Modern Mapmaking](14-modern-mapmaking.md)
