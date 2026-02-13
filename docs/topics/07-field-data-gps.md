# Topic 7: Field Data Collection and GPS

## Overview

Collecting your own spatial data in the field is fundamental to many GIS projects. GPS devices, mobile apps, and drones enable precise location recording and data capture for ground-truthing, surveys, and mapping.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand how GPS/GNSS works (trilateration)
- Recognize different GPS accuracy levels
- Collect field data using GPS devices and mobile apps
- Import GPS data into GIS software
- Understand UAV/drone remote sensing capabilities
- Plan field data collection campaigns
- Integrate field data with other GIS layers

---

## Global Positioning System (GPS)

### What is GPS?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**GPS** (Global Positioning System) is a satellite-based navigation system that provides location and time information anywhere on Earth where there's an unobstructed line of sight to four or more GPS satellites.

</div>

### GPS Constellation

**System components**:

**Space Segment**:
- 24+ satellites (nominal constellation)
- 6 orbital planes
- 4 satellites per plane
- Circular orbits at ~20,200 km altitude
- ~12-hour orbital period

**Control Segment**:
- Master Control Station (Colorado Springs)
- 5 Monitor Stations worldwide
  - Hawaii, Kwajalein, Ascension Island, Diego Garcia, Colorado
- Track satellites, update navigation messages
- Ensure orbit accuracy

**User Segment**:
- GPS receivers (phones, devices, survey equipment)
- Calculate position from satellite signals

---

### How GPS Works: Trilateration

**Basic principle**: Determine position by measuring distances to known locations (satellites)

**The Process**:

1. **Satellite signals**: Each satellite transmits:
   - Its precise location (ephemeris)
   - Current time (atomic clock)

2. **Distance calculation**: Receiver measures time delay
   - Signal travels at speed of light (~300,000 km/s)
   - Distance = Speed × Time

3. **Trilateration**: Need signals from multiple satellites
   - **1 satellite**: You're somewhere on a sphere
   - **2 satellites**: You're on a circle (intersection of spheres)
   - **3 satellites**: You're at 2 points (only 1 makes sense)
   - **4 satellites**: Precise 3D position + accurate time

!!! tip "Interactive Explanation"
    For an excellent visual explanation of GPS trilateration, visit:
    [ciechanow.ski/gps](https://ciechanow.ski/gps/)

![GPS Trilateration](../images/gps-trilateration.png)
*GPS uses distance measurements from multiple satellites to calculate position*

---

### GPS Accuracy Levels

| Type | Accuracy | Equipment | Cost | Use Case |
|------|----------|-----------|------|----------|
| **Consumer GPS** | 3-10m | Smartphone, basic GPS | $0-$200 | General navigation, recreation |
| **Recreational** | 2-5m | Handheld GPS (Garmin) | $200-$600 | Hiking, geocaching |
| **Mapping Grade** | 0.5-3m | Trimble, Garmin Pro | $1,000-$5,000 | GIS data collection |
| **Survey Grade** | 1-10cm | RTK GPS, Total Station | $10,000-$50,000 | Engineering, surveying |
| **Differential GPS** | < 1m | DGPS with corrections | $2,000-$10,000 | Professional mapping |

### Factors Affecting GPS Accuracy

**Satellite geometry** (HDOP/VDOP):
- More spread out = better
- Satellites clustered = worse

**Signal obstructions**:
- Buildings (urban canyons)
- Tree canopy
- Mountains, valleys

**Atmospheric conditions**:
- Ionosphere delays
- Troposphere delays
- Weather

**Multipath errors**:
- Signals bounce off buildings, ground
- Multiple paths to receiver = error

**Receiver quality**:
- Better antenna = better signal
- Processing power matters

---

### GNSS: Beyond GPS

**GNSS** = Global Navigation Satellite System (generic term)

**Major systems**:

| System | Country | Satellites | Status |
|--------|---------|------------|--------|
| **GPS** | USA | 31 | Fully operational |
| **GLONASS** | Russia | 24 | Fully operational |
| **Galileo** | Europe | 30+ | Operational |
| **BeiDou** | China | 35 | Fully operational |

**Multi-GNSS receivers** can use signals from all systems simultaneously:
- More satellites visible
- Better accuracy
- Improved reliability
- Faster position fixes

Modern smartphones use multi-GNSS!

---

## Field Data Collection Methods

### 1. Handheld GPS Devices

**Advantages**:
- Dedicated hardware, reliable
- Long battery life
- Rugged for fieldwork
- Waypoint management
- Track logging

**Common brands**:
- Garmin (GPSMAP series, eTrex)
- Trimble (Juno, Geo series)
- Bad Elf (mapping grade)

**Typical workflow**:
1. Mark waypoints at locations of interest
2. Record attributes (notes, photos)
3. Download to computer
4. Import into GIS (usually GPX or Shapefile format)

---

### 2. Smartphone/Tablet Apps

**Advantages**:
- Device you already have
- Camera integrated
- Easy data entry
- Internet connectivity
- Free or cheap apps

**Popular apps**:

| App | Platform | Features | Cost |
|-----|----------|----------|------|
| **SW Maps** | iOS/Android | Offline maps, forms, photos | Free-Paid |
| **Avenza Maps** | iOS/Android | Offline PDFs, georeferenced maps | Free-Paid |
| **QField** | Android | QGIS companion, syncs projects | Free |
| **Mergin Maps** | iOS/Android | QGIS-based, cloud sync | Free-Paid |
| **ArcGIS Field Maps** | iOS/Android | Esri ecosystem integration | Requires ArcGIS |
| **Collector for ArcGIS** | iOS/Android | Legacy Esri app | Requires ArcGIS |

**Workflow**:
1. Create data collection form (define fields)
2. Download offline basemaps
3. Collect data in field
4. Photos attached automatically
5. Sync to cloud or export

---

### 3. Survey-Grade GPS/GNSS

**Real-Time Kinematic (RTK)**:
- Uses base station + rover
- Real-time corrections
- Centimeter accuracy
- Expensive ($10k+)

**Post-Processed Kinematic (PPK)**:
- Corrections applied after fieldwork
- Slightly less expensive
- Still very accurate

**Use cases**:
- Property surveying
- Construction layout
- Scientific monitoring
- High-precision mapping

---

## Drones / UAVs for Data Collection

### What are UAVs?

**UAV** = Unmanned Aerial Vehicle (commonly called drones)

**Applications in GIS**:
- High-resolution imagery
- Elevation models (photogrammetry or LiDAR)
- Change detection
- 3D models
- Thermal imaging
- Multispectral imaging

---

### UAV Advantages

**Flexibility**:
- Fly when needed (cloud-free!)
- Choose exact study area
- Custom resolution
- Repeat as often as needed

**Cost-effective**:
- Cheaper than manned aircraft
- Much cheaper than satellites
- Own or rent equipment

**High resolution**:
- 1-5 cm pixels typical
- See individual plants, rocks, features

**Safety**:
- Access dangerous areas
- No personnel risk

---

### UAV Disadvantages

**Limitations**:
- **Area coverage**: Limited by battery (typically 20-40 min flight)
- **Weather dependent**: Can't fly in rain, high wind
- **Regulations**: FAA Part 107 license required (USA)
- **Flight planning**: Requires expertise
- **Processing**: Large data volumes, intensive computing
- **Equipment cost**: $1,000-$50,000+ for professional systems

---

### UAV Data Products

**Orthomosaic**:
- Stitched aerial photo
- Geometrically corrected
- True orthophoto (no distortion)
- GeoTIFF format

**Digital Surface Model (DSM)**:
- Elevation including buildings, trees
- Shows "top" of surfaces

**Digital Terrain Model (DTM)**:
- Bare earth elevation
- Vegetation/buildings removed

**3D Point Clouds**:
- Millions of XYZ points
- Can classify (ground, vegetation, buildings)
- .LAS format

**3D Meshes**:
- Textured 3D models
- OBJ, FBX formats
- For visualization

---

### UAV Workflow

1. **Mission Planning**:
   - Define study area
   - Set flight altitude (determines resolution)
   - Overlap settings (typically 70-80%)
   - Upload to drone

2. **Flight**:
   - Automated waypoint flight
   - Camera triggers automatically
   - Monitor progress

3. **Processing** (Photogrammetry software):
   - Structure from Motion (SfM)
   - Align photos
   - Build dense point cloud
   - Generate orthomosaic & DSM
   - Software: Pix4D, Agisoft, WebODM (free)

4. **GIS Integration**:
   - Import orthomosaic as raster
   - Import DSM for elevation analysis
   - Digitize features
   - Change detection

---

### UAV vs Satellite vs Manned Aircraft

| Platform | Resolution | Cost | Coverage | Flexibility | Update Frequency |
|----------|-----------|------|----------|-------------|------------------|
| **Satellite** | 0.3-30m | Free-$$$ | Global | Low | Days-weeks |
| **Manned Aircraft** | 5-50cm | $$$ | Regional | Medium | On demand |
| **UAV/Drone** | 1-10cm | $-$$ | Local | High | On demand |
| **Field GPS** | Point data | $ | Sparse | High | Real-time |

**Choose based on**:
- Study area size
- Required resolution
- Budget
- Timeline
- Update frequency needed

---

## GPS Data Formats

### Common GPS File Formats

**GPX** (GPS Exchange Format):
- XML-based
- Industry standard
- Waypoints, tracks, routes
- Human-readable
- Widely supported

**KML/KMZ** (Keyhole Markup Language):
- Google Earth format
- XML-based (KML)
- Compressed (KMZ)
- Includes styling

**GeoJSON**:
- JSON-based
- Web-friendly
- Lightweight
- Modern standard

**Shapefile**:
- Esri format
- Multiple files
- Attribute table included

**CSV with coordinates**:
- Simple text format
- Latitude, Longitude columns
- Easy to create/edit

---

### Converting GPS Data

**From GPS device to GIS**:

1. **Connect device or SD card**
2. **Export data**:
   - Usually GPX format
   - Sometimes proprietary format

3. **Import to GIS**:

=== "QGIS"

    **Add GPX**:
    - Layer → Add Layer → Add Vector Layer
    - Select GPX file
    - Choose waypoints, tracks, or routes
    
    **Or drag-and-drop** - QGIS recognizes GPX automatically

=== "ArcGIS Pro"

    **GPX to Features**:
    - Conversion Tools → From GPX → GPX to Features
    - Creates point, line, or polygon features

4. **Save as permanent layer**:
   - Export to GeoPackage or Shapefile
   - Specify coordinate system (usually WGS84)

---

## Planning Field Data Collection

### Before Fieldwork

**Define objectives**:
- What data do you need?
- What attributes to record?
- What accuracy required?

**Prepare forms/templates**:
- Design attribute schema
- Create dropdown lists for consistency
- Photo requirements

**Basemap preparation**:
- Download offline maps
- Create reference layers
- Mark target locations

**Equipment check**:
- Charge batteries
- Test GPS signal
- Backup power banks
- Extra SD cards

---

### During Fieldwork

**Best practices**:

1. **Allow GPS to settle** - Wait for good accuracy (< 5m)
2. **Record metadata** - Date, collector name, conditions
3. **Take photos** - Visual documentation crucial
4. **Notes** - Descriptive, detailed
5. **Check data** - Review attributes before moving on
6. **Backup regularly** - Don't lose a day's work!

**Environmental considerations**:
- Tree cover reduces accuracy
- Buildings block signals
- Open sky = best accuracy
- Avoid noon (satellite geometry)

---

### After Fieldwork

**Data validation**:
- Check for missing attributes
- Verify locations visually
- Look for outliers
- Ensure completeness

**Data cleaning**:
- Remove duplicate points
- Fix typos
- Standardize entries

**Integration**:
- Join with other datasets
- Reproject if needed
- Create final maps

**Backup**:
- Multiple copies
- Cloud storage
- External drive

---

## Integrating Field Data with GIS

### Typical Workflow

**Example**: Tree inventory survey

1. **Field collection**:
   - GPS points at each tree
   - Attributes: Species, DBH, Height, Condition
   - Photos of each tree

2. **Import to GIS**:
   - Load GPS points (GPX → GeoPackage)
   - Check coordinate system (WGS84)

3. **Reproject**:
   - Convert to local UTM for measurements
   - Preserves accuracy

4. **Analysis**:
   - Spatial distribution
   - Species composition
   - Tree density

5. **Map creation**:
   - Symbolize by species
   - Size by DBH
   - Labels for ID numbers

---

### Ground Truthing

**Purpose**: Verify remote sensing interpretations

**Workflow**:

1. **Generate sample points** from classification
2. **Navigate to points** using GPS
3. **Record actual land cover** at each point
4. **Compare** field data to satellite classification
5. **Calculate accuracy** (confusion matrix)
6. **Revise classification** if needed

**Essential for**:
- Land cover mapping
- Vegetation classification
- Change detection validation
- Model calibration

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **GPS uses trilateration** - Distance to 4+ satellites determines position
2. **Accuracy varies widely** - Consumer (3-10m) to survey-grade (<1cm)
3. **GNSS is broader than GPS** - Multiple satellite systems improve accuracy
4. **Smartphone apps work well** - For most GIS data collection needs
5. **Drones provide high-res data** - 1-10cm resolution, flexible timing
6. **Plan before fieldwork** - Define objectives, prepare forms, test equipment
7. **GPX is standard format** - Widely supported, easy to import
8. **Ground truthing validates** - Essential for remote sensing accuracy

</div>

---

## Further Reading

- [GPS.gov - How GPS Works](https://www.gps.gov/systems/gps/)
- [Interactive GPS Explanation](https://ciechanow.ski/gps/)
- [FAA Drone Regulations](https://www.faa.gov/uas)
- [QGIS GPS Tools Documentation](https://docs.qgis.org/3.28/en/docs/user_manual/working_with_gps/)

---

## Lab Exercise

!!! lab "Lab 7: GPS Field Data Collection"
    In [Lab 7](../labs/lab07.md), you'll:
    
    - Use a smartphone app to collect GPS waypoints
    - Record attributes and photos in the field
    - Import GPX data into QGIS
    - Clean and validate field data
    - Create a map from collected data
    - Calculate spatial statistics
    - Practice ground truthing with satellite imagery
    
    **Time Required**: 3-4 hours (includes fieldwork)
    
    [:octicons-arrow-right-24: Go to Lab 7](../labs/lab07.md)

---

## Next Topic

You've learned field data collection! Now back to raster analysis with DEMs:

[:octicons-arrow-right-24: Topic 8: Raster Data & DEMs](08-raster-data-dems.md)
