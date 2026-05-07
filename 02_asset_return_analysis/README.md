#  Financial Asset Return Analysis

> **Project 02 of 3** — [← Back to Portfolio Hub](../README.md)

A rigorous **statistical analysis of financial asset returns**, examining distributional properties, normality assumptions, tail risk, rolling volatility dynamics, and drawdown characteristics across multiple securities. This project forms the empirical foundation for risk assessment and informs portfolio construction decisions.

---

##  Table of Contents

- [Overview](#overview)
- [Methodology](#methodology)
- [Project Structure](#project-structure)
- [Key Results](#key-results)
- [Figures](#figures)
- [Data](#data)
- [Installation & Usage](#installation--usage)
- [Theoretical Background](#theoretical-background)

---

## Overview

Understanding the statistical properties of asset returns is fundamental to quantitative finance. This project moves beyond the naive normality assumption widely used in classical models and rigorously examines:

- **Return distributions** — shape, skewness, kurtosis, and fat-tail behaviour
- **Normality testing** — graphical (Q-Q plots) and statistical (Jarque-Bera, Shapiro-Wilk)
- **Time-varying volatility** — rolling standard deviation windows
- **Drawdown analysis** — magnitude and duration of peak-to-trough losses

The analysis spans multiple assets, enabling cross-sectional comparison of risk profiles.

---

## Methodology

### 1. Return Computation
- Adjusted closing prices sourced for each asset
- **Log returns** computed: `r_t = ln(P_t / P_{t-1})`
- Descriptive statistics: mean, standard deviation, skewness, excess kurtosis, min/max

### 2. Distribution Analysis
- Histogram overlaid with fitted normal distribution for each asset
- **Jarque-Bera test** for normality: `JB = (n/6)[S² + (K-3)²/4]`
- Fat-tail assessment via excess kurtosis (`K > 3` implies leptokurtosis)

### 3. Q-Q Plot Analysis
- Quantile-Quantile plots compare empirical return quantiles to a theoretical normal distribution
- Deviations in the tails reveal non-normality and tail risk

### 4. Rolling Volatility
- **21-day** (monthly) and **63-day** (quarterly) rolling standard deviations computed
- Annualized: `σ_annual = σ_daily × √252`
- Captures regime changes and volatility clustering

### 5. Drawdown Analysis
- Running maximum tracked: `D_t = (P_t - max(P_{1..t})) / max(P_{1..t})`
- **Maximum Drawdown (MDD)** identified per asset
- Drawdown duration and recovery periods noted

---

## Project Structure

```
02_asset_return_analysis/
├── 02_Financial_Asset_Return_Analysis.ipynb            ← Main analysis notebook
├── Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf ← Polished PDF report
│
├── figures/
│   ├── return_distribution.png      ← Return histograms with normal overlay
│   ├── qq_plot_returns.png          ← Q-Q plots for normality assessment
│   ├── rolling_volatility.png       ← Time-varying volatility (rolling windows)
│   └── drawdown_profile.png         ← Drawdown curves per asset
│
├── tables/
│   ├── risk_summary.csv             ← Aggregated risk statistics per asset
│   └── returns_data.csv             ← Full log return series
│
├── requirements.txt
└── README.md
```

---

## Key Results

| Metric | Interpretation |
|--------|---------------|
| **Excess Kurtosis > 0** | Fat tails — more extreme returns than normal distribution predicts |
| **Negative Skewness** | Left tail heavier — larger downside moves than upside |
| **Q-Q Deviation at Tails** | Confirms non-normality; normality assumption underestimates tail risk |
| **Rolling Volatility Spikes** | Volatility clustering present — calm periods interrupted by sharp bursts |
| **Maximum Drawdown** | Captures worst peak-to-trough loss per asset over the sample period |

> *Full statistics per asset are saved in `tables/risk_summary.csv`.*

---

## Figures

### Return Distribution
`figures/return_distribution.png`
Histogram of daily log returns for each asset overlaid with a fitted Gaussian curve. Excess kurtosis and skewness annotated directly on the chart.

### Q-Q Plot
`figures/qq_plot_returns.png`
Quantile-Quantile plots comparing empirical return quantiles to theoretical normal quantiles. Tail deviations highlighted, confirming leptokurtic behaviour.

### Rolling Volatility
`figures/rolling_volatility.png`
Time series of 21-day and 63-day rolling annualized volatility per asset. Volatility regime changes and clustering periods clearly visible.

### Drawdown Profile
`figures/drawdown_profile.png`
Percentage drawdown from rolling peak for each asset over the full sample. Maximum drawdown levels annotated with dashed reference lines.

---

## Data

| File | Description |
|------|-------------|
| `tables/returns_data.csv` | Daily log return series (date-indexed, one column per asset) |
| `tables/risk_summary.csv` | Summary statistics: mean, std, skewness, kurtosis, VaR, MDD per asset |

---

## Installation & Usage

```bash
# From the repo root
cd 02_asset_return_analysis

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Open notebook
jupyter notebook 02_Financial_Asset_Return_Analysis.ipynb
```

**Requirements** (`requirements.txt`):
```
numpy
pandas
scipy
matplotlib
seaborn
yfinance
jupyter
```

Run all cells sequentially. Figures are rendered inline and saved to `figures/`. Risk summary is exported to `tables/risk_summary.csv`.

---

## Theoretical Background

**Log Returns:**
$$r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)$$

**Skewness** (asymmetry of distribution):
$$S = \frac{E[(r - \mu)^3]}{\sigma^3}$$

**Excess Kurtosis** (tail heaviness):
$$K - 3 = \frac{E[(r - \mu)^4]}{\sigma^4} - 3$$

**Jarque-Bera Test:**
$$JB = \frac{n}{6}\left[S^2 + \frac{(K-3)^2}{4}\right] \sim \chi^2(2)$$

**Maximum Drawdown:**
$$MDD = \min_t \frac{P_t - \max_{s \leq t} P_s}{\max_{s \leq t} P_s}$$

The departure of empirical return distributions from normality has profound implications for risk management — models such as **VaR** based on Gaussian assumptions systematically underestimate tail risk, motivating more robust distributional frameworks.

---

##  Related Projects

- [01 — Efficient Frontier & Portfolio Optimization](../01_efficient_frontier/README.md)
- [03 — Financial Econometrics & Time Series](../03_financial_econometrics/README.md)

---

*Part of the [Quantitative Finance Portfolio](../README.md)*

