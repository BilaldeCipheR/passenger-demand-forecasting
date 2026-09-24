# Aviation Passenger Demand Forecasting

## Project Overview

This project develops a machine learning workflow for forecasting monthly passenger demand at San Francisco International Airport (SFO).

The project uses historical passenger traffic data to create a monthly forecasting dataset and compares several machine learning approaches against a simple previous-month baseline.

## Dataset

**Dataset:** SFO Air Traffic Passenger Statistics  
**Source:** San Francisco International Airport (SFO), City and County of San Francisco  

The passenger dataset contains monthly passenger traffic statistics for SFO, including totals by airline, region, terminal, and boarding area. The official SFO dataset is provided in CSV format with an associated data dictionary.

**Official source:** [San Francisco International Airport — Air Traffic Statistics](https://www.flysfo.com/vi/node/10066) — SFO's official statistics page confirms the dataset contains monthly totals by airline, region, terminal, and boarding area, provided as CSV files with data dictionaries.

**Downloadable dataset:** [San Francisco Open Data — Air Traffic Passenger Statistics](https://data.sfgov.org/Transportation/Air-Traffic-Passenger-Statistics/rkru-6vcg) — the CSV used in this project.

The raw CSV (`data/SF_Air_Traffic_Passenger_Statistics.csv`) is not tracked in Git because it is large and publicly available at the links above. Download it from either source and place it under `data/` to reproduce the notebooks. The aggregated monthly file is produced by the cleaning/aggregation notebooks.

## Project Objectives

* Explore historical SFO passenger traffic
* Prepare a clean monthly forecasting dataset
* Establish a naive forecasting baseline
* Train and compare multiple machine learning models
* Evaluate models using MAE and RMSE
* Analyze forecasting errors
* Identify areas for future improvement

## Models

The project compares:

1. **Previous Month Baseline** — The previous month's passenger count is used as the prediction for the current month.
2. **Linear Regression** — Uses previous-month passenger demand as the input feature.
3. **Feature-Engineered Linear Regression** — Linear Regression trained using lag, rolling-average, and calendar features.
4. **Random Forest** — Random Forest Regressor trained using the same engineered features.

## Evaluation Metrics

### Mean Absolute Error (MAE)

MAE measures the average absolute difference between actual and predicted passenger counts. Lower MAE indicates smaller average forecasting errors.

### Root Mean Squared Error (RMSE)

RMSE gives greater weight to larger prediction errors. Lower RMSE indicates fewer or smaller large forecasting errors.

## Results

| Model                                |        MAE |       RMSE |
| ------------------------------------ | ---------: | ---------: |
| Previous Month Baseline              | 326,970.92 | 384,439.04 |
| Linear Regression                    | 322,999.10 | 377,807.99 |
| Feature-Engineered Linear Regression | 320,793.76 | 388,692.52 |
| Random Forest                        | 334,348.84 | 447,614.83 |

**Relative to baseline:**

| Model                                | MAE Change | RMSE Change |
| ------------------------------------ | ---------: | ----------: |
| Baseline                             |      0.00% |       0.00% |
| Linear Regression                    |     -1.21% |      -1.72% |
| Feature-Engineered Linear Regression |     -1.89% |      +1.11% |
| Random Forest                        |     +2.26% |     +16.43% |

Feature-Engineered Linear Regression produced the lowest MAE, while basic Linear Regression produced the lowest RMSE.

The improvements over the previous-month baseline were relatively small, showing that the tested models did not dramatically outperform the simple baseline.

## Error Analysis

The error analysis showed that model performance varied across time.

Some of the largest errors occurred during periods of rapid passenger-demand changes, including portions of the post-COVID recovery period.

March had the highest average absolute error in the Linear Regression analysis. Five of the ten largest individual Linear Regression errors also occurred in March.

These results suggest that the current feature set does not capture all of the information needed to accurately predict passenger demand during these periods.

## Key Findings

* A simple previous-month baseline provided a strong benchmark.
* Linear Regression slightly improved upon the baseline.
* Feature engineering reduced MAE but increased RMSE.
* Random Forest performed worse than the baseline on both evaluation metrics.
* Greater model complexity did not automatically improve forecasting performance.
* Large errors were concentrated around periods of substantial changes in passenger demand.

## Future Improvements

Possible future improvements include:

* Adding additional seasonal features
* Incorporating holidays and calendar effects
* Testing additional lag and rolling-window features
* Evaluating time-series-specific forecasting methods
* Adding external explanatory variables
* Performing systematic hyperparameter tuning
* Using walk-forward or expanding-window validation

## Project Structure

```text
aviation-passenger-forecasting/
│
├── data/
│   ├── SF_Air_Traffic_Passenger_Statistics.csv  (not tracked)
│   └── processed/
│       └── monthly_passenger_demand.csv
│
├── 01_data_exploration.ipynb
├── 02_data_cleaning.ipynb
├── 03_baseline_model.ipynb
├── 04_linear_regression.ipynb
├── 05_feature_engineering.ipynb
├── 06_random_forest.ipynb
├── 07_model_evaluation.ipynb
│
├── .gitignore
├── README.md
└── requirements.txt
```

## Skills Demonstrated

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* Data cleaning
* Exploratory data analysis
* Feature engineering
* Regression modeling
* Model evaluation
* Error analysis
* Time-series forecasting concepts
* Git/GitHub project organization