# Project 2: Vector Data Analysis

## Learning Goals

By the end of this project, you should be able to:

1. Become familiar with vector processing operations in QGIS
2. Import and create GIS data
3. Perform basic joins and spatial operations such as buffer, dissolve, intersect, union
4. Style maps in a custom fashion based on columnar values
5. Understand different data types and corresponding data representations
6. Query and filter spatial datasets

---

## Written Questions [3 pts]

### Question 1: Vector Geometry Types

You're tasked with supporting several city projects. For each task, choose the **best/most appropriate vector geometry type** (Point, Line, or Polygon) and **justify your choice** in 1-2 sentences.

**Tasks**:

a. **Mapping individual street trees** for a maintenance inventory

b. **Delineating building footprints** for calculating rooftop solar potential

c. **Representing bus routes** for network analysis and travel time estimation

d. **Defining school attendance zones** for eligibility checks by address

e. **Locating reported potholes** submitted by residents via a mobile app

---

### Question 2: Attribute Data Types

You're designing an attribute table for a **municipal parcels polygon layer**. For each attribute (column), specify the **most appropriate data type** and **briefly justify your choice**.

**Data type options**: Integer, Float/Double, Text/String, Date/Time, Boolean

**Attributes**:

a. **Parcel_ID** (e.g., "003421-7")

b. **Owner_ZIP** (e.g., "02108")

c. **Assessed_Value** (in dollars)

d. **Impervious_Cover_Pct** (0–100 with decimals)

e. **Has_Easement** (yes/no)

---

### Question 3: Boundary Vagueness

Per the description of the positional accuracy of **wetland boundaries** in the textbook, discuss a different map feature (besides wetlands) whose boundaries are **inherently vague and difficult to map**.

**Consider**:
- Why are the boundaries vague?
- What makes them challenging to define precisely?
- How might this affect GIS analysis?

---

### Question 4: Accuracy Errors [EXTRA CREDIT: 1 pt]

What are the **five types of accuracy/precision errors** associated with geographic information? 

Provide an **example of each type of error**.

---

## Project Work [6 pts]

### Data Download

Download and unzip the **SPR Data** (Swanton Pacific Ranch):
- Available in Canvas: Week 1 folder
- [Direct link](link-to-data)

You will use this data to answer the following questions.

---

### Question 1: Unique Soil Names

Within the **sprSoil** layer, how many **unique values** are present in the **"SOILNAME"** field?

**Hint**: Use the **"Statistics by Categories"** tool

**Steps**:
1. Open sprSoil layer
2. Processing Toolbox → "Statistics by Categories"
3. Select SOILNAME field
4. Count unique values

---

### Question 2: Most Common Soil Type

Within the **sprSoil** layer, which type of soil (described in the **"SOILNAME"** field) occurs in the **largest number of polygons**?

**Questions**:
- What is the soil name?
- How many polygons consist of this soil type?

**Hint**: Use the **"Statistics by Categories"** tool

---

### Question 3: Land Use Acreage

Within the **sprLandUse** layer, what is the **total acreage of each land use type** (given in the **"LUtype"** field)?

**Hints**: 
- Use the **"Add Geometry Attributes"** tool
- And/or use the **"Statistics by Categories"** tool

**Steps**:
1. Add geometry attributes (area in appropriate units)
2. Convert to acres if needed (1 acre = 4046.86 m²)
3. Summarize by LUtype

---

## Tutorials [6 pts]

### Tutorial 1: Importing Spreadsheets/CSV [1.5 pts]

**Task**: Convert Excel file of latitudes/longitudes to a point shapefile

**Follow**: [Importing Spreadsheets or CSV Files](https://www.qgistutorials.com/en/docs/3/importing_spreadsheets_csv.html)

**Submit**: Screenshots showing:
- Final point layer displayed on map
- Attribute table
- Processing steps
- **Include date/time in screenshots!**

---

### Tutorial 2: Performing Table Joins [1.5 pts]

**Task**: Perform a tabular join

**Note**: Highly suggest downloading data directly from the tutorial, as opposed to navigating the census website!

**Follow**: [Performing Table Joins](https://www.qgistutorials.com/en/docs/3/performing_table_joins.html)

**Submit**: Screenshots showing:
- Joined attribute table
- Final map with joined data
- Processing steps
- **Include date/time in screenshots!**

---

### Tutorial 3: Performing Spatial Joins [1.5 pts]

**Task**: Perform a spatial join

**Follow**: [Performing Spatial Joins](https://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html)

**Submit**: Screenshots showing:
- Spatially joined layer
- Attribute table showing transferred attributes
- Final map
- **Include date/time in screenshots!**

---

### Tutorial 4: Performing Spatial Queries [1.5 pts]

**Task**: Perform a spatial query

**Follow**: [Performing Spatial Queries](https://www.qgistutorials.com/en/docs/3/performing_spatial_queries.html)

**Submit**: Screenshots showing:
- Query results
- Selected features
- Final map showing query results
- **Include date/time in screenshots!**

---

## Submission Requirements

Submit to Canvas **one document** containing:

1. ✅ **Answers to Written Questions 1-3** (and optionally Question 4 for extra credit)
2. ✅ **Answers to Project Work Questions 1-3** with supporting evidence
3. ✅ **Screenshots from all 4 tutorials** showing:
   - Final outputs
   - Processing steps taken
   - Date and time stamps visible

**File format**: PDF preferred, or Word document

---

## Grading Rubric

| Component | Points |
|-----------|--------|
| Written Questions 1-3 | 3 pts |
| Project Work Questions 1-3 | 6 pts |
| Tutorial 1: Importing CSV | 1.5 pts |
| Tutorial 2: Table Joins | 1.5 pts |
| Tutorial 3: Spatial Joins | 1.5 pts |
| Tutorial 4: Spatial Queries | 1.5 pts |
| Extra Credit: Question 4 | 1 pt |
| **TOTAL** | **15 pts (16 with EC)** |

---

## Tips for Success

### For Written Questions:
- **Think practically** - What data type makes sense for real-world use?
- **Justify thoroughly** - Don't just state the answer, explain why
- **Use examples** from class materials or textbook

### For Project Work:
- **Use the correct tools** - Statistics by Categories is your friend
- **Show your work** - Include screenshots of your analysis steps
- **Double-check units** - Acres vs square meters matters!
- **Save intermediate results** - Don't lose your work

### For Tutorials:
- **Follow step-by-step** - Don't skip ahead
- **Take screenshots progressively** - Easier than backtracking
- **Verify results** - Make sure outputs look correct
- **Include timestamps** - Required for credit

---

## Common Mistakes to Avoid

❌ **Using wrong geometry type** - Polygons for point data wastes space
❌ **Wrong data type** - Storing ZIP codes as integers loses leading zeros
❌ **Missing screenshots** - No screenshot = no credit
❌ **No timestamps** - Must prove you did the work yourself
❌ **Incomplete joins** - Check that all records matched
❌ **Wrong units** - Converting between acres and square meters

---

## Key Concepts Review

### Vector Geometry Types:
- **Points**: Discrete locations (trees, wells, survey markers)
- **Lines**: Linear features (roads, rivers, pipelines)
- **Polygons**: Areas (parcels, buildings, zones)

### Data Types:
- **Integer**: Whole numbers, no decimals
- **Float/Double**: Numbers with decimals
- **Text/String**: Alphanumeric text
- **Date/Time**: Temporal data
- **Boolean**: True/False, Yes/No

### Joins:
- **Tabular Join**: Match by common field (attribute)
- **Spatial Join**: Match by location (geometry)

---

## Resources

- [QGIS Tutorials](https://www.qgistutorials.com/)
- [SPR Data Download](link-to-canvas)
- [QGIS Vector Tools Documentation](https://docs.qgis.org/latest/en/docs/user_manual/working_with_vector/)
- [Attribute Table Management](https://docs.qgis.org/latest/en/docs/user_manual/working_with_vector/attribute_table.html)

---

## Getting Help

- **Office Hours**: See syllabus
- **Lab Sessions**: TAs available
- **QGIS Documentation**: Built-in help
- **GIS Stack Exchange**: Community Q&A

Good luck with vector analysis! 🗺️
