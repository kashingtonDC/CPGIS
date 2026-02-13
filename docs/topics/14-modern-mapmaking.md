# Topic 14: Modern Mapmaking and Web GIS

## Overview

The web has transformed how we share and interact with maps. Web GIS enables interactive maps accessible to anyone with a browser, democratizing geographic information and enabling real-time collaboration.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand web mapping fundamentals
- Distinguish between web maps and desktop GIS
- Create interactive online maps
- Use ArcGIS Online or similar web platforms
- Share GIS data and maps via the web
- Understand mobile GIS capabilities

---

## Web GIS Fundamentals

### What is Web GIS?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Web GIS** delivers GIS capabilities and content through web browsers and mobile devices, enabling users to access, visualize, and analyze spatial data without specialized desktop software.

</div>

### Desktop GIS vs Web GIS

| Aspect | Desktop GIS | Web GIS |
|--------|-------------|---------|
| **Access** | Licensed software on computer | Web browser, any device |
| **Installation** | Required | None |
| **Analysis** | Powerful, unlimited | Limited to available tools |
| **Sharing** | Export files | Share links instantly |
| **Collaboration** | Email files back and forth | Real-time updates |
| **Data updates** | Manual | Can be automatic |
| **Audience** | GIS professionals | Anyone with browser |
| **Cost** | Often expensive | Free to low cost |

---

### When to Use Web GIS

**Best for**:
- Sharing maps with non-GIS users
- Public-facing content
- Real-time data updates
- Collaboration
- Mobile access
- Simple viewing and queries

**Still need desktop for**:
- Complex analysis
- Large datasets
- Advanced geoprocessing
- Offline work
- Full customization

---

## Web Mapping Platforms

### Free/Open Source

**Leaflet.js** 📍:
- JavaScript library
- Lightweight, simple
- Great for custom maps
- Requires coding

**OpenLayers**:
- More features than Leaflet
- Handles more formats
- Steeper learning curve

**Mapbox**:
- Beautiful base maps
- Custom styling
- Free tier available
- GL JS library

**Felt**:
- Modern, intuitive
- No coding required
- Collaborative editing
- Free for personal use

---

### Commercial Platforms

**ArcGIS Online** (Esri):
- Full-featured
- Integrates with ArcGIS Pro
- Story maps
- Requires subscription

**Google Maps Platform**:
- Familiar interface
- API for custom apps
- Pay-per-use pricing

**CARTO**:
- Data science focused
- Great for analysis
- Beautiful visualizations

---

## ArcGIS Online (AGOL)

### Core Concepts

**Content Types**:
- **Web Maps**: Interactive maps
- **Web Apps**: Custom applications
- **StoryMaps**: Narrative-driven maps
- **Dashboards**: Real-time monitoring
- **Layers**: Published data

---

### Creating a Web Map

**Basic workflow**:

1. **Prepare data** in ArcGIS Pro or QGIS
2. **Publish layer** to AGOL
3. **Create web map** - add layers, configure pop-ups
4. **Style** - choose symbols, colors
5. **Configure** - set extent, bookmarks
6. **Share** - public, organization, or private

**No coding required!**

---

### Web Map Features

**Interactivity**:
- Click features for info (pop-ups)
- Search locations
- Filter data
- Measure distances/areas
- Print/export

**Customization**:
- Custom basemaps
- Symbol styling
- Pop-up configuration
- Bookmarks for key locations
- Legend and scale bar

**Sharing options**:
- Public (anyone)
- Organization (colleagues)
- Private (just you)
- Embedded in websites

---

### StoryMaps

**What are StoryMaps?**

Combine maps with narrative text, images, and multimedia to tell compelling stories with geographic context.

**Components**:
- Text blocks
- Maps (multiple!)
- Images and videos
- Sidecar layouts
- Timeline views
- Swipe/compare views

**Use cases**:
- Explain environmental issues
- Document field work
- Present research
- Public outreach
- Educational content

**Example**: https://storymaps.arcgis.com (explore gallery)

---

### Dashboards

**Real-time monitoring and KPIs**

**Elements**:
- Maps
- Charts (bar, line, pie)
- Gauges and indicators
- Lists
- Tables
- Rich text

**Update frequency**:
- Real-time (as data changes)
- Scheduled refresh
- On-demand

**Use cases**:
- Emergency response monitoring
- Facility management
- Fleet tracking
- Public health surveillance
- Election results

---

## Mobile GIS

### Mobile Data Collection

**Apps**:
- **ArcGIS Field Maps**: Esri's mobile solution
- **QField**: QGIS mobile companion
- **SW Maps**: Professional field mapping
- **Avenza Maps**: PDF map viewer with GPS

**Capabilities**:
- Collect points, lines, polygons
- Attach photos
- Fill out forms
- Work offline
- Sync to cloud

---

### Mobile Workflows

**Typical process**:

1. **Design form** in desktop GIS
2. **Publish** to cloud
3. **Download** to mobile device
4. **Collect data** in field (offline capable)
5. **Sync** when back online
6. **Review** in desktop GIS

**Benefits**:
- No paper forms
- Photos attached automatically
- GPS coordinates recorded
- Data immediately available
- Less data entry errors

---

## Sharing Maps

### Embedding Maps

**Iframe code** (for websites):

```html
<iframe src="https://your-map-url" 
        width="600" 
        height="400">
</iframe>
```

**Where to embed**:
- Websites
- Blog posts
- Reports (if web-based)
- Presentations (link to live map)

---

### Map Links

**Direct link**:
```
https://arcg.is/xyz123
```

**With parameters**:
```
https://arcg.is/xyz123?center=-120.5,35.3&level=12
```

**QR codes**:
- Generate QR code from link
- Print on posters
- Scan to open map

---

## Creating Interactive Maps

### Using Leaflet

**Simple example**:

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
</head>
<body>
  <div id="map" style="height: 600px;"></div>
  <script>
    var map = L.map('map').setView([35.28, -120.66], 13);
    
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
    
    L.marker([35.28, -120.66])
      .bindPopup('Cal Poly SLO')
      .addTo(map);
  </script>
</body>
</html>
```

**Result**: Interactive map with marker!

---

## Web Map Tiles

### How Web Maps Work

**Tile system**:
- Map split into 256×256 pixel tiles
- Zoom levels (0-22)
- Pre-rendered for fast display
- Cached for performance

**Zoom levels**:
- Level 0: Whole world in 1 tile
- Level 5: Continents
- Level 10: Cities
- Level 15: Streets
- Level 20: Buildings

**Tile providers**:
- OpenStreetMap
- Stamen Design
- Mapbox
- ESRI

---

## Best Practices for Web Maps

### Performance

**Keep it fast**:
- Limit features displayed
- Use clustering for many points
- Simplify complex geometries
- Optimize tile loading
- Cache tiles

---

### Design

**Make it usable**:
- Clear legend
- Intuitive symbols
- Good color choices
- Responsive to screen size
- Fast loading

**Accessibility**:
- Color-blind friendly palettes
- Text alternatives for images
- Keyboard navigation
- Screen reader compatible

---

### Mobile Optimization

**Consider mobile users**:
- Touch-friendly buttons (big enough!)
- Portrait and landscape modes
- Minimize data usage
- Offline capability when possible
- Simplified interface

---

## Future of Web GIS

### Emerging Trends

**Cloud-native GIS**:
- Processing in the cloud
- Scalable computing
- Serverless functions

**AI Integration**:
- Automated classification
- Predictive mapping
- Smart suggestions

**Real-time Collaboration**:
- Multiple users editing simultaneously
- Live updates
- Version control

**3D on the Web**:
- WebGL for 3D visualization
- Virtual reality integration
- Digital twins

**Edge Computing**:
- Process data at sensors
- Reduce latency
- IoT integration

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Web GIS shares broadly** - Anyone with browser can view
2. **No software installation** - Just a web link
3. **Real-time updates possible** - Dynamic data
4. **Mobile-first** - Collect data anywhere
5. **StoryMaps tell stories** - Combine maps with narrative
6. **Dashboards monitor** - Real-time KPIs
7. **Desktop still needed** - For complex analysis
8. **Choose platform wisely** - Based on needs and budget

</div>

---

## Further Reading

- [ArcGIS Online Documentation](https://doc.arcgis.com/en/arcgis-online/)
- [Leaflet Tutorials](https://leafletjs.com/examples.html)
- [Mapbox GL JS Guide](https://docs.mapbox.com/mapbox-gl-js/)
- [StoryMaps Best Practices](https://storymaps.arcgis.com/)

---

## Lab Exercise

!!! lab "Lab 14: Create a Web Map"
    In [Lab 14](../labs/lab14.md), you'll:
    
    - Create an interactive web map
    - Design custom pop-ups
    - Style layers for web display
    - Create a StoryMap
    - Share maps with public
    - Embed map in webpage
    - Explore mobile collection
    
    **Time Required**: 2-3 hours
    
    [:octicons-arrow-right-24: Go to Lab 14](../labs/lab14.md)

---

## Next Topic

You've learned modern mapmaking! Time to synthesize everything:

[:octicons-arrow-right-24: Topic 15: Course Synthesis](15-synthesis.md)
