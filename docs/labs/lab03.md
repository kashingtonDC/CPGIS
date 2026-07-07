# Lab 3: Coordinate Systems and Projections

!!! info "Lab Overview"
    **Topic**: Working with Coordinate Systems
    <br>**Time Required**: 2-3 hours
    <br>**Software**: QGIS or ArcGIS Pro

---

!!! note "Content Placeholder"
    This lab is under development. It will cover:
    
    - Identifying coordinate systems of layers
    - Comparing different projections visually
    - Reprojecting vector data
    - Measuring distances in different projections
    - Understanding distortion
    - Reprojecting vector data
    - Resampling options for reprojecting raster data
    - Setting project coordinate systems
    - Troubleshooting projection problems

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

[:octicons-arrow-right-24: Return to Lab Overview](overview.md)
