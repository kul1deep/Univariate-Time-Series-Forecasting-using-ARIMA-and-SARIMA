# Univariate-Time-Series-Forecasting-using-ARIMA-and-SARIMA


## Project Overview

This repository demonstrates how to build and evaluate classical time-series forecasting models — **ARIMA** and **SARIMA** — for a single numeric series. The goal is to take historical observations of a single variable (for example: daily sales, monthly passenger counts, electricity consumption, etc.) and forecast future values while covering the whole modeling workflow: EDA, preprocessing, stationarity checks, parameter selection, diagnostics, forecasting and evaluation.

## Dataset

* Explain here what dataset you used (replace with your dataset name). Example fields to include:

  * Source: (e.g., Kaggle / UCI / company data / generated)
  * Frequency: daily / weekly / monthly / hourly
  * Time span: e.g., `2015-01-01` to `2020-12-31`
  * Target column: e.g., `value`, `sales`


## Exploratory Data Analysis (EDA)

Key steps performed in the notebook:

* Plot raw time series (line plot) to inspect trends, seasonality, outliers.
* Seasonal decomposition (additive or multiplicative) to separate trend, seasonal, residual components.
* Histogram / density plot of values to inspect distribution.
* Rolling statistics (rolling mean and rolling std) to visualize non-stationarity.


## Modeling Approaches

### ARIMA

* Model general form: ARIMA(p, d, q) where

  * `p` = autoregressive order
  * `d` = order of differencing
  * `q` = moving average order
* Best used when series is roughly stationary after non-seasonal differencing.

### SARIMA

* SARIMA(p, d, q)(P, D, Q, s) extends ARIMA to include seasonal orders:

  * `(P, D, Q)` = seasonal AR, seasonal differencing, seasonal MA
  * `s` = seasonal period (for monthly data s=12, for daily weekly seasonality s=7)
* Use when the time series displays seasonal patterns.

## Model Selection & Hyperparameter Tuning

* Use ACF and PACF plots to get candidate `p` and `q` values.
* Use Augmented Dickey-Fuller (ADF) / KPSS tests for stationarity and to decide `d`.
* For seasonal data, inspect seasonal differences and seasonal ACF/PACF to decide `(P, Q, D, s)`.
* Grid search / auto_arima (pmdarima) can be used to automate selection using information criteria like AIC/BIC.
* Prefer simpler models with lower AIC/BIC and good residual diagnostics.

## Model Diagnostics & Validation

* Check residuals: should be uncorrelated (Ljung-Box test), mean ~0, and homoscedastic.
* Plot residuals histogram and Q-Q plot for approximate normality.
* Plot ACF of residuals to ensure no remaining autocorrelation.
* Walk-forward validation (time-series cross-validation) or hold-out last `k` periods for test evaluation.

## Evaluation Metrics

Typical metrics for regression/forecasting used in the notebook:

* **MAE** — Mean Absolute Error
* **MSE** — Mean Squared Error
* **RMSE** — Root Mean Squared Error
* **MAPE** — Mean Absolute Percentage Error (careful with zeros)

Include the error metrics on the test split and (optionally) for different forecast horizons.

## Results

* Summarize final selected model(s): e.g., `SARIMA(1,1,1)(0,1,1,12)`
* Report test metrics (MAE, RMSE, MAPE) and show example plots:

  * Forecast vs Actual (with confidence intervals)
  * Decomposed components
  * Residual diagnostics

> **Action for README:** Replace the example model and metrics above with your notebook’s final model and numbers.

## Repository Structure

```
├── data/
│   └── your_data.csv
├── notebooks/
│   └── Time Series.ipynb
├── src/
│   └── modeling.py
├── results/
│   └── figures/ (forecast plots, residuals, decomposition)
├── requirements.txt
├── README.md
└── LICENSE
```

## Dependencies

* Python 3.8+
* pandas
* numpy
* matplotlib
* statsmodels
* pmdarima (optional — for `auto_arima`)
* scipy
* jupyter
