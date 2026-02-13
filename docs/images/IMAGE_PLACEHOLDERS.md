# Image Placeholders - What to Add

This file lists all image placeholders throughout the course and describes what each image should contain.

## Banner Images

### `banners/gis-banner.jpg`
- Course header banner for home page
- Suggested: Satellite imagery, map overlays, or GIS visualization
- Dimensions: 1200x400px recommended
- Can be created using: QGIS screenshot, satellite imagery, or stock GIS imagery

---

## Topic Images

### Topic 1: What is GIS?

**`topics/gis-layers-concept.png`**
- Layered GIS data visualization
- Show different layers (roads, buildings, elevation) stacked

**`topics/gis-applications.png`**
- Collage or grid showing diverse GIS applications
- Examples: emergency response, urban planning, environmental monitoring

### Topic 2: Spatial Data Models

**`topics/vector-vs-raster-comparison.png`**
- Side-by-side comparison of vector and raster data
- Same feature (e.g., lake) shown in both formats

**`topics/vector-geometry-types.png`**
- Illustration of points, lines, and polygons
- Real-world examples for each type

**`topics/raster-structure.png`**
- Diagram showing raster grid structure
- Include: cells, rows, columns, values

### Topic 3: Coordinate Systems

**`topics/geographic-vs-projected.png`**
- Earth sphere vs flat map
- Show distortion concept

**`topics/projection-distortions.png`**
- Famous projections showing different distortions
- Mercator, Robinson, etc.

**`topics/utm-zones-map.png`**
- World map showing UTM zones
- Highlight a specific zone

**`topics/california-projections.png`**
- Same area in different projections
- Show shape/area differences

### Topic 4: Data Creation

**`topics/digitizing-workflow.png`**
- Screenshot of digitizing in QGIS
- Show snapping, editing tools

**`topics/topology-errors.png`**
- Visual examples of gaps, overlaps, dangles
- Annotated with error types

### Topic 5: Table Management

**`topics/attribute-table-example.png`**
- QGIS attribute table screenshot
- Show typical field types and data

**`topics/table-join-diagram.png`**
- Conceptual diagram of table join
- Show matching fields

**`topics/spatial-join-concept.png`**
- Visual showing spatial join operation
- Points joining to polygons, etc.

### Topic 6: Vector Geoprocessing

**`topics/buffer-operation.png`**
- Before/after buffer visualization
- Show zones created around features

**`topics/clip-operation.png`**
- Clipping demonstration
- Input → Clip boundary → Output

**`topics/intersect-union-difference.png`**
- Three operations shown side-by-side
- Visual results comparison

### Topic 7: Field Data & GPS

**`topics/gps-trilateration.png`**
- Diagram showing satellite trilateration
- 4 satellites determining position

**`topics/gps-accuracy-comparison.png`**
- Visual showing different GPS accuracy levels
- Consumer vs survey-grade

**`topics/mobile-gis-workflow.png`**
- Flowchart: design → collect → sync → analyze

### Topic 8: Raster Data & DEMs

**`topics/dem-visualization.png`**
- Digital Elevation Model rendered
- Hillshade or 3D view

**`topics/slope-aspect-hillshade.png`**
- Three-panel showing slope, aspect, hillshade
- Same DEM, different derivatives

**`topics/spectral-bands.png`**
- Satellite image bands separately
- RGB and NIR shown

### Topic 9: Raster Analysis

**`topics/map-algebra-example.png`**
- Visual example of raster calculator
- Input rasters → operation → output

**`topics/reclassification-example.png`**
- Before/after reclassification
- Show value ranges changing

**`topics/zonal-statistics-concept.png`**
- Diagram showing zones over raster
- Statistics being calculated

### Topic 10: Remote Sensing

**`topics/electromagnetic-spectrum.png`**
- EM spectrum diagram
- Highlight visible and NIR regions

**`topics/true-vs-false-color.png`**
- Same area in true color (RGB) and false color (NIR-R-G)
- Side-by-side comparison

**`topics/ndvi-example.png`**
- NDVI calculation visualization
- Color scale showing vegetation health

**`topics/satellite-comparison.png`**
- Landsat vs Sentinel imagery
- Show resolution differences

### Topic 11: Interpolation

**`topics/interpolation-concept.png`**
- Points → continuous surface
- Show transition

**`topics/idw-vs-kriging.png`**
- Same data interpolated with both methods
- Compare results

**`topics/semivariogram.png`**
- Example semivariogram plot
- Show range, sill, nugget

### Topic 12: Workflow Design

**`topics/gis-workflow-example.png`**
- Flowchart of typical GIS project
- Boxes and arrows

**`topics/folder-organization.png`**
- Screenshot of well-organized project folder
- Show structure

### Topic 13: Advanced Topics

**`topics/3d-visualization.png`**
- 3D terrain or building visualization
- QGIS 3D view

**`topics/network-analysis.png`**
- Route calculation visualization
- Show shortest path

### Topic 14: Modern Mapmaking

**`topics/web-map-example.png`**
- Screenshot of interactive web map
- Leaflet or ArcGIS Online

**`topics/storymap-example.png`**
- StoryMap screenshot
- Show narrative + map integration

### Topic 15: Synthesis

**`topics/gis-career-paths.png`**
- Diagram or infographic of GIS career options
- Various job roles and sectors

---

## Project Images

**`projects/qgis-interface.png`**
- Clean QGIS interface screenshot
- Labeled components

**`projects/arcgis-interface.png`**
- ArcGIS Pro interface screenshot
- Key areas labeled

**`projects/map-elements.png`**
- Example map showing all required elements
- Legend, scale bar, north arrow, etc.

**`projects/project-workflow.png`**
- Generic project workflow diagram
- Can be reused across projects

---

## Creating These Images

### Option 1: Create Your Own
- Use QGIS/ArcGIS screenshots
- Create diagrams in Draw.io
- Use PowerPoint and export as PNG

### Option 2: Use Placeholders
- Leave as-is and add images later
- Placeholder text helps students know what to expect

### Option 3: Find Open Source Images
- Wikimedia Commons
- USGS imagery
- OpenStreetMap screenshots
- Ensure proper attribution!

---

## Priority Images (Most Important)

If you can only add a few images, start with these:

1. **Banner**: `banners/gis-banner.jpg` - First impression!
2. **Vector vs Raster**: `topics/vector-vs-raster-comparison.png` - Fundamental concept
3. **Projections**: `topics/geographic-vs-projected.png` - Critical to understand
4. **Buffer**: `topics/buffer-operation.png` - Common operation
5. **NDVI**: `topics/ndvi-example.png` - Powerful remote sensing example
6. **Interpolation**: `topics/interpolation-concept.png` - Complex concept needs visual
7. **QGIS Interface**: `projects/qgis-interface.png` - Students need reference

---

## Image Dimensions Guide

- **Banners**: 1200x400px
- **Screenshots**: 1200-1600px wide
- **Diagrams**: 800-1200px wide
- **Icons**: 256x256px or SVG
- **Comparison images**: 1400px wide (700px per panel)

Keep images crisp but optimized (<500KB each when possible)!
