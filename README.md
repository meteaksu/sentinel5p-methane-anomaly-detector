# Sentinel-5P TROPOMI Spatial Methane Analysis & Anomaly Detection

## Executive Summary
This project demonstrates an end-to-end data processing and spatial analytics pipeline using Earth Observation (EO) satellite data. Using raw Level-2 Sentinel-5P (TROPOMI) satellite data from the European Space Agency (ESA / Copernicus), this project extracts atmospheric methane ($\text{CH}_4$) mixing ratios, applies rigorous quality control filtering, and utilizes an in-memory SQL database (**DuckDB**) for statistical spatial baseline computation and $2\sigma$ anomaly tracking.

---

##  Key Features & Technical Highlights

* **Multi-Dimensional Spatial Array Handling (`xarray`):** Ingested complex NetCDF4/HDF5 data structures (`group="PRODUCT"`) containing multi-layered spatial coordinates (time, scanline, ground_pixel).
* **Bias Correction & Quality Assurance:**
  * Replaced raw mixing ratios with `methane_mixing_ratio_bias_corrected` to eliminate systematic surface albedo and optical path biases.
  * Implemented an official ESA quality control threshold (`qa_value > 0.5`) to prune cloudy, high-angle, and noisy pixel observations.
* **In-Process Spatial Analytics (`DuckDB`):** Leveraged DuckDB's fast in-memory SQL execution engine to compute baseline atmospheric statistics and dynamic thresholds without persistent storage overhead.
* **Spatial Anomaly Detection:** Dynamically calculated statistical bounds ($\mu + 2\sigma$) to filter and map localized methane concentration spikes ($\text{CH}_4 > 1932.80\text{ ppb}$).

---

## Analytical Pipeline Workflow

[ Raw Sentinel-5P NetCDF Data ]
│
▼
[ xarray Extraction ] ──► (Latitude, Longitude, Bias-Corrected CH4, qa_value)
│
▼
[ Data Quality Filter ] ──► (qa_value > 0.5 Filter & NaN Masking)
│
▼
[ DuckDB In-Memory Engine ] ──► (Baseline Mean & StdDev Aggregations)
│
▼
[ Spatial Anomaly Isolation ] ──► (Dynamic Filter: CH4 > Baseline + 2σ)
│
▼
[ Matplotlib Spatial Map ] ──► (Publication-ready Visualization)


## Key Results & Metrics

| Metric | Value | Unit / Description |
| :--- | :--- | :--- |
| **Total Valid Data Points** | 3,032 | Filtered spatial pixels (`qa > 0.5`) |
| **Baseline Atmospheric $\text{CH}_4$** | 1,886.64 | Mean Concentration (ppb) |
| **Standard Deviation ($\sigma$)** | 23.08 | Variation Spread (ppb) |
| **Anomaly Detection Threshold** | 1,932.80 | Baseline $+ 2\sigma$ Epsilon |
| **Identified Spatial Anomalies** | 4 | Isolated High-Concentration Clusters |

---

## Tech Stack & Dependencies

* **Language:** Python 3.x
* **Spatial Array Processing:** `xarray`, `numpy`, `pandas`
* **In-Memory SQL Database:** `duckdb`
* **Visualization:** `matplotlib`

---

## How to Run

Clone the repository:
```bash
git clone https://github.com/meteaksu/sentinel5p-methane-anomaly-detector.git
cd sentinel5p-methane-anomaly-detector

Install required packages:
pip install xarray pandas numpy duckdb matplotlib

Place your Sentinel-5P NetCDF file (.nc) in the root directory and run the Jupyter Notebook:
jupyter notebook copernicus.ipynb

   

