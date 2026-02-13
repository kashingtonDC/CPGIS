# Topic 5: Table Management and Joins

## Overview

Attribute data is just as important as spatial data! Understanding how to manage attribute tables and join external data to spatial features is essential for GIS analysis and visualization.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand attribute table structure and field types
- Perform attribute queries and selections
- Create and calculate new fields
- Execute tabular joins to add external data
- Perform spatial joins based on location
- Distinguish between one-to-one and one-to-many joins
- Troubleshoot common join issues

---

## Understanding Attribute Tables

### What is an Attribute Table?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

An **attribute table** stores descriptive information about spatial features. Each row represents one feature, and each column represents one attribute.

</div>

### Table Structure

```
| FID | NAME        | POPULATION | AREA_SQ_MI | STATE |
|-----|-------------|------------|------------|-------|
| 1   | San Luis Obispo | 47,063  | 13.2       | CA    |
| 2   | Paso Robles | 31,490     | 20.5       | CA    |
| 3   | Morro Bay   | 10,757     | 10.4       | CA    |
```

**Components**:
- **FID/ObjectID**: Unique feature identifier
- **Geometry**: Shape information (hidden in table)
- **Attributes**: Descriptive data in columns

---

## Field Types

Understanding data types is crucial for proper storage and analysis.

| Field Type | Description | Examples | Storage |
|------------|-------------|----------|---------|
| **Text/String** | Alphanumeric characters | "Oak Street", "Forest" | Variable length |
| **Integer** | Whole numbers | 42, -17, 1000 | 16 or 32 bit |
| **Float/Double** | Decimal numbers | 3.14159, -122.4567 | 32 or 64 bit |
| **Date** | Date/time values | 2025-03-15, 14:30:00 | Timestamp |
| **Boolean** | True/False | TRUE, FALSE, 1, 0 | 1 bit |

!!! tip "Choose the Right Type"
    - Use **Integer** for counts, IDs, categories
    - Use **Float/Double** for measurements, coordinates
    - Use **Text** for names, descriptions, codes
    - Use **Date** for temporal data
    - Avoid storing numbers as text!

---

## Attribute Queries

### What is an Attribute Query?

Selecting features based on their attribute values, not their location.

### Query Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` | Equal to | `STATE = 'CA'` |
| `<>` or `!=` | Not equal to | `TYPE <> 'Water'` |
| `>` | Greater than | `POPULATION > 50000` |
| `<` | Less than | `AREA < 100` |
| `>=` | Greater or equal | `ELEVATION >= 1000` |
| `<=` | Less or equal | `YEAR <= 2020` |
| `LIKE` | Pattern matching | `NAME LIKE '%Forest%'` |
| `IN` | Match list | `STATE IN ('CA', 'OR', 'WA')` |
| `BETWEEN` | Range | `YEAR BETWEEN 2015 AND 2020` |
| `IS NULL` | No value | `OWNER IS NULL` |

### Logical Operators

Combine multiple conditions:

| Operator | Meaning | Example |
|----------|---------|---------|
| **AND** | Both must be true | `STATE = 'CA' AND POPULATION > 100000` |
| **OR** | Either can be true | `STATE = 'CA' OR STATE = 'NV'` |
| **NOT** | Inverse | `NOT STATE = 'CA'` |

### Query Examples

**Find large cities in California**:
```sql
"STATE" = 'CA' AND "POPULATION" > 50000
```

**Find forests or grasslands**:
```sql
"LANDCOVER" = 'Forest' OR "LANDCOVER" = 'Grassland'
```

**Find parcels without owners**:
```sql
"OWNER" IS NULL
```

**Find recent events**:
```sql
"EVENT_DATE" > '2024-01-01'
```

---

## Field Calculator

### Creating New Fields

Add calculated or derived attributes to your table.

**Common Uses**:
- Calculate area or length
- Concatenate text fields
- Convert units
- Extract parts of dates
- Create categories based on values

### Expression Syntax

**Basic arithmetic**:
```
POPULATION / AREA  // Calculate density
```

**Text concatenation**:
```
"FIRST_NAME" || ' ' || "LAST_NAME"  // Full name
```

**Conditional logic**:
```
CASE 
  WHEN POPULATION < 10000 THEN 'Small'
  WHEN POPULATION < 50000 THEN 'Medium'
  ELSE 'Large'
END
```

**Geometry calculations**:
```
$area / 4046.86  // Convert sq meters to acres
$length / 1609.34  // Convert meters to miles
```

### Example: Create Density Field

**Problem**: Calculate population density (people per square mile)

**Steps**:
1. Open attribute table
2. Open field calculator
3. Create new field: `POP_DENSITY` (Type: Float)
4. Expression: `"POPULATION" / "AREA_SQ_MI"`
5. Calculate

---

## Tabular Joins

### What is a Tabular Join?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **tabular join** links non-spatial data (like a CSV or Excel file) to spatial data based on a common field (key field). This adds new attribute columns to your spatial layer.

</div>

### Why Use Tabular Joins?

**Scenario**: You have:
1. A shapefile of counties (with geometry)
2. A CSV of county statistics (no geometry)

**Goal**: Visualize the statistics on a map

**Solution**: Join the CSV to the shapefile by matching county IDs!

---

### Join Requirements

For a successful join, you need:

1. **✅ Common field**: Both tables must have a matching column
2. **✅ Unique values**: Join field should have unique values (for 1:1)
3. **✅ Same data type**: Text to text, number to number
4. **✅ Exact matches**: Values must match exactly (case-sensitive!)

**Example**:

**Spatial Layer** (counties.shp):
```
| GEOID | NAME           | Geometry |
|-------|----------------|----------|
| 06079 | San Luis Obispo| Polygon  |
| 06083 | Santa Barbara  | Polygon  |
```

**Tabular Data** (population.csv):
```
| GEOID | POPULATION | INCOME |
|-------|------------|--------|
| 06079 | 283,111    | 72,345 |
| 06083 | 446,499    | 81,234 |
```

**After Join** → Add POPULATION and INCOME columns to counties layer!

---

### Performing a Tabular Join

=== "QGIS"

    **Method 1: Join by Field Value Tool**
    
    1. **Processing Toolbox** → "Join attributes by field value"
    2. **Input layer**: Your spatial layer (e.g., counties)
    3. **Table field**: Common field in spatial layer (e.g., GEOID)
    4. **Input layer 2**: Your CSV/table
    5. **Table field 2**: Matching field in CSV (e.g., GEOID)
    6. **Join type**: Usually "One-to-one"
    7. **Run**
    
    **Method 2: Layer Properties Join**
    
    1. Right-click layer → **Properties**
    2. **Joins** tab → Click **+**
    3. Select join layer, join field, target field
    4. **OK** → **Apply**

=== "ArcGIS Pro"

    1. Right-click layer → **Joins and Relates** → **Add Join**
    2. **Input Join Field**: Field in your spatial layer
    3. **Join Table**: Your CSV/Excel file
    4. **Join Table Field**: Matching field in CSV
    5. **OK**

---

### One-to-One vs One-to-Many Joins

**One-to-One Join** (Most Common)
- Each feature gets **one** matching record
- Example: Join counties to population stats (one pop value per county)
- Output: Same number of features as input

**One-to-Many Join**
- Each feature may match **multiple** records
- Example: Join counties to cities (multiple cities per county)
- Output: Features duplicated for each match
- Use carefully! Can explode dataset size

---

### Troubleshooting Tabular Joins

**Problem: No Records Match**

**Causes**:
- Field names don't match (typo)
- Data types don't match (text vs number)
- Values don't match exactly (spaces, case)
- Wrong join fields selected

**Solutions**:
- Verify field names in both tables
- Check a few values match exactly
- Ensure no leading/trailing spaces
- Make data types consistent

---

**Problem: Some Records Don't Match**

**Causes**:
- Missing values in one table
- Data entry inconsistencies
- Different naming conventions

**Solutions**:
- Identify unmatched records
- Standardize naming
- Clean data before joining
- Accept partial matches if appropriate

---

**Problem: Joined Fields Not Showing**

**Causes**:
- Join exists but fields not selected
- Join layer not loaded properly

**Solutions**:
- Check join configuration
- Remove and re-add join
- Ensure join table is loaded in project

---

## Spatial Joins

### What is a Spatial Join?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

A **spatial join** transfers attributes between layers based on their **spatial relationship** (location), not a common field. Features are matched by where they are on the map.

</div>

### How Spatial Joins Work

**Example**:
- Layer 1: Coffee shops (points)
- Layer 2: Neighborhoods (polygons)

**Goal**: Add neighborhood name to each coffee shop

**Solution**: Spatial join - assign each point the attributes of the polygon it falls within!

---

### Spatial Relationship Types

| Relationship | Description | Example |
|-------------|-------------|---------|
| **Intersects** | Features touch or overlap | Which parcels intersect the floodplain? |
| **Contains** | One feature completely inside another | Which neighborhood contains each cafe? |
| **Within** | Feature completely inside target | Which parks are within 1 mile of schools? |
| **Touches** | Features share a boundary | Which parcels touch this parcel? |
| **Nearest** | Closest feature | What's the nearest fire station to each house? |

---

### Performing a Spatial Join

=== "QGIS"

    **Processing Toolbox** → "Join attributes by location"
    
    1. **Input layer**: Target layer (gets new attributes)
    2. **Join layer**: Source layer (provides attributes)
    3. **Geometric predicate**: Choose relationship type
       - Intersects, Contains, Within, etc.
    4. **Join type**: 
       - One-to-one: First match only
       - One-to-many: All matches (duplicates target)
    5. **Run**

=== "ArcGIS Pro"

    **Analysis** → **Tools** → "Spatial Join"
    
    1. **Target Features**: Layer to receive attributes
    2. **Join Features**: Layer providing attributes
    3. **Match Option**: 
       - Intersect, Contains, Within, etc.
    4. **Join Type**:
       - One to one
       - One to many
    5. **Run**

---

### One-to-One Spatial Joins

**Output**: Each target feature gets **one** matching record from join layer

**Behavior**: If multiple matches exist, only one is selected (usually first or nearest)

**Example**: 
- Join cities (target) to climate zones (join)
- Each city gets one climate zone
- If city spans multiple zones, picks one

**Use When**: You want a single answer per feature

---

### One-to-Many Spatial Joins

**Output**: Target features **duplicated** for each matching join feature

**Behavior**: Creates new row for every match

**Example**:
- Join states (target) to cities (join)
- Texas has 254 cities
- Output: 254 rows for Texas (one per city)

**Use When**: You need to count or list all matches

!!! warning "Dataset Explosion!"
    One-to-many joins can greatly increase file size. A state with 1,000 cities becomes 1,000 rows!

---

### Spatial Join vs Tabular Join

| Aspect | Tabular Join | Spatial Join |
|--------|-------------|--------------|
| **Match Basis** | Common field value | Spatial relationship |
| **Requires** | Matching IDs/names | Overlapping geometries |
| **Use Case** | Add census data to counties | Find which county each point is in |
| **Speed** | Fast | Slower (spatial calculation) |
| **Data Needed** | Non-spatial table OK | Both layers must be spatial |

---

### Spatial Join vs Merge vs Union

**Spatial Join**:
- Combines **attributes** based on location
- Geometry stays same (usually)
- Example: Add county name to each city point

**Merge**:
- Combines **features** from multiple layers
- Stacks geometries together
- Example: Combine roads from 3 counties into one layer

**Union**:
- Combines **geometries** and creates all overlaps
- Splits features at intersections
- Example: Overlay land use and soil types

!!! tip "Quick Guide"
    - Need to **add attributes** from another layer? → Spatial Join
    - Need to **combine features** from similar layers? → Merge
    - Need to **overlay** two polygon layers? → Union

---

## Practical Examples

### Example 1: Add Population to Counties

**Scenario**: Counties shapefile + population CSV

**Steps**:
1. Load counties shapefile
2. Import population.csv as table
3. **Join attributes by field value**
4. Match field: `GEOID` (or county FIPS code)
5. Result: Population columns added to counties

**Visualize**: Create choropleth map showing population by county

---

### Example 2: Count Points in Polygons

**Scenario**: Count how many crimes occurred in each neighborhood

**Steps**:
1. Load neighborhoods (polygons)
2. Load crime incidents (points)
3. **Spatial join** (one-to-many) - join neighborhoods to crimes
4. **Dissolve** by neighborhood ID, count crimes
5. Result: Neighborhood polygons with crime count attribute

**Alternative**: Use "Count Points in Polygon" tool directly

---

### Example 3: Find Nearest Feature

**Scenario**: Assign each house to nearest fire station

**Steps**:
1. Load houses (points)
2. Load fire stations (points)
3. **Spatial join** with "Nearest" relationship
4. Result: Each house gets attributes of nearest station

**Use**: Calculate drive time to nearest service

---

## Summary Statistics

After joins, you often want to **summarize** data:

**Common operations**:
- **Count**: How many features per category?
- **Sum**: Total of a numeric field
- **Mean**: Average value
- **Min/Max**: Smallest/largest value

**Example**: After joining cities to states
- Count: How many cities per state?
- Sum: Total state population
- Mean: Average city size per state

**Tools**:
- QGIS: **Statistics by categories** or **Group stats**
- ArcGIS Pro: **Summary Statistics** or **Dissolve** with statistics

---

## Best Practices

### Before Joining

1. **✅ Inspect both tables** - Look at join fields
2. **✅ Check data types** - Ensure they match
3. **✅ Clean data** - Remove spaces, fix case
4. **✅ Verify unique values** - For one-to-one joins
5. **✅ Test on small subset** - Don't process huge dataset first

### During Joining

1. **✅ Choose correct join type** - One-to-one vs one-to-many
2. **✅ Select join fields carefully** - Must match exactly
3. **✅ Check projection** - For spatial joins, verify CRS matches
4. **✅ Document workflow** - Record what you joined and why

### After Joining

1. **✅ Verify results** - Check attribute table for new fields
2. **✅ Count features** - Did number change (expected for 1:many)?
3. **✅ Test a few records** - Spot check accuracy
4. **✅ Save results** - Export to new layer
5. **✅ Remove unsuccessful matches** - Clean if needed

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Tabular joins** match by common field, **spatial joins** match by location
2. **One-to-one** keeps same feature count, **one-to-many** duplicates features
3. **Join fields must match** exactly - same type, same values
4. **Spatial joins require matching CRS** - reproject if needed
5. **Clean data first** - remove spaces, fix inconsistencies
6. **Test before processing** - verify on small subset
7. **Document your joins** - record what, why, and how

</div>

---

## Further Reading

- [QGIS: Joins](https://docs.qgis.org/3.28/en/docs/user_manual/working_with_vector/vector_properties.html#joins-properties)
- [ArcGIS Pro: Joins and Relates](https://pro.arcgis.com/en/pro-app/latest/help/data/tables/joins-and-relates.htm)
- [Spatial Join Concepts](https://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html)

---

## Lab Exercise

!!! lab "Lab 5: Table Management & Joins"
    In [Lab 5](../labs/lab05.md), you'll:
    
    - Perform attribute queries and selections
    - Use field calculator to create new attributes
    - Execute tabular joins with CSV data
    - Perform spatial joins with multiple relationship types
    - Compare one-to-one vs one-to-many results
    - Troubleshoot join issues
    - Summarize joined data
    
    **Time Required**: 2-3 hours
    
    [:octicons-arrow-right-24: Go to Lab 5](../labs/lab05.md)

---

## Next Topic

You've mastered vector operations! Now let's dive into vector geoprocessing tools:

[:octicons-arrow-right-24: Topic 6: Vector Geoprocessing](06-vector-geoprocessing.md)
