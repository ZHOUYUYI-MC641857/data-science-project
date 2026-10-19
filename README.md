# data-science-project

# Imbalance in the Tide: Spatiotemporal Characteristics and Weather Effects of Shared Bicycle Morning-Peak Supply-Demand Tides in Xiamen

**Project status:** Ongoing  
**Course:** CISC7204 Data Science and Data Visualization  
**Author:** ZHOU YUYI

## Problem / Research Question

Shared bicycle systems often experience severe morning-peak supply-demand imbalance: some parking zones accumulate too many bicycles, while others face shortages. This project analyzes shared bicycle morning-peak “tidal imbalance” in Xiamen, China.

**Research questions:**

1. During morning peak hours (6:00–10:00 AM) in Xiamen, in which specific regions and time periods is shared bicycle tidal imbalance most severe?
2. What is the marginal effect of weather conditions (temperature, precipitation, wind speed, humidity) on the degree of tidal imbalance?

The project aims to build a reproducible analysis pipeline and an interactive visualization dashboard that helps operations personnel identify where and when redistribution is most needed.

## Dataset Source and Usage Permissions

**Data source:**

- Zenodo record: https://zenodo.org/records/17415891  
  DOI: 10.5281/zenodo.17415891
- Companion paper: https://www.nature.com/articles/s41597-025-06534-z

The dataset covers five consecutive weekdays from 21 to 25 December 2020 during morning peak hours (6:00–10:00 AM) in Xiamen. It includes:

- 220,675 validated trip records
- 2,849,243 GPS trajectory points
- 14,071 authorized parking zones
- OSM-derived road network and hourly weather observations

**Usage permissions:**

- The dataset is publicly available for research use. Before using or redistributing any data, check the license terms on the Zenodo record and the companion paper.
- This repository does **not** redistribute raw trip records, raw GPS trajectories, or restricted datasets. It stores code, documentation, aggregated outputs, and visualizations only.
- Users are responsible for complying with the original dataset license and privacy requirements.
- No passwords, API keys, personal data, or restricted datasets are included in this repository.

## Methods and Tools

**Methods:**

1. Data loading and data-quality assessment: missing-value matrices, outlier checks, and data dictionary.
2. Tidal imbalance quantification: for each parking zone, compute net inflow = inflow trips − outflow trips at 30-minute intervals, standardized by parking zone capacity.
3. Spatiotemporal clustering: group parking zones with similar tidal characteristics using multi-scale spatiotemporal clustering.
4. Hotspot identification: identify the most severely vehicle-deficient and vehicle-accumulated areas during morning peak.
5. Weather-effect modeling: multiple regression with parking-zone and date fixed effects; XGBoost/Random Forest for prediction and feature importance.
6. Redistribution simulation: compare a simple pre-positioning scenario with a no-redistribution baseline.
7. Interactive visualization: Folium/Plotly dashboard supporting filtering by date, time period, parking-zone cluster, and weather condition.

**Tools:**

- Python
- Pandas, NumPy, GeoPandas
- Statsmodels, scikit-learn, XGBoost
- Folium, Plotly, Matplotlib
- Jupyter Notebook

## Key Findings and One Limitation

**Preliminary key findings (ongoing; to be updated after modeling):**

- The repository currently documents a reproducible pipeline for processing 220,675 trip records, 2,849,243 GPS trajectory points, and 14,071 parking zones.
- Initial visualizations are designed to show spatiotemporal imbalance patterns by parking-zone cluster and 30-minute interval, including the contrast between “first-in-then-out” and “first-out-then-in” tidal patterns.
- Weather marginal effects and model performance results are being estimated and will be updated after the regression and machine-learning tasks are completed.

> Note: Empirical findings in this section are preliminary and should not be cited as final results until the analysis is completed.

**One limitation:**

The dataset covers only five consecutive weekdays (21–25 December 2020) during 6:00–10:00 AM in Xiamen. Therefore, findings may not generalize to weekends, other seasons, other times of day, or other cities.

## Visualizations

At least two visualizations are included in the `figures/` folder:

1. **Figure 1: Spatiotemporal heatmap of morning-peak tidal imbalance.**  
   Faceted heatmap with 30-minute time periods on the x-axis and parking-zone clusters on the y-axis, colored by net inflow/outflow ratio. Red indicates accumulation; blue indicates deficit.

   ![Figure 1: Spatiotemporal heatmap of tidal imbalance](figures/fig1_tidal_imbalance_heatmap.png)

2. **Figure 2: Marginal effects of weather variables on tidal imbalance.**  
   Coefficient plot showing standardized regression coefficients and 95% confidence intervals for precipitation, temperature, wind speed, and humidity.

   ![Figure 2: Weather marginal effects](figures/fig2_weather_marginal_effects.png)

Additional planned visualization: an interactive Folium dashboard for date switching, time-period filtering, and parking-zone-level tidal curves.

## Repository Structure

```text
data-science-project/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/                 # Not committed; download from Zenodo
│   └── processed/           # Aggregated/derived data only
├── notebooks/
│   ├── 01_data_loading_quality.ipynb
│   ├── 02_tidal_imbalance_clustering.ipynb
│   ├── 03_weather_effect_modeling.ipynb
│   ├── 04_redistribution_simulation.ipynb
│   └── 05_visualization_dashboard.ipynb
├── src/
│   ├── data_cleaning.py
│   ├── tidal_index.py
│   ├── clustering.py
│   └── modeling.py
├── figures/
│   ├── fig1_tidal_imbalance_heatmap.png
│   └── fig2_weather_marginal_effects.png
└── outputs/
    ├── tables/
    └── dashboard/
