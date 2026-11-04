# METHODOLOGY.md

Workflow for the USA May Runoff Trend Analysis (2000–2025), completed in ArcGIS Pro 3.x.

## Data

| Property | Value |
|---|---|
| Dataset | NOAA GDAS total runoff, provided through GGR276 |
| Time period | May of each year, 2000–2025 (26 layers) |
| Coverage | Continental USA |
| Units | Millimetres (mm) |
| Spatial reference | WGS 1984 |

Before analysis, I checked that all 26 layers were present, shared the same extent, and had values in a plausible range.

## Step 1: Build a multidimensional raster

**Tool:** Make Multidimensional Raster Layer

I combined the 26 May layers into a single multidimensional raster with time (StdTime) as the dimension. This makes it possible to view the whole time series and query any cell across all years.

## Step 2: Calculate statistical layers

**Tool:** Aggregate Multidimensional Raster (across the full time series)

| Statistic | What it shows | Cell values |
|---|---|---|
| Mean | Typical May runoff at each cell | 0–769 mm |
| Standard deviation | How far each year varies from the mean | 0–1,491 mm |
| Minimum | Lowest May runoff recorded at each cell | 0–476 mm |
| Maximum | Highest May runoff recorded at each cell | 0–4,747 mm |

**Range layer:** calculated with Raster Calculator as Maximum − Minimum (cell values 0–4,709 mm).

Note: the range layer's highest value (4,709 mm) is lower than the maximum layer's highest value (4,747 mm) because range is calculated per cell. The cell with the highest maximum also has a minimum above zero.

## Step 3: Trend analysis

**Tool:** Generate Trend Raster (linear trend)

I fit a linear trend to each cell's 26 values to create a slope layer, in mm per year:

- **Positive slope (green):** May runoff increasing over time
- **Near zero (yellow):** little or no change
- **Negative slope (red):** May runoff decreasing over time

## Step 4: Temporal profiles

I extracted time series at five locations to compare regions:

| Location | Region represented |
|---|---|
| Portland, OR | West Coast |
| Boston, MA | East Coast |
| Pierre, SD | Inland Midwest |
| Victoria, TX | South Coast |
| Gallatin National Forest, MT | Rocky Mountains (personal point of interest) |

## Step 5: Cartography

Each map includes a title, legend, scale bar, north arrow, coordinate grid labels, and coordinate system details. Maps are displayed in WGS 1984 Web Mercator Auxiliary Sphere.

## Quality checks

- Confirmed all 26 layers were present with matching extents
- Compared statistical layers against the original time series to make sure the patterns matched what was visible in the data (for example, high variability on the NW and NE coasts)
- Checked that outlier years in the temporal profiles also appeared in the maximum and range layers

## Limitations

- Uses runoff, not precipitation
- One month (May) per year, so results reflect late-spring and snowmelt conditions
- 26 data points per cell, with no significance testing on the trend layer
- Linear trends can be pulled by single extreme years
- Each sample location is a single coarse grid cell

## Reproducing this analysis

1. Obtain the 26 May total runoff layers (2000–2025)
2. Follow Steps 1–3 in ArcGIS Pro using the tools named above
3. Use the temporal profile tool on the five locations in Step 4
