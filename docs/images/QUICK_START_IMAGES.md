# Quick Start: Adding Images to Your Course

## Step 1: Add the Banner (HIGHEST PRIORITY!)

**File needed**: `docs/images/banners/gis-banner.jpg`

The course is already configured to look for this banner on the home page. Simply add a GIS-related image:

### Options:
1. **Screenshot from QGIS**: Open QGIS with a nice map, screenshot, crop to 1200x400px
2. **Satellite imagery**: Use any Landsat/Sentinel image, crop and resize
3. **Stock image**: Search "GIS mapping" on Unsplash or Pixabay (free with attribution)

### Quick creation:
```bash
# Using ImageMagick (if installed):
convert your-image.jpg -resize 1200x400^ -gravity center -extent 1200x400 gis-banner.jpg
```

---

## Step 2: Test That Images Work

Add a simple test image to verify your setup:

1. Find ANY image on your computer  
2. Copy it to: `docs/images/topics/test.png`
3. Open any topic file (e.g., `docs/topics/02-spatial-data-models.md`)
4. Add this line anywhere:

```markdown
![Test Image](../images/topics/test.png)
```

5. Run `mkdocs serve` and check if image appears
6. If YES ✅ your image setup works!
7. If NO ❌ check the file path and file exists

---

## Step 3: Priority Images to Add

If you're short on time, just add these 7 images:

### 1. Banner (docs/images/banners/gis-banner.jpg)
Already referenced in `docs/index.md`

### 2. Vector vs Raster (docs/images/topics/vector-vs-raster-comparison.png)  
Already referenced in `docs/topics/02-spatial-data-models.md` (line ~54)

**What to show**: Same area shown as vector (clean lines) and raster (pixels)

**How to create**:
- Open QGIS
- Load a polygon layer (vector)
- Create a rasterized version
- Screenshot both side-by-side
- Export as PNG

### 3. Buffer Operation (docs/images/topics/buffer-operation.png)
Needs to be added to `docs/topics/06-vector-geoprocessing.md`

**What to show**: Features with buffer zones around them

**How to create**:
- In QGIS: Load any line or polygon layer
- Run Buffer tool (500m)
- Screenshot before/after
- Annotate with arrows

### 4. DEM Visualization (docs/images/topics/dem-visualization.png)
Needs to be added to `docs/topics/08-raster-data-dems.md`

**What to show**: Elevation model with hillshade

**How to create**:
- Download free DEM from USGS
- Style with hillshade in QGIS
- Screenshot
- Export as PNG

### 5. NDVI Example (docs/images/topics/ndvi-example.png)
Needs to be added to `docs/topics/10-remote-sensing.md`

**What to show**: NDVI calculated from satellite, color-coded green to red

**How to create**:
- Download Landsat/Sentinel from USGS or Copernicus
- Calculate NDVI: (NIR - Red) / (NIR + Red)
- Apply color ramp: red (low) to green (high)
- Screenshot

### 6. Interpolation Concept (docs/images/topics/interpolation-concept.png)
Needs to be added to `docs/topics/11-interpolation.md`

**What to show**: Points → continuous surface

**How to create**:
- Create random points with values
- Run IDW interpolation
- Screenshot points + resulting surface
- Side-by-side comparison

### 7. QGIS Interface (docs/images/projects/qgis-interface.png)
Needs to be added to `docs/projects/project1.md`

**What to show**: Clean QGIS interface with labels

**How to create**:
- Open QGIS
- Load sample data
- Screenshot
- Annotate: Map Canvas, Layers Panel, Toolbar, Browser

---

## Step 4: Image Placement in Markdown

### Basic Placement

```markdown
![Description](../images/topics/filename.png)
*Caption explaining what the figure shows*
```

**Path Notes**:
- From `docs/index.md` → use `images/banners/...`
- From `docs/topics/01-...md` → use `../images/topics/...`
- From `docs/projects/...md` → use `../images/projects/...`

The `../` means "go up one directory"

### Centered with Figure

```markdown
<figure markdown>
  ![Buffer Example](../images/topics/buffer-operation.png)
  <figcaption>Figure 3: Buffer operation creating 500m zones</figcaption>
</figure>
```

---

## Step 5: Where Images Are Referenced

### Already Added:
- ✅ `docs/index.md` - Banner image (line 3)
- ✅ `docs/topics/02-spatial-data-models.md` - Vector vs Raster (line 54)

### Need to Add:

**Topic 3: Coordinate Systems**
```markdown
![Geographic vs Projected](../images/topics/geographic-vs-projected.png)
*Figure: 3D Earth vs 2D flat map - the fundamental challenge of projections*
```
Add after discussing projections (around line 80)

**Topic 6: Vector Geoprocessing**
```markdown
![Buffer Operation](../images/topics/buffer-operation.png)
*Figure: Buffer creating zones around stream features*
```
Add in Buffer section (around line 100)

```markdown
![Clip Operation](../images/topics/clip-operation.png)
*Figure: Clip removes features outside the boundary*
```
Add in Clip section (around line 150)

**Topic 8: Raster Data & DEMs**
```markdown
![DEM Visualization](../images/topics/dem-visualization.png)
*Figure: Digital Elevation Model with hillshade rendering*
```
Add in DEM section (around line 80)

**Topic 9: Raster Analysis**
```markdown
![Map Algebra Example](../images/topics/map-algebra-example.png)
*Figure: Combining rasters using map algebra*
```
Add in Map Algebra section (around line 50)

```markdown
![Zonal Statistics Concept](../images/topics/zonal-statistics-concept.png)
*Figure: Calculating raster statistics within polygon zones*
```
Add in Zonal Statistics section (around line 200)

**Topic 10: Remote Sensing**
```markdown
![Electromagnetic Spectrum](../images/topics/electromagnetic-spectrum.png)
*Figure: EM spectrum with visible and infrared regions*
```
Add early when discussing EM radiation (around line 40)

```markdown
![True vs False Color](../images/topics/true-vs-false-color.png)
*Figure: True color (RGB) vs false color (NIR-R-G) composites*
```
Add in band combinations section (around line 120)

```markdown
![NDVI Example](../images/topics/ndvi-example.png)
*Figure: NDVI showing vegetation health*
```
Add in NDVI section (around line 180)

---

## Tips for Success

1. **Start with banner** - Makes biggest visual impact
2. **Screenshots work great** - Don't overcomplicate
3. **Optimize images** - Use TinyPNG.com before adding
4. **Test locally** - Always run `mkdocs serve` to check
5. **Consistent naming** - lowercase-with-hyphens.png
6. **Add captions** - The `*text*` under image is helpful

---

## Free Image Resources

- **QGIS/ArcGIS screenshots**: Create your own!
- **Satellite imagery**: USGS Earth Explorer, Copernicus
- **Icons/diagrams**: Draw.io, PowerPoint, Google Drawings
- **Stock photos**: Unsplash.com, Pixabay.com (free with attribution)

---

## Not Critical

The course works fine WITHOUT images - they just enhance learning. Add them as you have time!

The most important thing is getting the course content deployed. Images can be added incrementally over time.

For now, just add the **banner** and maybe **2-3 concept diagrams** if you have time.

**Happy mapping! 🗺️**
