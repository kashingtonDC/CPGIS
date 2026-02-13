# Topic 8: Raster Data and DEMs

## Overview

Raster data represents the world as a grid of cells (pixels), each containing a value. From satellite imagery to elevation models, rasters are fundamental for environmental analysis, remote sensing, and surface modeling.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand raster data structure and characteristics
- Distinguish between continuous and discrete rasters
- Work with multispectral satellite imagery
- Understand spatial resolution and its implications
- Create and analyze Digital Elevation Models (DEMs)
- Extract terrain derivatives (slope, aspect, hillshade)
- Generate contour lines from elevation data
- Choose appropriate raster data for analysis

---

## What is Raster Data?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Raster data** represents spatial information as a grid of cells (pixels), where each cell stores a numeric value representing a measurement or category.

</div>

### Simple Rule of Thumb

**If it's pixelated → It's a raster!**

- Photographs → Raster
- Satellite images → Raster  
- Digital elevation models → Raster
- Temperature surfaces → Raster
- Land cover maps → Raster

!!! note "Etymology"
    "Raster" comes from Latin meaning "screen" - think of your computer screen as a grid of pixels!

---

## Raster Data Structure

### Grid Components

Every raster has:

1. **Cells/Pixels**: Individual grid squares
2. **Rows & Columns**: Organization of cells
3. **Extent**: Geographic boundaries (xmin, xmax, ymin, ymax)
4. **Cell Size**: Spatial resolution (e.g., 30m × 30m)
5. **Cell Values**: Data stored in each pixel
6. **No Data Value**: Represents missing data (often -9999)

![Raster Structure](../images/raster-structure.png)
*Basic raster structure showing grid of cells with values*

---

### Spatial Resolution

**Spatial resolution** = the "real-world" size of each pixel

| Resolution | Pixel Size | Common Use |
|------------|-----------|------------|
| **Very High** | < 1 meter | Drone imagery, detailed mapping |
| **High** | 1-10 meters | Landsat, urban planning |
| **Medium** | 10-100 meters | Regional analysis, land cover |
| **Low** | 100m - 1km | Climate data, global studies |
| **Very Low** | > 1km | Weather models, ocean data |

!!! tip "Resolution Trade-off"
    **Higher resolution** = More detail but larger file sizes and slower processing
    
    **Lower resolution** = Faster processing but less detail

### Example Resolutions

- **WorldView-3**: 0.3m (can see cars!)
- **Landsat 8**: 30m (can see fields)
- **MODIS**: 250m-1km (regional/global)
- **Climate models**: 10-50km (atmospheric processes)

---

## Types of Raster Data

### 1. Continuous Rasters

**Definition**: Values change gradually across space with no distinct boundaries.

**Characteristics**:
- Measured values on a scale
- Smooth transitions between cells
- Infinite possible values

**Examples**:
- **Elevation** (40.5m, 40.7m, 41.2m...)
- **Temperature** (15.3°C, 15.5°C, 15.8°C...)
- **Rainfall** (2.3mm, 2.5mm, 2.7mm...)
- **Slope** (5.2°, 5.4°, 5.6°...)

![Continuous Raster Example](../images/continuous-raster.png)
*Elevation DEM showing continuous values*

---

### 2. Discrete (Categorical) Rasters

**Definition**: Values represent distinct categories or classes.

**Characteristics**:
- Integer values as codes
- Clear boundaries between classes
- Finite set of values

**Examples**:
- **Land cover** (1=Forest, 2=Urban, 3=Water)
- **Soil types** (1=Sandy, 2=Clay, 3=Loam)
- **Zones** (1=Zone A, 2=Zone B, 3=Zone C)

| Value | Category |
|-------|----------|
| 1 | Water |
| 2 | Forest |
| 3 | Grassland |
| 4 | Urban |
| 5 | Barren |

![Discrete Raster Example](../images/discrete-raster.png)
*Land cover map showing discrete categories*

---

## Digital Elevation Models (DEMs)

### What is a DEM?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **Digital Elevation Model (DEM)** is a raster dataset where each cell value represents elevation (height above sea level) at that location.

</div>

**Key Characteristics**:
- Continuous surface
- Values in meters or feet
- Foundation for terrain analysis
- Used for hydrologic modeling, viewshed analysis, slope stability

### Common DEM Sources

| Source | Resolution | Coverage | URL |
|--------|-----------|----------|-----|
| **SRTM** | 30m | Global (60°N-56°S) | [earthexplorer.usgs.gov](https://earthexplorer.usgs.gov) |
| **ASTER** | 30m | Global | [asterweb.jpl.nasa.gov](https://asterweb.jpl.nasa.gov) |
| **NED** | 10m, 30m | USA | [USGS 3DEP](https://www.usgs.gov/3d-elevation-program) |
| **ALOS** | 12.5m | Global | [asf.alaska.edu](https://asf.alaska.edu) |
| **Copernicus** | 30m, 90m | Global | [copernicus.eu](https://dataspace.copernicus.eu) |
| **LiDAR** | < 1m | Limited areas | Various state/local sources |

!!! tip "Quick DEM Downloads"
    For SRTM 30m DEMs worldwide, use: [dwtkns.com/srtm30m](https://dwtkns.com/srtm30m)

---

## Terrain Analysis

DEMs enable powerful terrain analysis! You can derive many useful products from elevation data.

### 1. Slope

**What it shows**: Steepness of terrain (how much it rises/falls)

**Units**: Degrees (0-90°) or Percent (0-100%+)

**Formula**: 
```
Slope = arctan(rise / run)
```

**Applications**:
- **Erosion risk**: Steep slopes erode more
- **Agriculture**: Flat land preferred for crops
- **Construction**: Building on steep slopes is expensive
- **Recreation**: Ski run difficulty

**Interpretation**:
- **0-5°**: Flat (easy to build, walk, farm)
- **5-15°**: Gentle slope
- **15-30°**: Moderate slope (hillside)
- **30-45°**: Steep (difficult terrain)
- **>45°**: Very steep (cliffs, unstable)

![Slope Map](../images/slope-map.png)
*Slope derived from DEM showing terrain steepness*

---

### 2. Aspect

**What it shows**: Direction the slope faces (compass direction)

**Units**: Degrees (0-360°)
- 0° = North
- 90° = East
- 180° = South
- 270° = West

**Applications**:
- **Solar exposure**: South-facing slopes get more sun (Northern Hemisphere)
- **Snow accumulation**: North-facing slopes hold snow longer
- **Vegetation**: Affects microclimate and plant species
- **Fire behavior**: Influences fire spread direction

**Example Use**:
Find south-facing slopes for:
- Solar panel placement
- Vineyards (more sun)
- Ski resorts (north-facing = more snow)

---

### 3. Hillshade

**What it shows**: 3D visualization of terrain with simulated shadows

**Purpose**: Makes elevation patterns visually obvious

**Parameters**:
- **Azimuth**: Sun direction (0-360°)
- **Altitude**: Sun angle above horizon (0-90°)

**Best for**:
- Base maps
- Visual terrain interpretation
- Beautiful map backgrounds!

![Hillshade Example](../images/hillshade.png)
*Hillshade showing terrain relief*

---

### 4. Contour Lines

**What they are**: Lines connecting points of equal elevation

**Characteristics**:
- **Contour interval**: Vertical distance between lines (e.g., 20m)
- **Index contours**: Thicker lines (usually every 5th contour)
- **Spacing indicates slope**: 
  - Close together = Steep
  - Far apart = Gentle

**Applications**:
- Topographic maps
- Hiking maps
- Engineering design
- Visualizing terrain

**Reading Contours**:
- Lines never cross (except overhangs/caves)
- V-shapes point upstream in valleys
- Circles indicate peaks or depressions

---

### Creating Terrain Derivatives

=== "QGIS"

    **Slope**:
    - Raster → Analysis → Slope
    - Input: DEM
    - Output units: Degrees or Percent
    
    **Aspect**:
    - Raster → Analysis → Aspect
    - Output: 0-360° compass direction
    
    **Hillshade**:
    - Raster → Analysis → Hillshade
    - Set azimuth (sun direction): Usually 315°
    - Set altitude (sun angle): Usually 45°
    
    **Contours**:
    - Raster → Extraction → Contour
    - Set interval (e.g., 20m, 100ft)
    - Creates vector polylines

=== "ArcGIS Pro"

    **All terrain tools**:
    - Spatial Analyst → Surface
    
    Options:
    - Slope
    - Aspect
    - Hillshade
    - Contour

---

## Multispectral Imagery

### What is Multispectral Data?

Satellite sensors capture images in multiple **spectral bands** (wavelengths of light).

**Think of it as**: Multiple rasters stacked together, each representing different wavelengths.

### Common Bands

| Band Name | Wavelength (μm) | Color | Use |
|-----------|----------------|-------|-----|
| **Blue** | 0.45-0.52 | Blue | Water, clouds, aerosols |
| **Green** | 0.52-0.60 | Green | Vegetation vigor, algae |
| **Red** | 0.63-0.69 | Red | Chlorophyll absorption, soil |
| **NIR** | 0.77-0.90 | Near-Infrared | Vegetation biomass, water bodies |
| **SWIR** | 1.55-1.75 | Shortwave IR | Moisture content, geology |

### True Color vs False Color

**True Color** (Natural to our eyes):
- Red band → Display as Red
- Green band → Display as Green
- Blue band → Display as Blue
- Result: Looks like a photograph

**False Color** (Highlight vegetation):
- NIR band → Display as Red
- Red band → Display as Green
- Green band → Display as Blue
- Result: Vegetation appears bright red!

!!! tip "Why False Color?"
    Healthy vegetation reflects strongly in NIR (which we can't see). By displaying NIR as red, vegetation "pops" visually - making it easy to identify forests, crops, and plant health!

---

## Raster File Formats

| Format | Extension | Description | Use Case |
|--------|-----------|-------------|----------|
| **GeoTIFF** | .tif, .tiff | Industry standard | Most common, best choice |
| **IMG** | .img | ERDAS format | Legacy, still common |
| **JP2** | .jp2 | JPEG 2000 | Compressed satellite data |
| **NetCDF** | .nc | Multidimensional | Climate/ocean models |
| **HDF** | .hdf, .h5 | Hierarchical | NASA products |
| **ASCII Grid** | .asc | Text format | Simple, human-readable |

!!! success "Recommended Format"
    **Use GeoTIFF (.tif)** for most work:
    - Widely supported
    - Preserves georeferencing
    - Can compress without data loss
    - Works in all GIS software

---

## Raster Metadata

Essential information about a raster:

**Spatial Properties**:
- Coordinate system (CRS/projection)
- Extent (bounding box)
- Cell size (resolution)
- Number of rows and columns

**Data Properties**:
- Number of bands
- Data type (Int16, Float32, etc.)
- No data value
- Min/max values
- Units of measurement

**Source Information**:
- Sensor/source
- Acquisition date
- Processing level
- Cloud cover (for imagery)

---

## Working with Rasters: Best Practices

### 1. Check Resolution

Always verify pixel size matches your analysis needs:
- Too coarse → Miss important details
- Too fine → Unnecessarily large files, slow processing

---

### 2. Verify Coordinate System

**Critical**: Ensure CRS is correct before analysis!

```
Right-click layer → Properties → Information
```

Look for:
- Coordinate system name
- EPSG code
- Units (meters, degrees, feet)

---

### 3. Understand No Data

Rasters use special values for "no data" (missing information):
- Common: -9999, -3.4e38, 255
- Can cause errors in calculations if not handled
- Most GIS software respects no data automatically

**Check**: Layer Properties → Information → No Data Value

---

### 4. Mind File Sizes

Rasters can be HUGE!

**Example**: 10,000 × 10,000 pixels = 100 million cells
- As 32-bit float: ~400 MB per band
- Multi-band imagery: GBs per scene

**Tips**:
- Clip to study area
- Resample if appropriate
- Compress (LZW compression in GeoTIFF)
- Use pyramids for faster display

---

## Raster vs Vector: When to Use Which?

| Scenario | Best Choice | Why |
|----------|-------------|-----|
| **Elevation analysis** | Raster (DEM) | Continuous surface |
| **Temperature mapping** | Raster | Smooth transitions |
| **Satellite imagery** | Raster | Already pixelated |
| **Land parcels** | Vector | Discrete boundaries |
| **Roads** | Vector | Linear features |
| **Political boundaries** | Vector | Precise lines |
| **Continuous phenomena** | Raster | Temperature, elevation |
| **Discrete objects** | Vector | Buildings, parcels |

---

## Common Applications

### Environmental Analysis
- **Habitat modeling**: Elevation, slope, aspect requirements
- **Watershed delineation**: Flow direction and accumulation from DEM
- **Erosion risk**: Slope + soil + rainfall
- **Solar potential**: Slope + aspect + hillshade

### Agriculture
- **Crop health monitoring**: NDVI from satellite imagery
- **Irrigation planning**: Elevation + slope
- **Yield prediction**: Multispectral analysis
- **Field variability**: Identify management zones

### Disaster Management
- **Flood modeling**: Elevation + precipitation
- **Landslide risk**: Slope + geology + rainfall
- **Fire behavior**: Aspect + slope + fuel loads
- **Earthquake vulnerability**: Slope stability

### Urban Planning
- **Viewshed analysis**: What's visible from location?
- **Solar panel placement**: South-facing roofs
- **Development suitability**: Slope + land use
- **Line of sight**: Communications towers

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Rasters are grids** - Each pixel stores a value
2. **Spatial resolution matters** - Pixel size affects detail and file size
3. **Continuous vs discrete** - Elevation/temperature vs land cover/classes
4. **DEMs enable terrain analysis** - Slope, aspect, hillshade, contours
5. **Multispectral = multiple bands** - Different wavelengths reveal different info
6. **False color highlights vegetation** - NIR displayed as red
7. **Check CRS and resolution** - Before any analysis!
8. **GeoTIFF is standard** - Use .tif format for most work

</div>

---

## Further Reading

- [QGIS Raster Guide](https://docs.qgis.org/3.28/en/docs/user_manual/working_with_raster/)
- [USGS 3DEP DEMs](https://www.usgs.gov/3d-elevation-program)
- [Landsat Missions](https://landsat.gsfc.nasa.gov/)
- [Copernicus Data Space](https://dataspace.copernicus.eu/)

---

## Lab Exercise

!!! lab "Lab 8: Raster Data & Terrain Analysis"
    In [Lab 8](../labs/lab08.md), you'll:
    
    - Download and load DEM data
    - Calculate slope, aspect, and hillshade
    - Generate contour lines
    - Work with multispectral satellite imagery
    - Create true color and false color composites
    - Extract terrain information for analysis
    - Compare continuous and discrete rasters
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 8](../labs/lab08.md)

---

## Next Topic

Now that you understand raster data, let's learn how to analyze it:

[:octicons-arrow-right-24: Topic 9: Raster Analysis](09-raster-analysis.md)
