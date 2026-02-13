# Topic 10: Remote Sensing Fundamentals

## Overview

Remote sensing is the science of obtaining information about Earth from a distance using satellites, aircraft, and drones. It provides critical data for monitoring vegetation, land cover, water resources, climate, and environmental change.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand the electromagnetic spectrum and spectral bands
- Distinguish between active and passive remote sensing
- Work with multispectral satellite imagery
- Calculate and interpret spectral indices (NDVI, NDWI, etc.)
- Understand the resolution trade-off (spatial, temporal, spectral)
- Download and process satellite data
- Apply remote sensing to environmental problems

---

## What is Remote Sensing?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Remote sensing** is the science of obtaining information about objects or areas from a distance, typically from aircraft or satellites.

</div>

**Simple analogy**: Just as X-rays and MRIs revolutionized medical imaging ~100 years ago, remote sensing is revolutionizing Earth imaging today!

### Key Components

1. **Energy source** (Sun or sensor)
2. **Interaction with target** (Earth's surface)
3. **Sensor** (detects reflected/emitted energy)
4. **Data transmission** (satellite → ground station)
5. **Analysis** (GIS processing!)

### Why Remote Sensing Matters

- **Global coverage**: Monitor entire planet
- **Temporal**: Track changes over time
- **Cost-effective**: Cheaper than field surveys
- **Objective**: Consistent measurements
- **Inaccessible areas**: Reach anywhere

!!! quote "Scale of Data"
    Satellites generate **>10 TB of data per day**. We need GIS skills to make sense of it!

---

## The Electromagnetic Spectrum

### What is the EM Spectrum?

**EM radiation** is energy that travels as waves. The spectrum includes all types from radio waves to gamma rays.

**Humans see** a tiny portion: Visible light (400-700 nm)

**Other parts** are used for:
- **Radio waves**: Communication, WiFi
- **Microwaves**: Cell phones, radar
- **Infrared**: Remote controls, thermal imaging
- **UV**: Sterilization, detecting minerals
- **X-rays**: Medical imaging

![EM Spectrum](../images/em-spectrum.png)
*The electromagnetic spectrum showing different wavelength regions*

---

### Human Vision

**Humans have 3 types of cones** (photoreceptors):
- Red cone (560-580 nm)
- Green cone (520-565 nm)
- Blue cone (420-440 nm)

**Combining RGB** = Full color vision

**Comparison**:
- **Dogs**: 2 cones (dichromatic) - limited color
- **Mantis shrimp**: 12 cones! (Can see UV, polarized light)
- **Satellites**: Many bands beyond visible!

---

### The Key Insight

**Different materials reflect different wavelengths!**

- **Healthy vegetation**: High NIR reflection, low red
- **Water**: Absorbs NIR, reflects blue
- **Soil**: Varies by composition
- **Urban**: High reflection in visible, low in NIR

**This is the foundation of remote sensing analysis!**

---

## Types of Remote Sensing

### Passive Remote Sensing

**Definition**: Measures natural energy reflected or emitted by Earth

**Energy source**: Sun (daytime) or Earth's heat (thermal)

**Examples**:
- **Optical satellites**: Landsat, Sentinel-2, MODIS
- **Cameras**: Aerial photography, drones
- **Thermal**: ASTER, Landsat thermal bands

**Advantages**:
- Simple, well-understood
- Global coverage
- Long time series available

**Limitations**:
- Requires sunlight (optical)
- Affected by clouds
- Can't penetrate vegetation canopy

---

### Active Remote Sensing

**Definition**: Sensor emits energy and measures what returns

**Examples**:

**RADAR** (Radio Detection and Ranging):
- Microwave pulses
- Penetrates clouds
- Measures surface roughness
- Example: Sentinel-1

**LiDAR** (Light Detection and Ranging):
- Laser pulses
- 3D point clouds
- High-resolution elevation
- Example: Airborne LiDAR

**SONAR**:
- Sound waves underwater
- Bathymetry (ocean depth)

**Advantages**:
- Works day or night
- Penetrates clouds (radar)
- 3D information (LiDAR)
- Measures distances directly

**Limitations**:
- More complex
- Requires specialized sensors
- Expensive

---

## Spectral Bands

### What is a Spectral Band?

A **band** is a specific range of wavelengths that a sensor can detect.

**Multispectral** = Multiple bands (typically 3-10)
<br>**Hyperspectral** = Many narrow bands (100+)

### Common Spectral Bands

| Band Name | Wavelength (μm) | Use | What it Shows |
|-----------|----------------|-----|---------------|
| **Blue** | 0.45-0.52 | Water bodies, clouds, atmosphere | Water depth, sediment |
| **Green** | 0.52-0.60 | Vegetation vigor | Plant health, algae |
| **Red** | 0.63-0.69 | Chlorophyll absorption | Bare soil, urban areas |
| **NIR** | 0.77-0.90 | Vegetation biomass | Healthy vegetation (bright) |
| **SWIR 1** | 1.55-1.75 | Moisture content | Vegetation moisture, geology |
| **SWIR 2** | 2.08-2.35 | Geology, moisture | Minerals, soil moisture |
| **Thermal** | 10.4-12.5 | Temperature | Surface temperature, fires |

---

### Band Combinations

**True Color** (RGB):
- Red band → Red
- Green band → Green
- Blue band → Blue
- **Result**: Natural looking image

**False Color** (NIR-R-G):
- NIR band → Red
- Red band → Green
- Green band → Blue
- **Result**: Vegetation appears bright red!

!!! tip "Why Use False Color?"
    Healthy vegetation reflects strongly in NIR (which we can't see). By displaying NIR as red, vegetation "pops" - making forests, crops, and vegetation easy to identify!

**Other Combinations**:
- **Agriculture** (SWIR-NIR-Blue): Crops vs soil
- **Natural Color** (SWIR-NIR-Green): Enhanced natural
- **Vegetation Analysis** (NIR-SWIR-Red): Vegetation health

---

## Major Satellite Missions

### Landsat Program (NASA/USGS)

**Mission**: Longest-running Earth observation program (1972-present)

**Current**: Landsat 8 & 9

**Specifications**:
- **Resolution**: 30m (visible/NIR), 100m (thermal)
- **Revisit time**: 16 days
- **Bands**: 11 (visible, NIR, SWIR, thermal)
- **Swath**: 185 km

**Best for**:
- Land cover change
- Urban growth
- Deforestation
- Agriculture

**Access**: Free via [USGS EarthExplorer](https://earthexplorer.usgs.gov)

---

### Sentinel-2 (ESA/Copernicus)

**Mission**: European monitoring program

**Specifications**:
- **Resolution**: 10m (visible/NIR), 20m (SWIR)
- **Revisit time**: 5 days (2 satellites)
- **Bands**: 13 (visible, NIR, SWIR)
- **Swath**: 290 km

**Best for**:
- Agriculture monitoring
- Forest health
- Land cover mapping
- Water quality

**Access**: Free via [Copernicus Data Space](https://dataspace.copernicus.eu)

---

### MODIS (NASA)

**Mission**: Moderate Resolution Imaging Spectroradiometer

**Specifications**:
- **Resolution**: 250m-1km
- **Revisit time**: Daily!
- **Bands**: 36
- **Coverage**: Global

**Best for**:
- Large-scale monitoring
- Daily cloud-free composites
- Vegetation phenology
- Fire detection
- Ocean color

**Access**: Free via [NASA Earthdata](https://earthdata.nasa.gov)

---

### Satellite Comparison

| Satellite | Resolution | Revisit | Bands | Best For |
|-----------|-----------|---------|-------|----------|
| **Landsat** | 30m | 16 days | 11 | Regional mapping |
| **Sentinel-2** | 10m | 5 days | 13 | Agriculture, detailed |
| **MODIS** | 250m-1km | Daily | 36 | Global, frequent |
| **Planet** | 3m | Daily | 4 | High-res monitoring |
| **WorldView** | 0.3m | On demand | 8 | Very high detail |

---

## Resolution Trade-offs

### The 4 Types of Resolution

**1. Spatial Resolution**
- Pixel size (e.g., 30m, 10m, 1m)
- Higher = more detail, but...

**2. Temporal Resolution**
- Revisit time (e.g., daily, weekly)
- Higher frequency = better monitoring, but...

**3. Spectral Resolution**
- Number of bands
- More bands = more info, but...

**4. Radiometric Resolution**
- Bit depth (8-bit, 12-bit, 16-bit)
- Higher = more sensitivity, but...

### The Trade-off

**You can't have it all!**

- High spatial resolution → Lower coverage, less frequent
- High temporal resolution → Lower spatial resolution
- More spectral bands → More data volume

**Example**:
- **Landsat**: 30m, every 16 days, 11 bands
- **MODIS**: 250m, every day, 36 bands
- **WorldView**: 0.3m, on-demand, 8 bands (expensive!)

**Choose based on your needs!**

---

## Spectral Indices

### What are Spectral Indices?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Spectral indices** are mathematical combinations of spectral bands designed to highlight specific features or phenomena.

</div>

**Purpose**: Enhance differences between features

**How**: Combine bands using ratios, differences, or normalized differences

---

### NDVI (Normalized Difference Vegetation Index)

**The most important and widely-used index!**

**Formula**:
```
NDVI = (NIR - Red) / (NIR + Red)
```

**Why it works**:
- **Healthy vegetation**:
  - Absorbs red (chlorophyll)
  - Reflects NIR (cell structure)
  - **High NDVI** (0.6 - 0.9)

- **Bare soil/urban**:
  - Similar red and NIR
  - **Low NDVI** (0.1 - 0.3)

- **Water**:
  - Absorbs both
  - **Negative NDVI** (< 0)

**Value ranges**:

| NDVI Value | Interpretation |
|------------|----------------|
| **< 0** | Water, clouds, snow |
| **0 - 0.1** | Barren rock, sand |
| **0.1 - 0.2** | Sparse vegetation |
| **0.2 - 0.4** | Grassland, shrubs |
| **0.4 - 0.6** | Crops, moderate vegetation |
| **0.6 - 0.9** | Dense vegetation, forests |

**Applications**:
- Crop health monitoring
- Drought assessment
- Deforestation detection
- Vegetation phenology
- Biomass estimation

![NDVI Example](../images/ndvi-example.png)
*NDVI map showing healthy vegetation in green*

---

### Calculating NDVI

**For Landsat 8**:
- Band 4 = Red
- Band 5 = NIR

**Expression**:
```
NDVI = (Band5 - Band4) / (Band5 + Band4)
```

**For Sentinel-2**:
- Band 4 = Red
- Band 8 = NIR

**Expression**:
```
NDVI = (Band8 - Band4) / (Band8 + Band4)
```

**In QGIS Raster Calculator**:
```
("NIR@1" - "Red@1") / ("NIR@1" + "Red@1")
```

---

### Other Important Indices

**NDWI (Normalized Difference Water Index)**

**Formula**:
```
NDWI = (Green - NIR) / (Green + NIR)
```

**Purpose**: Detect water bodies
- **High values** (>0.3) = Water
- **Low values** = Land

**Use**: Water extent mapping, flood monitoring

---

**NDBI (Normalized Difference Built-up Index)**

**Formula**:
```
NDBI = (SWIR - NIR) / (SWIR + NIR)
```

**Purpose**: Identify urban/built areas
- **High values** = Buildings, pavement
- **Low values** = Vegetation, water

**Use**: Urban growth tracking

---

**NBR (Normalized Burn Ratio)**

**Formula**:
```
NBR = (NIR - SWIR) / (NIR + SWIR)
```

**Purpose**: Detect burn scars from fires
- **Before fire**: High NBR (healthy veg)
- **After fire**: Low NBR (burned area)

**dNBR** (difference NBR) = NBR_before - NBR_after

**Use**: Fire severity mapping, burn area delineation

---

**EVI (Enhanced Vegetation Index)**

**Formula**:
```
EVI = 2.5 * (NIR - Red) / (NIR + 6*Red - 7.5*Blue + 1)
```

**Purpose**: Improved version of NDVI
- Less affected by soil background
- Less saturated in dense vegetation
- Better in high biomass areas

**Use**: Tropical forests, dense vegetation monitoring

---

### Time Series Analysis with Indices

**Power of satellite time series**: Track changes over time!

**Example applications**:

**Crop Monitoring**:
- NDVI time series shows crop phenology
- Planting → Growth → Maturity → Harvest
- Compare to previous years

**Drought Detection**:
- Declining NDVI indicates stress
- Compare current to historical average
- Identify affected areas

**Forest Health**:
- Sudden NDVI drop = Disturbance
- Could be fire, disease, logging
- Monitor recovery over time

**Urban Expansion**:
- NDVI declining, NDBI increasing
- Track development over years

---

## Working with Satellite Data

### Downloading Sentinel-2 Data

**Copernicus Data Space Browser**:
1. Go to: [dataspace.copernicus.eu](https://dataspace.copernicus.eu)
2. Draw area of interest
3. Set date range
4. Apply cloud cover filter (< 10%)
5. Select product (S2 L2A - atmospherically corrected)
6. Download bands needed

**For NDVI**: Download Band 4 (Red) and Band 8 (NIR)

---

### Downloading Landsat Data

**USGS EarthExplorer**:
1. Go to: [earthexplorer.usgs.gov](https://earthexplorer.usgs.gov)
2. Define search area
3. Date range
4. Datasets → Landsat → Landsat Collection 2 Level-2
5. Cloud cover filter
6. Search and download

**For NDVI**: Download Band 4 (Red) and Band 5 (NIR)

---

### Pre-processing Satellite Data

**Typical workflow**:

1. **Atmospheric correction** (if not L2A product)
2. **Cloud masking** - Remove clouds
3. **Mosaicking** - Combine tiles if needed
4. **Clipping** - Extract study area
5. **Resampling** - Match resolutions if needed
6. **Index calculation** - NDVI, NDWI, etc.

**Good news**: Landsat Collection 2 and Sentinel-2 L2A are already atmospherically corrected!

---

## Practical Applications

### Agriculture

**Crop Health Monitoring**:
- NDVI time series reveals crop stress
- Early detection of problems
- Variable rate fertilization

**Yield Prediction**:
- Peak NDVI correlates with yield
- Monitor throughout season

**Field Boundaries**:
- Segment fields using classification
- Track individual field performance

---

### Forestry

**Deforestation Detection**:
- Sudden NDVI decline
- Before/after comparison
- Quantify area lost

**Forest Health**:
- Gradual NDVI decline = stress
- Could indicate disease, drought
- Monitor recovery

**Biomass Estimation**:
- NDVI correlates with biomass
- Create biomass maps

---

### Water Resources

**Water Body Mapping**:
- NDWI highlights water
- Track reservoir levels
- Monitor flood extent

**Water Quality**:
- Chlorophyll concentration (algal blooms)
- Turbidity (sediment)
- Early warning system

---

### Disaster Response

**Fire Monitoring**:
- Active fire detection (thermal bands)
- Burn severity mapping (NBR)
- Recovery monitoring

**Flood Mapping**:
- Rapid water extent mapping
- Compare to baseline
- Assess damage

---

## Change Detection

### Temporal Analysis

**Goal**: Identify what changed between dates

**Methods**:

**1. Direct Comparison**:
```
Change = Image_2025 - Image_2024
```

**2. Index Differencing**:
```
dNDVI = NDVI_2025 - NDVI_2024
```

**Positive** = Increase (greening, growth)
<br>**Negative** = Decrease (loss, stress)

**3. Classification Comparison**:
- Classify each date
- Compare categories
- From-To matrix

---

### Example: Detect Vegetation Loss

**Steps**:

1. Calculate NDVI for both dates
2. Compute difference:
   ```
   dNDVI = NDVI_new - NDVI_old
   ```
3. Threshold for significant change:
   ```
   Loss = dNDVI < -0.2
   ```
4. Vectorize to create polygons
5. Calculate area of loss

**Result**: Map and quantify vegetation loss

---

## Best Practices

### Data Selection

1. **✅ Choose appropriate satellite** - Match resolution to needs
2. **✅ Filter by cloud cover** - <10% ideally
3. **✅ Select correct season** - Consider phenology
4. **✅ Use L2A products** - Pre-corrected data
5. **✅ Check for quality flags** - Clouds, shadows, snow

---

### Processing

1. **✅ Mask clouds** - Don't include in analysis
2. **✅ Use appropriate indices** - Match to application
3. **✅ Validate with ground truth** - Field data when possible
4. **✅ Consider multiple dates** - Time series more robust
5. **✅ Document methods** - Processing steps, formulas

---

### Analysis

1. **✅ Understand seasonality** - Vegetation changes naturally
2. **✅ Compare similar dates** - Same time of year
3. **✅ Use appropriate thresholds** - NDVI varies by biome
4. **✅ Visual inspection** - Always check results
5. **✅ Statistical validation** - Accuracy assessment

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Remote sensing = obtaining info from distance** - Satellites, aircraft, drones
2. **EM spectrum has many bands** - We only see visible light
3. **Different materials reflect differently** - Foundation of RS analysis
4. **NDVI is king** - (NIR - Red) / (NIR + Red) for vegetation
5. **Resolution trade-offs exist** - Spatial vs temporal vs spectral
6. **Free data available** - Landsat, Sentinel-2, MODIS
7. **Spectral indices enhance features** - NDVI, NDWI, NBR, etc.
8. **Time series reveals change** - Compare dates to detect trends

</div>

---

## Further Reading

- [NASA EarthData](https://earthdata.nasa.gov/)
- [Copernicus Open Access Hub](https://dataspace.copernicus.eu/)
- [USGS Landsat Missions](https://www.usgs.gov/landsat-missions)
- [Awesome Spectral Indices](https://awesome-ee-spectral-indices.readthedocs.io/)

---

## Lab Exercise

!!! lab "Lab 10: Remote Sensing & NDVI Analysis"
    In [Lab 10](../labs/lab10.md), you'll:
    
    - Download Sentinel-2 satellite imagery
    - Calculate NDVI from Red and NIR bands
    - Create true color and false color composites
    - Perform NDVI time series analysis
    - Detect vegetation change over time
    - Calculate other spectral indices (NDWI, NBR)
    - Interpret results and create maps
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 10](../labs/lab10.md)

---

## Next Topic

You've completed the core analytical topics! Next, we'll explore more advanced applications:

[:octicons-arrow-right-24: Topic 11: Interpolation & Zonal Statistics](11-interpolation.md)
