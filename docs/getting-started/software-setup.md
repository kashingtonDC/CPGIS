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

## Verifying Your Installation

### QGIS Check

1. Launch QGIS Desktop
2. Go to **Layer → Add Layer → Add Vector Layer**
3. Can you see the file browser?
4. Close QGIS

✅ If yes, you're ready! [:octicons-arrow-right-24: Set up your file system](../getting-started/storage-and-file-management.md)

### ArcGIS Pro Check

1. Launch ArcGIS Pro
2. Create a new project
3. Can you see the ribbon and catalog pane?
4. Close ArcGIS Pro

✅ If yes, you're ready! [:octicons-arrow-right-24: Set up your file system](../getting-started/storage-and-file-management.md)


