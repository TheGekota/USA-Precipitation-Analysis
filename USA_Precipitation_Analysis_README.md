# 25-Year USA Precipitation & Runoff Trend Analysis

**A spatial data science analysis identifying regional precipitation patterns and long-term trends across the continental United States (2000–2025)**

---

## 🎯 Project Overview

This analysis examines 25 years of monthly runoff data (May 2000–2025) across the continental USA to identify spatial patterns, regional trends, and climate-related shifts in precipitation. Using raster statistics and spatial modeling, the project reveals:

- **Where precipitation is concentrated** (coastal dominance vs. inland aridity)
- **How variability differs by region** (coastal instability vs. inland consistency)
- **Where runoff is increasing/decreasing** (predictive slope analysis)

**Key Finding:** Coastal regions show 3–4× higher precipitation and variability than inland areas, but recent decades show a westward inland shift of runoff into previously dry mountain regions.

---

## 📊 Key Metrics & Insights

### **Summary Statistics (May 2000–2025)**

| Metric | Value | Interpretation |
|--------|-------|-----------------|
| **Mean Precipitation (USA)** | 769 mm | Wide variability: West Coast averages 200+ mm; Desert Southwest ~50 mm |
| **Standard Deviation** | 1,491 mm | High variability regions: Northwest & Northeast coasts; Rocky Mountains |
| **Maximum Recorded** | 4,747 mm | Extreme events concentrated in coastal areas and mountainous terrain |
| **Minimum Recorded** | 0 mm | Persistent dry zones: Interior West, parts of Southwest |
| **Range** | 4,709 mm | Difference between wettest and driest regions |

---

### **Regional Patterns**

#### 🌊 **Highest Precipitation Zones**
- **Pacific Northwest (Portland, OR):** 50–150 mm avg | High variability (coastal storms, atmospheric rivers)
- **Northeast Coast (Boston, MA):** 25–140 mm avg | Variable (nor'easters, hurricanes)
- **East South-Central (TN, MS, AL):** 30–80 mm avg | Moderate variability

#### 🏜️ **Lowest Precipitation Zones**
- **Great Plains (Pierre, SD):** 0–25 mm avg | Extremely consistent (rarely exceeds 25 mm)
- **South Central (Victoria, TX):** 0–25 mm avg | Stable, with rare storm spikes
- **Great Basin/Southwest:** Near-zero baseline

#### ⛰️ **Anomaly Zones (Highest Variability)**
- **Rocky Mountains:** Low baseline BUT extreme events (650+ mm in single months during snow melt)
- **Colorado/Utah:** Historically dry, now showing increasing runoff (positive slope)

---

### **Temporal Trends (2000–2025)**

#### **Declining Regions (Negative Slope)**
- **Northeast Coast:** -0.3 to -0.5 mm/year trend
- **Pacific Northwest:** -0.2 mm/year trend
- **Implication:** Historically wet regions drying, consistent with climate models

#### **Increasing Regions (Positive Slope)**
- **Rocky Mountains:** +0.8 to +1.2 mm/year trend ⚠️ **Strongest positive trend**
- **East South-Central:** +0.4 mm/year trend
- **Interior West (CO, UT, NV):** Now experiencing runoff in historically dry zones
- **Implication:** Precipitation shifting eastward from coasts; inland areas becoming wetter

#### **Stable Regions**
- **Great Plains:** ~0 slope (consistent dryness)
- **Most of interior USA:** Minimal change

---

### **Key Outlier Events**

Extreme precipitation events clustered around specific years, suggesting large-scale climate patterns:

| Year | Region(s) Affected | Magnitude | Likely Cause |
|------|-------------------|-----------|--------------|
| **2005** | Nationwide (all 5 study points spiked) | 60–150 mm | Major hurricane season (Katrina, Rita) |
| **2017** | West Coast, Rocky Mountains | 100–200 mm | Atmospheric river events |
| **2018** | Gallatin National Forest, MT | 650 mm | Extreme snow melt / flooding |
| **2020** | East South-Central region | Multiple peaks | Midwest derecho & wet pattern |

**Insight:** Outliers align across regions, indicating **shared continental weather patterns** rather than local variability.

---

## 📈 Statistical Outputs Generated

### **Raster Layers Created**

1. **Mean Layer** (0–769 mm)
   - Average runoff per cell over 25 years
   - Visualizes "typical" precipitation for each location

2. **Standard Deviation Layer** (0–1,491 mm)
   - Measures year-to-year variability
   - High values = unpredictable; Low values = stable

3. **Minimum Layer** (0–476 mm)
   - Driest single month recorded in each location
   - Identifies baseline precipitation

4. **Maximum Layer** (0–4,747 mm)
   - Wettest single month recorded
   - Highlights extreme event zones

5. **Range Layer** (0–4,709 mm)
   - Difference between max and min
   - Shows total variability over 25 years

6. **Slope Layer** (negative to +1.2 mm/year)
   - Linear trend in precipitation over time
   - **Red (negative):** Drying trends
   - **Green (positive):** Increasing trends
   - **Yellow:** No significant change

---

## 💡 Insights for Data Science Interviews

### **What This Project Demonstrates**

✅ **Statistical Analysis:** Mean, std dev, range, trend slopes  
✅ **Spatial Reasoning:** Identified coastal vs. inland patterns; elevation effects  
✅ **Temporal Analysis:** Tracked 25 years of data; identified multi-year trends  
✅ **Predictive Thinking:** Slope maps predict future precipitation patterns  
✅ **Data Visualization:** Professional cartography with legends, scale, coordinates  
✅ **Domain Knowledge:** Interpreted climate/geography, connected stats to real-world causes  

### **Elevator Pitch**

> "I analyzed 25 years of national precipitation data and found that while coastal regions remain the wettest, runoff is increasingly shifting inland into the Rocky Mountains. By calculating trend slopes, I identified regions drying (-0.5 mm/yr in Northeast) and regions intensifying (+1.2 mm/yr in Rockies), with implications for water resource planning and climate adaptation."

---

## 📂 Project Structure

```
USA-Precipitation-Analysis/
├── README.md                          # This file
├── data/
│   ├── GDAS_Runoff_2000-2025.tif     # Original raster (GDAS dataset)
│   └── data_sources.md               # Citation & metadata
├── analysis/
│   ├── statistical_summary.txt       # Mean, std dev, min, max, range values
│   └── temporal_analysis.csv         # Point-based time series (5 locations)
├── outputs/
│   ├── mean_precipitation_map.tif    # Mean layer raster
│   ├── std_dev_precipitation_map.tif # Standard deviation layer
│   ├── slope_trend_map.tif           # Trend slope (positive/negative change)
│   ├── Mean_Precipitation_Map.jpg    # Cartographic output
│   └── StdDev_Precipitation_Map.jpg  # Cartographic output
├── notebooks/
│   └── analysis_workflow.md          # Step-by-step ArcGIS/spatial process
└── docs/
    ├── METHODOLOGY.md                # Detailed methods & formulas
    └── INTERVIEW_BRIEF.md            # 2-min summary for recruiters
```

---

## 🔧 Methodology

### **Data Source**
- **Dataset:** GDAS (NOAA Global Data Assimilation System) Runoff
- **Temporal Coverage:** May 2000–May 2025 (25 years, monthly resolution)
- **Spatial Coverage:** Continental USA (CONUS)
- **Resolution:** 0.5° × 0.5° grid (~55 km cells)

### **Analysis Steps**

1. **Multidimensional Raster Processing**
   - Stacked monthly runoff rasters into time-series cube
   - Applied ArcGIS "Make Multidimensional Raster" tool

2. **Statistical Layer Derivation**
   - Calculated mean, std dev, min, max across time dimension
   - Generated range (max − min) for variability across 25 years

3. **Trend Analysis**
   - Fitted linear regression per raster cell: `Runoff = a + b*Year`
   - Slope values (b) indicate acceleration/deceleration of precipitation
   - Positive slope = increasing runoff; Negative = decreasing

4. **Temporal Profile Extraction**
   - Extracted time-series data at 5 representative locations (coast, inland, elevation)
   - Analyzed patterns relative to latitude, elevation, climate zone

5. **Cartographic Synthesis**
   - Styled layers with quantile classification for clarity
   - Applied standard GIS cartography (scale bar, north arrow, legend, coordinates)

---

## 📍 Study Points & Trends

### **Location Comparison (May 2000–2025)**

| Location | Region | Avg (mm) | Range (mm) | Trend | Pattern |
|----------|--------|----------|-----------|-------|---------|
| **Portland, OR** | Pacific NW | 100 | 50–150 | Slight decline | High, stable |
| **Boston, MA** | Northeast | 80 | 25–140 | Declining | High variability |
| **Pierre, SD** | Great Plains | 12 | 0–25 | Stable | Low, consistent |
| **Victoria, TX** | South Central | 10 | 0–60 | Stable | Very dry |
| **Gallatin NF, MT** | Rocky Mtn | 45 | 0–650 | Increasing | Extreme outliers |

---

## 🔍 Key Findings Summary

### **Finding 1: Coastal Dominance**
Coastal regions (NW, NE, SE) receive **3–7× more precipitation** than interior regions. This is driven by atmospheric moisture, ocean proximity, and orographic effects.

### **Finding 2: Inland Expansion**
Since ~2017, precipitation patterns show **eastward shift** from coasts into historically dry zones. Rocky Mountain region now experiences extreme events (650+ mm) previously rare.

### **Finding 3: High Variability = High Risk**
Regions with high std dev (coasts, mountains) are **unpredictable year-to-year**, making water resource planning difficult. Great Plains, by contrast, are reliably dry.

### **Finding 4: Climate-Scale Events**
Outlier years (2005, 2017, 2018, 2020) occur **simultaneously across regions**, indicating continental-scale weather patterns (hurricanes, atmospheric rivers, mega-storms) rather than local variation.

### **Finding 5: Drying Coasts, Wetting Mountains**
- Northeast Coast: **−0.5 mm/year** (trend declining)
- Rocky Mountains: **+1.2 mm/year** (trend intensifying)
- Suggests long-term atmospheric circulation shift

---

## 🎓 Academic Context

**Course:** Spatial Data Science I (GGR276)  
**Institution:** University of Toronto Mississauga  
**Instructor:** [Course Instructor]  
**Year:** Winter 2026  

**Learning Outcomes Addressed:**
- Multidimensional raster analysis
- Spatial statistics & inferential methods
- Temporal trend detection
- Professional cartography & interpretation

---

## 📚 Data Sources & Citations

```bibtex
@data{GDAS_2025,
  title={NOAA Global Data Assimilation System (GDAS) Runoff},
  author={NOAA Earth Resources Observation and Science Center},
  year={2025},
  url={https://www.ncei.noaa.gov/products/noaa-global-data-assimilation-system}
}
```

**Spatial Reference:** WGS 84 (EPSG:4326)  
**Projection:** Mercator Auxiliary Sphere (for map outputs)

---

## 🤝 Contact & Usage

**Author:** Ava De Mello  
**Student ID:** 1010862238  
**Last Updated:** September 2026  

**License:** Academic use. For research applications, credit analysis as: 
> "Precipitation trend analysis by Ava De Mello (University of Toronto Mississauga, 2026)"

---

## 📝 How to Use This Repo

1. **For Interviews:** Read this README + download `INTERVIEW_BRIEF.md` (2-min summary)
2. **For Deeper Dive:** Check `METHODOLOGY.md` for step-by-step analysis
3. **For Reproducibility:** Use `.tif` files + analysis workflows to recreate outputs
4. **For Portfolio:** Share link to this repo + sample map images

---

## ✨ Next Steps / Future Work

- [ ] Port analysis to Python (rasterio, xarray for reproducibility)
- [ ] Add interactive Jupyter notebook with visualizations
- [ ] Incorporate climate model data (CMIP6) to contextualize trends
- [ ] Extend to all months (not just May) for annual summary
- [ ] Publish findings as brief technical note

---

**Questions?** Contact: [your-email@utoronto.ca]
