# Course Images Directory

## Directory Structure

```
images/
├── banners/           # Course banner and header images
├── topics/            # Topic-specific images
├── projects/          # Project-related screenshots/diagrams
└── labs/              # Lab tutorial screenshots
```

## How to Add Images

### 1. Add Your Image Files

Place image files in the appropriate subdirectory:
- Course banner: `images/banners/gis-banner.jpg`
- Topic images: `images/topics/topic-01-example.png`
- Project images: `images/projects/project1-screenshot.png`

### 2. Reference Images in Markdown

**Basic syntax**:
```markdown
![Alt Text](../images/folder/filename.png)
```

**With caption**:
```markdown
![Map Example](../images/topics/buffer-example.png)
*Figure 1: Buffer operation creating 500m zones around features*
```

**Centered with styling** (if using Material theme):
```markdown
<figure markdown>
  ![Buffer Example](../images/topics/buffer-example.png)
  <figcaption>Buffer operation example</figcaption>
</figure>
```

### 3. Recommended Image Formats

- **PNG**: Screenshots, diagrams, maps with transparency
- **JPG**: Photos, satellite imagery, large images
- **SVG**: Icons, logos, simple graphics (scales perfectly)
- **GIF**: Animated tutorials (use sparingly)

### 4. Image Guidelines

**File Naming**:
- Use lowercase
- Use hyphens instead of spaces
- Be descriptive: `coordinate-system-comparison.png`
- NOT: `Image1.PNG` or `Screen Shot 2024.png`

**File Size**:
- Optimize images before adding (use tools like TinyPNG)
- Target < 500 KB per image
- Screenshots: 1200-1600px wide is usually sufficient

**Alt Text**:
- Always provide descriptive alt text
- Helps with accessibility
- Example: `![QGIS interface showing buffer tool dialog](path/to/image.png)`

## Image Placeholders in Course

Throughout the course, you'll see placeholders like:

```markdown
![Vector vs Raster](../images/topics/vector-vs-raster-comparison.png)
*Comparison of vector and raster data models*
```

These indicate where images should be added. The filenames suggest what the image should contain.

## Creating Your Own Images

### Screenshots

**For tutorials**:
1. Use high-resolution display
2. Crop to relevant area (don't show entire desktop)
3. Annotate with arrows/circles if needed (use Snagit, Greenshot, etc.)
4. Save as PNG

**Tools**:
- Windows: Snipping Tool, Snagit
- Mac: Command+Shift+4, Skitch
- Cross-platform: Greenshot, ShareX

### Diagrams

**For concepts**:
- Draw.io / diagrams.net (free!)
- Lucidchart
- PowerPoint → Export as PNG
- Inkscape (free, for SVG)

### Maps

**From QGIS/ArcGIS**:
1. Design your map with proper symbology
2. Export as PNG or PDF
3. Crop if needed
4. Optimize file size

## Quick Reference

**From `docs/index.md` file**:
```markdown
![GIS Banner](images/banners/gis-banner.jpg)
```

**From `docs/topics/01-what-is-gis.md` file**:
```markdown
![Example Map](../images/topics/example-map.png)
```

**From `docs/projects/project1.md` file**:
```markdown
![QGIS Interface](../images/projects/qgis-interface.png)
```

The `../` goes up one directory level from the current location.

## Need Help?

- [Markdown Image Syntax](https://www.markdownguide.org/basic-syntax/#images-1)
- [Material for MkDocs Images](https://squidfunk.github.io/mkdocs-material/reference/images/)
- [Image Optimization Tools](https://tinypng.com/)
