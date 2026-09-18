# METHODOLOGY: USA Precipitation & Runoff Analysis
## Step-by-Step Technical Guide

---

## 📋 Overview

This document describes the exact steps used to analyze 25 years of USA precipitation data, generate statistical layers, and identify spatial trends. The workflow is reproducible and can be adapted to other geospatial datasets.

**Tools Used:** ArcGIS Pro 3.x (Spatial Statistics, Raster Analysis tools)  
**Alternative:** GDAL/Python (rasterio, xarray) for open-source reproducibility  
**Data:** NOAA GDAS Runoff (monthly, 0.5° resolution)

---

## 📥 STEP 1: Data Acquisition & Preparation

### **1.1 Data Source**

| Property | Value |
|----------|-------|
| **Dataset** | NOAA Global Data Assimilation System (GDAS) Runoff |
| **Variable** | Total Runoff (mm/month) |
| **Temporal Range** | May 2000 – May 2025 (300 monthly layers) |
| **Spatial Coverage** | Continental USA (±60° to 130°W, 24° to 50°N) |
| **Resolution** | 0.5° × 0.5° (~55 km grid cells) |
| **Spatial Reference** | WGS 84 (EPSG:4326) |
| **Format** | GeoTIFF (.tif, single-band per month) |

**Access:** NOAA EROS Data Center (Earth Resources Observation and Science)  
**URL:** https://www.ncei.noaa.gov/products/noaa-global-data-assimilation-system

### **1.2 Data Organization**

```
raw_data/
├── GDAS_Runoff_202005.tif
├── GDAS_Runoff_202006.tif
├── ...
└── GDAS_Runoff_202505.tif
```

Organize monthly files in chronological order. Use consistent naming: `GDAS_Runoff_YYYYMM.tif`

### **1.3 Data Checks**

- Verify all 300 files present (25 years × 12 months = 300 expected)
- Confirm spatial extent is identical across files
- Check for missing data (NA/NoData values) — document as 0 mm or exclude
- Validate value ranges (typical range: 0–5000 mm for May in USA)

---

## 🔧 STEP 2: Multidimensional Raster Creation

### **2.1 Stack Rasters into Multidimensional Cube**

**ArcGIS Workflow:**

1. Open **ArcGIS Pro**
2. Go to: **Raster Analysis** > **Make Multidimensional Raster**
3. **Input Rasters:** Select all 300 monthly GDAS files
4. **Dimension Definition:** Time (default)
5. **Variable Definition:** Total Runoff (mm)
6. **Temporal Information:**
   - **Start Date:** May 1, 2000
   - **Time Step:** 1 Month
   - **Time Unit:** Monthly
7. **Output:** Save as `GDAS_Runoff_TimeSeries_2000-2025.crf`

**What this does:** Combines 300 separate rasters into a single 3D dataset where you can query any location across all 25 years.

### **2.2 Verify Multidimensional Cube**

In the **Raster Properties** pane, confirm:
- Dimensions tab shows "Time" with 300 slices
- Time range: 2000-05-01 to 2025-05-01
- Data type: Float or Double (not Integer)

---

## 📊 STEP 3: Generate Statistical Layers

Statistical layers extract summary information **across the time dimension** at each grid cell.

### **3.1 Mean Layer**

**Purpose:** Average runoff per cell over 25 years. Shows typical precipitation for each location.

**ArcGIS Steps:**
1. **Raster Analysis** > **Multidimensional Analysis** > **Aggregate Multidimensional Raster**
2. **Input Multidimensional Raster:** `GDAS_Runoff_TimeSeries_2000-2025.crf`
3. **Dimension:** Time
4. **Statistic:** Mean
5. **Aggregation Type:** Entire Time Series (not by year/month)
6. **Output:** `MEAN_GDAS_Runoff_2000-2025.tif`

**Interpretation:**
- High values (200+ mm) = Coastal regions, high precipitation zones
- Low values (0–50 mm) = Interior, desert, arid regions
- Map shows "typical" runoff for May

**Expected Range:** 0–769 mm (min to max across USA)

---

### **3.2 Standard Deviation Layer**

**Purpose:** Measures year-to-year variability. High values = unpredictable; Low values = stable.

**ArcGIS Steps:**
1. **Raster Analysis** > **Multidimensional Analysis** > **Aggregate Multidimensional Raster**
2. **Input Multidimensional Raster:** `GDAS_Runoff_TimeSeries_2000-2025.crf`
3. **Dimension:** Time
4. **Statistic:** Standard Deviation
5. **Aggregation Type:** Entire Time Series
6. **Output:** `STDDEV_GDAS_Runoff_2000-2025.tif`

**Interpretation:**
- High std dev (500+ mm) = Coastal regions, high variability from storms/hurricanes
- Low std dev (0–100 mm) = Great Plains, consistent/predictable
- Ratio of std dev to mean = "Coefficient of Variation" (CoV)
  - CoV > 1.0 = Highly variable (risky for planning)
  - CoV < 0.5 = Stable (predictable)

**Expected Range:** 0–1,491 mm

---

### **3.3 Minimum Layer**

**Purpose:** Lowest single month of runoff in the 25-year record. Shows driest conditions.

**ArcGIS Steps:**
1. **Raster Analysis** > **Multidimensional Analysis** > **Aggregate Multidimensional Raster**
2. **Statistic:** Minimum
3. **Output:** `MIN_GDAS_Runoff_2000-2025.tif`

**Interpretation:**
- Reveals baseline precipitation (can be 0 mm in driest zones)
- Identifies reliably dry regions
- Used with Maximum layer to understand range

**Expected Range:** 0–476 mm

---

### **3.4 Maximum Layer**

**Purpose:** Highest single month runoff. Shows extreme event zones.

**ArcGIS Steps:**
1. **Raster Analysis** > **Multidimensional Analysis** > **Aggregate Multidimensional Raster**
2. **Statistic:** Maximum
3. **Output:** `MAX_GDAS_Runoff_2000-2025.tif`

**Interpretation:**
- Identifies regions prone to extreme precipitation events
- Coastal & mountain regions show 2000–5000 mm (atmospheric rivers, hurricanes)
- Used for flood risk planning

**Expected Range:** 0–4,747 mm

---

### **3.5 Range Layer**

**Purpose:** Difference between max and min. Shows total variability.

**Calculation (Raster Calculator):**
```
Range = Maximum − Minimum
```

**ArcGIS Steps:**
1. **Raster Analysis** > **Raster Calculator**
2. **Expression:** `MAX_GDAS_Runoff_2000-2025 - MIN_GDAS_Runoff_2000-2025`
3. **Output:** `RANGE_GDAS_Runoff_2000-2025.tif`

**Interpretation:**
- High values (3000+ mm) = Coastal/mountain areas with extreme swings
- Low values (0–500 mm) = Stable interior regions
- **Different from std dev:** Range shows total span; std dev shows clustering

**Expected Range:** 0–4,709 mm

---

## 📈 STEP 4: Trend Analysis (Linear Regression per Cell)

**Purpose:** Quantify whether each location is getting wetter or drier over time.

### **4.1 Extract Time-Series per Cell**

Before running regression, verify data quality by extracting time-series at known points.

**Sample Points (for QA/QC):**
- Portland, OR (West Coast): Expected 50–150 mm/month
- Boston, MA (East Coast): Expected 25–140 mm/month
- Pierre, SD (Great Plains): Expected 0–25 mm/month

**ArcGIS Steps:**
1. Create point shapefile with known locations
2. **Spatial Analysis** > **Sample** (sample raster at point locations)
3. Export as CSV: `TimeSeries_SamplePoints.csv`

**Expected output:**
```
Location, Date, Runoff_mm
Portland_OR, 2000-05-01, 95
Portland_OR, 2000-06-01, 88
...
Pierre_SD, 2000-05-01, 12
Pierre_SD, 2000-06-01, 8
```

### **4.2 Fit Linear Regression per Cell**

**Formula:**
```
Runoff(year) = a + b * Year
```

Where:
- **a** = intercept (baseline runoff at year 2000)
- **b** = slope (mm/year change; positive = wetting, negative = drying)
- **Year** = number since 2000 (0–25)

**ArcGIS Steps (using Band Math / Raster Calculator):**

Since ArcGIS doesn't have built-in per-cell regression, use Python alternative or manual approach:

1. **Manual Approach:**
   - Export multidimensional data to NetCDF
   - Process in Python (xarray + numpy) or R (raster package)

2. **Python Approach (recommended):**

```python
import rasterio
import numpy as np
from scipy import stats
import rasterio.transform

# Load all 300 monthly rasters
years = np.arange(0, 25.084, 1/12)  # 0 to 25 years (monthly)
runoff_stack = []

for month in range(300):
    with rasterio.open(f'GDAS_Runoff_{month:03d}.tif') as src:
        runoff_stack.append(src.read(1).flatten())

runoff_array = np.array(runoff_stack)  # Shape: (300 months, N cells)

# Calculate slope per cell
slopes = np.zeros(runoff_array.shape[1])
for cell in range(runoff_array.shape[1]):
    slope, intercept, r_value, p_value, std_err = stats.linregress(years, runoff_array[:, cell])
    slopes[cell] = slope

# Reshape back to raster and save
slopes_raster = slopes.reshape(original_shape)
# ... save as GeoTIFF
```

**Output:** `SLOPE_GDAS_Runoff_2000-2025.tif`

### **4.3 Interpret Slope Values**

| Slope (mm/year) | Interpretation | Example |
|-----------------|-----------------|---------|
| **+1.2** | Rapidly wetting (wetter each year) | Rocky Mountains |
| **+0.4** | Moderately wetting | East South-Central |
| **0.0** | No trend (stable) | Great Plains |
| **−0.3** | Moderately drying | Northeast Coast |
| **−0.5** | Rapidly drying (drier each year) | Pacific Northwest |

**Statistical Significance:**
- Slopes > ±0.3 mm/year are meaningful over 25 years (±7.5 mm total change)
- Slopes < ±0.1 mm/year are within noise; treat as stable

---

## 🎨 STEP 5: Cartographic Visualization

### **5.1 Classification Schemes**

**For Mean Layer (0–769 mm):**
- Use Quantile (5 classes) or Natural Breaks (Jenks)
- Recommended: Natural Breaks to highlight distinct regions

**Classes:**
- 0–50 mm (light yellow) = Arid
- 50–100 mm (yellow) = Semi-arid
- 100–200 mm (light blue) = Moderate
- 200–400 mm (blue) = Wet
- 400+ mm (dark blue) = Very wet

**For Slope Layer (−0.5 to +1.2 mm/year):**
- Diverging color scheme (Red = drying, Yellow = stable, Green = wetting)
- Classes: <−0.3 (red), −0.3 to 0 (orange), 0 to +0.3 (yellow), +0.3 to +0.8 (light green), >+0.8 (dark green)

### **5.2 Map Elements**

**Required for professional output:**
- ✅ Title: "Mean Total Monthly Runoff (mm) in Continental USA (May 2000–2025)"
- ✅ Legend: Labeled, color-coded classes
- ✅ Scale bar: 0–500–1000 km
- ✅ North arrow: Standard compass
- ✅ Coordinate grid: Latitude/longitude labels (±5° intervals)
- ✅ Data source: "NOAA GDAS (2025)"
- ✅ Author: "Ava De Mello, Student ID 1010862238"
- ✅ Projection: WGS 84 Web Mercator Auxiliary Sphere
- ✅ Date: "September 2026"

### **5.3 Export Settings**

**For presentations/portfolios:**
- Export as **GeoTIFF** (maintains georeferencing) + **JPG** (visual presentation)
- Resolution: 300 dpi (print quality)
- Extent: Clip to CONUS (exclude Alaska/Hawaii for clarity)

---

## ✅ STEP 6: Validation & Quality Assurance

### **6.1 Sanity Checks**

Before finalizing, verify:

- [ ] **Coastal regions are wetter than interior** (Mean map shows blue coasts, yellow interior)
- [ ] **Coasts have higher variability** (Std Dev map peaks on coasts, flat inland)
- [ ] **Outlier years visible in time series** (2005, 2017, 2018 peaks in charts)
- [ ] **Slope map shows negative values on coasts, positive on mountains** (Red/green pattern)
- [ ] **Range layer is similar to std dev × 2** (Approximate check)

### **6.2 Accuracy Assessment**

Compare outputs to known climate patterns:

| Expected Pattern | Your Result | Match? |
|------------------|------------|--------|
| PNW (Portland) wet | 50–150 mm mean ✓ | ✓ |
| Great Plains dry | 0–25 mm mean ✓ | ✓ |
| Summer more rain than winter | May avg reasonable ✓ | ✓ |
| Coastal storms exist | High max values ✓ | ✓ |

### **6.3 Document Assumptions**

- **Missing data handling:** Treat as 0 mm (conservative)
- **Scale of inference:** Cell-based (0.5° = ~55 km); don't apply to sub-cell accuracy
- **Temporal limitations:** 25 years is short for climate; 30+ year standard is preferred
- **Bias:** May data only; full-year analysis needed for annual summary

---

## 📊 STEP 7: Generate Final Statistical Summary

### **7.1 Tabular Summary**

Create a summary table with statistics per region:

```
Region            Mean(mm)  Std(mm)  Min(mm)  Max(mm)  Slope(mm/yr)  Interpretation
Pacific NW        95        45       50       150      -0.2          Wet, slightly drying
Northeast         80        55       25       140      -0.5          Wet, rapidly drying
Great Plains      12        8        0        25       +0.1          Dry, stable
Rocky Mountains   45        120      0        650      +1.2          Highly variable, wetting
East South Cent   55        25       20       95       +0.4          Moderate, wetting
```

### **7.2 Correlation Analysis (Optional)**

If adding elevation data:
```
Correlation(Elevation, Mean Runoff) = r
Correlation(Elevation, Std Dev Runoff) = r
```

Higher elevation → lower mean (mountains colder → less evaporation)  
Higher elevation → higher variability (extreme events at peaks)

---

## 🔄 REPRODUCIBILITY CHECKLIST

- [ ] Raw data (300 .tif files) documented with URLs
- [ ] Multidimensional raster creation steps recorded
- [ ] Statistical layer calculations documented (mean, std dev, etc.)
- [ ] Slope regression code saved (Python/R script)
- [ ] Classification schemes recorded (for each layer)
- [ ] Cartographic settings documented (colors, fonts, scale)
- [ ] Validation results published (sanity checks passed)
- [ ] Data publication ready (GitHub repo with methods + outputs)

---

## 📚 References & Further Reading

### **Data Sources**
- NOAA GDAS: https://www.ncei.noaa.gov/products/noaa-global-data-assimilation-system
- USGS Earth Explorer: https://earthexplorer.usgs.gov/

### **Methods**
- ArcGIS Raster Analysis: https://desktop.arcgis.com/en/arcmap/latest/tools/spatial-analyst-toolbox/
- Multidimensional Raster Analysis: https://pro.arcgis.com/en/pro-app/latest/help/analysis/raster-analysis/multidimensional-raster-analysis.htm

### **Climate Context**
- IPCC Climate Change Report (2021): Regional precipitation trends
- NOAA Climate.gov: USA Precipitation Trends (https://www.climate.gov/news)

---

## 📝 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | Sept 2026 | Initial methodology document |
| 1.1 | — | (Placeholder for future updates) |

---

**Prepared by:** Ava De Mello  
**Course:** Spatial Data Science I (GGR276)  
**Institution:** University of Toronto Mississauga  
**Date:** September 2026
