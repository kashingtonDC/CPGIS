# Topic 12: Workflow Design and Best Practices

## Overview

Effective GIS work requires organized workflows, consistent methods, and good documentation. This topic covers professional practices that make your work reproducible, efficient, and collaborative.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Design efficient GIS workflows
- Organize files and folders properly
- Document your methods
- Create reproducible analyses
- Troubleshoot common problems
- Collaborate effectively on GIS projects

---

## GIS Workflow Design

### What is a Workflow?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **workflow** is a sequence of connected steps that transforms input data into desired outputs using specific tools and methods.

</div>

###

 Typical GIS Project Workflow

```
1. Define Question/Objective
   ↓
2. Identify Required Data
   ↓
3. Acquire Data
   ↓
4. Assess Data Quality
   ↓
5. Prepare Data (clean, reproject, clip)
   ↓
6. Analyze Data
   ↓
7. Create Maps/Visualizations
   ↓
8. Interpret Results
   ↓
9. Document Methods
   ↓
10. Share/Present Findings
```

---

## File Organization

### Project Structure

**Recommended folder hierarchy**:

```
ProjectName/
├── 01_RawData/          # Original, untouched data
│   ├── Elevation/
│   ├── LandCover/
│   └── Boundaries/
├── 02_ProcessedData/    # Cleaned, reprojected data
│   ├── Clipped/
│   ├── Reprojected/
│   └── Merged/
├── 03_Analysis/         # Analysis outputs
│   ├── BufferResults/
│   ├── Statistics/
│   └── Classifications/
├── 04_Maps/             # Map layouts and exports
│   ├── PDFs/
│   └── PNGs/
├── 05_Scripts/          # Processing scripts if any
├── 06_Documentation/    # Metadata, reports
│   ├── Methods.md
│   ├── DataSources.txt
│   └── ChangeLog.md
└── ProjectFile.qgz      # QGIS project file
```

---

### Naming Conventions

**Be consistent and descriptive!**

**Good examples**:
```
elevation_10m_utm10n_clipped.tif
landcover_2024_sentinel2_classified.tif
counties_california_wgs84.gpkg
analysis_slope_greater_than_30deg.tif
```

**Bad examples**:
```
data1.tif
final_FINAL_v3.shp
output.gpkg
temp_layer_123.tif
```

---

### File Naming Best Practices

1. **✅ Use descriptive names** - `elevation_srtm_30m` not `dem1`
2. **✅ Include key metadata** - Resolution, date, projection hint
3. **✅ Use underscores/hyphens** - Not spaces! `land_cover` not `land cover`
4. **✅ Add dates if time matters** - `YYYYMMDD` format: `fire_perimeter_20241015`
5. **✅ Avoid special characters** - Stick to letters, numbers, `-` and `_`
6. **✅ Keep names reasonably short** - But not cryptic
7. **✅ Use consistent case** - lowercase recommended
8. **✅ Number for order** - `01_download`, `02_reproject`, `03_clip`

---

## Version Control

### Track Changes

**Methods**:

**Version numbers in filenames** (Simple):
```
analysis_v1.0.qgz
analysis_v1.1.qgz
analysis_v2.0_final.qgz
```

**Date stamps** (Better):
```
analysis_20241015.qgz
analysis_20241016.qgz
```

**Git** (Best for scripts/code):
- Track changes to Python/R scripts
- Collaborate with others
- Revert to previous versions

---

### Changelog

**Keep a project log**:

```markdown
# Project Changelog

## 2024-10-15
- Downloaded Sentinel-2 imagery (Band 4, Band 8)
- Calculated NDVI using raster calculator
- Clipped to study area extent

## 2024-10-16
- Reclassified NDVI into 5 categories
- Calculated area statistics per class
- Created final map layout

## 2024-10-17
- Fixed projection issue (was WGS84, should be UTM 10N)
- Re-ran all analysis
- Updated maps
```

---

## Documentation

### Why Document?

**For future you**:
- "What did I do 6 months ago?"
- "Why did I make this choice?"

**For others**:
- Colleagues need to understand
- Reviewers need to verify
- Reproducibility is essential

---

### What to Document

**Data sources**:
```
Dataset: SRTM 30m DEM
Source: USGS EarthExplorer
Download date: 2024-10-15
URL: https://earthexplorer.usgs.gov
Coverage: Central California
Resolution: 30m
Projection: WGS84
```

**Processing steps**:
```
1. Reprojected DEM from WGS84 to UTM 10N
   Tool: Warp (Reproject)
   Target CRS: EPSG:32610
   
2. Calculated slope
   Tool: Slope
   Units: Degrees
   
3. Reclassified slope into 4 categories
   0-10°  = Flat
   10-20° = Gentle
   20-35° = Moderate
   >35°   = Steep
```

**Analysis parameters**:
```
Buffer analysis:
- Distance: 500 meters
- Dissolution: Yes
- End cap style: Round

Zonal statistics:
- Statistics: Mean, Max, StdDev
- Input zones: Watersheds
- Value raster: Precipitation
```

---

### Methods Documentation Template

```markdown
# Project: [Name]

## Objective
[What question are you answering?]

## Data Sources
| Dataset | Source | Date | Resolution | CRS |
|---------|--------|------|------------|-----|
| DEM | USGS | 2024-01 | 30m | WGS84 |
| Land cover | Sentinel | 2024-06 | 10m | UTM 10N |

## Processing Workflow

### 1. Data Preparation
- Step 1: ...
- Step 2: ...

### 2. Analysis
- Tool: ...
- Parameters: ...

### 3. Results
- Output: ...
- Format: ...

## Results Summary
[Brief summary of findings]

## Known Issues/Limitations
- Cloud cover in northeast corner
- Missing data for...
```

---

## Troubleshooting

### Debugging Philosophy

**When something doesn't work**:

1. **Read the error message** - Carefully!
2. **Search the error** - Google/ChatGPT exact text
3. **Check inputs** - Are they what you expect?
4. **Simplify** - Test with smaller dataset
5. **Restart** - QGIS/ArcGIS can get confused
6. **Ask for help** - GIS Stack Exchange, colleagues

---

### Common Issues & Solutions

**Issue**: Layers don't align visually

**Causes**:
- Different coordinate systems
- Different datums

**Solutions**:
- Check CRS of each layer
- Reproject all to same CRS
- Enable "on-the-fly" reprojection

---

**Issue**: Geoprocessing tool fails

**Causes**:
- Invalid geometries
- Projection mismatch
- Memory limitations

**Solutions**:
```
1. Fix geometries first
   - Vector → Geometry Tools → Fix Geometries

2. Ensure matching CRS
   - Reproject all inputs

3. Try smaller extent
   - Clip to test area first
```

---

**Issue**: Output looks wrong

**Causes**:
- Wrong parameters
- Incorrect units
- Bad input data

**Solutions**:
- Review parameters carefully
- Check units (meters vs degrees vs feet)
- Visualize intermediate results
- Compare to expected outcome

---

## Collaboration Best Practices

### Working with Others

**File sharing**:
- Use cloud storage (OneDrive, Google Drive, Dropbox)
- Relative file paths, not absolute!
- Share entire project folder, not just .qgz file

**Relative paths example**:
```
Good: ./Data/elevation.tif
Bad:  C:\Users\YourName\Documents\GIS\Data\elevation.tif
```

---

### Standards for Teams

**Agree on**:
- Coordinate system for projects
- Naming conventions
- Folder structure
- File formats
- Documentation requirements

**Create templates**:
- Project folder structure
- Map layouts
- Metadata files

---

## Quality Control

### Check Your Work

**Before finalizing**:

1. **✅ Verify CRS** - All layers match?
2. **✅ Check extents** - Layers align?
3. **✅ Inspect attributes** - No missing/wrong values?
4. **✅ Review statistics** - Do min/max make sense?
5. **✅ Visual check** - Zoom in, look for errors
6. **✅ Test calculations** - Spot check formulas
7. **✅ Map check** - Print/export, review carefully

---

### Validation Checklist

**Data quality**:
- [ ] Correct coordinate system
- [ ] Appropriate resolution
- [ ] Complete coverage
- [ ] No corrupt files
- [ ] Metadata present

**Analysis**:
- [ ] Documented methods
- [ ] Parameters recorded
- [ ] Intermediate results saved
- [ ] Results make sense
- [ ] Checked against known values

**Outputs**:
- [ ] Maps have legends
- [ ] North arrows and scale bars
- [ ] Proper labeling
- [ ] Citations included
- [ ] Final files organized

---

## Reproducibility

### Make Your Work Reproducible

**Goals**:
- Someone else can recreate your analysis
- Future you can understand what you did
- Results can be verified

**How**:

1. **Document everything** - See documentation section
2. **Save intermediate results** - Don't delete!
3. **Use scripts when possible** - Python, R, Model Builder
4. **Standard file paths** - Relative, not absolute
5. **Include test data** - Small example dataset
6. **Version your data** - Track changes

---

### Model Builder / Graphical Modeler

**Visual workflow tools**:

=== "QGIS"
    
    **Processing Modeler**:
    - Create visual workflows
    - Chain multiple tools
    - Save as reusable model
    - Share with others
    - Document automatically

=== "ArcGIS Pro"

    **Model Builder**:
    - Drag-and-drop interface
    - Connect tools visually
    - Run repeatedly
    - Share as toolbox

**Benefits**:
- Visual documentation
- Repeatable
- Batch processing
- Error checking

---

## Efficiency Tips

### Work Smarter

**Save time**:

1. **Use keyboard shortcuts** - Learn them!
2. **Create favorites** - Frequently used tools
3. **Templates** - Map layouts, projects
4. **Batch processing** - Multiple files at once
5. **Scripts** - Automate repetitive tasks
6. **Clip early** - Don't process entire world
7. **Lower resolution for testing** - Speed up iteration

---

### Processing Large Datasets

**Strategies**:

**Test on subset**:
- Clip to small area first
- Verify workflow
- Then run on full dataset

**Break into tiles**:
- Process tiles separately
- Merge at end

**Simplify**:
- Reduce resolution if acceptable
- Simplify geometries
- Remove unnecessary fields

**Increase memory**:
- Close other programs
- Adjust QGIS settings
- Use 64-bit software

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Organize systematically** - Consistent folder structure
2. **Name descriptively** - Future you will thank you
3. **Document everything** - Methods, sources, decisions
4. **Version control** - Track changes over time
5. **Check your work** - Validate before finalizing
6. **Make it reproducible** - Others should be able to recreate
7. **Save intermediate results** - Don't lose work
8. **Collaborate effectively** - Use relative paths, standard formats

</div>

---

## Further Reading

- [QGIS Project Best Practices](https://docs.qgis.org/latest/en/docs/user_manual/introduction/project_files.html)
- [GIS Data Management](https://www.esri.com/about/newsroom/arcuser/data-management-best-practices/)
- [Reproducible GIS Research](https://book.archivists.org/)

---

## Lab Exercise

!!! lab "Lab 12: Project Organization"
    In [Lab 12](../labs/lab12.md), you'll:
    
    - Set up a properly organized project folder structure
    - Create naming convention standards
    - Document a complete workflow
    - Build a processing model
    - Create a reproducible analysis
    - Practice troubleshooting techniques
    
    **Time Required**: 2-3 hours
    
    [:octicons-arrow-right-24: Go to Lab 12](../labs/lab12.md)

---

## Next Topic

You've learned professional workflows! Now explore advanced GIS topics:

[:octicons-arrow-right-24: Topic 13: Advanced Topics](13-advanced-topics.md)
