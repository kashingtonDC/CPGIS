# Topic 4: Data Creation and Editing

## Overview

Creating and editing spatial data is a fundamental GIS skill. Whether digitizing features from imagery, collecting field data, or cleaning existing datasets, you need to understand how to create accurate, high-quality spatial data.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Create new point, line, and polygon features
- Edit existing feature geometry and attributes
- Use snapping and topology tools for accuracy
- Understand topology rules and relationships
- Digitize features from imagery and maps
- Calculate geometry attributes (area, length)
- Fix common data quality issues

---

## Why Create Your Own Data?

Sometimes the data you need simply doesn't exist! You may need to:

- **Digitize historical maps** not available digitally
- **Create custom study areas** specific to your research
- **Collect field observations** (tree locations, sample sites)
- **Update outdated datasets** with current information
- **Combine data** from multiple sources into new layers
- **Fix errors** in existing datasets

---

## Vector Data Creation Methods

### 1. Manual Digitizing

**What it is**: Manually tracing features on screen using aerial imagery, satellite data, or scanned maps as a reference.

**When to use**:
- Historical map digitization
- Custom area of interest
- Features not in existing datasets
- High accuracy needed

**Tools Required**:
- Base layer for reference (imagery, scanned map)
- Digitizing toolbar
- Snapping settings

---

### 2. GPS/GNSS Collection

**What it is**: Collecting point, line, or track data using GPS devices in the field.

**When to use**:
- Field surveys
- Ground truthing
- Real-time location tracking
- Asset inventory

**Typical Accuracy**:
- Consumer GPS: 3-10 meters
- Differential GPS: <1 meter
- Survey-grade GPS: Centimeter-level

---

### 3. Importing Tabular Data

**What it is**: Converting spreadsheets or databases containing latitude/longitude into spatial features.

**When to use**:
- CSV/Excel files with coordinates
- Database records with locations
- Survey data with GPS coordinates

**Requirements**:
- Coordinate columns (lat/lon or X/Y)
- Known coordinate system

---

### 4. Geocoding

**What it is**: Converting addresses to geographic coordinates.

**When to use**:
- Address lists need to be mapped
- Customer locations from database
- Historical address records

---

## Creating Features in GIS

### Creating Point Features

**Use Cases**:
- Tree inventory locations
- Sample sites
- Building centroids
- Observation points

**Workflow**:

1. **Create new layer**
   - Choose point geometry
   - Define attribute fields
   - Set coordinate system

2. **Start editing**
   - Toggle editing mode ON
   - Select "Add Point Feature" tool

3. **Add points**
   - Click map to place point
   - Fill out attribute form
   - Repeat for each feature

4. **Save edits**
   - Save layer edits
   - Toggle editing mode OFF

---

### Creating Line Features

**Use Cases**:
- Trails
- Custom roads
- Stream centerlines
- Flight paths

**Workflow**:

1. **Create new layer**
   - Choose line geometry
   - Define fields
   - Set coordinate system

2. **Enable snapping** (important!)
   - Enable snapping toolbar
   - Set snap tolerance
   - Choose snap to vertices/segments

3. **Add lines**
   - Click to add first vertex
   - Click to add intermediate vertices
   - Right-click (or press ESC) to finish line
   - Fill attributes

---

### Creating Polygon Features

**Use Cases**:
- Study area boundaries
- Land parcels
- Vegetation patches
- Building footprints
- Custom zones

**Workflow**:

1. **Create new layer**
   - Choose polygon geometry
   - Define fields (consider including area!)
   - Set coordinate system

2. **Configure snapping & topology**
   - Enable topological editing
   - Enable "Avoid Overlap on Active Layer"
   - Set snap tolerance

3. **Digitize polygons**
   - Click to add vertices
   - Right-click to close polygon
   - Fill attributes
   - Use advanced tools as needed

---

## Essential Digitizing Tools

### Snapping 📐

**What it does**: Automatically aligns vertices to nearby features, vertices, or segments.

**Why it matters**: Ensures features connect properly without gaps or overlaps.

**Snap modes**:
- **Vertex**: Snap to existing vertices
- **Segment**: Snap to line/polygon edges
- **Self**: Snap to vertices in current feature

**Best Practice**: Always enable snapping when digitizing adjacent features!

---

### Topological Editing 🔗

**What it is**: Maintains spatial relationships between features while editing.

**Key Options**:

**Enable Topological Editing**
- Moves shared vertices/edges together
- Example: Moving a shared boundary moves both adjacent polygons

**Avoid Overlap on Active Layer**
- Prevents new polygons from overlapping existing ones
- Automatically trims overlaps

**Enable Snapping**
- Ensures features connect properly

!!! tip "Topology = Clean Data"
    Using topology tools during editing prevents most data quality issues! Much easier than fixing them later.

---

## Advanced Editing Tools

### Vertex Tool ✏️

**What it does**: Adds, deletes, or moves individual vertices.

**Common tasks**:
- Reshape polygon boundaries
- Adjust line paths
- Add detail to features
- Remove unnecessary vertices

**How to use**:
- Select vertex tool
- Click feature to select
- Drag vertices to move
- Double-click to add vertex
- Delete key to remove vertex

---

### Split Features ✂️

**What it does**: Divides a line or polygon into multiple features.

**Use cases**:
- Split parcel into smaller lots
- Divide road segment at intersection
- Separate vegetation patches

**How to use**:
1. Select feature to split
2. Activate split tool
3. Draw line across feature
4. Feature splits into two

---

### Merge Features ⊕

**What it does**: Combines multiple features into one.

**Use cases**:
- Join adjacent parcels
- Combine segmented lines
- Merge vegetation patches

**How to use**:
1. Select features to merge
2. Use merge tool
3. Choose which attributes to keep

---

### Rotate Features 🔄

**What it does**: Rotates selected features around a point.

**Use cases**:
- Align building footprints
- Adjust directional symbols
- Orient features correctly

---

### Auto-complete Polygons 🔲

**What it does**: Automatically completes a polygon by following existing boundaries.

**Use cases**:
- Filling gaps between parcels
- Creating adjacent polygons quickly

**How to use**:
1. Start digitizing polygon
2. When you reach existing boundary, stop
3. Tool auto-completes along shared edge

---

## Topology Rules

### What is Topology?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Topology** defines spatial relationships between features - how they connect, overlap, or relate spatially. Topology rules enforce data quality standards.

</div>

### Common Topology Rules

| Rule | Description | Example |
|------|-------------|---------|
| **Must Not Overlap** | Polygons cannot overlap | Land parcels |
| **Must Not Have Gaps** | No empty space between polygons | Land use coverage |
| **Must Not Have Dangles** | Lines must connect at endpoints | Road networks |
| **Must Be Inside** | Points must fall within polygons | Wells within aquifers |
| **Boundary Must Be Covered By** | Boundary matches another layer | County boundaries match state |

### Topology Errors

**Common Problems**:

**Gaps** 🕳️
- Unintended space between polygons
- Fix: Extend boundary or create new polygon

**Overlaps** ⚠️
- Features covering same area
- Fix: Use "Avoid Overlap" or trim excess

**Dangles** 🎣
- Line endpoints that don't connect
- Fix: Extend line or snap to network

**Slivers** 🔪
- Thin polygons from imperfect digitizing
- Fix: Merge with adjacent polygon or delete

---

## Calculating Geometry Attributes

### Area Calculation

Calculate polygon area in appropriate units:

**For accurate area**:
1. Ensure layer is in projected CRS (UTM)
2. Use field calculator
3. Expression: `$area`
4. Result in square meters

**Convert to acres**:
```
$area / 4046.86
```

**Convert to hectares**:
```
$area / 10000
```

---

### Length Calculation

Calculate line length:

**Expression**: `$length`

**Convert meters to miles**:
```
$length / 1609.34
```

**Convert meters to kilometers**:
```
$length / 1000
```

---

### Perimeter Calculation

For polygons:

**Expression**: `$perimeter`

---

## Field Calculator & Attribute Editing

### Creating New Fields

Add new attribute columns to store calculated values:

**Common field types**:
- **Integer**: Whole numbers (ID, count)
- **Decimal**: Numbers with decimals (area, length)
- **Text**: Alphanumeric strings (name, category)
- **Date**: Date/time values

---

### Concatenating Text Fields

Combine multiple text fields into one:

**Example**: Create Parcel ID from Book-Page-Parcel

**Expression**:
```
"book" || '-' || "page" || '-' || "parcel"
```

**Result**: `025-142-003`

---

### Conditional Calculations

Calculate values based on conditions:

**Example**: Categorize parcels by size

**Expression**:
```
CASE 
  WHEN $area < 2000 THEN 'Small'
  WHEN $area < 10000 THEN 'Medium'
  ELSE 'Large'
END
```

---

## Best Practices for Data Creation

### Before You Start

1. **✅ Plan your schema** - What fields do you need?
2. **✅ Choose appropriate geometry type** - Point, line, or polygon?
3. **✅ Set coordinate system** - Match existing data or use UTM
4. **✅ Define attribute fields** - Name, type, and size
5. **✅ Prepare base layer** - Imagery or map for reference

---

### While Digitizing

1. **✅ Enable snapping** - Prevents gaps and overlaps
2. **✅ Use topology tools** - Maintains relationships
3. **✅ Zoom in close** - Better accuracy
4. **✅ Be consistent** - Follow same rules throughout
5. **✅ Save frequently** - Don't lose work!
6. **✅ Check as you go** - Verify features look correct

---

### After Creating Data

1. **✅ Validate topology** - Check for errors
2. **✅ Fix geometries** - Repair invalid features
3. **✅ Complete attributes** - Fill all required fields
4. **✅ Calculate geometry** - Area, length, etc.
5. **✅ Document metadata** - When, how, why created
6. **✅ Set appropriate symbology** - Make it readable

---

## Data Quality Issues & Fixes

### Problem: Invalid Geometry

**Symptoms**:
- Geoprocessing tools fail
- Error: "Feature has invalid geometry"
- Features don't display correctly

**Solutions**:

=== "QGIS"
    Use **Fix Geometries** tool:
    - Vector → Geometry Tools → Fix Geometries
    - Creates new layer with repaired features

=== "ArcGIS Pro"
    Use **Repair Geometry** tool:
    - Data Management → Features → Repair Geometry
    - Repairs features in place

---

### Problem: Unclosed Polygons

**Symptoms**:
- Polygon won't close
- Last vertex doesn't connect to first

**Solution**:
- Ensure snapping is enabled
- Manually click on first vertex to close
- Use vertex tool to drag endpoint

---

### Problem: Self-Intersecting Polygons

**Symptoms**:
- Polygon crosses itself
- "Bowtie" or figure-8 shape

**Solution**:
- Use vertex tool to untangle
- May need to split into separate features
- Use Fix Geometries tool

---

### Problem: Duplicate Features

**Symptoms**:
- Same feature digitized twice
- Overlapping identical geometries

**Solution**:
- Select duplicates manually
- Delete extra features
- Use "Remove Duplicate Vertices" tool

---

## Digitizing from Different Sources

### From Aerial Imagery

**Best Practices**:
- Use highest resolution available
- Zoom in to ~1:1000 scale
- Be consistent with edge interpretation
- Consider seasonal differences

**Tips**:
- Buildings: Trace roof edges
- Roads: Follow centerline or edge consistently
- Vegetation: Define clear boundaries

---

### From Scanned Maps

**Workflow**:
1. **Georeference** the scanned map first
2. Set proper coordinate system
3. Digitize features using map as reference
4. Cross-reference with other sources

**Challenges**:
- May have distortion
- Resolution limits
- Accuracy varies

---

### From GPS Data

**Workflow**:
1. Download GPS tracks/points from device
2. Import into GIS (usually as GPX or CSV)
3. Check coordinate system (usually WGS84)
4. Reproject if needed
5. Clean up track noise if necessary

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Enable snapping** - Prevents gaps and ensures connections
2. **Use topology tools** - Maintains spatial relationships automatically
3. **Project your data** - Use UTM or appropriate CRS for accurate geometry
4. **Save frequently** - Editing sessions can crash
5. **Fix geometries** - Repair invalid features before analysis
6. **Calculate after editing** - Update area/length fields after changes
7. **Document your work** - Record methods, sources, accuracy
8. **Validate quality** - Check for errors before finalizing

</div>

---

## Further Reading

- [QGIS Digitizing Tutorial](https://docs.qgis.org/3.28/en/docs/training_manual/create_vector_data/)
- [ArcGIS Pro: Edit Features](https://pro.arcgis.com/en/pro-app/latest/help/editing/overview-of-desktop-editing.htm)
- [Topology in GIS](https://docs.qgis.org/3.28/en/docs/user_manual/working_with_vector/vector_properties.html#topology)

---

## Lab Exercise

!!! lab "Lab 4: Data Creation & Editing"
    In [Lab 4](../labs/lab04.md), you'll:
    
    - Create new point, line, and polygon layers
    - Digitize features from aerial imagery
    - Use snapping and topology tools
    - Edit vertices and reshape features
    - Split and merge features
    - Calculate area and length
    - Fix invalid geometries
    - Create a complete spatial dataset from scratch
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 4](../labs/lab04.md)

---

## Next Topic

Now that you can create spatial data, let's learn how to manage and join attribute tables:

[:octicons-arrow-right-24: Topic 5: Table Management & Joins](05-table-management.md)
