# INTERVIEW BRIEF — USA Precipitation Analysis
## The 2-Minute Pitch for Recruiters

---

## ⏱️ THE 30-SECOND VERSION

> "I analyzed 25 years of USA precipitation data (2M+ grid cells, 300 monthly snapshots) and found that while coasts remain wettest, rainfall is shifting eastward into the Rocky Mountains. Using spatial statistics and trend analysis, I discovered the Northeast and Northwest are drying (−0.5 mm/year), mountains are intensifying (+1.2 mm/year), revealing a long-term atmospheric circulation shift with water resource implications."

---

## 📊 THE HEADLINE NUMBERS

- **Data scale:** 25 years | 2M+ cells | 300 time steps
- **Key finding:** Coastal drying (−0.5 mm/yr) + mountain wetting (+1.2 mm/yr)
- **Disparity:** Coasts 8–10× wetter than interior; coasts getting drier; mountains getting wetter
- **Outlier sync:** Extreme events (2005, 2017, 2018, 2020) occur across all regions simultaneously
- **Implication:** Water infrastructure based on 1990s assumptions is outdated

---

## 💡 WHY THIS MATTERS (Pick 1–2 based on the role)

### **For Product Analyst roles:**
*"Large datasets require statistical literacy. I used mean, std dev, min, max, and linear regression to extract meaning from 300 raster layers. In a Product Analyst role, I'd apply the same approach to user behavioral data: identify patterns, quantify uncertainty, and tell a story stakeholders can act on."*

### **For Data Analyst roles:**
*"I worked with geospatial data, but the methods are universal: temporal trend detection, anomaly identification, spatial correlation. The precipitation data has analogues in business: customer churn trends, regional market shifts, outlier event detection."*

### **For UX Research + Analytics roles:**
*"This project bridged research and data: I started with a research question (how is precipitation changing?), designed an analysis approach, and interpreted findings for a non-technical audience using maps and visuals. That's the same workflow in UX: gather data, analyze, communicate to stakeholders."*

---

## ✅ SKILLS DEMONSTRATED

| Skill | Evidence |
|-------|----------|
| **Data manipulation** | Stacked 300 layers; calculated statistics across time dimension |
| **Statistics** | Mean, std dev, range, linear regression; understood variability metrics |
| **Spatial reasoning** | Identified coastal vs. interior patterns; connected geography to precipitation |
| **Temporal analysis** | Tracked 25-year trend; identified outlier years (2005, 2017, 2018, 2020) |
| **Visualization** | Professional cartography; designed multi-layer maps with proper legends |
| **Communication** | Translated statistics to actionable insights (e.g., "water infrastructure needs updating") |

---

## 🎯 IF THEY ASK...

**Q: "How does this apply to our work?"**

A: *"This project taught me to work with large, complex datasets, extract patterns, and prioritize findings for decision-makers. If you're building a product, that's what matters: sifting through data to identify what users care about and communicating it clearly. The domain (precipitation vs. user behavior) is secondary to the method."*

**Q: "What was your biggest challenge?"**

A: *"Interpreting variability. The Rocky Mountains showed the strongest positive trend (+1.2 mm/yr), but they still have lower average rainfall than coasts. I realized: trend ≠ absolute value. Communicating that nuance—'wetting doesn't mean wet'—was harder than running the regression."*

**Q: "What surprised you?"**

A: *"Outlier events were synchronized. I expected regional variation, but 2005, 2017, 2018 spiked across geographically distinct regions (NW, NE, Rocky Mountains). That revealed continental-scale systems dominate local variation. For forecasting or risk modeling, that's a critical insight."*

**Q: "How would you improve this?"**

A: *"I'd add interactivity: Jupyter notebooks with widgets to explore different months/regions. I'd incorporate climate model projections (CMIP6) to contextualize whether we're seeing climate change or natural variation. And I'd extend to full-year data, not just May—seasonal patterns matter."*

---

## 📂 WHAT TO SHARE

**GitHub Repo Link:** [link to your repo]

**Quick links to include:**
- 📄 Full README (technical depth)
- 📈 Sample maps (visual proof)
- 📊 Key metrics sheet (this)
- 🔧 Methodology (reproducibility)

**In your portfolio/resume:**
```
USA Precipitation Trend Analysis | Spatial Data Science
• Analyzed 25 years of precipitation data (2M+ grid cells, 300 monthly layers)
• Calculated mean, std dev, min/max, and linear trend slopes per location
• Identified coastal drying (−0.5 mm/year) and mountain intensification (+1.2 mm/year)
• Created professional cartography revealing long-term atmospheric circulation shifts
• Technologies: ArcGIS Pro, Raster Analysis, Geospatial Statistics

[GitHub Repo] | [Live Map] | [Technical Brief]
```

---

## 🎓 PROOF POINTS (If they want credentials)

- **Course:** Spatial Data Science I (GGR276), University of Toronto Mississauga
- **Grade:** [Your grade if 85+]
- **Instructor:** [Name if available]
- **Dataset:** NOAA Global Data Assimilation System (GDAS)
- **Analysis Tools:** ArcGIS Pro, Python (scipy, rasterio), GIS cartography

---

## ⚡ CONVERSATION FLOW (Mock Interview)

**Interviewer:** "Tell me about a data project you're proud of."

**You:** "I analyzed 25 years of US precipitation data to identify regional patterns and trends. I used spatial statistics—calculating mean, variability, and trend slopes—to discover that coasts are drying while mountains are becoming wetter. [Pause for reaction]"

**Interviewer:** "Interesting. What surprised you?"

**You:** "The synchronization of extreme events. Outlier years like 2005 and 2018 spiked across all regions simultaneously, revealing that continental-scale weather systems dominate over local variation. For forecasting, that means risk is correlated—multiple regions fail at once, not independently."

**Interviewer:** "How does that apply here?"

**You:** "It taught me to look for systemic patterns, not just local noise. In your product, I'd do the same: identify whether changes are user-driven (local) or market-driven (systemic). That distinction changes how you respond."

---

## 🚀 READY TO GO?

- [ ] GitHub repo set up with README, methodology, maps
- [ ] This brief memorized (practice 2-min delivery)
- [ ] Sample maps ready to show (high-res JPG, not data files)
- [ ] Key metrics sheet saved to share
- [ ] Portfolio link updated with project

---

## 📸 VISUAL ASSETS TO INCLUDE

1. **Mean Precipitation Map** (shows where it rains)
   - File: `Mean_Precipitation_Map.jpg` (high-res)
   
2. **Standard Deviation Map** (shows variability)
   - File: `StdDev_Precipitation_Map.jpg` (high-res)

3. **Slope/Trend Map** (shows wetting/drying)
   - File: `Slope_Trend_Map.jpg` (high-res, red=drying, green=wetting)

4. **Time-Series Chart** (shows outliers at 5 locations)
   - File: `TimeSeries_5Locations.png` (1000px wide)

5. **One-Page Infographic** (summary of key findings)
   - File: `Project_Summary_1Pager.pdf`

---

## ✨ FINAL TIPS

1. **Lead with impact, not methods.** Say "I discovered precipitation is shifting inland" before "I calculated linear regression."

2. **Know your numbers cold.** Be able to cite: 25 years, 2M cells, −0.5 to +1.2 mm/year trends without notes.

3. **Translate to their domain.** If they ask "why does this matter?" always connect back to decision-making or business impact.

4. **Be honest about limitations.** "25 years is shorter than climate scientists prefer" shows maturity, not weakness.

5. **Use the maps.** Visual proof is powerful. Show a printed map or share screen during video interview.

6. **Practice the pitch.** 30 seconds should be smooth; 2 minutes should have natural pauses for questions.

---

**Last updated:** September 2026  
**Status:** Interview-ready ✅
