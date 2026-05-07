#  Financial Econometrics & Time Series Analysis

> **Project 03 of 3** — [← Back to Portfolio Hub](../README.md)

A comprehensive application of **financial econometrics** to asset return time series — covering stationarity testing, autoregressive integrated moving average (ARIMA) modelling, and Generalized Autoregressive Conditional Heteroskedasticity (GARCH) volatility estimation. Model accuracy is benchmarked with RMSE metrics and validated through residual diagnostics.

---

##  Table of Contents

- [Overview](#overview)
- [Methodology](#methodology)
- [Project Structure](#project-structure)
- [Key Results](#key-results)
- [Figures](#figures)
- [Data & Outputs](#data--outputs)
- [Installation & Usage](#installation--usage)
- [Theoretical Background](#theoretical-background)

---

## Overview

Time series econometrics provides the formal toolkit for modelling the **dynamic structure** of financial data — capturing mean reversion, trend, seasonality, and volatility clustering. This project applies a full modelling pipeline:

1. **Stationarity Testing** — Augmented Dickey-Fuller (ADF) test to determine if differencing is required
2. **ARIMA Modelling** — Identify, estimate, and forecast with ARIMA(p,d,q) models selected via AIC/BIC
3. **GARCH Modelling** — Capture time-varying volatility and volatility clustering using GARCH(1,1)
4. **Forecast Evaluation** — RMSE-based comparison across model specifications

This pipeline is applicable to equities, FX, fixed income, and commodity return series.

---

## Methodology

### 1. Stationarity Analysis
- Raw return series plotted and visually inspected for trend and seasonal patterns
- **Augmented Dickey-Fuller (ADF) test** applied:
  - H₀: Unit root present (non-stationary)
  - H₁: Series is stationary
- Results tabulated: test statistic, p-value, critical values at 1%, 5%, 10%
- First differencing applied where non-stationarity detected; ADF re-run on differenced series

### 2. ARIMA Modelling
- ACF and PACF plots guide initial order selection: `(p, d, q)`
- Model estimated using `statsmodels.tsa.arima.model.ARIMA`
- **Information criteria** (AIC, BIC) used for model comparison across candidate orders
- Best-fit model selected; in-sample fit and out-of-sample forecasts generated
- Residual diagnostics: Ljung-Box test for autocorrelation in residuals

### 3. GARCH Volatility Modelling
- ARIMA residuals (or log returns directly) tested for **ARCH effects** (Engle's LM test)
- **GARCH(1,1)** estimated using the `arch` library:
  - Mean equation: constant or ARIMA residuals
  - Variance equation: `σ²_t = ω + α·ε²_{t-1} + β·σ²_{t-1}`
- Conditional volatility series extracted and annualized
- Persistence measured: `α + β` (values near 1 imply high volatility persistence)
- Full model summary saved to `outputs/garch_summary.txt`

### 4. Model Evaluation
- **Root Mean Square Error (RMSE)** computed for each model specification
- Benchmark: naive random walk forecast
- Results tabulated in `tables/rmse_table.csv` and `rmse_table.xlsx`

---

## Project Structure

```
03_financial_econometrics/
├── 03_Financial_Econometrics_TimeSeries.ipynb          ← Main analysis notebook
├── Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf ← Polished PDF report
│
├── figures/
│   ├── returns_series.png           ← Raw return series time plot
│   ├── adf_test_chart.png           ← ADF test visualisation & rolling statistics
│   ├── arima_forecast_clean.png     ← ARIMA fitted values + forecast with CI bands
│   └── garch_volatility.png         ← GARCH(1,1) conditional volatility series
│
├── tables/
│   ├── adf_results.csv              ← ADF test statistics and p-values
│   ├── adf_results.xlsx             ← ADF results (Excel format)
│   ├── arima_forecast.csv           ← Forecasted values with confidence intervals
│   ├── garch_volatility.csv         ← Conditional volatility series (daily)
│   ├── rmse_table.csv               ← RMSE comparison across model specifications
│   └── rmse_table.xlsx              ← RMSE table (Excel format)
│
├── outputs/
│   ├── arima_summary.txt            ← Full ARIMA model estimation output
│   └── garch_summary.txt            ← Full GARCH model estimation output
│
├── requirements.txt
└── README.md
```

---

## Key Results

### Stationarity (ADF Test)

| Series | ADF Statistic | p-value | Result |
|--------|--------------|---------|--------|
| Raw prices | — | > 0.05 | Non-stationary (unit root) |
| Log returns | — | < 0.05 | Stationary ✓ |

> *Full ADF results in `tables/adf_results.csv`.*

### ARIMA Forecast Performance

| Model | AIC | BIC | RMSE |
|-------|-----|-----|------|
| ARIMA(p,d,q) | — | — | — |
| Naive (RW) | — | — | — |

> *Full RMSE comparison in `tables/rmse_table.csv`.*

### GARCH Volatility

| Parameter | Estimate | Interpretation |
|-----------|----------|----------------|
| ω (constant) | — | Long-run variance component |
| α (ARCH term) | — | Sensitivity to past shocks |
| β (GARCH term) | — | Volatility persistence |
| α + β | — | Total persistence (< 1 for stationarity) |

> *Full GARCH output in `outputs/garch_summary.txt`.*

---

## Figures

### Return Series
`figures/returns_series.png`
Time plot of the log return series showing volatility clustering — periods of calm interrupted by high-volatility regimes — motivating GARCH modelling.

### ADF Test Chart
`figures/adf_test_chart.png`
Rolling mean and rolling standard deviation plotted alongside the return series to visualise stationarity properties. ADF critical value thresholds annotated.

### ARIMA Forecast
`figures/arima_forecast_clean.png`
In-sample fitted values and out-of-sample point forecasts plotted against observed returns, with 95% confidence interval bands. Clean, presentation-ready layout.

### GARCH Conditional Volatility
`figures/garch_volatility.png`
Estimated conditional volatility (annualised) from the GARCH(1,1) model, plotted over time. Volatility spikes align with known market stress periods.

---

## Data & Outputs

| File | Format | Description |
|------|--------|-------------|
| `tables/adf_results.csv` | CSV | ADF test statistic, p-value, critical values |
| `tables/adf_results.xlsx` | Excel | Same as above, formatted |
| `tables/arima_forecast.csv` | CSV | Forecast values + 95% CI bounds |
| `tables/garch_volatility.csv` | CSV | Daily conditional volatility estimates |
| `tables/rmse_table.csv` | CSV | RMSE by model specification |
| `tables/rmse_table.xlsx` | Excel | RMSE table, formatted |
| `outputs/arima_summary.txt` | Text | `statsmodels` ARIMA estimation output |
| `outputs/garch_summary.txt` | Text | `arch` GARCH estimation output |

---

## Installation & Usage

```bash
# From the repo root
cd 03_financial_econometrics

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Open notebook
jupyter notebook 03_Financial_Econometrics_TimeSeries.ipynb
```

**Requirements** (`requirements.txt`):
```
numpy
pandas
scipy
statsmodels
arch
matplotlib
seaborn
yfinance
openpyxl
jupyter
```

Run all cells sequentially. Model summaries are printed inline and saved to `outputs/`. All tables are exported in both CSV and Excel formats.

---

## Theoretical Background

**ADF Test Regression:**
$$\Delta y_t = \alpha + \beta t + \gamma y_{t-1} + \sum_{i=1}^{p} \delta_i \Delta y_{t-i} + \varepsilon_t$$
H₀: γ = 0 (unit root) vs H₁: γ < 0 (stationary)

**ARIMA(p,d,q) Model:**
$$\phi(B)(1-B)^d y_t = \theta(B)\varepsilon_t$$
where B is the backshift operator, φ(B) the AR polynomial, θ(B) the MA polynomial.

**GARCH(1,1) Variance Equation:**
$$\sigma_t^2 = \omega + \alpha \varepsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

Conditions for stationarity: `ω > 0`, `α ≥ 0`, `β ≥ 0`, `α + β < 1`

**RMSE:**
$$RMSE = \sqrt{\frac{1}{n}\sum_{t=1}^{n}(\hat{y}_t - y_t)^2}$$

GARCH models capture the empirically observed phenomenon of **volatility clustering** — large price moves tend to be followed by large moves — which standard ARIMA models applied to returns cannot explain.

---

##  Related Projects

- [01 — Efficient Frontier & Portfolio Optimization](../01_efficient_frontier/README.md)
- [02 — Financial Asset Return Analysis](../02_asset_return_analysis/README.md)

---

*Part of the [Quantitative Finance Portfolio](../README.md)*
