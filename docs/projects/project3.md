# Project 3: Raster Data Analysis

## Learning Goals

By the end of this project, you should be able to:

1. Become familiar with raster data analysis and GIS concepts such as:
   - Statistics and measures of central tendency
   - Clipping rasters to vectors and zonal statistics
   - Working with remote sensing datasets, deriving geophysical properties
   - Dealing with NoData values and masks
2. Chain together commands to achieve desired outcomes
3. Work with messy data to produce viable analysis for real-world problems

---

## Written Questions [4 pts]

### Question 1: Vector vs Raster Data

What are the differences between **vector** and **raster** data?

**Consider discussing**:
- Data structure
- How they represent features
- Storage methods
- Best use cases
- Advantages/disadvantages

---

### Question 2: Real-World Data Examples

Give **3 examples** of real-world data that are best described by:

**A. Vector datasets**
- Example 1:
- Example 2:
- Example 3:

**B. Raster datasets**
- Example 1:
- Example 2:
- Example 3:

**For each example, explain your reasoning** (why is this format appropriate?)

---

### Question 3: Pixel Size and Spatial Resolution

What is the importance of **pixel size** and **spatial resolution** in raster data?

**Consider**:
- How does resolution affect analysis?
- What are the trade-offs of high vs low resolution?
- How do you choose appropriate resolution?

---

### Question 4: Common Raster Data Types

What are some **common types of raster data** used in GIS?

**Hint**: We have worked with many of them in class so far.

**Examples might include**:
- Digital Elevation Models (DEMs)
- Satellite imagery
- Land cover classifications
- Temperature surfaces
- Etc.

---

## Project Work [6 pts]

### Data Required

Download the following datasets:

1. **SPR Elevation Data**
   - Available in Canvas: Week 4 folder
   - [Direct link](link-to-elevation)

2. **SPR Vector Data** (if not already downloaded)
   - Available in Canvas: Week 1 folder
   - [Direct link](link-to-vector)

**Files you'll need**:
- sprBoundary.geojson
- sprFlumes.geojson
- sprParcels.geojson
- SPR Elevation raster (DEM)

---

### Question 1: Swanton Ranch Elevation Statistics [2 pts]

Report the following elevation statistics **within the boundary of Swanton Ranch** (as defined in sprBoundary.geojson):

1. **Minimum** elevation
2. **Maximum** elevation
3. **Mean** elevation
4. **Median** elevation

**Tools to use**:
- Clip Raster by Mask Layer (to clip DEM to boundary)
- Raster Layer Statistics or Zonal Statistics

**Units**: Report in meters

---

### Question 2: Flume Elevations [2 pts]

What are the **exact elevations** of the **highest** and **lowest** Flumes in Swanton Ranch (as described in sprFlumes.geojson)?

**Report**:
- Elevation of highest flume: ___ meters
- Elevation of lowest flume: ___ meters

**Tools to use**:
- Sample Raster Values (point sampling)
- Or: Extract values to points

---

### Question 3: Mean Slope by Parcel [2 pts]

Report the **mean slope (in degrees)** for parcels (as defined in sprParcels.geojson) with the following APN numbers:

- **"057-131-60"**
- **"057-141-01"**
- **"057-121-14"**

**Steps**:
1. Calculate slope from elevation DEM (in degrees)
2. Use Zonal Statistics to calculate mean slope per parcel
3. Filter results for the specified APNs

**Report**:
- APN 057-131-60: ___ degrees
- APN 057-141-01: ___ degrees
- APN 057-121-14: ___ degrees

---

## Tutorials [6 pts]

### Tutorial 1: Sampling Raster Data [1.5 pts]

**Task**: Sample raster data using points or polygons

**Follow**: [Sampling Raster Data](https://www.qgistutorials.com/en/docs/3/sampling_raster_data.html)

**What you'll learn**:
- Extract raster values at point locations
- Calculate statistics within polygon zones
- Point sampling vs zonal statistics

**Submit**: 
- Screenshots of final outputs
- Processing steps
- Maps showing results
- **Include date/time!**

---

### Tutorial 2: Calculating Raster Area [1.5 pts]

**Task**: Calculate land use areas from raster data describing landcover

**Follow**: [Calculating Raster Area](https://www.qgistutorials.com/en/docs/3/calculating_raster_area.html)

**What you'll learn**:
- Count pixels by category
- Convert pixel counts to area
- Summarize raster classifications

**Submit**:
- Screenshots of area calculations
- Final statistics table
- Processing steps
- **Include date/time!**

---

### Tutorial 3: Creating Heatmaps [1.5 pts]

**Task**: Create a raster heatmap from point data

**Follow**: [Creating Heatmaps](https://www.qgistutorials.com/en/docs/3/creating_heatmaps.html)

**What you'll learn**:
- Kernel density estimation
- Point pattern analysis
- Heatmap visualization

**Submit**:
- Screenshots of heatmap outputs
- Maps with different parameters
- Processing steps
- **Include date/time!**

---

### Tutorial 4: Basic Raster Styling and Analysis [1.5 pts]

**Task**: Apply basic raster styling and analysis

**Follow**: [Basic Raster Styling and Analysis](https://www.qgistutorials.com/en/docs/3/raster_styling_and_analysis.html)

**What you'll learn**:
- Raster symbology
- Color ramps and classification
- Terrain visualization

**Submit**:
- Screenshots of styled rasters
- Different color schemes applied
- Processing steps
- **Include date/time!**

---

## Submission Requirements

Submit to Canvas **one document** containing:

1. ✅ **Answers to Written Questions 1-4**
2. ✅ **Answers to Project Work Questions 1-3** with:
   - All required statistics
   - Explanation of methods used
   - Screenshots showing calculations
3. ✅ **Maps/screenshots from Tutorials 1-4** showing:
   - Final products
   - Processing steps
   - Date/time stamps

**File format**: PDF preferred

---

## Grading Rubric

| Component | Points |
|-----------|--------|
| Written Questions 1-4 | 4 pts |
| Project Question 1: Elevation Stats | 2 pts |
| Project Question 2: Flume Elevations | 2 pts |
| Project Question 3: Parcel Slopes | 2 pts |
| Tutorial 1: Sampling Raster Data | 1.5 pts |
| Tutorial 2: Calculating Raster Area | 1.5 pts |
| Tutorial 3: Creating Heatmaps | 1.5 pts |
| Tutorial 4: Raster Styling | 1.5 pts |
| **TOTAL** | **16 pts** |

---

## Tips for Success

### For Written Questions:
- **Be specific** - Don't just say "rasters are different"
- **Use examples** from class and real-world applications
- **Explain trade-offs** - Every choice has pros and cons

### For Project Work:
- **Check units** - Elevation in meters, slope in degrees
- **Clip first** - Clip DEM to boundary before statistics
- **Filter carefully** - Use exact APN strings (watch for spaces!)
- **Document steps** - Screenshot your process
- **Verify results** - Do the numbers make sense?

### For Tutorials:
- **Follow exactly** - Don't skip steps
- **Experiment** - Try different parameters
- **Compare outputs** - What changes with different settings?
- **Screenshots required** - No proof = no credit

---

## Common Mistakes to Avoid

❌ **Wrong units** - Reporting slope in radians instead of degrees
❌ **Not clipping** - Statistics for entire DEM instead of boundary
❌ **Typos in APNs** - "057-131-60" ≠ "057-13160"
❌ **Forgetting NoData** - Make sure to handle NoData values correctly
❌ **Missing timestamps** - Required on all screenshots
❌ **Using wrong tool** - Point sampling vs zonal statistics

---

## Key Tools Reference

### Clipping Rasters:
- **Tool**: Raster → Extraction → Clip Raster by Mask Layer
- **Use**: Clip DEM to boundary polygon

### Raster Statistics:
- **Tool**: Raster → Analysis → Raster Layer Statistics
- **Use**: Get min/max/mean/median for entire raster

### Zonal Statistics:
- **Tool**: Processing → Zonal Statistics
- **Use**: Calculate statistics per polygon (e.g., per parcel)

### Sample Raster Values:
- **Tool**: Processing → Sample Raster Values
- **Use**: Extract raster values at point locations

### Calculate Slope:
- **Tool**: Raster → Analysis → Slope
- **Use**: Derive slope from DEM
- **Units**: Set to degrees!

---

## Conceptual Review

### Raster vs Vector:
- **Raster**: Grid of cells, continuous surfaces, imagery
- **Vector**: Points/lines/polygons, discrete features

### Resolution:
- **High resolution**: Small pixels, more detail, larger files
- **Low resolution**: Large pixels, less detail, smaller files

### NoData:
- Special value indicating no measurement
- Common: -9999, -3.4e38
- Must handle properly in analysis

### Zonal Statistics:
- Calculate statistics of raster within zones (polygons)
- Examples: Mean elevation per watershed, max slope per parcel

---

## Resources

- [QGIS Raster Analysis Documentation](https://docs.qgis.org/latest/en/docs/user_manual/working_with_raster/)
- [SPR Data Download](link-to-canvas)
- [QGIS Tutorials](https://www.qgistutorials.com/)
- [Raster Processing Tools](https://docs.qgis.org/latest/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html)

---

## Getting Help

- **Office Hours**: Check syllabus
- **Lab Sessions**: TAs available for help
- **QGIS Documentation**: Built-in help system
- **Online Forums**: GIS Stack Exchange

Welcome to raster analysis! 🗺️
