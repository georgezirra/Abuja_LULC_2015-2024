# Abuja LULC Change Detection (2015–2024)

**Land Use and Land Cover Change Analysis of Nigeria's Federal Capital Territory using Google Earth Engine, Random Forest Classification, and Multi-Sensor Satellite Imagery.**

---

## Overview

This project maps and quantifies land use and land cover (LULC) changes across the Federal Capital Territory (FCT) of Abuja, Nigeria, between 2015 and 2024. Using cloud-based geospatial processing on Google Earth Engine, I classified Landsat 8 (2015) and Sentinel-2 (2024) imagery into four LULC classes — Urban, Vegetation, Open Land, and Water — and performed change detection to reveal the scale of Abuja's urban transformation over nine years.

Abuja is one of Africa's fastest-growing capitals, with the FCT attracting over 6 million residents since its designation as Nigeria's capital. This study provides a reproducible, data-driven account of how that growth has reshaped the landscape.

---

## Key Findings

| Metric | Value |
|--------|-------|
| Urban area gained (2015–2024) | **1,596 km²** |
| Urban growth factor | **~7×** |
| Vegetation lost | **424 km²** |
| 2015 classification accuracy (Landsat 8) | **89.4%** |
| 2024 classification accuracy (Sentinel-2) | **97.5%** |
| 2024 Kappa coefficient | **0.96** |
| Training sample points | **1,006** |
| Study area | **~8,000 km²** |

### Notable Land Cover Transitions
- Vegetation → Urban: largest single transition driver
- Vegetation → Open Land: 424 km² of conversion
- Open Land → Urban: secondary urbanisation pathway

---

## Study Area

**Location:** Federal Capital Territory (FCT), Abuja, Nigeria  
**Coordinate system:** WGS 84  
**Area covered:** ~8,000 km² (entire FCT, not just AMAC)

> Note: Urban figures in this study are larger than AMAC-focused studies in the literature because the entire FCT is analysed, not just the Abuja Municipal Area Council.

---

## Data Sources

| Year | Sensor | Resolution | Product |
|------|--------|------------|---------|
| 2015 | Landsat 8 OLI | 30 m | USGS Collection 2 Level-2 Surface Reflectance |
| 2024 | Sentinel-2 MSI | 10 m | ESA Copernicus Harmonized Surface Reflectance |

Both datasets were filtered for cloud cover and composited within Google Earth Engine.

---

## Methodology

1. **AOI Definition** — Federal Capital Territory boundary loaded as a feature collection in GEE
2. **Image Compositing** — Median composites built from cloud-masked image collections for each year
3. **Feature Engineering** — Spectral bands + derived indices (NDVI, NDWI, NDBI) computed per image
4. **Training Sample Collection** — 1,006 reference points manually digitised across 4 LULC classes
5. **Classification** — Random Forest (100 trees) trained independently per year on sensor-specific spectral signatures
6. **Accuracy Assessment** — Confusion matrix, overall accuracy, and Kappa coefficient computed for each year
7. **Change Detection** — Pixel-level comparison of 2015 and 2024 classified maps to derive transition matrix
8. **Export** — Classified maps exported as GeoTIFFs at native resolution; change statistics exported as CSV

---

## LULC Classes

| Class | Description |
|-------|-------------|
| 🔴 Urban | Built-up areas, roads, impervious surfaces |
| 🟢 Vegetation | Forest, shrubland, farmland with canopy cover |
| 🟡 Open Land | Bare soil, degraded land, cleared areas |
| 🔵 Water | Rivers, reservoirs, wetlands |

---

## Tools & Technologies

- **Google Earth Engine (GEE)** — Cloud-based geospatial processing platform
- **JavaScript (GEE API)** — Full classification pipeline, change detection, accuracy assessment, export scripting
- **Landsat 8 OLI** — Baseline 2015 imagery (USGS/NASA)
- **Sentinel-2 MSI** — Analysis 2024 imagery (ESA Copernicus)
- **Random Forest** — 100-tree ensemble classifier
- **QGIS / ArcGIS Pro** — Post-processing and cartographic output

---

## Repository Structure

```
abuja-lulc-change-detection/
│
├── scripts/
│   └── abuja_lulc_gee.js        # Main GEE classification & change detection script
│
├── figures/
│   ├── lulc_2015.png             # Classified LULC map — 2015
│   ├── lulc_2024.png             # Classified LULC map — 2024
│   └── change_map.png            # Urban expansion change map 2015–2024
│
├── outputs/
│   ├── lulc_2015.tif             # GeoTIFF export — 2015 classification
│   ├── lulc_2024.tif             # GeoTIFF export — 2024 classification
│   └── change_statistics.csv     # LULC transition matrix (area in km²)
│
├── portfolio/
│   └── abuja-lulc-project.html   # Interactive portfolio page
│
└── README.md
```

---

## How to Run

### Prerequisites
- A Google Earth Engine account ([sign up here](https://earthengine.google.com/))
- No local installation required — all processing runs in the GEE cloud environment

### Steps

1. Open [Google Earth Engine Code Editor](https://code.earthengine.google.com/)
2. Copy the contents of `scripts/abuja_lulc_gee.js` into a new script
3. Click **Run**
4. The script will:
   - Load and composite Landsat 8 (2015) and Sentinel-2 (2024) imagery
   - Apply Random Forest classification
   - Display classified maps in the GEE map panel
   - Print accuracy assessment results to the Console
   - Export GeoTIFFs to your Google Drive (check the Tasks panel)

> The script is fully reproducible. You can swap the AOI boundary for any other region to apply the same methodology elsewhere.

---

## Accuracy Assessment Summary

### 2015 — Landsat 8

| Metric | Value |
|--------|-------|
| Overall Accuracy | 89.4% |
| Kappa Coefficient | 0.85 |

### 2024 — Sentinel-2

| Metric | Value |
|--------|-------|
| Overall Accuracy | 97.5% |
| Kappa Coefficient | 0.96 |

Both results meet and exceed the commonly accepted 85% accuracy threshold for remote sensing classification studies.

---

## Author

**George Zirra**  
GIS Analyst · Remote Sensing  
[Portfolio](https://georgezirra.github.io/my_portfolio/)

---

## License

This project is licensed under the [MIT License](LICENSE). You are free to use, adapt, and share the code with attribution.
