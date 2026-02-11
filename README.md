<div align="center">

# Merowe Dam Water Quality Monitoring

### Multi-Parameter Satellite-Based Analysis Using Sentinel-2 & Google Earth Engine

[![Sentinel-2](https://img.shields.io/badge/Satellite-Sentinel--2%20SR-blue?logo=satellite&logoColor=white)](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED)
[![Google Earth Engine](https://img.shields.io/badge/Platform-Google%20Earth%20Engine-green?logo=google-earth&logoColor=white)](https://earthengine.google.com/)
[![Python](https://img.shields.io/badge/Python-3.8+-yellow?logo=python&logoColor=white)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter&logoColor=white)](Merowe_Dam_Water_Quality_v3.ipynb)
[![LinkedIn](https://img.shields.io/badge/Repost_on-LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/posts/osman-o-a-ibrahim-a02a9a197_remotesensing-waterquality-googleearthengine-activity-7427338005549350912-h3jJ)

---

**A comprehensive remote sensing pipeline for monitoring water quality dynamics across Merowe Dam reservoir (925.7 km²), Sudan, using Sentinel-2 multispectral imagery (2023-2024) processed through Google Earth Engine and XArray.**

[Features](#features) | [Parameters](#water-quality-parameters) | [Results](#results) | [Getting Started](#getting-started) | [Methodology](#methodology) | [Citation](#citation)

</div>

---

## Study Area

**Merowe Dam** is a large hydroelectric dam on the Nile River in northern Sudan. The reservoir extends over **925.7 km²** and is a critical water resource for the region. This project monitors its water quality using freely available satellite data.

| Property | Value |
|---|---|
| **Location** | Northern Sudan (18.4°N - 19.3°N, 31.7°E - 32.8°E) |
| **Reservoir Area** | 925.7 km² |
| **Satellite** | Sentinel-2 SR Harmonized (10-20m resolution) |
| **Time Period** | January 2023 - December 2024 |
| **Images Processed** | 510 cloud-filtered scenes |

## Features

- **Automated cloud masking** using cloud probability + SCL band dual-filtering
- **JRC Global Surface Water** boundary for precise water body delineation
- **7 water quality parameters** derived from published empirical algorithms
- **Monthly spatiotemporal maps** at 10m resolution
- **Time series analysis** with Mann-Kendall trend testing
- **Trophic State Index** classification (Carlson TSI)
- **Algal bloom detection** and frequency mapping
- **Composite Water Quality Index** (weighted multi-parameter)
- **Upstream vs downstream** spatial gradient analysis
- **Seasonal variability** and inter-parameter correlation analysis

## Water Quality Parameters

| Parameter | Algorithm | Reference |
|---|---|---|
| **Chlorophyll-a** | Red-Edge ratio (B5/B4) | Empirical band ratio |
| **Chlorophyll-a (NDCI)** | Quadratic NDCI model | Mishra & Mishra (2012) |
| **NDCI** | (B5-B4)/(B5+B4) | Normalized Difference Chlorophyll Index |
| **Turbidity (FNU)** | Red band reflectance model | Dogliotti et al. (2015) |
| **TSS** | Linear red band model | Empirical |
| **CDOM** | Blue/Green ratio exponential | Brezonik et al. (2015) |
| **Secchi Depth** | Blue/Green log-ratio | Empirical |
| **FAI** | NIR baseline difference | Hu (2009) |

## Results

### Monthly Chlorophyll-a Maps
<img src="Images/1.png" width="100%">

### Monthly Turbidity Maps
<img src="Images/2.png" width="100%">

### Monthly Total Suspended Solids
<img src="Images/3.png" width="100%">

### Monthly CDOM
<img src="Images/4.png" width="100%">

### Monthly Secchi Depth
<img src="Images/5.png" width="100%">

### Multi-Parameter Time Series
<img src="Images/6.png" width="100%">

### Inter-Parameter Correlation
<img src="Images/7.png" width="60%">

### Seasonal Box Plots
<img src="Images/8.png" width="100%">

### Chlorophyll-a Anomaly from Long-Term Mean
<img src="Images/9.png" width="100%">

### Trophic State Index (Carlson TSI)
<img src="Images/10.png" width="100%">

### Algal Bloom Frequency Map
<img src="Images/11.png" width="60%">

### Monthly Water Quality Index
<img src="Images/12.png" width="100%">

### Monthly Chlorophyll-a Heatmap
<img src="Images/13.png" width="100%">

## Key Findings

- **Trophic State**: The reservoir is classified as **eutrophic** (99.4% of observations), with occasional hypereutrophic episodes (0.6%)
- **Chlorophyll-a Trend**: Statistically significant **increasing trend** (Mann-Kendall p=0.04, Sen's slope = +0.0034/timestep)
- **Seasonal Pattern**: Highest Chl-a in summer (JJA), peaking in July (~111 ug/L); lowest in winter (DJF, ~98 ug/L)
- **Bloom Hotspots**: Algal bloom frequency is highest near the dam wall (southwest) and upstream inflow areas
- **Strong Correlations**: Chl-a and TSS (R=0.74), Chl-a and NDCI (R=0.85), CDOM and Secchi Depth (R=1.00)

## Getting Started

### Prerequisites

- Python 3.8+
- A [Google Earth Engine](https://earthengine.google.com/) account
- A GEE cloud project (for high-volume API access)

### Installation

```bash
# Clone the repository
git clone https://github.com/Osman-Geomatics93/Merowe-Dam-Water-Quality.git
cd Merowe-Dam-Water-Quality

# Install dependencies
pip install -r requirements.txt
```

### Authentication

```python
import ee
ee.Authenticate()
ee.Initialize(project="your-project-id", opt_url="https://earthengine-highvolume.googleapis.com")
```

### Unlock the Notebook

This notebook uses a **Social Unlock** system. To run it:

1. Open the [LinkedIn post](https://www.linkedin.com/posts/osman-o-a-ibrahim-a02a9a197_remotesensing-waterquality-googleearthengine-activity-7427338005549350912-h3jJ)
2. **Repost** it to support the project and help it reach more people
3. Copy the post URL from your browser
4. Run the first code cell in the notebook and paste the URL when prompted

The notebook will verify the URL and unlock automatically.

### Run

Open `Merowe_Dam_Water_Quality_v3.ipynb` in Jupyter Notebook or Google Colab and run all cells sequentially.

## Methodology

```
Sentinel-2 SR Harmonized (L2A)
        |
        v
Cloud Masking (Cloud Prob + SCL)
        |
        v
JRC Water Boundary Clipping
        |
        v
Water Quality Algorithms (7 params)
        |
        v
XArray Dataset (510 timesteps)
        |
        +---> Monthly Spatial Maps
        +---> Time Series Analysis
        +---> Mann-Kendall Trend Test
        +---> Trophic State Index (TSI)
        +---> Algal Bloom Detection
        +---> Water Quality Index (WQI)
        +---> Upstream vs Downstream Gradient
        +---> Seasonal & Correlation Analysis
```

## Tech Stack

| Tool | Purpose |
|---|---|
| **Google Earth Engine** | Cloud-based satellite image processing |
| **XArray + xee** | N-dimensional labeled array operations |
| **Matplotlib + Seaborn** | Scientific visualization |
| **Pandas** | Tabular data analysis |
| **Folium** | Interactive map preview |
| **pyMannKendall** | Non-parametric trend testing |

## Project Structure

```
Merowe-Dam-Water-Quality/
|-- Merowe_Dam_Water_Quality_v3.ipynb   # Main analysis notebook
|-- Images/                              # Output visualizations
|   |-- 1.png  ... 13.png
|-- requirements.txt                     # Python dependencies
|-- LICENSE                              # MIT License
|-- README.md                            # This file
```

## Citation

If you use this work in your research, please cite:

```bibtex
@software{merowe_water_quality_2025,
  author    = {Osman},
  title     = {Multi-Parameter Water Quality Monitoring of Merowe Dam Using Sentinel-2 and Google Earth Engine},
  year      = {2025},
  url       = {https://github.com/Osman-Geomatics93/Merowe-Dam-Water-Quality}
}
```

### Algorithm References

- Mishra, S. & Mishra, D.R. (2012). Normalized difference chlorophyll index. *Remote Sensing of Environment*.
- Dogliotti, A.I. et al. (2015). A single band algorithm for turbidity retrieval. *Remote Sensing of Environment*.
- Brezonik, P. et al. (2015). Factors affecting CDOM in lakes. *Limnology and Oceanography*.
- Hu, C. (2009). A novel ocean color index to detect floating algae. *Remote Sensing of Environment*.
- Carlson, R.E. (1977). A trophic state index for lakes. *Limnology and Oceanography*.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with Google Earth Engine and Python**

</div>
