# USA Precipitation & Runoff Trend Analysis

A spatial data science analysis identifying regional precipitation patterns and long-term trends across the continental United States (2000–2025)

## Overview

This analysis examines 25 years of monthly runoff data across the continental USA to identify spatial patterns, regional trends, and climate-related shifts in precipitation. Using raster statistics and spatial modeling, the project reveals where precipitation is concentrated, how variability differs by region, and where runoff is increasing or decreasing.

Key Finding: Coastal regions show high precipitation but are drying. Mountain regions are becoming wetter. This suggests a westward shift in atmospheric precipitation patterns with implications for water resource planning.

## Key Metrics

| Metric | Value | Interpretation |
|--------|-------|-----------------|
| Mean Precipitation (USA) | 769 mm | Wide variability across regions |
| Standard Deviation | 1,491 mm | High variability in coastal and mountain zones |
| Maximum Recorded | 4,747 mm | Extreme events in coastal/mountain regions |
| Minimum Recorded | 0 mm | Persistent dry zones in interior West |
| Range | 4,709 mm | Vast difference between wettest and driest regions |

## Key Findings

### Coastal Dominance with Coastal Decline
Coasts receive 3–7 times more precipitation than interior regions, but both coasts show negative slopes (−0.5 mm/year), meaning they're drying over 25 years.

### The Inland Shift
Interior West now experiences extreme events (650+ mm) previously rare. The Rocky Mountain region shows the strongest positive trend (+1.2 mm/year).

### Great Plains Consistency
Great Plains are reliably dry but highly predictable (low variability). This makes water planning simpler but highlights chronic water stress.

### Synchronized Outlier Events
Extreme precipitation years (2005, 2017, 2018, 2020) occurred simultaneously across regions, indicating continental-scale weather systems drive precipitation rather than local variation.

## Regional Patterns

Highest Precipitation: Pacific Northwest (Portland, OR) and Northeast (Boston, MA) - 80-100 mm average

Lowest Precipitation: Great Plains (Pierre, SD) and South Central (Victoria, TX) - 10-12 mm average

Highest Variability: Rocky Mountains and Coastal Regions - std dev 300+ mm

Strongest Positive Trend: Rocky Mountains (+1.2 mm/year)

Strongest Negative Trend: Northeast Coast (−0.5 mm/year)


## Skills Demonstrated

- Spatial Statistics: Mean, standard deviation, min/max, range calculations
- Temporal Analysis: 25-year trend detection via linear regression
- Raster Analysis: Multidimensional data processing (2M+ grid cells)
- Data Visualization: Professional cartography with ArcGIS Pro
- Communication: Clear documentation of complex spatial analysis
- Domain Knowledge: Understanding climate, geography, and water resources

## Methodology

Analysis Steps:
1. Stacked 300 monthly raster layers into multidimensional cube
2. Calculated mean, std dev, min, max, range across time dimension
3. Fitted linear regression per grid cell to derive trend slopes
4. Extracted time-series at 5 representative locations
5. Created professional cartographic outputs with legends, scale bars, and coordinates

Tools: ArcGIS Pro 3.x, NOAA GDAS Runoff data

## Data Source

NOAA Global Data Assimilation System (GDAS) Runoff
- Temporal Range: May 2000 – May 2025 (25 years, monthly resolution)
- Spatial Coverage: Continental USA
- Resolution: 0.5° × 0.5° grid (~55 km cells)
- Variables: Total Runoff (mm)

## Key Insights for Interviews

Coastal Drying Crisis: Historically wet regions are becoming less reliable for water supply planning

Inland Intensification: Previously dry mountain regions now experience extreme precipitation events

Synchronized Risk: Outlier years occur simultaneously across regions—risk is correlated, not independent

Implications: Water infrastructure built on 1990s assumptions is becoming obsolete

## Files

- README.md - This file (project overview)
- KEY_METRICS_INSIGHTS.md - Detailed findings and statistics
- METHODOLOGY.md - Technical workflow and reproducibility
- sample_maps/ - Professional cartographic outputs
- data/ - NOAA data source documentation
- analysis/ - Statistical summary tables

## Contact

Ava De Mello
Course: Spatial Data Science I
Institution: University of Toronto Mississauga

---

Created: March 2026
