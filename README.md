# Agrivoltaic Site Optimizer — Jodhpur District, Rajasthan

Spatial intelligence system for identifying optimal agrivoltaic installation
zones across Jodhpur District, Rajasthan, using **Multi-Criteria Decision
Analysis (MCDA)** combined with **K-Means clustering**.

**Program:** M.Sc. Agriculture Analytics — IIRS-ISRO, Dehradun (Semester 2, 2026)
**Role:** Member 2 — ML & Spatial Analysis Engineer
**Team:** SpatioFarm (Himanshu · Sathwik Ramaka · Swati Patil · K. Yaswanthi)

---

## Key Results

| Metric | Value |
|--------|-------|
| Study Area | Jodhpur District, Rajasthan |
| Total Pixels Analysed | 47,593,250 |
| Agricultural Pixels | 17,041,548 (35.8%) |
| Prime Agrivoltaic Zone (Class 5) | ~3,265 km² |
| MCDA Score Range | 0.60 – 0.70 |
| K-Means Clusters | 5 (elbow point K=3, K=5 selected for alignment) |
| GPU Accelerated | NVIDIA RTX 5060 (CUDA 12.8, PyTorch 2.11) |

---

## MCDA Weight Matrix

| Criterion | Weight | Rationale |
|-----------|--------|-----------|
| Land Use / Land Cover (LULC) | 30% | Identifies agricultural land eligible for agrivoltaic co-location |
| Global Horizontal Irradiance (GHI) | 25% | Solar energy potential — primary driver of PV output |
| Grid Distance | 20% | Proximity to existing power grid reduces infrastructure cost |
| Road Distance | 10% | Accessibility for installation and maintenance |
| Slope | 10% | Terrain suitability for panel installation |
| Aspect | 5% | South-facing orientation preference for solar efficiency |

---

## Pipeline Overview

Cell 1  → Environment verification (PyTorch, GeoPandas, Rasterio)

Cell 2  → MCDA weight matrix definition and validation

Cell 3  → File path configuration

Cell 4  → Raster alignment verification (CRS, resolution, bounds)

Cell 5  → Raster resampling and alignment to reference grid

Cell 6  → LULC agricultural mask generation

Cell 7  → Min-Max normalisation of all layers

Cell 8  → Weighted MCDA composite score computation

Cell 9  → Percentile-based suitability classification (5 tiers)

Cell 10 → K-Means clustering (Elbow method K=2–7, final K=5)

Cell 11 → Results summary and output delivery

---

## Input Data

| Layer | Source | Format |
|-------|--------|--------|
| DEM | SRTM | `.tif` |
| Slope | Derived from DEM | `.tif` |
| Aspect | Derived from DEM | `.tif` |
| LULC | Sentinel-2 classification | `.tif` |
| GHI (Solar Irradiance) | NASA POWER / PVGIS | `.tif` |
| Grid Distance | OSM transmission lines | `.tif` |
| Road Distance | OSM road network | `.tif` |
| AOI Boundary | Jodhpur District | `.shp` |

---

## Tools & Libraries

- **Language:** Python 3.11.9
- **ML/Clustering:** `scikit-learn` (KMeans)
- **Spatial:** `geopandas`, `rasterio`, `numpy`
- **GPU:** PyTorch 2.11 + CUDA 12.8 (RTX 5060)
- **Visualization:** `matplotlib`
- **GIS:** QGIS (output visualisation)

---

## Outputs

| File | Description |
|------|-------------|
| `agrivoltaic_suitability.tif` | MCDA suitability raster (5-class) |
| `cluster_output.tif` | K-Means cluster raster (5 clusters) |
| `elbow_chart.png` | Elbow method plot for optimal K selection |

---

## How to Run

**1. Install dependencies:**

```bash
pip install geopandas rasterio numpy scikit-learn matplotlib torch
```

**2. Set up folder structure:**

agrivoltaic-site-optimizer-jodhpur/

├── data/

│   ├── raw/          ← input rasters and shapefile

│   └── output/       ← auto-created by notebook

└── agrivoltaic_optimizer.ipynb

**3. Run the notebook:**

Open `agrivoltaic_optimizer.ipynb` in Jupyter and run all cells sequentially.

> GPU (CUDA) recommended for large raster processing. CPU fallback works but is slower.

---

## Repository Structure

agrivoltaic-site-optimizer-jodhpur/

├── agrivoltaic_optimizer.ipynb   # Full 11-cell pipeline

├── README.md                     # Project documentation

├── .gitignore                    # Python gitignore

└── LICENSE                       # MIT License

---

## Author

**Sathwik Ramaka**
M.Sc. Agriculture Analytics | Remote Sensing & Carbon MRV
[LinkedIn](https://www.linkedin.com/in/sathwik-ramaka-1ba40227a/) · [GitHub](https://github.com/sathwikramaka)
