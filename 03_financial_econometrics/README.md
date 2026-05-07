<div align="center">

<br>

# Financial Econometrics & Time Series Analysis

### Project 03 of 3 — Quantitative Finance Portfolio

<br>

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)
[![statsmodels](https://img.shields.io/badge/statsmodels-%E2%89%A50.14-4B8BBE?style=flat-square)]()
[![arch](https://img.shields.io/badge/arch-%E2%89%A56.0-E07B39?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)]()

<br>

[← Back to Portfolio Hub](../README.md)

<br>

</div>

---

## Overview

A comprehensive implementation of the **financial econometrics modelling pipeline** applied to asset return time series — following the same systematic workflow used in academic empirical finance research and quantitative finance practice. The project progresses through five formal stages: exploratory time series analysis, unit root testing, conditional mean modelling, conditional variance modelling, and out-of-sample forecast evaluation.

The modelling sequence is deliberately structured and economically motivated. **Augmented Dickey-Fuller (ADF) unit root testing** first establishes whether the series is stationary — the prerequisite for any time series model. **ARIMA(p,d,q)** identification, estimation, and diagnostics then capture any linear autocorrelation structure in the conditional mean. The ARIMA residuals are tested for **ARCH effects** using Engle's LM test; when confirmed, a **GARCH(1,1)** model is fitted to the conditional variance — capturing the volatility clustering that is the defining empirical feature of daily financial return data and that the ARIMA mean model structurally cannot address. Finally, forecast accuracy is evaluated via **RMSE**, with the ARIMA model benchmarked against a naive random walk baseline on a held-out test set.

All model outputs, parameter estimates, diagnostic statistics, and forecasts are exported in both CSV and Excel formats for maximum portability and downstream usability.

**What this project demonstrates:**

- The complete Box-Jenkins ARIMA identification, estimation, and diagnostic workflow applied to a financial series
- Why financial returns require specialized conditional variance models beyond standard linear regression
- GARCH(1,1) estimation, parameter interpretation, volatility persistence measurement, and conditional volatility forecasting
- Formal out-of-sample forecast evaluation using RMSE with a principled naive benchmark
- The econometric rationale for every modelling decision at each stage of the pipeline

---

## 📄 PDF Portfolio Showcase

<div align="center">

### [`Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf`](./Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf)

*A complete, professional-quality presentation of this project — no code or Python environment required*

</div>

<br>

The PDF showcase is the recommended starting point for reviewers, recruiters, and professional contacts. It is a fully self-contained, print-ready document presenting every stage of the econometric pipeline — all test results, estimation outputs, forecasting charts, diagnostic plots, and written interpretation — without requiring Python, Jupyter, or any technical setup.

**Complete contents of the PDF:**

| # | Section | What Is Included |
|---|---------|-----------------|
| 1 | **Executive Summary** | Econometric pipeline overview, asset and sample description, and key modelling results |
| 2 | **Exploratory Time Series Analysis** | Return series time plot — volatility clustering, heteroskedasticity, and structural features highlighted; rolling mean and rolling standard deviation analysis |
| 3 | **ADF Stationarity Test Results** | Full results table — ADF test statistic, p-value, and critical values at 1%, 5%, and 10% levels for both the raw price series and the log return series; interpretation of unit root vs stationarity |
| 4 | **ARIMA Model Selection Table** | AIC and BIC values for all candidate (p,d,q) specifications tested, with the selected model clearly highlighted; rationale for selection |
| 5 | **ARIMA Estimation Output** | Full model summary — coefficient estimates, standard errors, t-statistics, p-values, log-likelihood, AIC, BIC; interpretation of each estimated parameter |
| 6 | **ARIMA Forecast Chart** | Clean, presentation-quality chart — in-sample fitted values overlaid on actual returns, out-of-sample point forecast with shaded 95% confidence interval bands, vertical train/test split line |
| 7 | **ARCH-LM Test** | Engle's Lagrange multiplier test result — test statistic and p-value confirming the presence of ARCH effects in ARIMA residuals; interpretation of what this means for model adequacy |
| 8 | **GARCH(1,1) Estimation Output** | Full model summary — ω, α, and β estimates with standard errors and t-statistics; α+β persistence; implied unconditional variance; log-likelihood, AIC, BIC; innovation distribution used |
| 9 | **Conditional Volatility Chart** | GARCH(1,1) estimated annualized conditional volatility plotted across the full sample; long-run unconditional variance level annotated as a horizontal dashed baseline; high-volatility regime periods highlighted |
| 10 | **RMSE Benchmarking Table** | Out-of-sample RMSE for ARIMA model vs naive random walk baseline; percentage improvement or deterioration; interpretation of forecast accuracy in context |
| 11 | **Residual Diagnostics** | ACF plot of standardized GARCH residuals (checking for remaining autocorrelation); standardized residual histogram vs normal distribution overlay; Ljung-Box test results |
| 12 | **Parameter Interpretation** | Plain-English economic interpretation of every estimated ARIMA and GARCH coefficient — what each number means and what it implies for the asset's return and volatility dynamics |

<br>

> **Tip for reviewers:** The PDF is entirely self-contained. Open it directly to evaluate this project without running any code.

---

## Table of Contents

- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Figures](#figures)
- [Data & Outputs](#data--outputs)
- [Key Results](#key-results)
- [Theoretical Background](#theoretical-background)
- [Installation & Usage](#installation--usage)
- [Related Projects](#related-projects)

---

## Project Structure

```
03_financial_econometrics/
│
├── 03_Financial_Econometrics_TimeSeries.ipynb              ← Full reproducible analysis notebook
├── Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf ← ★ PDF Portfolio Showcase
│
├── figures/
│   ├── returns_series.png          ← Full return series time plot (volatility clustering visible)
│   ├── adf_test_chart.png          ← Rolling mean and rolling std overlay for stationarity assessment
│   ├── arima_forecast_clean.png    ← In-sample fit + out-of-sample forecast + 95% CI bands
│   └── garch_volatility.png        ← GARCH(1,1) conditional volatility + unconditional baseline
│
├── tables/
│   ├── adf_results.csv             ← ADF test statistic, p-value, critical values
│   ├── adf_results.xlsx            ← Same, formatted for Excel
│   ├── arima_forecast.csv          ← Date, point forecast, 95% CI lower bound, 95% CI upper bound
│   ├── garch_volatility.csv        ← Date, daily conditional σ, annualized conditional σ
│   ├── rmse_table.csv              ← Model, RMSE, comparison vs naive baseline
│   └── rmse_table.xlsx             ← Same, formatted for Excel
│
├── outputs/
│   ├── arima_summary.txt           ← Full statsmodels ARIMA .summary() output
│   └── garch_summary.txt           ← Full arch GARCH .summary() output
│
├── requirements.txt
└── README.md
```

---

## Methodology

### Step 1 — Exploratory Time Series Analysis

The log return series is plotted across the full sample period (`figures/returns_series.png`) for initial visual inspection. The chart is examined for:

- **Trend or drift in the mean** — a trending mean implies non-stationarity that must be addressed before modelling
- **Non-constant variance (heteroskedasticity)** — regions of wider and narrower return magnitudes are visually distinguishable
- **Volatility clustering** — the defining feature of daily equity return series: extended quiet periods punctuated by bursts of large returns in both directions, persisting for days to weeks before subsiding
- **Structural breaks** — abrupt changes in the distributional regime that may require sample restriction or dummy variable treatment

Rolling mean and rolling standard deviation (60-day window) are computed and overlaid on the return series in `figures/adf_test_chart.png`. A roughly flat rolling mean and non-trending rolling standard deviation provide visual evidence of (weak) stationarity — formally tested in Step 2.

---

### Step 2 — Unit Root Testing: Augmented Dickey-Fuller

Time series models require **stationary** inputs — series whose mean, variance, and autocovariance structure do not change over time. Financial log prices are non-stationary (they trend, drift, and contain a unit root). Log returns are typically stationary. The ADF test formalizes this distinction.

**ADF test regression:**

$$\Delta y_t = \alpha + \beta t + \gamma y_{t-1} + \sum_{i=1}^{p} \delta_i \Delta y_{t-i} + \varepsilon_t$$

- **H₀:** γ = 0 — unit root present; shocks are permanent, the series never mean-reverts
- **H₁:** γ < 0 — series is stationary; shocks decay over time

Lag length p is selected by minimizing AIC over candidate specifications. The test is applied to both the raw log price series and the log return series. Results — ADF statistic, p-value, and critical values at 1%, 5%, and 10% — are exported to `tables/adf_results.csv` and `adf_results.xlsx`.

**Expected finding:** Log prices contain a unit root (fail to reject H₀; p > 0.05). Log returns are stationary (reject H₀; p < 0.01). This confirms that one round of differencing (taking log returns from log prices) is sufficient to achieve stationarity, establishing d = 1 in the ARIMA specification.

---

### Step 3 — ARIMA Identification, Estimation & Forecasting

**Order Identification:**
ACF (Autocorrelation Function) and PACF (Partial Autocorrelation Function) plots of the stationary return series are examined for significant lags indicating the appropriate AR order (p) and MA order (q). The identification rules are:

| Pattern | Implication |
|---------|------------|
| PACF cuts off after lag p; ACF decays | AR(p) process |
| ACF cuts off after lag q; PACF decays | MA(q) process |
| Both ACF and PACF decay exponentially | Mixed ARMA(p,q) process |

**Model Selection:**
Multiple candidate ARIMA(p, d, q) specifications are estimated and compared by AIC and BIC:

$$AIC = -2\ell(\hat{\theta}) + 2k \qquad BIC = -2\ell(\hat{\theta}) + k\ln(n)$$

where ℓ(θ̂) is the maximized log-likelihood and k is the number of free parameters. BIC penalizes model complexity more heavily and typically selects more parsimonious models. The full model selection table is saved in the ADF results and printed inline, and is reproduced in the PDF showcase.

**Estimation:**
The selected ARIMA(p, d, q) is estimated by maximum likelihood using `statsmodels.tsa.arima.model.ARIMA`. The full estimation output is saved to `outputs/arima_summary.txt`.

**Forecasting:**
Out-of-sample point forecasts and 95% confidence intervals are generated over a specified horizon and exported to `tables/arima_forecast.csv`. The forecast chart (`figures/arima_forecast_clean.png`) clearly delineates the in-sample fitted values from the out-of-sample projection region.

**Residual Diagnostics:**
Model adequacy is verified by testing that residuals behave as white noise:
- **Ljung-Box test** — tests for remaining serial autocorrelation in residuals across multiple lags simultaneously
- **Residual ACF plot** — visually confirms absence of significant spikes beyond what chance produces
- **Residual histogram** — checks for gross departures from approximate normality in the innovations

Passing all three diagnostics confirms the ARIMA has absorbed the available linear autocorrelation structure in the conditional mean. Failing suggests model misspecification and prompts re-specification.

---

### Step 4 — GARCH(1,1) Conditional Variance Modelling

**Testing for ARCH Effects:**
Even after fitting an adequate ARIMA model, squared residuals from financial return series almost universally exhibit persistent serial autocorrelation — the signature of **ARCH effects** (time-varying conditional variance). Engle's ARCH-LM test is applied:

The test regresses ε̂²_t on its lagged values and tests joint significance. A significant result (p < 0.05) confirms that variance is not constant over time and that a conditional variance model is justified.

**GARCH(1,1) Specification (Bollerslev, 1986):**

$$\sigma_t^2 = \omega + \alpha \varepsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

where:
- `σ²_t` — conditional variance at time t (the quantity being modelled)
- `ε²_{t-1}` — squared return innovation from the prior period (**ARCH term**): measures the impact of the most recent shock on current variance
- `σ²_{t-1}` — conditional variance from the prior period (**GARCH term**): measures how much of yesterday's variance carries forward
- `ω`, `α`, `β` — parameters estimated by maximum likelihood

The model is estimated using `arch.arch_model` with `vol='GARCH'`, `p=1`, `q=1`. Both Normal and Student-t innovation distributions are evaluated; the better fit by log-likelihood is selected. The full estimation summary is saved to `outputs/garch_summary.txt`.

**Conditional Volatility Export:**
The fitted conditional standard deviation series σ_t is extracted, annualized (`σ_t × √252`), and exported to `tables/garch_volatility.csv`. This is the model's estimate of time-varying annualized risk at each point in the sample — the primary practical output of the GARCH model.

**Volatility Persistence:**
The sum `α + β` is the single most important summary statistic from the GARCH(1,1). It governs how quickly a volatility shock decays toward the long-run unconditional level. For daily equity returns, `α + β` typically falls in the range 0.97 to 0.99, meaning elevated volatility following a major shock persists for many weeks before subsiding — with direct implications for risk forecasting horizons and option pricing.

---

### Step 5 — Forecast Evaluation: RMSE Benchmarking

ARIMA model forecast accuracy on the held-out test set is evaluated using **Root Mean Square Error (RMSE)**:

$$RMSE = \sqrt{\frac{1}{n}\sum_{t=1}^{n}\!\left(\hat{r}_t - r_t\right)^2}$$

The ARIMA forecasts are benchmarked against a **naive random walk baseline** (forecast = last observed value):

$$\hat{r}_{t+1}^{\text{naive}} = r_t$$

The random walk is the canonical baseline for financial return forecasting because it reflects the efficient markets hypothesis: in efficient markets, the best forecast of tomorrow's return is today's return (or zero, for zero-drift processes). A model that cannot beat the random walk provides no practical forecasting value.

RMSE results are tabulated in `tables/rmse_table.csv` and `rmse_table.xlsx`, with percentage improvement or deterioration relative to the naive baseline clearly reported.

---

## Figures

### `figures/returns_series.png`

Full time series plot of log returns for the target asset across the complete sample period. The y-axis shows return magnitude; the x-axis shows calendar dates.

Volatility clustering is immediately visible as the defining structural feature: extended stretches of small-magnitude, tightly distributed returns alternate with turbulent periods of large, high-magnitude returns persisting for days to weeks. This visual pattern is the primary motivation for GARCH modelling — conditional variance is predictable from past conditional variance and squared shocks, even when the conditional mean is not. Significant macro events or market stress periods corresponding to visible volatility spikes can be annotated directly on the chart.

---

### `figures/adf_test_chart.png`

The return series plotted alongside two rolling statistics computed over a 60-day window:

- **Rolling mean** — flat or near-zero horizontal movement is consistent with stationarity of the mean
- **Rolling standard deviation** — bounded, non-trending movement is consistent with constant unconditional variance

A constant rolling mean and bounded rolling standard deviation together provide visual evidence of weak stationarity. The ADF test statistic and p-value for both the price and return series are annotated directly on the chart, linking the visual evidence to the formal test result.

---

### `figures/arima_forecast_clean.png`

A clean, publication-quality forecast chart with a clear train/test split, composed of two regions separated by a vertical dashed line:

**In-sample region:** realized return observations plotted in neutral grey; ARIMA fitted (in-sample) values overlaid in a contrasting color, showing how well the model tracks the historical series.

**Out-of-sample region:** realized test-set observations plotted in grey (where available for direct comparison); ARIMA point forecasts plotted as a solid colored line; **shaded 95% confidence interval bands** surrounding the forecast — naturally widening over the forecast horizon as multi-step ahead uncertainty accumulates.

The chart is formatted for direct inclusion in professional presentations and academic documents — minimal grid, clean axes, no unnecessary elements.

---

### `figures/garch_volatility.png`

Time series plot of the GARCH(1,1) estimated **annualized conditional volatility** (`σ_t × √252`) across the full sample period:

- **Conditional volatility series** — the model's time-varying estimate of annualized risk at each trading date; peaks during market stress periods are prominent and clearly interpretable
- **Unconditional (long-run) baseline** — horizontal dashed line at `ω / (1 − α − β)`, the model-implied long-run average volatility level to which conditional volatility mean-reverts
- **Regime structure** — extended periods where conditional volatility lies substantially above or below the unconditional level correspond respectively to high-risk regimes (elevated post-shock persistence) and low-risk regimes (calm market conditions)
- **Volatility spikes** — sharp upward movements corresponding to macro events or market shocks demonstrate that conditional variance responds rapidly to news

This chart is the central practical output of the GARCH model and directly demonstrates the value of time-varying over constant volatility estimation.

---

## Data & Outputs

| File | Format | Description |
|------|--------|-------------|
| `tables/adf_results.csv` | CSV | ADF test statistic, p-value, critical values at 1% / 5% / 10% for each tested series |
| `tables/adf_results.xlsx` | Excel | Same, with column formatting and conditional highlighting |
| `tables/arima_forecast.csv` | CSV | Date, point forecast, 95% CI lower bound, 95% CI upper bound |
| `tables/garch_volatility.csv` | CSV | Date, daily conditional σ, annualized conditional σ (= daily σ × √252) |
| `tables/rmse_table.csv` | CSV | Model name, RMSE, percentage improvement / deterioration vs naive baseline |
| `tables/rmse_table.xlsx` | Excel | Same, with formatting and conditional color-coding |
| `outputs/arima_summary.txt` | TXT | Complete `statsmodels` ARIMA `.summary()` — all coefficients, diagnostics, and information criteria |
| `outputs/garch_summary.txt` | TXT | Complete `arch` GARCH `.summary()` — ω, α, β, persistence, unconditional variance, log-likelihood |

---

## Key Results

Results are computed at notebook runtime and exported to the files above. All values are also fully populated in the **PDF Portfolio Showcase** without requiring any code execution. The schemas below document the output structure.

### ADF Stationarity Results

| Series Tested | ADF Statistic | p-value | Decision |
|--------------|:------------:|:-------:|:--------:|
| Log price level | — | > 0.05 | **Fail to reject H₀** — unit root, non-stationary |
| Log returns | — | < 0.01 | **Reject H₀** — stationary ✓ |

### GARCH(1,1) Parameter Estimates

| Parameter | Symbol | Estimate | Std. Error | Interpretation |
|-----------|:------:|:--------:|:----------:|----------------|
| Constant | ω | — | — | Baseline contribution to conditional variance — long-run variance floor |
| ARCH term | α | — | — | Sensitivity of today's variance to yesterday's squared shock |
| GARCH term | β | — | — | Fraction of yesterday's conditional variance carried forward to today |
| **Persistence** | **α + β** | — | — | **Total volatility shock persistence — must be < 1 for covariance stationarity** |

Unconditional (long-run) variance: `σ̄² = ω / (1 − α − β)`

### RMSE Forecast Comparison

| Model | RMSE | vs Naive Baseline |
|-------|:----:|:-----------------:|
| ARIMA(p,d,q) | — | — |
| Naive random walk | — | Baseline |

Full results with all values populated are in the exported tables and in the PDF showcase.

---

## Theoretical Background

**ADF Unit Root Test:**

$$\Delta y_t = \alpha + \beta t + \gamma y_{t-1} + \sum_{i=1}^{p} \delta_i \Delta y_{t-i} + \varepsilon_t$$

A unit root (γ = 0) means shocks to the series are permanent — the series has infinite memory and never returns to any fixed level. Financial log prices exhibit unit roots; log returns, obtained by first-differencing log prices, typically do not.

**ARIMA(p, d, q):**

$$\phi(B)(1-B)^d y_t = c + \theta(B)\varepsilon_t$$

B is the backshift operator, `φ(B) = 1 − φ₁B − ⋯ − φₚBᵖ` is the AR polynomial, `θ(B) = 1 + θ₁B + ⋯ + θ_qBq` is the MA polynomial, and d is the order of integration. For log returns d = 1 (one difference of log prices gives log returns).

**GARCH(1,1) Conditional Variance:**

$$\sigma_t^2 = \omega + \alpha \varepsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

**Stationarity conditions:** ω > 0, α ≥ 0, β ≥ 0, and **α + β < 1** (covariance stationarity — volatility shocks eventually decay to the long-run level).

**Unconditional (long-run) variance:**

$$\bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \beta}$$

**Volatility persistence interpretation:**

| α + β | Practical Meaning |
|:-----:|------------------|
| < 0.90 | Moderate persistence — volatility shocks dissipate within weeks |
| 0.90 – 0.97 | High persistence — elevated volatility can last months |
| > 0.97 | Very high persistence — typical for daily equity returns; shocks decay over many months |
| = 1.00 | **Integrated GARCH (IGARCH)** — unit root in variance; unconditional variance does not exist |

For daily equity return series, `α + β` in the range 0.97–0.99 is standard. This means a major volatility shock — such as a market crisis — can sustain elevated conditional variance for a year or more before returning to the unconditional level, which has significant implications for multi-horizon risk forecasting and options pricing.

**RMSE:**

$$RMSE = \sqrt{\frac{1}{n}\sum_{t=1}^{n}(\hat{r}_t - r_t)^2}$$

For daily financial return series, the signal-to-noise ratio in the conditional mean is very low — close to zero. The random walk is therefore an extremely competitive benchmark. The practical value of ARIMA modelling in daily return forecasting is often modest; GARCH models for the conditional variance typically offer more genuine out-of-sample value for risk management applications, since conditional variance is far more persistent and forecastable than the conditional mean.

---

## Installation & Usage

```bash
# Navigate to this project from the repository root
cd 03_financial_econometrics

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# Install all dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook 03_Financial_Econometrics_TimeSeries.ipynb
```

**`requirements.txt`:**
```
numpy>=1.24
pandas>=2.0
scipy>=1.10
statsmodels>=0.14
arch>=6.0
matplotlib>=3.7
seaborn>=0.12
yfinance>=0.2
openpyxl>=3.1
jupyter>=1.0
```

Run all cells sequentially. The notebook will: retrieve and prepare the return series → conduct ADF tests and export results → identify and estimate the ARIMA model → run residual diagnostics → test for ARCH effects → estimate the GARCH(1,1) → generate all forecasts → compute RMSE benchmarks → save all figures to `figures/`, all tables to `tables/`, and all model summaries to `outputs/`.

> **No code required.** Open [`Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf`](./Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf) for the complete results in a fully self-contained document.

---

## Related Projects

| Project | Relationship to This Work |
|---------|--------------------------|
| [01 — Efficient Frontier & Portfolio Optimization](../01_efficient_frontier/README.md) | Portfolio construction using assets whose return dynamics are formally modelled here; the constant-variance assumption of Markowitz theory is challenged by the time-varying volatility documented in this project |
| [02 — Financial Asset Return Analysis](../02_asset_return_analysis/README.md) | The rolling volatility analysis and non-normality evidence from Project 02 provide the empirical motivation for GARCH modelling — this project formalizes those observations into an estimated econometric model |

<br>

[← Back to Portfolio Hub](../README.md)
