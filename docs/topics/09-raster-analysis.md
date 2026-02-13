# Topic 9: Raster Analysis and Map Algebra

## Overview

Raster analysis uses mathematical operations on grid cells to extract information, classify data, and model spatial phenomena. Map algebra provides a powerful framework for combining rasters to answer complex spatial questions.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand and apply map algebra operations
- Use the raster calculator for complex analyses
- Perform raster reclassification
- Extract raster values at point, line, and polygon locations
- Calculate zonal statistics
- Convert between raster and vector formats
- Build multi-step raster analysis workflows

---

## Map Algebra Fundamentals

### What is Map Algebra?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Map algebra** is a language for performing mathematical operations on rasters. It treats raster layers as variables in equations, performing calculations cell-by-cell.

</div>

### Core Concept

Each cell in output = Function of corresponding cells in inputs

**Simple example**:
```
Output_Raster = Raster_A + Raster_B
```

For each cell location (row, column):
```
Output[i,j] = Raster_A[i,j] + Raster_B[i,j]
```

---

## Types of Map Algebra Operations

### 1. Local Operations

**Definition**: Operations performed on single cell or corresponding cells across multiple rasters.

**Characteristics**:
- Cell-by-cell calculation
- No influence from neighboring cells
- Output cell depends only on input cell(s) at same location

**Examples**:

**Addition**:
```
Raster_C = Raster_A + Raster_B
```

**Subtraction** (Change detection):
```
Change = NDVI_2025 - NDVI_2024
```

**Multiplication**:
```
Habitat_Score = Vegetation * Proximity_Water
```

**Boolean logic**:
```
Suitable = (Elevation < 1000) AND (Slope < 15)
```

---

### 2. Focal (Neighborhood) Operations

**Definition**: Output cell value calculated from neighborhood of cells around it.

**Common Types**:

**Moving Window Statistics**:
- Mean filter (smoothing)
- Maximum filter
- Minimum filter
- Standard deviation

**Kernel Operations**:
- Gaussian blur
- Edge detection
- Sharpening

**Applications**:
- **Noise reduction**: Smooth raster data
- **Terrain**: Calculate slope, aspect (uses 3×3 neighborhood)
- **Texture analysis**: Identify patterns

---

### 3. Zonal Operations

**Definition**: Calculate statistics for groups of cells (zones) defined by another raster or vector layer.

**Examples**:
- Mean elevation per county
- Total precipitation per watershed
- Maximum NDVI per land cover class

**See detailed section on Zonal Statistics below!**

---

### 4. Global Operations

**Definition**: Output considers all cells in entire raster.

**Examples**:
- Euclidean distance (distance to nearest feature)
- Cost distance (least-cost path)
- Watershed delineation
- Viewshed analysis

---

## Raster Calculator

The **Raster Calculator** is the main tool for map algebra in GIS software.

### Basic Syntax

**Arithmetic**:
```
"DEM" + 100          # Add constant
"Raster_A" - "Raster_B"   # Subtract rasters
"Temp_C" * 1.8 + 32  # Celsius to Fahrenheit
"Population" / "Area"     # Density
```

**Comparison Operators**:
```
"Elevation" > 1000   # Boolean: 1 where true, 0 where false
"Slope" <= 15        # Gentle slopes
"NDVI" >= 0.3        # Healthy vegetation
```

**Logical Operators**:
```
("Elevation" < 500) AND ("Slope" < 10)
("Land_Cover" == 2) OR ("Land_Cover" == 3)
NOT ("Soil_Type" == 1)
```

**Conditional (IF-THEN)**:
```
("Elevation" < 100) * 1 + ("Elevation" >= 100) * 0
```

This creates binary output: 1 below 100m, 0 above

---

### Raster Calculator Examples

**Example 1: Find suitable agricultural land**

**Criteria**:
- Elevation < 500m
- Slope < 10°
- Soil type = 2 or 3

**Expression**:
```
("Elevation@1" < 500) AND ("Slope@1" < 10) AND 
(("Soil@1" == 2) OR ("Soil@1" == 3))
```

**Result**: Binary raster (1 = suitable, 0 = not suitable)

---

**Example 2: Calculate NDVI**

**Formula**: `NDVI = (NIR - Red) / (NIR + Red)`

**Expression**:
```
("Band8@1" - "Band4@1") / ("Band8@1" + "Band4@1")
```

**Result**: NDVI values (-1 to +1)

---

**Example 3: Change detection**

**Find areas where NDVI decreased significantly**:
```
("NDVI_2024@1" - "NDVI_2025@1") > 0.2
```

**Result**: 1 where vegetation decreased, 0 elsewhere

---

**Example 4: Distance-weighted suitability**

**Weight by distance to roads** (closer = better):
```
"Suitability@1" * (1 / ("Distance_Roads@1" + 1))
```

Adding 1 prevents division by zero!

---

## Raster Reclassification

### What is Reclassification?

**Reclassification** assigns new values to cells based on their current values, grouping continuous data into categories or changing category codes.

### When to Reclassify

**Simplify continuous data**:
- Elevation → Low/Medium/High
- Slope → Flat/Gentle/Moderate/Steep

**Standardize scales**:
- Convert different scales to 1-10 suitability scores

**Create categories**:
- Temperature → Cold/Moderate/Hot

**Harmonize datasets**:
- Match land cover codes from different sources

---

### Reclassification Methods

**Method 1: Manual Reclassification Table**

| Old Value | New Value | Description |
|-----------|-----------|-------------|
| 0-15 | 1 | Flat |
| 15-30 | 2 | Gentle |
| 30-45 | 3 | Moderate |
| 45-90 | 4 | Steep |

**Method 2: Expression-Based**

Using raster calculator:
```
(("Slope@1" >= 0) AND ("Slope@1" < 15)) * 1 +
(("Slope@1" >= 15) AND ("Slope@1" < 30)) * 2 +
(("Slope@1" >= 30) AND ("Slope@1" < 45)) * 3 +
("Slope@1" >= 45) * 4
```

---

### Reclassification Tools

=== "QGIS"

    **Reclassify by Table**:
    - Processing Toolbox → "Reclassify by table"
    - Define min-max ranges and new values
    - Can save table for reuse
    
    **r.reclass** (GRASS):
    - More powerful options
    - Can use rules files

=== "ArcGIS Pro"

    **Reclassify** tool:
    - Spatial Analyst → Reclass → Reclassify
    - Interactive interface
    - Set ranges and new values

---

### Reclassification Example

**Task**: Create fire risk zones from slope

**Input**: Slope (degrees, 0-90)

**Reclassification**:

| Slope Range | New Value | Risk Level |
|-------------|-----------|------------|
| 0-10° | 1 | Low |
| 10-20° | 2 | Moderate |
| 20-35° | 3 | High |
| > 35° | 4 | Extreme |

**Why?** Steeper slopes → faster fire spread

---

## Extracting Raster Values

### Point Sampling

**Task**: Extract raster values at point locations

**Use Cases**:
- Get elevation at weather stations
- Extract NDVI at field sample sites
- Determine land cover type at GPS points

**Tool**: Sample Raster Values

=== "QGIS"

    Processing Toolbox → "Sample raster values"
    - Input: Point layer
    - Raster layer: DEM (or other raster)
    - Output: Adds raster values to point attributes

=== "ArcGIS Pro"

    **Extract Values to Points**:
    - Spatial Analyst → Extraction → Extract Values to Points

**Result**: Point layer with new field(s) containing raster values

---

### Line Sampling

**Task**: Extract raster values along lines

**Use Cases**:
- Elevation profile along trail
- NDVI along transect
- Temperature along road

**Workflow**:

1. **Densify line** - add vertices every X meters
   - Processing Toolbox → Vector Geometry → Densify by Interval
   
2. **Convert to points** - create points at vertices
   - Vector Geometry → Points along Geometry
   
3. **Sample raster** - extract values at points
   - Sample Raster Values

**Result**: Points with raster values along line

---

### Polygon Sampling: Zonal Statistics

**Task**: Calculate statistics of raster within polygons

**This is so important, it gets its own section below!**

---

## Zonal Statistics

### What are Zonal Statistics?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Zonal statistics** calculate summary statistics of a raster dataset within zones defined by polygons or another raster.

</div>

**Key Concept**: For each polygon (zone), calculate statistics from all raster cells that fall within it.

---

### Common Statistics

| Statistic | Description | Example Use |
|-----------|-------------|-------------|
| **Mean** | Average value | Average elevation per county |
| **Sum** | Total of all values | Total precipitation per watershed |
| **Min** | Minimum value | Lowest temperature per state |
| **Max** | Maximum value | Highest NDVI per field |
| **Count** | Number of cells | Number of pixels per zone |
| **Std Dev** | Standard deviation | Terrain variability per parcel |
| **Median** | Middle value | Median slope per land unit |
| **Range** | Max - Min | Elevation range per region |

---

### Zonal Statistics Workflow

**Inputs**:
1. **Value raster**: Contains data to summarize (e.g., DEM, NDVI)
2. **Zone layer**: Defines zones (polygons or raster)

**Output**:
- New fields added to zone layer with statistics

**Example**: 
- Value raster = Elevation (DEM)
- Zones = Counties (polygons)
- Output = Counties with mean_elevation, max_elevation fields

---

### Zonal Statistics Tools

=== "QGIS"

    **Zonal Statistics**:
    - Processing Toolbox → "Zonal statistics"
    - Input layer: Polygons
    - Raster layer: Data to summarize
    - Statistics: Select which to calculate
    - Result: Adds fields to polygon layer

=== "ArcGIS Pro"

    **Zonal Statistics as Table**:
    - Spatial Analyst → Zonal → Zonal Statistics as Table
    - Creates separate table
    
    **Zonal Statistics** (creates raster):
    - Output is raster, not table

---

### Zonal Statistics Examples

**Example 1: Mean elevation per watershed**

**Question**: What's the average elevation of each watershed?

**Inputs**:
- Watersheds (polygons)
- DEM (raster)

**Tool**: Zonal Statistics

**Result**: Watersheds with `mean_elev` field

**Use**: Understand watershed characteristics

---

**Example 2: Total precipitation per county**

**Inputs**:
- Counties (polygons)
- Annual precipitation (raster, mm)

**Statistic**: Sum

**Result**: Total rainfall per county

**Use**: Water resource planning

---

**Example 3: Maximum slope per parcel**

**Inputs**:
- Land parcels (polygons)
- Slope (raster, degrees)

**Statistic**: Maximum

**Result**: Steepest slope per parcel

**Use**: Construction suitability assessment

---

## Converting Between Raster and Vector

### Why Convert?

**Raster → Vector**:
- Create polygons from classified raster
- Convert contours (lines) from DEM
- Generate vector boundaries from zones

**Vector → Raster**:
- Use vector attributes in raster analysis
- Create distance rasters from features
- Rasterize for modeling

---

### Rasterization (Vector → Raster)

**What it does**: Converts vector features to raster cells

**Use Cases**:
- Create raster from soil polygon attributes
- Rasterize roads for cost-distance analysis
- Convert land parcels to grid

**Key Decisions**:
1. **Cell size**: Resolution of output
2. **Field to rasterize**: Which attribute to convert
3. **Assignment method**: How to handle overlaps

=== "QGIS"

    **Rasterize (Vector to Raster)**:
    - Raster → Conversion → Rasterize
    - Select vector layer
    - Field to use: Choose attribute
    - Output raster size: Set resolution in pixels

=== "ArcGIS Pro"

    **Polygon to Raster** / **Polyline to Raster** / **Point to Raster**:
    - Conversion Tools → To Raster
    - Set value field and cell size

**Example**: Rasterize soil polygons by K-factor (erodibility)

---

### Polygonization (Raster → Vector)

**What it does**: Converts raster cells to polygon features

**Use Cases**:
- Create polygons from classified land cover
- Vectorize elevation zones
- Convert suitable areas to parcels

**How it works**:
- Groups connected cells with same value
- Creates polygon for each group
- Assigns raster value as attribute

=== "QGIS"

    **Polygonize (Raster to Vector)**:
    - Raster → Conversion → Polygonize
    - Select raster
    - Band to use: Usually band 1
    - Output: Polygon layer

=== "ArcGIS Pro"

    **Raster to Polygon**:
    - Conversion Tools → From Raster → Raster to Polygon

**Note**: Can create MANY small polygons! Consider simplifying.

---

### Example Workflow: Segment High NDVI Areas

**Goal**: Create polygons of areas with high vegetation (NDVI > 0.6)

**Steps**:

1. **Create binary raster** using Raster Calculator:
   ```
   "NDVI@1" > 0.6
   ```
   Result: 1 where NDVI > 0.6, 0 elsewhere

2. **Polygonize** the binary raster:
   - Raster → Conversion → Polygonize
   - Result: Polygons of high vegetation areas

3. **Optional - Simplify**:
   - Remove small polygons
   - Smooth boundaries

**Use**: Identify and measure vegetated patches

---

## Advanced Raster Operations

### Proximity (Distance) Rasters

**What it does**: Calculates distance from each cell to nearest feature

**Use Cases**:
- Distance to roads
- Distance to water bodies
- Distance to fire stations

**Tool**: Proximity (Raster Distance)

**Input**: Binary raster (1 = feature, 0 = background)

**Output**: Raster where each cell value = distance to nearest feature

**Example**: Create distance-to-streams raster

1. Rasterize stream lines
2. Run Proximity tool
3. Result: Distance from every pixel to nearest stream

---

### Focal Statistics

**What it does**: Calculates statistics for each cell using values from surrounding cells

**Common Operations**:
- Mean (smoothing/noise reduction)
- Maximum (local peaks)
- Minimum (local valleys)
- Range (local variability)

**Parameters**:
- **Neighborhood**: Shape and size (3×3, 5×5, circular)
- **Statistic**: Mean, max, min, etc.

**Use Cases**:
- Smooth noisy data
- Find local extremes
- Texture analysis
- Terrain analysis

**Tool**: Focal Statistics (QGIS: r.neighbors)

---

## Multi-Criteria Suitability Analysis

### Overview

Combine multiple factors to identify suitable locations.

**Example**: Find suitable locations for solar farm

**Factors**:
1. High solar exposure (south-facing slopes)
2. Gentle terrain (slope < 15°)
3. Not too high elevation
4. Near existing roads
5. Not in protected areas

---

### Weighted Overlay Approach

**Steps**:

1. **Reclassify each factor** to 1-10 scale (10 = most suitable)

2. **Assign weights** based on importance:
   - Solar exposure: 40%
   - Slope: 25%
   - Distance to roads: 20%
   - Elevation: 15%

3. **Calculate weighted sum**:
   ```
   Suitability = (Solar * 0.40) + (Slope * 0.25) + 
                 (Roads * 0.20) + (Elevation * 0.15)
   ```

4. **Apply constraints** (Boolean AND):
   ```
   Final = Suitability * (NOT Protected_Areas)
   ```

**Result**: Continuous suitability score (0-10)

---

### Boolean Overlay Approach

**Alternative**: Use strict criteria (YES/NO)

**Example**:
```
Suitable = (Aspect >= 135) AND (Aspect <= 225) AND
           (Slope < 15) AND
           (Elevation < 1000) AND
           (Distance_Roads < 5000) AND
           (Protected == 0)
```

**Result**: Binary (1 = suitable, 0 = not suitable)

**Simpler but less flexible than weighted approach!**

---

## Best Practices

### Before Raster Analysis

1. **✅ Check projections** - All rasters must be in same CRS
2. **✅ Verify resolution** - Match resolutions if combining rasters
3. **✅ Check extents** - Align extents for pixel-by-pixel operations
4. **✅ Understand no data** - Handle appropriately in calculations
5. **✅ Inspect value ranges** - Understand min/max of each raster

---

### During Analysis

1. **✅ Save intermediate outputs** - Don't lose work!
2. **✅ Use descriptive names** - `slope_deg` not `output1`
3. **✅ Document workflow** - Record steps and formulas
4. **✅ Test on small area first** - Verify before processing large area
5. **✅ Check units** - Degrees vs radians, meters vs feet

---

### After Analysis

1. **✅ Verify output** - Does it make sense?
2. **✅ Check min/max values** - Are they reasonable?
3. **✅ Visualize results** - Use appropriate symbology
4. **✅ Validate with ground truth** - Compare to known data
5. **✅ Calculate statistics** - Summarize results

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Map algebra = math on rasters** - Cell-by-cell calculations
2. **Raster calculator is powerful** - Combine rasters with expressions
3. **Reclassify simplifies** - Group continuous into categories
4. **Point sampling extracts at points** - Get raster values at locations
5. **Zonal statistics summarize by zones** - Mean, sum, etc. per polygon
6. **Convert between formats** - Rasterize vectors, polygonize rasters
7. **Multi-criteria analysis** - Combine factors for suitability
8. **Always check alignment** - Same CRS, resolution, extent

</div>

---

## Further Reading

- [QGIS Raster Analysis](https://docs.qgis.org/3.28/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html)
- [Map Algebra Concepts](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/map-algebra.htm)
- [Zonal Statistics Explained](https://docs.qgis.org/3.28/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html#zonal-statistics)

---

## Lab Exercise

!!! lab "Lab 9: Raster Analysis & Map Algebra"
    In [Lab 9](../labs/lab09.md), you'll:
    
    - Use raster calculator for multi-criteria analysis
    - Perform reclassification on continuous data
    - Calculate zonal statistics for watersheds
    - Extract raster values at points and along lines
    - Convert between raster and vector formats
    - Build a complete suitability analysis workflow
    - Create distance rasters and apply boolean logic
    
    **Time Required**: 4-5 hours
    
    [:octicons-arrow-right-24: Go to Lab 9](../labs/lab09.md)

---

## Next Topic

You've mastered raster analysis! Now let's explore remote sensing and spectral indices:

[:octicons-arrow-right-24: Topic 10: Remote Sensing Fundamentals](10-remote-sensing.md)
