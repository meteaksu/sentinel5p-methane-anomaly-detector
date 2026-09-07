# Sentinel-5P TROPOMI Spatial Methane Emission & Anomaly Detector

## 📌 Executive Summary
This project builds an end-to-end spatial data pipeline to detect and monitor point-source atmospheric methane ($\text{CH}_4$) concentration patterns using satellite imagery from the **Sentinel-5P TROPOMI** instrument. 

By integrating multi-dimensional satellite telemetry (`.nc` format) with **DuckDB** spatial queries and **Matplotlib** heatmaps, the framework establishes regional background concentration baselines ($\mu = 1867.4 \text{ ppb}$) and isolates statistically significant emission spikes ($>2\sigma$) for Climate Tech risk monitoring and ESG regulatory tracking.

---

## 🛠️ Tech Stack & Methodology
* **Telemetry & Spatial Processing:** `xarray`, `netCDF4`, `Pandas`, `NumPy`
* **In-Memory Spatial SQL Engine:** `DuckDB`
* **Geospatial Visualization:** `Matplotlib`
* **Data Source:** European Space Agency (ESA) Copernicus Data Space Ecosystem (Sentinel-5P OFFL L2 $\text{CH}_4$)

---

## 📊 Key Findings & Analytics Pipeline
1. **Satellite Telemetry Ingestion:** Extracted multi-dimensional grid dimensions (`latitude`, `longitude`, `methane_mixing_ratio`, `qa_value`) from raw NetCDF files using `xarray`.
2. **Spatial SQL & Baseline Calculation:** Queried coordinate matrices via `DuckDB` to establish regional concentration parameters:
   * **Baseline ($\mu$):** $1867.4 \text{ ppb}$
   * **Standard Deviation ($\sigma$):** $30.81 \text{ ppb}$
   * **Statistical Anomaly Threshold ($\mu + 2\sigma$):** $1929.02 \text{ ppb}$
3. **Point-Source Anomaly Mapping:** Isolated high-concentration emission spikes exceeding $2000 \text{ ppb}$ and visualized spatial heatmaps to pinpoint potential point-source leaks.

---

## 🚀 How to Run
1. Clone this repository:
   ```bash
   git clone [https://github.com/meteaksu/sentinel5p-methane-anomaly-detector.git](https://github.com/meteaksu/sentinel5p-methane-anomaly-detector.git)

   pip install xarray netCDF4 duckdb pandas matplotlib
