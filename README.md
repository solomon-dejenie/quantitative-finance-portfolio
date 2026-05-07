<div align="center">

<br>

# Quantitative Finance Portfolio

### Three professional-grade projects in portfolio optimization, statistical risk analysis, and financial econometrics

<br>

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)
[![NumPy](https://img.shields.io/badge/NumPy-%E2%89%A51.24-013243?style=flat-square&logo=numpy&logoColor=white)]()
[![pandas](https://img.shields.io/badge/pandas-%E2%89%A52.0-150458?style=flat-square&logo=pandas&logoColor=white)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](./LICENSE)
[![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)]()

<br>

*Three independent projects · Full end-to-end reproducibility · PDF Portfolio Showcases · Publication-ready outputs*

<br>

</div>

---

## About This Repository

This repository is a structured quantitative finance research portfolio comprising three independent, professional-grade analytical projects. Each covers a distinct pillar of applied financial analysis and is delivered in a consistent dual-format structure: a **fully documented Jupyter notebook** for end-to-end reproducibility, and a **standalone PDF Portfolio Showcase** — a polished, print-ready document presenting the complete methodology, all visualizations, results tables, and written interpretation, without requiring any code execution or Python environment.

The projects form a deliberate analytical progression. **Project 02** establishes the empirical foundation by rigorously characterizing the statistical properties of individual asset return distributions — examining non-normality, fat tails, negative skewness, volatility clustering, and drawdown structure. **Project 01** builds on that foundation to construct optimal multi-asset portfolios using Markowitz mean-variance theory. **Project 03** advances to formal econometric time series modelling, applying ARIMA and GARCH frameworks to model return dynamics and estimate time-varying conditional volatility.

Together, the three projects cover the quantitative methods most central to roles in asset management, risk, and quantitative research.

---

## 📄 PDF Portfolio Showcases

Each project ships with a standalone, professionally formatted PDF — designed specifically for sharing with **recruiters, hiring managers, academic reviewers, and professional contacts**. Each document is fully self-contained: all methodology, charts, results tables, and written interpretation are included, with no code execution or technical setup required.

<br>

<div align="center">

| # | Project | PDF Portfolio Showcase | Jupyter Notebook |
|:-:|---------|----------------------|-----------------|
| **01** | Efficient Frontier & Portfolio Optimization | [📄 Open PDF Showcase](./01_efficient_frontier/Efficient_Frontier_Portfolio_Optimization_Showcase.pdf) | [📓 Open Notebook](./01_efficient_frontier/01_Efficient_Frontier_Portfolio_Optimization.ipynb) |
| **02** | Financial Asset Return Analysis | [📄 Open PDF Showcase](./02_asset_return_analysis/Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf) | [📓 Open Notebook](./02_asset_return_analysis/02_Financial_Asset_Return_Analysis.ipynb) |
| **03** | Financial Econometrics & Time Series | [📄 Open PDF Showcase](./03_financial_econometrics/Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf) | [📓 Open Notebook](./03_financial_econometrics/03_Financial_Econometrics_TimeSeries.ipynb) |

</div>

<br>

> **For recruiters and reviewers:** the PDF showcases are the fastest path to evaluating each project. They are print-ready, fully self-contained, and require zero technical setup.

---

### What Each PDF Portfolio Showcase Contains

<details>
<summary><strong>📄 Project 01 — Efficient Frontier & Portfolio Optimization Showcase</strong>&nbsp; (click to expand)</summary>

<br>

| # | Section | Contents |
|---|---------|---------|
| 1 | **Executive Summary** | Project scope, analytical approach, and headline findings |
| 2 | **Data & Return Computation** | Asset universe, data sources, log return methodology, annualization conventions |
| 3 | **Monte Carlo Simulation** | Feasible set construction — 10,000+ portfolios, constraint enforcement, risk-return metrics |
| 4 | **Efficient Frontier Chart** | Annotated scatter of simulated portfolios colored by Sharpe ratio, with frontier curve, MVP and MSP markers, and Capital Market Line |
| 5 | **Analytical Optimization** | SLSQP quadratic programming — MVP and MSP derivation with full step-by-step methodology |
| 6 | **Optimal Weight Allocations** | Per-asset weight breakdown for both MVP and MSP — fully populated numeric table |
| 7 | **Performance Metrics Table** | Annualized return, volatility, and Sharpe ratio for MVP, MSP, and equal-weight benchmark — all values populated |
| 8 | **Cumulative Return Backtest** | Out-of-sample chart: $1 invested in MVP vs MSP vs equal-weight, terminal values annotated |
| 9 | **Correlation Heatmap** | Annotated Pearson correlation matrix, hierarchically clustered, with diversification commentary |
| 10 | **Theoretical Background** | Portfolio variance, Sharpe ratio, Capital Market Line, and mutual fund separation theorem |

</details>

<details>
<summary><strong>📄 Project 02 — Financial Asset Return Analysis Showcase</strong>&nbsp; (click to expand)</summary>

<br>

| # | Section | Contents |
|---|---------|---------|
| 1 | **Executive Summary** | Research motivation, scope, and key distributional findings across all assets |
| 2 | **The Non-Normality Problem** | Why the Gaussian assumption fails for financial returns and the risk management consequences |
| 3 | **Risk Summary Table** | Annualized return, volatility, skewness, excess kurtosis, 5% historical VaR, and MDD — fully populated for every asset |
| 4 | **Return Distribution Charts** | Histograms with fitted Gaussian overlay — annotated with skewness, kurtosis, and Jarque-Bera p-value per asset |
| 5 | **Jarque-Bera Test Results** | Formal normality test statistics and p-values with verdict per asset |
| 6 | **Q-Q Normality Plots** | Empirical quantile vs theoretical normal — tail deviation and S-curve analysis per asset |
| 7 | **Rolling Volatility Charts** | 21-day and 63-day annualized rolling volatility with volatility clustering and regime commentary |
| 8 | **Drawdown Profile Charts** | Peak-to-trough drawdown curves with maximum drawdown magnitude and recovery duration annotated |
| 9 | **Implications** | What the distributional findings mean for portfolio construction and risk management in practice |

</details>

<details>
<summary><strong>📄 Project 03 — Financial Econometrics & Time Series Showcase</strong>&nbsp; (click to expand)</summary>

<br>

| # | Section | Contents |
|---|---------|---------|
| 1 | **Executive Summary** | Econometric pipeline overview, motivation, and key modelling results |
| 2 | **Exploratory Analysis** | Return series time plot with volatility clustering and heteroskedasticity highlighted |
| 3 | **ADF Stationarity Results** | Full results table — ADF statistic, p-value, critical values at 1%/5%/10% for price and return series |
| 4 | **ARIMA Model Selection** | AIC/BIC comparison table across candidate (p,d,q) specifications with selected model highlighted |
| 5 | **ARIMA Estimation Output** | Coefficient estimates, standard errors, t-statistics, p-values, log-likelihood, information criteria |
| 6 | **ARIMA Forecast Chart** | In-sample fitted values + out-of-sample point forecast + shaded 95% confidence interval bands |
| 7 | **ARCH-LM Test** | Engle's test result confirming conditional heteroskedasticity in ARIMA residuals |
| 8 | **GARCH(1,1) Estimation Output** | ω, α, β estimates with standard errors; α+β persistence; unconditional variance; log-likelihood; AIC/BIC |
| 9 | **Conditional Volatility Chart** | GARCH(1,1) time-varying conditional volatility with long-run unconditional baseline annotated |
| 10 | **RMSE Benchmarking** | ARIMA vs naive random walk — out-of-sample RMSE table with percentage comparison |
| 11 | **Residual Diagnostics** | ACF of standardized residuals; residual histogram vs normal overlay; Ljung-Box test results |
| 12 | **Parameter Interpretation** | Economic meaning of all estimated ARIMA and GARCH coefficients |

</details>

---

## 🗂️ Repository Structure

```
quantitative-finance-portfolio/
│
├── README.md                                                              ← Portfolio hub (this file)
├── LICENSE
│
├── 01_efficient_frontier/
│   ├── 01_Efficient_Frontier_Portfolio_Optimization.ipynb                ← Full analysis notebook
│   ├── Efficient_Frontier_Portfolio_Optimization_Showcase.pdf            ← ★ PDF Portfolio Showcase
│   ├── figures/
│   │   ├── efficient_frontier.png                                        ← Feasible set + frontier curve + CML
│   │   ├── cumulative_returns.png                                        ← Backtested cumulative returns (MVP / MSP / EW)
│   │   └── correlation_heatmap.png                                       ← Pearson correlation matrix (clustered)
│   ├── tables/
│   │   ├── asset_prices.csv                                              ← Adjusted closing prices
│   │   ├── log_returns.csv                                               ← Daily log returns
│   │   ├── expected_returns.csv                                          ← Annualized expected returns
│   │   ├── covariance_matrix.csv                                         ← Annualized covariance matrix Σ
│   │   └── correlation_matrix.csv                                        ← Pearson correlation matrix
│   ├── outputs/
│   │   └── run_summary.txt                                               ← Optimal weights & performance metrics
│   ├── requirements.txt
│   └── README.md
│
├── 02_asset_return_analysis/
│   ├── 02_Financial_Asset_Return_Analysis.ipynb                          ← Full analysis notebook
│   ├── Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf            ← ★ PDF Portfolio Showcase
│   ├── figures/
│   │   ├── return_distribution.png                                       ← Return histograms + Gaussian overlay
│   │   ├── qq_plot_returns.png                                           ← Q-Q plots: empirical vs theoretical normal
│   │   ├── rolling_volatility.png                                        ← 21-day and 63-day rolling volatility
│   │   └── drawdown_profile.png                                          ← Peak-to-trough drawdown curves
│   ├── tables/
│   │   ├── returns_data.csv                                              ← Full daily log return series
│   │   └── risk_summary.csv                                              ← Risk statistics per asset
│   ├── requirements.txt
│   └── README.md
│
└── 03_financial_econometrics/
    ├── 03_Financial_Econometrics_TimeSeries.ipynb                        ← Full analysis notebook
    ├── Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf          ← ★ PDF Portfolio Showcase
    ├── figures/
    │   ├── returns_series.png                                            ← Return series time plot
    │   ├── adf_test_chart.png                                            ← Rolling stats + stationarity visual
    │   ├── arima_forecast_clean.png                                      ← In-sample fit + forecast + CI bands
    │   └── garch_volatility.png                                          ← GARCH(1,1) conditional volatility
    ├── tables/
    │   ├── adf_results.csv / adf_results.xlsx                           ← ADF test statistics & critical values
    │   ├── arima_forecast.csv                                            ← Point forecasts + 95% CI bounds
    │   ├── garch_volatility.csv                                          ← Conditional volatility time series
    │   └── rmse_table.csv / rmse_table.xlsx                             ← RMSE model comparison
    ├── outputs/
    │   ├── arima_summary.txt                                             ← Full ARIMA estimation output
    │   └── garch_summary.txt                                             ← Full GARCH estimation output
    ├── requirements.txt
    └── README.md
```

---

## 🚀 Projects

### [01 — Efficient Frontier & Portfolio Optimization](./01_efficient_frontier/README.md)

> 📄 [PDF Portfolio Showcase](./01_efficient_frontier/Efficient_Frontier_Portfolio_Optimization_Showcase.pdf) &nbsp;·&nbsp; 📓 [Jupyter Notebook](./01_efficient_frontier/01_Efficient_Frontier_Portfolio_Optimization.ipynb)

Implements the complete **Markowitz Mean-Variance framework** from first principles. Over 10,000 random portfolios are simulated via Monte Carlo (Dirichlet-sampled weights) to map the full feasible investment set on the risk-return plane. `scipy.optimize` with SLSQP then solves analytically for the **Minimum Variance Portfolio (MVP)** — the leftmost feasible point — and the **Maximum Sharpe Ratio Portfolio (MSP)** — the Capital Market Line tangency portfolio. The efficient frontier is traced by solving the parametric minimum-variance problem across a fine grid of target return levels. Both optimal portfolios are backtested out-of-sample against an equal-weight (1/N) benchmark.

| Key Output | Description |
|------------|-------------|
| `efficient_frontier.png` | 10,000+ simulated portfolios (Sharpe-colored) + frontier curve + MVP/MSP markers + CML |
| `cumulative_returns.png` | Out-of-sample backtested cumulative returns: MVP vs MSP vs equal-weight |
| `correlation_heatmap.png` | Annotated Pearson correlation matrix, hierarchically clustered |
| `run_summary.txt` | Optimal per-asset weights and full annualized performance metrics |

**Methods:** Mean-variance optimization · Monte Carlo simulation · SLSQP quadratic programming · Sharpe ratio maximization · Capital Market Line · Efficient frontier construction · Out-of-sample backtesting

---

### [02 — Financial Asset Return Analysis](./02_asset_return_analysis/README.md)

> 📄 [PDF Portfolio Showcase](./02_asset_return_analysis/Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf) &nbsp;·&nbsp; 📓 [Jupyter Notebook](./02_asset_return_analysis/02_Financial_Asset_Return_Analysis.ipynb)

A rigorous **statistical characterization of asset return distributions** across a multi-asset universe — formally dismantling the normality assumption embedded in classical portfolio and risk theory. Jarque-Bera testing and Q-Q plots provide quantitative and graphical evidence of fat tails and negative skewness. Rolling standard deviation windows (21-day and 63-day) capture time-varying volatility clustering regimes. Drawdown profiling quantifies worst-case historical loss magnitude and duration per asset. All risk metrics are consolidated into a portable risk summary table.

| Key Output | Description |
|------------|-------------|
| `return_distribution.png` | Return histograms with fitted Gaussian overlay, annotated per asset |
| `qq_plot_returns.png` | Q-Q plots: empirical return quantiles vs theoretical normal |
| `rolling_volatility.png` | 21-day and 63-day annualized rolling volatility across the full sample |
| `drawdown_profile.png` | Peak-to-trough drawdown curves with MDD annotated per asset |
| `risk_summary.csv` | Return, vol, skewness, excess kurtosis, 5% VaR, and MDD per asset |

**Methods:** Log return computation · Descriptive statistics · Jarque-Bera normality testing · Q-Q analysis · Rolling volatility (21-day / 63-day) · Historical VaR · Maximum drawdown profiling

---

### [03 — Financial Econometrics & Time Series](./03_financial_econometrics/README.md)

> 📄 [PDF Portfolio Showcase](./03_financial_econometrics/Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf) &nbsp;·&nbsp; 📓 [Jupyter Notebook](./03_financial_econometrics/03_Financial_Econometrics_TimeSeries.ipynb)

Applies the **complete econometric modelling pipeline** to financial return time series, following the methodology standard in academic empirical finance and quantitative research. ADF unit root testing establishes stationarity. ACF/PACF-guided ARIMA specification and AIC/BIC model comparison determine the conditional mean model. Engle's ARCH-LM test confirms conditional heteroskedasticity in residuals, motivating GARCH(1,1) for the variance equation. Out-of-sample ARIMA forecast accuracy is evaluated via RMSE, benchmarked against a naive random walk. All model outputs, parameter estimates, and forecasts are exported in both CSV and Excel formats.

| Key Output | Description |
|------------|-------------|
| `adf_results.csv / .xlsx` | ADF statistic, p-value, critical values at 1% / 5% / 10% |
| `arima_forecast_clean.png` | In-sample fit + out-of-sample forecast + shaded 95% CI bands |
| `garch_volatility.png` | GARCH(1,1) conditional volatility + long-run unconditional baseline annotated |
| `arima_summary.txt` | Full `statsmodels` ARIMA estimation output |
| `garch_summary.txt` | Full `arch` GARCH output — ω, α, β, persistence, log-likelihood |
| `rmse_table.csv / .xlsx` | RMSE: ARIMA vs naive random walk, with percentage improvement |

**Methods:** ADF unit root testing · ARIMA(p,d,q) identification & estimation · ACF/PACF order selection · AIC/BIC model comparison · Engle ARCH-LM test · GARCH(1,1) conditional variance · Volatility persistence · RMSE benchmarking · Ljung-Box residual diagnostics

---

## 🛠️ Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| `numpy` | ≥ 1.24 | Matrix algebra, numerical computation, random sampling |
| `pandas` | ≥ 2.0 | Time series data handling, CSV and Excel I/O |
| `scipy` | ≥ 1.10 | Portfolio optimization (SLSQP), statistical tests |
| `statsmodels` | ≥ 0.14 | ARIMA modelling, ADF testing, Ljung-Box diagnostics |
| `arch` | ≥ 6.0 | GARCH(1,1) conditional variance estimation |
| `matplotlib` | ≥ 3.7 | Core visualization engine |
| `seaborn` | ≥ 0.12 | Statistical graphics and correlation heatmaps |
| `yfinance` | ≥ 0.2 | Historical market price data retrieval |
| `openpyxl` | ≥ 3.1 | Excel (.xlsx) export for results tables |
| `jupyter` | ≥ 1.0 | Interactive notebook environment |

**Python 3.10 or higher required.** Each project is fully self-contained with its own `requirements.txt`. There are no cross-project dependencies.

---

## ⚡ Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/your-username/quantitative-finance-portfolio.git
cd quantitative-finance-portfolio

# 2. Enter any project directory
cd 01_efficient_frontier
# cd 02_asset_return_analysis
# cd 03_financial_econometrics

# 3. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# 4. Install project dependencies
pip install -r requirements.txt

# 5. Launch Jupyter and open the notebook
jupyter notebook
```

Run all cells sequentially from top to bottom. All figures, tables, and output files are generated and saved to their respective subdirectories automatically.

> **No code required to review results.** Open any of the three **PDF Portfolio Showcases** above for the complete analysis — methodology, all charts, all tables, and full written interpretation — in a single, self-contained document.

---

## 📦 Project Delivery Format

Every project folder ships with an identical, fully self-contained delivery structure:

| Component | File(s) | Purpose |
|-----------|---------|---------|
| **Analysis Notebook** | `.ipynb` | Fully documented, end-to-end reproducible analysis |
| **PDF Portfolio Showcase** | `.pdf` | Professional presentation document — complete results, no code required |
| **Figures** | `figures/*.png` | Publication-quality charts exported at high resolution |
| **Data Tables** | `tables/*.csv` / `*.xlsx` | All inputs and results in portable, structured format |
| **Model Outputs** | `outputs/*.txt` | Model estimation summaries, run logs, and diagnostics |
| **Dependencies** | `requirements.txt` | Pinned library versions for exact environment reproducibility |
| **Documentation** | `README.md` | Full methodology, figure descriptions, theory, and usage guide |

---

## 📄 License

Licensed under the terms of the [MIT License](./LICENSE).

---

<div align="center">

<br>

**Your Name**

*Quantitative Finance · Statistical Modelling · Financial Econometrics*

<br>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/your-profile)
&nbsp;&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/your-username)
&nbsp;&nbsp;
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:your@email.com)

<br>

</div>

