# Boreal Forest Resilience Analysis

This repository contains the code and selected outputs for my master's thesis:

**Resilience Change in Boreal Forests: A Comparison of Satellite Data and Resilience Metrics for Monitoring Stability**

## Project overview

Boreal forests are an important part of the global climate system, but their resilience to environmental disturbances is still not fully understood. Satellite-derived vegetation time series are often used to estimate resilience, but it is not always clear which dataset or metric best represents real recovery behaviour.

This project compares satellite datasets and theoretical resilience indicators by benchmarking them against empirical recovery rates estimated from detected disturbance events.

The main research question is:

**Which combinations of satellite dataset and resilience metric best reflect actual vegetation recovery behaviour in boreal forests?**

## Datasets

The analysis uses three satellite-derived vegetation datasets:

- **MODIS NDVI (MOD13C2)**  
  Optical vegetation index representing vegetation greenness.

- **VODCA CXKu**  
  Microwave-based vegetation optical depth product, sensitive to vegetation water content and vegetation structure.

- **GPP derived from MOD17A2HGF**  
  Gross primary productivity, representing ecosystem carbon uptake.

These datasets were selected because they represent different aspects of vegetation dynamics: greenness, canopy water/structure, and ecosystem function.

## Methodological approach

The workflow follows a transition-based resilience analysis.

The main steps are:

1. Load and harmonise the three satellite datasets.
2. Align datasets to a common spatial grid.
3. Apply boreal-region masking and quality filtering.
4. Use valid-pixel analysis instead of relying on full rectangular dataset extents.
5. Preprocess each time series using the rolling-mean detrending and harmonic deseasoning method following Smith and Boers.
6. Detect disturbance transitions in the residual time series.
7. Estimate empirical recovery rates (`lambda_emp`) by fitting exponential recovery trajectories after detected disturbances.
8. Compute theoretical resilience indicators before disturbances.
9. Benchmark theoretical indicators against empirical recovery rates.
10. Rank all dataset–metric combinations.
11. Analyse temporal changes in resilience metrics using rolling windows.

## Preprocessing

The final workflow uses the method of Smith and Boers, based on:

- rolling-mean detrending
- harmonic seasonal fitting
- residual extraction

This approach preserves missing values and is suitable for boreal satellite records where winter snow cover and observation gaps can strongly affect the time series.

All disturbance detection, recovery estimation, theoretical metric calculation, and rolling-window analysis are performed on the resulting residual time series.

## Resilience metrics

The following theoretical resilience metrics are calculated:

- **Variance**
- **Lag-1 autocorrelation (AC1)**
- **AR(1)-based recovery-rate proxy (`lambda_ar1`)**
- **Variance-based recovery-rate proxy (`lambda_var`)**
- **GLSAR-based stability metric (`a_glsar`)**

These metrics are compared against the empirical recovery rate `lambda_emp`.

## Benchmarking

Each dataset–metric combination is evaluated using:

- Spearman correlation
- Pearson correlation
- mean absolute error
- coverage
- statistical significance

The purpose of the benchmarking is not to assume that any resilience metric is valid in advance, but to test which metrics best match observed recovery behaviour.

## Main result

The final analysis shows that the best-performing dataset–metric combinations are based on **VODCA**, especially VODCA combined with lag-1 autocorrelation and related recovery-rate indicators.

This suggests that microwave-based vegetation optical depth provides more consistent support for critical-slowing-down-based resilience analysis in the boreal zone than the tested MODIS NDVI and GPP combinations.

## Repository contents

```text
notebooks/
    Main analysis notebook

outputs/
    Selected final figures and result tables

README.md
    Project description

requirements.txt
    Python package requirements

LICENSE
    Repository license

## Data availability

The full raw datasets are not included in this repository because of their size.

The analysis was performed using externally obtained satellite datasets and preprocessed intermediate files stored locally or in Google Drive. To reproduce the workflow, dataset paths must be adapted in the configuration section of the notebook.

## Notes on missing data and valid footprints

Some datasets contain substantial missing values, especially during winter months. In addition, some products are stored on rectangular grids even when the selected study region is irregular. Therefore, cells outside the valid data footprint may appear as structurally missing.

The analysis accounts for this using valid-pixel filtering and dataset-specific quality checks before disturbance detection and benchmarking.

## Software

The analysis was implemented in Python using scientific computing libraries including NumPy, pandas, xarray, SciPy, statsmodels, matplotlib, rasterio, rioxarray, and netCDF4.

## Author

Vaibhav Bhupendra Pawar

## Thesis context

This repository accompanies a master's thesis submitted at the Technical University of Munich.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.