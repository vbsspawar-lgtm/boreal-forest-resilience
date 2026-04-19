# Boreal Forest Resilience Analysis

This repository contains the code and selected outputs for my master's thesis on resilience analysis of boreal forests using satellite time-series datasets.

## Project overview

The aim of this project is to evaluate which satellite dataset and which resilience metric best reflect actual vegetation recovery after disturbance in boreal forests.

The workflow compares:

- **empirical recovery rates** estimated from detected disturbance events
- **theoretical resilience indicators** derived from time-series statistics

This allows the project to test which indicators are most meaningful, rather than assuming they are valid in advance.

## Research question

Which satellite dataset and which resilience metric best represent actual vegetation recovery behaviour in boreal forests?

## Datasets used

The analysis uses three datasets representing different aspects of vegetation dynamics:

- **MODIS NDVI (MOD13C2)**  
  Optical vegetation index representing greenness.

- **VODCA CXKu**  
  Microwave-based vegetation optical depth, sensitive to vegetation water content and structure.

- **GPP (derived from MOD17A2HGF)**  
  Gross primary productivity, representing ecosystem carbon uptake.

## Main workflow

The code implements the following steps:

1. load and harmonize all datasets
2. align them to a common spatial grid
3. apply boreal-region masking and stratified pixel sampling
4. preprocess time series using STL decomposition
5. detect disturbance transitions using a Taylor-style method
6. estimate empirical recovery rates (`lambda_emp`)
7. compute theoretical resilience metrics:
   - variance
   - lag-1 autocorrelation (`AC1`)
   - AR(1)-based recovery-rate proxy (`lambda_ar1`)
   - GLSAR-based stability metric (`a_glsar`)
8. benchmark theoretical metrics against empirical recovery
9. rank dataset–metric combinations
10. analyse rolling resilience patterns over time

## Repository contents

- `boreal_resilience_colab_full_run_stl_taylor_glsar.ipynb`  
  Main Google Colab notebook for the full analysis.

- `outputs/`  
  Selected output figures and result files from the final pipeline.

## Main outputs

The repository includes selected outputs such as:

- dataset–metric ranking
- benchmark results
- event counts by dataset
- event level benchmark table
- figure dataset metric ranking
- figure rolling variance
- figure rolling AC1
- figure rolling AR-based recovery rate
- figure rolling GLSAR metric
- gpp sampled pixels
- modis sampled pixels
- pixel summary
- rolling metrics all
- vodca sampled pixels

## Data availability

The full raw datasets are **not included in this repository** because of their size.

The analysis was run using externally obtained satellite datasets and preprocessed intermediate files stored locally / in Google Drive.

To reproduce the workflow, dataset paths in the notebook configuration section must be adapted to the local setup.

## Notes on data structure

Some datasets, especially MODIS NDVI and VODCA, contain strong seasonal missingness in winter months.

The preprocessed GPP file is stored on a rectangular grid around a manually selected AppEEARS region. As a result, some cells outside the actual selected footprint appear as structurally missing, although they were not intended to represent true missing observations within the analysis region.

## Thesis context

This repository accompanies my master's thesis on boreal forest resilience analysis.

## Author

Vaibhav Bhupendra Pawar

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.