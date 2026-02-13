# Topic 3: Coordinate Systems, Map Projections, and Datums

## Overview

One of the most important (and often challenging) aspects of GIS is understanding how we represent the 3D Earth on a 2D map. Coordinate reference systems are the foundation of all spatial analysis - get this wrong and your entire analysis will be wrong!

!!! warning "Critical Topic"
    Understanding coordinate systems is **essential** for proper GIS work. Projection mismatches are one of the most common sources of errors in GIS projects. Taking time to master this will save you countless hours of debugging later.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Distinguish between geographic and projected coordinate systems
- Explain what datums are and why they matter
- Recognize common coordinate systems (WGS84, UTM, State Plane)
- Identify types of projection distortion
- Reproject vector and raster data between coordinate systems
- Choose appropriate coordinate systems for analysis

---

## The Fundamental Challenge

### Earth is Round, Maps are Flat

**The problem**: The Earth is a 3D ellipsoid (slightly squashed sphere), but maps are 2D surfaces.

**The reality**: There is **no perfect solution** - every map projection involves some type of distortion!

Think about trying to flatten an orange peel - you'll either tear it, stretch it, or compress it. The same happens when we project Earth's surface onto a flat map.

!!! example "Test Your Understanding"
    Visit [The True Size](https://www.thetruesize.com) to see how map projections distort the size of countries. Try dragging Greenland to the equator - you'll be surprised at how much smaller it actually is!

---

## Geographic Coordinate Systems (GCS)

### What is a Geographic Coordinate System?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **Geographic Coordinate System (GCS)** uses angles (latitude and longitude) to define positions on Earth's three-dimensional curved surface.

</div>

### Key Components

**Unit of Measure**: Degrees (°)

**Coordinates**:
- **Latitude**: Measured relative to the equator
  - 0° at the equator
  - +90° at North Pole
  - -90° at South Pole
  - Lines run East-West (parallel to equator)
  
- **Longitude**: Measured relative to the Prime Meridian
  - 0° at Greenwich, England
  - +180° East
  - -180° West
  - Lines run North-South (converge at poles)

### Example Coordinates

| Location | Latitude | Longitude |
|----------|----------|-----------|
| San Luis Obispo, CA | 35.2828° N | -120.6596° W |
| Equator at Prime Meridian | 0° | 0° |
| North Pole | 90° N | Any longitude |

### The Graticule

The graticule is the network of latitude and longitude lines covering the Earth. Think of it as Earth's address system!

---

## Projected Coordinate Systems

### What is a Projected Coordinate System?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **Projected Coordinate System (PCS)** transforms locations from a three-dimensional spherical coordinate system to a two-dimensional planar system - essentially, flattening the Earth onto a map.

</div>

### Key Differences from GCS

| Aspect | Geographic (GCS) | Projected (PCS) |
|--------|------------------|-----------------|
| **Surface** | 3D curved (sphere/ellipsoid) | 2D flat (plane) |
| **Units** | Degrees | Linear units (meters, feet) |
| **Coordinates** | Latitude/Longitude | X/Y or Easting/Northing |
| **Measurements** | Difficult (curved surface) | Easy (flat surface) |
| **Distortion** | Minimal on globe | Always present |

### Why Use Projected Coordinates?

1. **Easy measurements**: Distances and areas are straightforward in meters/feet
2. **Accurate analysis**: Calculations work correctly on flat surfaces
3. **Practical mapping**: We view maps on flat screens and paper

!!! tip "When to Use What"
    - **Use GCS** (lat/lon) for:
        - Global datasets
        - Web mapping (Google Maps uses WGS84)
        - Data storage and exchange
    
    - **Use PCS** (projected) for:
        - Measuring distances and areas
        - Spatial analysis
        - Local/regional mapping

---

## Map Projections: Types and Distortion

### The Three Main Projection Surfaces

Map projections use geometric surfaces that can be "unrolled" into flat maps:

#### 1. Planar (Azimuthal)
- Projects onto a flat plane
- Plane touches Earth at one point
- Good for polar regions
- Examples: Lambert Azimuthal Equal Area

#### 2. Conical
- Projects onto a cone touching Earth
- Cone "unrolls" into a flat wedge
- Good for mid-latitude regions
- Examples: Albers Equal Area Conic, Lambert Conformal Conic

#### 3. Cylindrical
- Projects onto a cylinder wrapped around Earth
- Cylinder "unrolls" into a rectangle
- Good for equatorial regions or world maps
- Examples: Mercator, Transverse Mercator

![Projection Types](../images/projection-types.png)
*Three main projection surfaces: planar, conical, and cylindrical*

---

### Types of Distortion

Every projection distorts **at least one** of these properties:

| Property | What's Affected | Example Projections |
|----------|----------------|---------------------|
| **Shape (Conformal)** | Angles and local shapes | Mercator, Lambert Conformal Conic |
| **Area (Equal-area)** | Relative sizes | Albers Equal Area, Mollweide |
| **Distance (Equidistant)** | Distances from specific points | Azimuthal Equidistant |
| **Direction (Azimuthal)** | Directions from specific points | Gnomonic |

!!! warning "You Cannot Have It All!"
    No projection can preserve shape AND area simultaneously. You must choose which property is most important for your analysis!

### Common Projection Trade-offs

**Mercator Projection** ⚓
- Preserves shape (conformal)
- Great for navigation
- **Severely** distorts area near poles (Greenland looks huge!)
- Used for web maps

**Albers Equal Area Conic** 📊
- Preserves area (equal-area)
- Good for thematic maps
- Distorts shape
- Used for statistical mapping

---

## Common Coordinate Reference Systems

### WGS84 (EPSG:4326)

**Full Name**: World Geodetic System 1984

**Type**: Geographic Coordinate System

**When to Use**:
- GPS data
- Web mapping (Google Maps, OpenStreetMap)
- Global datasets
- Data exchange/storage

**Coordinates**: Latitude/Longitude in decimal degrees

---

### UTM (Universal Transverse Mercator)

**What is UTM?**

UTM divides the world into 60 vertical zones, each 6° of longitude wide. Each zone uses a Transverse Mercator projection optimized for that region.

**Key Features**:
- **Units**: Meters
- **Coordinates**: Easting (X) and Northing (Y)
- **Zones**: Numbered 1-60 from 180°W eastward
- **Hemispheres**: North and South variants

**California Coverage**:
- **UTM Zone 10N** (EPSG:32610): Western California
- **UTM Zone 11N** (EPSG:32611): Eastern California

**When to Use UTM**:
- Measuring distances and areas
- Regional analysis
- Field data collection
- When accuracy matters!

!!! tip "UTM is Usually Your Best Choice"
    For most regional GIS analysis in the US, UTM is the appropriate choice. It provides:
    
    - Accurate distance measurements
    - Simple units (meters)
    - Minimal distortion within a zone

### UTM Zone Map

![UTM Zones](../images/utm-zones.png)
*UTM zones covering North America*

---

### State Plane Coordinate System

**What is State Plane?**

A coordinate system designed specifically for US states, with each state having one or more zones optimized for its shape and extent.

**When to Use**:
- US-specific projects
- Working with government data (often in State Plane)
- Very high accuracy needed for surveying

**Units**: Usually feet (US Survey Feet or International Feet)

**Example**: California has 6 State Plane zones!

---

## Datums: The Foundation

### What is a Datum?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **datum** is a reference framework that defines:
- The size and shape of the Earth (ellipsoid)
- The origin and orientation of coordinate systems
- How to measure positions on Earth's surface

</div>

Think of a datum as the "starting point" for all measurements.

### Why Datums Matter

The same latitude/longitude can refer to different physical locations depending on the datum! This is because:

- Earth isn't a perfect sphere
- Different datums use different ellipsoid models
- Datums are optimized for different regions

**Example**: The same coordinates in NAD27 vs. NAD83 can differ by over 100 meters!

### Common Datums

| Datum | Region | When Used |
|-------|--------|-----------|
| **WGS84** | Global | GPS, web mapping, modern global data |
| **NAD83** | North America | US government data, current standard |
| **NAD27** | North America | Historical US data (pre-1990s) |
| **ED50** | Europe | Historical European data |

!!! warning "Datum Mismatch = Wrong Locations"
    Always check that all your data uses the same datum! Mixing datums will cause spatial misalignment.

---

## Reprojection: Transforming Coordinate Systems

### What is Reprojection?

**Reprojection** (also called transformation or warping) is the process of converting spatial data from one coordinate system to another.

### When to Reproject

You **must** reproject when:

1. **Mixing data sources** with different coordinate systems
2. **Measuring distances or areas** (reproject to a local projected system like UTM)
3. **Performing spatial analysis** (all layers must match!)
4. **Creating maps** (choose projection appropriate for your region)

!!! danger "Don't Skip Reprojection!"
    GIS software may display layers together even if they're in different coordinate systems, but any measurements or analysis will be WRONG!

### Reprojection Workflow

**For Vector Data**:
1. Identify current CRS of your data
2. Choose target CRS appropriate for your analysis
3. Use reprojection tool (maintains feature shapes)
4. Verify the output

**For Raster Data**:
1. Identify current CRS
2. Choose target CRS
3. Choose resampling method (Nearest Neighbor, Bilinear, Cubic)
4. Use warp/reproject tool
5. Verify output resolution and alignment

### Raster Reprojection Considerations

Raster reprojection is more complex because pixels must be:
1. **Warped**: Pixel outlines reprojected (creates irregular grid)
2. **Resampled**: Converted back to regular grid

This can change pixel values! Choose your resampling method carefully:

| Method | Best For | Preserves Values? |
|--------|----------|-------------------|
| **Nearest Neighbor** | Categorical data (land cover, classes) | Yes |
| **Bilinear** | Continuous data (elevation, temperature) | No (averages) |
| **Cubic** | Smooth continuous data (high-quality DEMs) | No (interpolates) |

---

## Choosing the Right Coordinate System

### Decision Framework

```
Is your analysis global or regional?
│
├─ Global → Use WGS84 (EPSG:4326)
│
└─ Regional
   │
   ├─ Do you need to measure distances/areas?
   │  │
   │  ├─ Yes → Use UTM for your zone
   │  │         or State Plane if in US
   │  │
   │  └─ No → WGS84 is fine
   │
   └─ What's your existing data in?
      → Consider matching existing CRS
        to avoid reprojection errors
```

### Best Practices

1. **Check your data**: Always verify the CRS of new data
2. **Project early**: Reproject at the start of your workflow
3. **Match your region**: Use UTM zone that covers your study area
4. **Document everything**: Note which CRS you used and why
5. **Never assume**: Even if data displays correctly, check the CRS!

---

## EPSG Codes

**EPSG** codes are unique numeric identifiers for coordinate reference systems, maintained by the International Association of Oil & Gas Producers (formerly European Petroleum Survey Group).

### Common EPSG Codes

| EPSG Code | Coordinate System | Description |
|-----------|-------------------|-------------|
| **4326** | WGS 84 | Geographic, lat/lon, global |
| **3857** | Web Mercator | Google Maps, OpenStreetMap |
| **32610** | UTM Zone 10N (WGS84) | Western California, Oregon, Washington |
| **32611** | UTM Zone 11N (WGS84) | Eastern California, Nevada, Idaho |
| **26910** | UTM Zone 10N (NAD83) | Same region, NAD83 datum |
| **2227** | CA State Plane Zone 3 | San Francisco Bay Area |

Find EPSG codes at: [epsg.io](https://epsg.io)

---

## Practical Examples

### Example 1: Local Analysis

**Task**: Measure the area of a park in San Luis Obispo

**Solution**:
1. Data comes in WGS84 (EPSG:4326)
2. Reproject to UTM Zone 10N (EPSG:32610)
3. Calculate area (result in square meters)
4. Convert to acres if needed

**Why**: UTM provides accurate area measurements

---

### Example 2: Web Mapping

**Task**: Create an interactive web map

**Solution**:
- Keep data in WGS84 (EPSG:4326) or Web Mercator (EPSG:3857)
- Most web mapping libraries expect these

**Why**: Standard for web mapping platforms

---

### Example 3: Multi-Region Study

**Task**: Compare forests in California and Colorado

**Solution**:
- California: UTM Zone 10N or 11N
- Colorado: UTM Zone 13N
- For combined analysis: Reproject both to Albers Equal Area Conic (preserves area for comparison)

**Why**: Equal-area projection preserves size relationships

---

## Troubleshooting Common Issues

### "My Layers Don't Align"

**Cause**: Different coordinate systems or datums

**Solution**:
1. Check CRS of each layer (Layer Properties → Information)
2. Reproject all to same CRS
3. Verify they align properly

---

### "My Distances are Wrong"

**Cause**: Measuring in geographic coordinates (degrees)

**Solution**:
- Reproject to projected CRS (UTM, State Plane)
- Re-measure in appropriate units

---

### "Reprojection Failed"

**Cause**: Missing projection files or corrupted data

**Solution**:
- Verify data isn't corrupted
- Try different reprojection method
- Check for required transformation grids

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **No perfect projection** - all projections distort something
2. **GCS vs PCS** - Geographic uses degrees (lat/lon), Projected uses meters/feet (X/Y)
3. **UTM for analysis** - Use UTM when measuring distances or areas regionally
4. **Always reproject** - Match all data to same CRS before analysis
5. **Check your datums** - Different datums = different positions!
6. **EPSG codes** - Use these to precisely specify coordinate systems
7. **Document your choice** - Record which CRS and why you chose it

</div>

---

## Further Reading

- [QGIS Documentation: Projections](https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/coordinate_reference_systems.html)
- [ESRI: Coordinate Systems](https://pro.arcgis.com/en/pro-app/latest/help/mapping/properties/coordinate-systems-and-projections.htm)
- [EPSG.io](https://epsg.io) - Look up any coordinate system
- Interactive: [The True Size](https://www.thetruesize.com)

---

## Lab Exercise

!!! lab "Lab 3: Working with Projections"
    In [Lab 3](../labs/lab03.md), you'll:
    
    - Identify coordinate systems of your data
    - Compare distortion in different projections visually
    - Reproject vector and raster data
    - Measure distances in different coordinate systems
    - Fix projection mismatches
    - Choose appropriate CRS for analysis
    
    **Time Required**: 2-3 hours
    
    [:octicons-arrow-right-24: Go to Lab 3](../labs/lab03.md)

---

## Next Topic

Now that you understand coordinate systems, let's learn how to create and edit spatial data:

[:octicons-arrow-right-24: Topic 4: Data Creation & Editing](04-data-creation.md)
