# Software Setup

This course uses industry-standard GIS software. You'll need to install at least one (preferably both) of the following:

---

## Option 1: QGIS (Recommended for Beginners)

**QGIS** is free, open-source GIS software with powerful capabilities. It's cross-platform and regularly updated.

### Why QGIS?

✅ **Free and open-source**
<br>✅ **Cross-platform** (Windows, Mac, Linux)
<br>✅ **Large community** and extensive documentation
<br>✅ **No licensing hassles**
<br>✅ **Extensible** with plugins

### Installation

#### Windows & Mac

1. Visit [https://qgis.org/download/](https://qgis.org/download/)
2. Download the **Long Term Release (LTR)** version for stability
3. Run the installer and follow prompts
4. Default settings are fine for most users

#### Linux

```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install qgis qgis-plugin-grass

# Fedora
sudo dnf install qgis python3-qgis

# Arch
sudo pacman -S qgis
```

### Recommended Plugins

After installation, install these plugins via **Plugins → Manage and Install Plugins**:

- **QuickMapServices**: Easy basemap access (OpenStreetMap, Google, etc.)
- **QGIS Resource Sharing**: Access to additional resources
- **Profile Tool**: Elevation profile creation
- **Point Sampling Tool**: Extract raster values at points

---

## Option 2: ArcGIS Pro (Industry Standard)

**ArcGIS Pro** by ESRI is the industry-standard GIS software used by many organizations. It's powerful but requires a license.

### Why ArcGIS Pro?

✅ **Industry standard** - most widely used in professional settings
<br>✅ **Powerful analysis tools**
<br>✅ **Excellent 3D capabilities**
<br>✅ **ArcGIS Online integration**
<br>⚠️ **Requires license** (paid)
<br>⚠️ **Windows only**

### Installation

#### For Students

Many universities provide free ArcGIS Pro licenses:

1. **Check with your institution**
   - Cal Poly students: Visit [GIF Lab Resources](https://gif.calpoly.edu/)
   - Contact your IT department or GIS lab

2. **Student License**
   - ESRI offers 1-year student licenses
   - Visit [esri.com/training/student](https://www.esri.com/training/catalog/5d76dcf7e9ccda09bef61253/get-started-with-arcgis-pro/)

3. **Download & Install**
   - Sign in to your ArcGIS account
   - Download installer from My ESRI
   - Run installer (requires administrator rights)
   - Authorize using your license

#### System Requirements

- **OS**: Windows 10/11 (64-bit)
- **CPU**: 4+ cores recommended
- **RAM**: 8GB minimum, 16GB+ recommended
- **Graphics**: 4GB+ GPU memory for 3D
- **Disk**: 10GB+ free space

!!! warning "Mac Users"
    ArcGIS Pro only runs on Windows. Options:
    
    - Use lab computers
    - Install Windows via Boot Camp or Parallels
    - Use QGIS instead

---

## Cloud Storage Setup

### OneDrive (Recommended for Cal Poly Students)

Cal Poly provides 1TB of OneDrive storage to all students:

**Benefits:**
- Access files from any computer (lab or personal)
- Automatic backups
- Easy file sharing
- Works with both QGIS and ArcGIS Pro

**Setup:**

1. Download [OneDrive](https://www.microsoft.com/en-us/microsoft-365/onedrive/download)
2. Sign in with your Cal Poly credentials
3. Create a folder structure:
   ```
   OneDrive/
   └── GIS_Course/
       ├── Labs/
       ├── Projects/
       ├── Data/
       └── Maps/
   ```
4. Set this folder to sync locally

!!! tip "Pro Tip"
    Store all your GIS project files in your synced OneDrive folder. This way:
    
    - Projects are automatically backed up
    - You can work from any computer
    - No lost work if your computer crashes!

### Alternative: Google Drive

If not using OneDrive:

1. Install [Google Drive Desktop](https://www.google.com/drive/download/)
2. Create similar folder structure
3. Note: Some GIS file formats may sync slowly

---

## Additional Software (Optional but Useful)

### Text Editor

For working with code or data files:

- **VS Code**: [code.visualstudio.com](https://code.visualstudio.com/) (recommended)
- **Notepad++**: Windows only
- **Sublime Text**: Cross-platform

### Python Setup (For Advanced Users)

Some labs may include optional Python exercises:

```bash
# Install Anaconda (includes Python + data science libraries)
# Download from: https://www.anaconda.com/download

# Create GIS environment
conda create -n gis python=3.11
conda activate gis
conda install -c conda-forge geopandas rasterio folium
```

Useful Python GIS libraries:
- **GeoPandas**: Vector data manipulation
- **Rasterio**: Raster data I/O
- **Folium**: Interactive web maps
- **Shapely**: Geometric operations

### GDAL/OGR

Command-line tools for geospatial data:

- Included with QGIS
- Separate install: [gdal.org](https://gdal.org/)
- Useful for batch processing

---

## Verifying Your Installation

### QGIS Check

1. Launch QGIS Desktop
2. Go to **Layer → Add Layer → Add Vector Layer**
3. Can you see the file browser?
4. Close QGIS

✅ If yes, you're ready!

### ArcGIS Pro Check

1. Launch ArcGIS Pro
2. Create a new project
3. Can you see the ribbon and catalog pane?
4. Close ArcGIS Pro

✅ If yes, you're ready!

---

## File Organization Best Practices

### Folder Structure

Create a clear hierarchy:

```
GIS_Course/
│
├── Labs/
│   ├── Lab01/
│   │   ├── Data/
│   │   ├── Lab01_Project.qgz (or .aprx)
│   │   └── Lab01_Map.pdf
│   ├── Lab02/
│   └── ...
│
├── Projects/
│   ├── Project01/
│   └── ...
│
├── Data/
│   ├── Downloaded/
│   ├── Created/
│   └── Reference/
│
└── Documentation/
    └── notes.md
```

### File Naming Conventions

!!! success "Good Practices"
    - Use descriptive names: `watershed_boundary.shp` not `data1.shp`
    - No spaces: Use underscores or hyphens
    - Include dates: `fire_perimeter_2024-08-15.gpkg`
    - Lowercase is easier: `my_project` not `My_Project`

!!! danger "Avoid"
    - Special characters: `&, *, ?, <, >`
    - Spaces in folder names
    - Very long names (> 50 characters)

---

## Getting Help

### QGIS Resources

- **Official Documentation**: [docs.qgis.org](https://docs.qgis.org/)
- **Tutorials**: [qgistutorials.com](https://www.qgistutorials.com/)
- **YouTube**: QGIS Official Channel
- **Community**: GIS StackExchange

### ArcGIS Pro Resources

- **Official Documentation**: [pro.arcgis.com](https://pro.arcgis.com/en/pro-app/latest/help/main/welcome-to-the-arcgis-pro-app-help.htm)
- **Learn ArcGIS**: [learn.arcgis.com](https://learn.arcgis.com/)
- **ESRI Community**: [community.esri.com](https://community.esri.com/)
- **YouTube**: ESRI Training Videos

### General GIS Help

- **GIS Stack Exchange**: [gis.stackexchange.com](https://gis.stackexchange.com/)
- **Reddit r/gis**: [reddit.com/r/gis](https://www.reddit.com/r/gis/)
- **Discord/Slack**: Many GIS communities

---

## Troubleshooting Common Issues

### "Can't see my files"

- Check file extensions are not hidden (Windows: View → File name extensions)
- Ensure you're looking in the right folder
- Files may be in Downloads instead of your project folder

### "Software crashes when opening large files"

- Your computer may not have enough RAM
- Try using lab computers with better specs
- Simplify/subset your data

### "Projection errors or features not visible"

- Check that all layers use compatible coordinate systems
- Use "Zoom to Layer" to find your data
- Verify the data actually has coordinate information

### "Can't install plugins (QGIS)"

- Check internet connection
- Go to Settings → Options → Network: Ensure proxy settings are correct
- Try from a different network

---

## Ready to Start?

Once your software is installed:

1. ✅ Verify installation works
2. ✅ Set up cloud storage
3. ✅ Create folder structure
4. ✅ Bookmark help resources

[:octicons-arrow-right-24: Start with Topic 1: What is GIS?](../topics/01-what-is-gis.md)

---

**Need More Help?**

If you encounter installation issues, check with:
- Your university's IT help desk
- GIS lab staff
- Course instructor during office hours
