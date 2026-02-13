# Topic 11: Spatial Interpolation

## Overview

Spatial interpolation creates continuous surfaces from point data, allowing you to estimate values at unsampled locations. This is essential for creating surfaces like temperature maps, precipitation zones, or elevation models from scattered measurements.

---

## Learning Objectives

By the end of this topic, you should be able to:

- Understand the concept of spatial interpolation
- Distinguish between deterministic and geostatistical methods
- Apply IDW, Spline, and Kriging interpolation
- Choose appropriate interpolation methods for different data types
- Evaluate interpolation accuracy
- Create continuous surfaces from point data

---

## What is Spatial Interpolation?

<div class="admonition definition" markdown>
<p class="admonition-title">Definition</p>

**Spatial interpolation** estimates unknown values at locations where no measurements exist, based on known values at nearby sampled points.

</div>

### The Core Concept

**Given**: Sample points with known values (e.g., temperature at weather stations)

**Goal**: Estimate values everywhere else (create continuous surface)

**Assumption**: Nearby things are more similar than distant things (Tobler's First Law of Geography)

![Interpolation Concept](../images/interpolation-concept.png)
*From point measurements to continuous surface*

---

## When to Use Interpolation

**Common applications**:

**Climate & Weather**:
- Temperature surfaces from weather stations
- Precipitation maps from rain gauges
- Air quality from monitoring sites

**Environmental**:
- Soil properties from sample points
- Groundwater levels from wells
- Pollution concentration from sensors

**Topography**:
- Elevation (DEM) from survey points
- Bathymetry from depth soundings

**Socioeconomic**:
- Population density from census centroids
- Property values from sales data
- Disease rates from reported cases

---

## Types of Interpolation

### Deterministic Methods

**Based on mathematical formulas**:
- Use measured values only
- No probability assessment
- Faster to compute

**Examples**: IDW, Spline, Trend Surface

---

### Geostatistical Methods

**Based on statistical models**:
- Consider spatial autocorrelation
- Provide error estimates
- More computationally intensive

**Examples**: Kriging (Ordinary, Universal, Simple)

---

## Inverse Distance Weighting (IDW)

### How IDW Works

**Principle**: Closer points have more influence

**Formula**:
```
Z(s₀) = Σ(wᵢ × zᵢ) / Σ(wᵢ)

where:
wᵢ = 1 / (dᵢ)^p

Z(s₀) = estimated value at location s₀
zᵢ = known value at point i
dᵢ = distance from s₀ to point i
p = power parameter (usually 2)
```

**In plain English**:
1. Find nearby sample points
2. Weight each by inverse of distance
3. Weighted average = interpolated value

---

### IDW Parameters

**Power (p)**:
- **p = 1**: Linear decay with distance
- **p = 2**: Quadratic decay (default, most common)
- **Higher p**: Closer points dominate more

**Search radius**:
- **Fixed**: Use all points within X meters
- **Variable**: Use N nearest neighbors

**Barriers**:
- Optional: Prevent interpolation across barriers (mountains, rivers)

---

### IDW Characteristics

**Advantages** ✅:
- Simple to understand and explain
- Fast computation
- No assumptions about data distribution
- Good for evenly distributed points

**Disadvantages** ❌:
- No error assessment
- "Bull's eye" pattern around points
- Exact interpolator (passes through points)
- Sensitive to outliers
- Tends toward local mean (no peaks/valleys between points)

**Best for**:
- Quick exploratory analysis
- Evenly distributed data
- Simple presentations

---

## Spline Interpolation

### How Spline Works

**Principle**: Fit smooth curves that minimize surface curvature

**Analogy**: Like bending a flexible metal plate through the points

**Types**:

**Regularized Spline**:
- Smooth surface
- May not pass exactly through points
- Better for noisy data

**Tension Spline**:
- Follows points more closely
- Less smooth
- Better for accurate data

---

### Spline Characteristics

**Advantages** ✅:
- Very smooth surfaces
- Good for natural phenomena (temperature, elevation)
- Visually appealing
- Handles gradual trends well

**Disadvantages** ❌:
- Can create unrealistic peaks/valleys
- Overshoots possible
- Sensitive to outliers
- No error estimates

**Best for**:
- Smooth, continuous phenomena
- Elevation, temperature
- Clean data without errors

---

## Kriging

### What is Kriging?

**Most sophisticated interpolation method!**

**Named after**: Danie Krige (South African mining engineer)

**Principle**: Use spatial autocorrelation structure to:
1. Weight nearby points
2. Estimate values
3. Provide uncertainty estimates

---

### Kriging Process

**Step 1: Semivariogram Analysis**

Calculate how similarity decreases with distance:

```
γ(h) = 1/(2N) × Σ[z(xᵢ) - z(xᵢ+h)]²

where:
γ(h) = semivariance at distance h
N = number of point pairs at distance h
z = measured values
```

**Step 2: Model Fitting**

Fit theoretical model to semivariogram:
- Spherical
- Exponential
- Gaussian
- Linear

**Step 3: Interpolation**

Use model to weight nearby points and estimate values

**Step 4: Validation**

Assess prediction errors

---

### Semivariogram Components

![Semivariogram](../images/semivariogram.png)
*Typical semivariogram showing range, sill, and nugget*

**Nugget**:
- Variation at zero distance
- Measurement error + micro-scale variation

**Sill**:
- Maximum variance
- Where curve levels off

**Range**:
- Distance where correlation stops
- Beyond range = spatially independent

---

### Types of Kriging

**Ordinary Kriging**:
- Most common
- Assumes constant unknown mean
- Best for most applications

**Universal Kriging**:
- Accounts for trends in data
- Removes drift before interpolating

**Simple Kriging**:
- Assumes known constant mean
- Rarely used in practice

**Indicator Kriging**:
- For categorical or binary data
- Estimates probability of exceeding threshold

---

### Kriging Characteristics

**Advantages** ✅:
- Best Linear Unbiased Predictor (BLUP)
- Provides error estimates (prediction variance)
- Honors spatial structure in data
- Can incorporate trends
- Optimal weights for each point

**Disadvantages** ❌:
- Complex to understand
- Requires expertise (semivariogram modeling)
- Computationally intensive
- Needs sufficient data points (>30 recommended)
- Assumes stationarity

**Best for**:
- Important decisions requiring error estimates
- Scientific research
- Sparse, valuable data
- Natural resources (mining, groundwater)

---

## Comparison of Methods

| Method | Speed | Smoothness | Errors | Outliers | Best For |
|--------|-------|------------|--------|----------|----------|
| **IDW** | Fast | Moderate | None | Sensitive | Quick analysis, dense data |
| **Spline** | Moderate | Very smooth | None | Sensitive | Smooth phenomena, clean data |
| **Kriging** | Slow | Depends on model | Yes | Less sensitive | Scientific analysis, sparse data |

---

## Choosing an Interpolation Method

### Decision Framework

```
What type of data?
│
├─ Densely sampled, evenly distributed
│  └─ Use IDW (fast, good enough)
│
├─ Smooth, continuous phenomenon
│  └─ Use Spline (temperature, elevation)
│
├─ Sparse, valuable data needing accuracy
│  └─ Use Kriging (provides errors)
│
└─ Exploratory analysis
   └─ Try multiple, compare
```

---

### Data Considerations

**Sample size**:
- **< 30 points**: IDW or Spline
- **30-100 points**: Any method
- **> 100 points**: Kriging becomes feasible

**Distribution**:
- **Clustered**: Kriging handles better
- **Even grid**: IDW works well
- **Random**: Any method

**Phenomenon**:
- **Smooth gradients**: Spline
- **Localized effects**: IDW
- **Complex patterns**: Kriging

**Accuracy needs**:
- **General pattern**: IDW
- **Precise estimates**: Kriging

---

## Performing Interpolation in GIS

### IDW in QGIS

**Tool**: IDW Interpolation

**Steps**:
1. Raster → Interpolation → IDW Interpolation
2. Select input point layer
3. Choose interpolation attribute
4. Set power parameter (usually 2)
5. Define output raster extent and resolution
6. Run

---

### Spline in QGIS

**Tool**: TIN Interpolation or GRASS r.surf.idw

**GRASS r.surf.contour** for smooth surfaces:
1. Processing Toolbox → GRASS → r.surf.contour
2. Input points with values
3. Set output resolution
4. Run

---

### Kriging in QGIS

**Tool**: SAGA Ordinary Kriging

**Steps**:
1. Processing Toolbox → SAGA → Ordinary Kriging
2. Select points and field
3. Choose variogram model (spherical often good)
4. Set range (based on data exploration)
5. Define grid extent and resolution
6. Run

**Output**: 
- Prediction grid
- Variance grid (prediction error)

---

## Validating Interpolation

### Cross-Validation

**Leave-One-Out Method**:

1. Remove one point
2. Interpolate at that location using remaining points
3. Compare predicted vs actual value
4. Repeat for all points

**Metrics**:

**Mean Error (ME)**:
```
ME = Σ(predicted - actual) / n
```
- Should be close to 0
- Indicates bias

**Root Mean Square Error (RMSE)**:
```
RMSE = √[Σ(predicted - actual)² / n]
```
- Lower is better
- Same units as data
- Measures average error magnitude

**Mean Absolute Error (MAE)**:
```
MAE = Σ|predicted - actual| / n
```
- Easier to interpret than RMSE
- Less sensitive to outliers

---

### Visual Assessment

**Check for**:
- Unrealistic values (negative elevations, etc.)
- Artificial peaks/valleys between points
- Bull's eye patterns (IDW)
- Over-smoothing
- Edge effects

**Compare**:
- Different methods
- Different parameters
- Known ground truth

---

## Best Practices

### Data Preparation

1. **✅ Check for outliers** - Remove or investigate errors
2. **✅ Ensure data quality** - Accurate measurements matter
3. **✅ Transform if needed** - Log transform skewed data
4. **✅ Check spatial distribution** - Avoid large gaps
5. **✅ Use appropriate units** - Consistent measurement units

---

### Parameter Selection

1. **✅ Test multiple parameters** - Compare results
2. **✅ Use cross-validation** - Quantify accuracy
3. **✅ Consider phenomenon** - Match method to data type
4. **✅ Set appropriate resolution** - Match data density
5. **✅ Define reasonable extent** - Don't extrapolate too far

---

### Interpretation

1. **✅ Show uncertainty** - Especially for Kriging
2. **✅ Don't over-interpolate** - Sparse data = high uncertainty
3. **✅ Consider barriers** - Rivers, mountains affect patterns
4. **✅ Validate with known data** - Ground truth when possible
5. **✅ Document methods** - Record parameters used

---

## Common Applications

### Climate Mapping

**Task**: Create temperature surface from weather stations

**Method**: Ordinary Kriging
- Captures spatial autocorrelation
- Provides error estimates
- Accounts for elevation trend (Universal Kriging)

---

### Elevation Modeling

**Task**: Create DEM from survey points

**Method**: Spline or Kriging
- Spline for smooth terrain
- Kriging for complex topography
- TIN for irregular distributions

---

### Soil Properties

**Task**: Map soil pH from sample points

**Method**: Ordinary Kriging
- Soil properties spatially autocorrelated
- Samples expensive, need accuracy
- Error estimates guide future sampling

---

### Pollution Mapping

**Task**: Air quality surface from monitors

**Method**: IDW or Kriging
- IDW for quick assessment
- Kriging for regulatory work
- Consider barriers (mountains)

---

## Key Takeaways

<div class="admonition success" markdown>
<p class="admonition-title">✅ Remember These Points</p>

1. **Interpolation estimates unknown values** - From known sample points
2. **Nearby points matter more** - Tobler's First Law
3. **IDW is simple and fast** - Good for quick analysis
4. **Spline creates smooth surfaces** - Best for gradual phenomena
5. **Kriging is most sophisticated** - Provides error estimates
6. **Choose based on data & needs** - No single best method
7. **Validate your results** - Cross-validation quantifies errors
8. **Don't extrapolate too far** - Uncertainty increases with distance

</div>

---

## Further Reading

- [QGIS Interpolation Tutorial](https://docs.qgis.org/3.28/en/docs/user_manual/processing_algs/qgis/interpolation.html)
- [Kriging Explained](https://pro.arcgis.com/en/pro-app/latest/tool-reference/3d-analyst/how-kriging-works.htm)
- [Semivariogram Modeling](https://desktop.arcgis.com/en/arcmap/latest/extensions/geostatistical-analyst/understanding-a-semivariogram.htm)

---

## Lab Exercise

!!! lab "Lab 11: Spatial Interpolation"
    In [Lab 11](../labs/lab11.md), you'll:
    
    - Create temperature surfaces from weather station data
    - Apply IDW, Spline, and Kriging methods
    - Compare interpolation methods visually
    - Perform cross-validation
    - Calculate RMSE for each method
    - Model semivariograms for Kriging
    - Create prediction and error surfaces
    
    **Time Required**: 3-4 hours
    
    [:octicons-arrow-right-24: Go to Lab 11](../labs/lab11.md)

---

## Next Topic

You've mastered interpolation! Next, learn about workflow design and automation:

[:octicons-arrow-right-24: Topic 12: Workflow Design & Automation](12-workflow-design.md)
