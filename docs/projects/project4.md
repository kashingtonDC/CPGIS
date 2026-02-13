# Project 4: Remote Sensing, Image Analysis, and Modeling

## Learning Goals

By the end of this project, you should be able to:

1. Become familiar with remote sensing and imagery analysis in QGIS
2. Perform basic data analysis with numerous remote sensing data layers
3. Work in groups to answer practical questions about an area
4. Integrate multiple datasets and criteria into a suitability analysis

---

## Project Overview

You are a **team of GIS analysts** tasked with finding the ideal location(s) at **Swanton Pacific Ranch** for one of the following sites.

**Choose ONE project per group:**

---

## Option 1: Hemp Farm 🌱

### Objective
Propose a site in Swanton Pacific Ranch to grow **industrial hemp**.

### Requirements

**Minimum Size**:
- The site must be **at least 20 acres**

**Land Use Restrictions**:
- Site **cannot** be on existing:
  - Forest land
  - Crop land use

**Multi-Site Option**:
If proposing multiple sites:
- Smallest site must be **larger than 5 acres**
- Sites cannot be more than **500 feet apart** from nearest site
- All sites must be at least **200 feet inside** ranch boundary

---

## Option 2: Student Housing Site 🏘️

### Objective
Propose a site to build **student housing** at Swanton Pacific Ranch.

### Requirements

**Land Use Restrictions**:
- Site must **not** be in existing:
  - Crop areas
  - Natural land use areas

**Terrain**:
- Site needs to be **15% slope or lower**

**Size**:
- Minimum size of **two acres**

**Shape**:
- Ideal shape is a **circle**

---

## Option 3: Helicopter Landing Site 🚁

### Objective
Propose a **helicopter landing site** in Swanton Pacific Ranch.

### Requirements

**Helicopter Specifications**:
- Must accommodate **Sikorsky S-92 helicopter**
- Research specifications:
  - Rotor diameter: ~56 feet
  - Required clear area: varies by regulations
  - Slope requirements: typically <5 degrees
  - Clearance zones: no obstacles

**Additional Considerations**:
- Accessibility
- Safety zones
- Approach/departure paths
- Proximity to facilities (if needed)

---

## Deliverables

### 1. Project Report and Map

Submit **one merged PDF** containing both report and map(s).

#### Report Sections

**A. Project Title**
- Descriptive title
- Group member names

**B. Introduction**
- **Objective statement**: What are you trying to find?
- **Criteria**: List all criteria with brief explanation
  - Why was each criterion chosen?
  - How does it relate to suitability?

**C. Methods**
- **Model diagram/flowchart/schematic**:
  - What processing steps did you undertake?
  - Show workflow visually (boxes and arrows)
  - Include tool names
- **Assumptions/uncertainties**:
  - What assumptions did you make?
  - What are sources of uncertainty?
  - How might these affect results?

**D. Results/Conclusions**
- **Findings**: What site(s) did you identify?
- **Commentary**: Why is this the best location?
- **Supporting graphics**: 
  - Charts showing area calculations
  - Comparison tables
  - Statistics

**E. References**
- All data sources
- Any supporting citations
- Use **correct and consistent format** (APA, MLA, Chicago)

**F. Map(s)**
- Map should be **self-contained**
- All necessary information for understanding
- Detailed caption describing what is shown
- **Required map elements**:
  - ✅ Legend
  - ✅ Scale bar
  - ✅ North arrow
  - ✅ Title
  - ✅ Data sources
  - ✅ Your name/group
  - ✅ Date

---

### 2. Project Presentation

**10-minute group presentation** on **Tuesday, December 5th**

#### Presentation Structure

**1. Title Slide**
- Project title
- Group members

**2. Introduction** (2 minutes)
- Objective statement
- Criteria with explanations

**3. Methods** (3 minutes)
- Model diagram/flowchart
- Processing steps
- Assumptions/uncertainties

**4. Map(s)** (2 minutes)
- Show final map(s)
- Explain what is displayed
- Highlight proposed site(s)

**5. Results/Conclusions** (3 minutes)
- Statement of findings
- Comments on suitability
- Supporting graphics/charts
- Limitations and future work

---

## Suggested Workflow

### Phase 1: Planning (Week 1)
1. **Choose project option**
2. **Identify criteria**
3. **List required data layers**
4. **Sketch workflow diagram**

### Phase 2: Data Preparation (Week 1-2)
1. **Gather data**:
   - SPR boundary
   - Land use
   - Elevation/slope
   - Any other needed layers
2. **Verify projections**
3. **Clip to study area**
4. **Check data quality**

### Phase 3: Analysis (Week 2)
1. **Apply each criterion**:
   - Reclassify or filter data
   - Create constraint layers
2. **Combine criteria**:
   - Boolean overlay (AND logic)
   - Or weighted suitability
3. **Calculate areas**
4. **Identify candidate sites**

### Phase 4: Validation (Week 2-3)
1. **Check results**:
   - Do sites meet all criteria?
   - Calculate exact areas
   - Verify constraints
2. **Refine if needed**
3. **Select final site(s)**

### Phase 5: Documentation (Week 3)
1. **Create final map**
2. **Write report**
3. **Prepare presentation**
4. **Merge into one PDF**

---

## Analysis Tips by Project

### Hemp Farm Tips
**Key criteria**:
- Buffer boundary inward 200 feet
- Identify non-forest, non-crop areas
- Calculate area of candidate polygons
- If multiple sites: check distance between them

**Suggested tools**:
- Buffer (negative buffer for inset)
- Intersect or Erase
- Calculate Geometry
- Spatial query (distance)

---

### Student Housing Tips
**Key criteria**:
- Calculate slope from DEM
- Reclassify slope ≤15%
- Exclude crop and natural areas
- Find areas ≥2 acres
- Prefer circular shapes

**Suggested tools**:
- Slope analysis
- Reclassify raster
- Vector selection
- Calculate Geometry
- Shape analysis (optional)

---

### Helicopter Landing Site Tips
**Key criteria**:
- Research Sikorsky S-92 specs
- Very flat area (<5 degrees slope)
- Clear approach/departure zones
- No obstacles nearby

**Suggested tools**:
- Slope analysis
- Buffer (clearance zones)
- 3D visualization (if available)
- Viewshed (optional)

---

## Grading Rubric

| Component | Points |
|-----------|--------|
| **Report** | |
| Introduction (objectives, criteria) | 2 pts |
| Methods (workflow, assumptions) | 3 pts |
| Results/Conclusions | 2 pts |
| Map quality | 3 pts |
| References | 1 pt |
| **Presentation** | |
| Content clarity | 3 pts |
| Visual aids | 2 pts |
| Timing (10 minutes) | 1 pt |
| Group participation | 1 pt |
| **Analysis Quality** | |
| Criteria application | 3 pts |
| Technical execution | 3 pts |
| **TOTAL** | **24 pts** |

---

## Tips for Success

### For Report:
- **Be thorough** - Explain your reasoning
- **Show workflow** - Diagrams help!
- **Document assumptions** - What did you assume and why?
- **Professional writing** - Proofread!
- **Complete maps** - All elements required

### For Presentation:
- **Practice timing** - 10 minutes is strict
- **Visual aids** - Maps should be visible
- **Clear speech** - Project to back of room
- **Share responsibility** - All members speak
- **Anticipate questions** - Know your analysis

### For Analysis:
- **Check each criterion** - One at a time
- **Save intermediate results** - Don't lose work
- **Verify units** - Feet vs meters matters!
- **Calculate accurately** - Use proper tools
- **Validate results** - Do they make sense?

---

## Common Mistakes to Avoid

❌ **Unclear criteria** - Vague requirements yield vague results
❌ **Wrong units** - Mixing feet and meters
❌ **Incomplete workflow** - Missing steps in diagram
❌ **Poor map design** - Missing elements, unreadable
❌ **No validation** - Didn't check if site actually meets criteria
❌ **Running over time** - Presentations > 10 minutes cut off
❌ **Unequal participation** - All group members should contribute

---

## Example Workflow (Hemp Farm)

```
1. Load Data
   ↓
2. Reproject all to UTM
   ↓
3. Buffer boundary inward -200 feet
   ↓
4. Select non-forest, non-crop areas
   ↓
5. Clip to buffered boundary
   ↓
6. Calculate area of each polygon
   ↓
7. Select polygons ≥20 acres
   ↓
8. If multiple sites: check distances
   ↓
9. Create final map
   ↓
10. Write report
```

---

## Resources

- [QGIS Processing Tools](https://docs.qgis.org/latest/en/docs/user_manual/processing/)
- [Multi-Criteria Analysis Guide](https://docs.qgis.org/latest/en/docs/training_manual/)
- [Sikorsky S-92 Specifications](https://www.lockheedmartin.com/)
- [Map Design Principles](https://www.axismaps.com/guide/general/map-design)

---

## Getting Help

- **Office Hours**: Regular times
- **Group work encouraged**: Collaborate!
- **Lab sessions**: TAs available
- **Peer review**: Have another group check your work

Good luck with your suitability analysis! This is real-world GIS! 🗺️
