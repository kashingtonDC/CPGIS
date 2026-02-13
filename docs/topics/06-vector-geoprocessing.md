# Topic 6: Vector Geoprocessing Operations

## Overview

Vector geoprocessing operations are the fundamental tools for spatial analysis. These tools allow you to answer complex spatial questions by manipulating and analyzing the geometric relationships between features.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand common vector geoprocessing operations
- Apply buffers, clips, intersects, and unions appropriately
- Combine multiple geoprocessing tools to solve spatial problems
- Choose the right tool for specific spatial analysis questions
- Troubleshoot common geoprocessing errors

---

## What is Geoprocessing?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Geoprocessing** is the manipulation and analysis of geographic data to create new information. It involves using tools that transform, combine, or extract spatial data to answer questions or solve problems.

</div>

Think of geoprocessing tools as spatial "verbs" - they perform actions on your geographic data:

- **Buffer**: Create zones around features
- **Clip**: Extract features within a boundary
- **Intersect**: Find where features overlap
- **Union**: Combine features together
- **Dissolve**: Merge features with common attributes

---

## Essential Geoprocessing Operations

### 1. Buffer 📏

**What it does**: Creates polygon zones at a specified distance around point, line, or polygon features.

**When to use**:
- Create zones of influence (e.g., 500m around schools)
- Identify areas within distance of features (e.g., parcels within 100m of a road)
- Environmental setbacks (e.g., 30m riparian buffer along streams)

**Example Questions Buffer Can Answer**:
- Which houses are within 1 mile of a fire station?
- What land area falls within 50 meters of a stream?
- How many parks are within walking distance (400m) of each neighborhood?

![Buffer Example](../images/buffer-example.png)
*Buffer creates zones around features at a specified distance*

**QGIS Tool**: Vector → Geoprocessing Tools → Buffer
<br>**ArcGIS Pro Tool**: Analysis → Proximity → Buffer

!!! warning "Projection Required!"
    Buffers require a **projected coordinate system** (like UTM) to work correctly. If your data is in geographic coordinates (lat/lon), reproject first!

---

### 2. Clip ✂️

**What it does**: Extracts features from one layer that fall within the boundary of another layer. Like using cookie cutters!

**When to use**:
- Extract data for your study area
- Remove data outside a region of interest
- Create subsets of larger datasets

**Example Questions Clip Can Answer**:
- What roads are within my county boundary?
- Which land parcels fall inside the city limits?
- Extract all streams within my watershed?

![Clip Example](../images/clip-example.png)
*Clip extracts only features within the boundary*

**Input Requirements**:
- **Input features**: The layer you want to cut (any geometry type)
- **Clip features**: The boundary to cut by (must be polygons)

**QGIS Tool**: Vector → Geoprocessing Tools → Clip
<br>**ArcGIS Pro Tool**: Analysis → Extract → Clip

---

### 3. Intersect ⊗

**What it does**: Finds where features from multiple layers overlap, creating new features only where they coincide. Preserves attributes from **both** input layers.

**When to use**:
- Find areas that meet multiple criteria
- Identify overlapping regions
- Combine attributes from multiple layers

**Example Questions Intersect Can Answer**:
- Which areas are both high elevation AND within protected lands?
- Where do soil types overlap with vegetation types?
- What parcels intersect with flood zones?

![Intersect Example](../images/intersect-example.png)
*Intersect creates features only where inputs overlap*

**Key Difference from Clip**:
- **Clip**: Keeps original attributes, just cuts geometry
- **Intersect**: Combines attributes from both layers

**QGIS Tool**: Vector → Geoprocessing Tools → Intersection
<br>**ArcGIS Pro Tool**: Analysis → Overlay → Intersect

---

### 4. Union ⊕

**What it does**: Combines all features from multiple layers into one layer, preserving all geometries and attributes. Creates features for **all** areas - overlapping and non-overlapping.

**When to use**:
- Combine multiple polygon layers completely
- Preserve information from all input layers
- Create comprehensive coverage

**Example Questions Union Can Answer**:
- Combine land ownership with land use - what's the ownership of each land use type?
- Merge multiple jurisdictions into one layer with all boundaries preserved
- Overlay census tracts with city boundaries

![Union Example](../images/union-example.png)
*Union combines all features from both inputs*

**Result**: Contains every possible combination of overlapping areas!

**QGIS Tool**: Vector → Geoprocessing Tools → Union
<br>**ArcGIS Pro Tool**: Analysis → Overlay → Union

---

### 5. Dissolve 🔀

**What it does**: Merges adjacent features that share common attribute values into single features.

**When to use**:
- Simplify datasets by combining similar features
- Aggregate data (e.g., combine census blocks into districts)
- Remove unnecessary boundaries

**Example Questions Dissolve Can Answer**:
- Combine all parcels owned by the same person
- Merge census tracts by county
- Group forests by vegetation type

![Dissolve Example](../images/dissolve-example.png)
*Dissolve merges features with matching attribute values*

**Options**:
- **Dissolve field**: Attribute to group by
- **Statistics**: Can calculate sums, means, etc. for dissolved features

**QGIS Tool**: Vector → Geoprocessing Tools → Dissolve
<br>**ArcGIS Pro Tool**: Data Management → Generalization → Dissolve

---

### 6. Merge (Append) ➕

**What it does**: Combines multiple layers of the **same geometry type** into a single layer. No geometric operations - just stacks features together.

**When to use**:
- Combine datasets from different sources
- Merge adjacent tiles (e.g., neighboring counties)
- Compile data from multiple dates/sources

**Example Questions Merge Can Answer**:
- Combine road networks from multiple counties
- Merge tree point data from different surveys
- Append this year's data to last year's

**Key Difference from Union**:
- **Union**: Splits overlapping features and combines attributes
- **Merge**: Just stacks features together, no splitting

**QGIS Tool**: Vector → Data Management Tools → Merge Vector Layers
<br>**ArcGIS Pro Tool**: Data Management → General → Merge

---

### 7. Erase (Difference) ➖

**What it does**: Removes portions of features that overlap with another layer. Opposite of clip!

**When to use**:
- Remove features from an area
- Create "donut" shapes
- Subtract one area from another

**Example Questions Erase Can Answer**:
- What land area is **outside** protected areas?
- Remove developed areas from wildlife habitat
- Exclude waterbodies from land use analysis

![Erase Example](../images/erase-example.png)
*Erase removes overlapping portions*

**QGIS Tool**: Vector → Geoprocessing Tools → Difference
<br>**ArcGIS Pro Tool**: Analysis → Overlay → Erase

---

### 8. Symmetric Difference ⊕

**What it does**: Returns features that are in either input layer but **NOT** in both. Finds areas that are unique to each input.

**When to use**:
- Identify differences between datasets
- Find areas that changed (before/after comparison)
- Locate unique features

**Example**: Compare land ownership from 2020 and 2025 - what parcels changed?

**QGIS Tool**: Vector → Geoprocessing Tools → Symmetrical Difference
<br>**ArcGIS Pro Tool**: Analysis → Overlay → Symmetrical Difference

---

## Geoprocessing Tool Comparison

| Tool | Output Location | Attributes | Use Case |
|------|----------------|-----------|----------|
| **Buffer** | Around features | From input | Distance-based zones |
| **Clip** | Inside boundary | From input | Extract study area |
| **Intersect** | Overlap only | Both inputs | Find coincidence |
| **Union** | All areas | Both inputs | Complete combination |
| **Dissolve** | Merged features | Aggregated | Simplify/combine |
| **Merge** | All features | Stacked | Combine same types |
| **Erase** | Non-overlap | From input | Remove areas |
| **Sym. Diff** | Non-overlap | Both inputs | Find differences |

---

## Chaining Operations: Multi-Step Analysis

Real-world spatial questions often require **multiple** geoprocessing steps!

### Example Workflow: Site Selection

**Question**: Find suitable locations for a new park that are:
- Within 500m of schools
- On public land
- Outside floodplains
- Larger than 2 acres

**Workflow**:

1. **Buffer** schools by 500m
2. **Intersect** buffer with public lands
3. **Erase** floodplains from result
4. **Select** polygons > 2 acres
5. **Dissolve** to create final candidate sites

Each step narrows down the solution!

---

## Troubleshooting Common Issues

### Invalid Geometries

**Error**: "Feature has invalid geometry"

**Causes**:
- Self-intersecting polygons
- Duplicate vertices
- Corrupted features

**Solutions**:

=== "QGIS"
    - Use **Fix Geometries** tool
    - Vector → Geometry Tools → Fix Geometries

=== "ArcGIS Pro"
    - Use **Repair Geometry** tool
    - Data Management → Features → Repair Geometry

---

### Empty Output

**Problem**: Geoprocessing tool runs but creates empty layer

**Common Causes**:
1. **No spatial overlap** - features don't actually intersect
2. **Projection mismatch** - data in different coordinate systems
3. **Invalid geometries** - corrupted data

**Debugging Steps**:
1. Zoom to each layer - do they overlap visually?
2. Check coordinate systems - are they the same?
3. Fix geometries on input layers
4. Try simpler test with fewer features

---

### Projection Errors

**Problem**: "Coordinate system mismatch" or inaccurate results

**Solution**:
- **Always reproject** all layers to same CRS before geoprocessing
- Use a projected CRS (like UTM) for accurate measurements
- Verify output CRS after running tools

---

## Best Practices

1. **✅ Reproject first** - Get all data into same CRS before analysis
2. **✅ Fix geometries** - Run fix/repair tools on problem layers
3. **✅ Save intermediate results** - Don't lose work if something fails
4. **✅ Check outputs** - Open attribute tables, verify feature counts
5. **✅ Document workflow** - Record tools used and parameters
6. **✅ Use descriptive names** - `schools_500m_buffer` not `output1`

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Right tool for the job** - Different operations for different spatial questions
2. **Projection matters** - Reproject to projected CRS before geoprocessing
3. **Chain operations** - Complex problems need multiple steps
4. **Fix geometries** - Invalid geometry is a common error source
5. **Check your outputs** - Verify results make spatial sense
6. **Intersect vs Union vs Clip** - Know when to use which overlay tool
7. **Buffer needs projection** - Must use meters/feet, not degrees

</div>

---

## Further Reading

- [QGIS Geoprocessing Tools](https://docs.qgis.org/3.28/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html)
- [ArcGIS Pro Geoprocessing](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/an-overview-of-the-analysis-toolbox.htm)
- [Vector Overlay Operations Explained](https://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html)

---

## Lab Exercise

!!! lab "Lab 6: Vector Geoprocessing"
    In [Lab 6](../labs/lab06.md), you'll:
    
    - Apply buffers to create distance zones
    - Use clip to extract study area data
    - Perform intersect and union operations
    - Chain multiple tools for site selection analysis
    - Troubleshoot invalid geometries
    - Create a multi-criteria suitability map
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 6](../labs/lab06.md)

---

## Next Topic

You've mastered vector geoprocessing! Now let's explore how to collect field data with GPS:

[:octicons-arrow-right-24: Topic 7: Field Data & GPS](07-field-data-gps.md)
