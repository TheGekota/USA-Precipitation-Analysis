# USA May Runoff Trend Analysis (2000–2025)

A spatial analysis of 26 years of May total runoff across the continental United States, built with multidimensional raster analysis in ArcGIS Pro. Completed for GGR276 (Spatial Data Science I) at the University of Toronto Mississauga, Winter 2026.

![Standard deviation of May total runoff, continental USA, 2000–2025](StdDev_Precipitation_Map.jpg)

## Summary

- **Where runoff is highest:** The Pacific Northwest and Northeast coasts have the highest average May runoff, with scattered high cells through the Rocky Mountains.
- **Where it varies most:** The same areas. The NW and NE coasts and the Rockies swing the most from year to year, while the interior stays consistently low.
- **How it's changing:** The trend (slope) layer shows declining May runoff along the Northeast coast and parts of the Northwest coast, and increases in the Rocky Mountains (including parts of Colorado and Utah) and the East South Central region. Most of the interior shows little to no change.
- **Shared spikes:** Several locations spike in the same years (the mid-2000s and 2017–2018), which points to large weather systems rather than purely local events. The biggest single spike was about 650 mm at Gallatin National Forest, Montana, in 2018.

> **A note on runoff vs. precipitation:** This project uses *total runoff*, the water that flows off the land surface after evaporation and infiltration. It follows precipitation and snowmelt, but it isn't the same as rainfall, so the findings describe runoff only.

## Data

| Property | Value |
|---|---|
| Variable | Total runoff (mm) |
| Source | NOAA GDAS, provided through the GGR276 course |
| Time period | May of each year, 2000–2025 (26 layers) |
| Coverage | Continental USA |
| Spatial reference | WGS 1984 (maps shown in WGS 1984 Web Mercator Auxiliary Sphere) |

## Method

1. Combined the 26 May runoff layers into one multidimensional raster (time dimension: StdTime).
2. Calculated mean, standard deviation, minimum, and maximum across time for every cell, and a range layer (max − min).
3. Generated a linear trend (slope) layer, in mm per year, to show where May runoff is increasing or decreasing.
4. Extracted temporal profiles at five locations to compare regions.
5. Built finished maps with legends, scale bars, north arrows, and coordinate grids.

Full steps are in [METHODOLOGY.md](METHODOLOGY.md).

## Results at a glance

These are the ranges of cell values in each output layer, not national averages.

| Layer | Cell values | What it shows |
|---|---|---|
| Mean | 0–769 mm | Typical May runoff at each location |
| Standard deviation | 0–1,491 mm | How much May runoff varies year to year |
| Minimum | 0–476 mm | The driest May on record for each cell |
| Maximum | 0–4,747 mm | The wettest May on record for each cell |
| Range | 0–4,709 mm | Spread between the wettest and driest May |

More detail, including the five sample locations, is in [KEY_METRICS_INSIGHTS.md](KEY_METRICS_INSIGHTS.md).

![May total runoff at five locations, 2000–2025](Timeseries_5Locations.png)

## Limitations

- **Runoff is not precipitation.** Results describe surface runoff only.
- **May only.** Each year contributes one month, so this captures late-spring conditions (including snowmelt), not annual totals.
- **Short record.** 26 data points per cell is a short window for climate trends, and no significance testing was done, so the trend layer shows direction, not confirmed long-term change.
- **Sensitive to single events.** One extreme year (like Gallatin in 2018) can noticeably pull a linear slope.
- **Point profiles are single cells.** Each sample location represents one coarse grid cell, not a whole region.

## Next steps

- Add significance testing to the trend layer to separate real trends from noise
- Extend the analysis to all months to compare seasons
- Reproduce the workflow in Python for a fully scripted version
- Publish the trend layer as an interactive web map

## Files

- `README.md` – Project overview (this file)
- `KEY_METRICS_INSIGHTS.md` – Detailed findings and sample locations
- `METHODOLOGY.md` – Step-by-step workflow
- `StdDev_Precipitation_Map.jpg` – Standard deviation map
- `Timeseries_5Locations.png` – Temporal profiles at five locations

## Author

Ava De Mello · University of Toronto Mississauga
[Portfolio](https://thegekota.github.io/Gekotas-Nook/) · [LinkedIn](https://www.linkedin.com/in/ava-de-mello-274778302)
