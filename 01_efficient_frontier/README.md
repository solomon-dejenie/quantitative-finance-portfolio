#  Efficient Frontier & Portfolio Optimization

> **Project 01 of 3** — [← Back to Portfolio Hub](../README.md)

A complete implementation of **Markowitz Mean-Variance Portfolio Theory**, constructing the efficient frontier via Monte Carlo simulation and analytical optimization. This project identifies optimal portfolio allocations, compares risk-return trade-offs across thousands of simulated portfolios, and backtests performance using historical asset prices.

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

Modern Portfolio Theory (MPT), introduced by Harry Markowitz (1952), provides a mathematical framework for constructing portfolios that maximize expected return for a given level of risk. This project:

- Fetches and processes historical price data for a multi-asset universe
- Computes log returns, expected returns, and the covariance matrix
- Simulates **10,000+ random portfolios** to map the feasible investment set
- Solves analytically for the **Minimum Variance Portfolio (MVP)** and **Maximum Sharpe Ratio Portfolio (MSP)**
- Plots the **efficient frontier** and backtests cumulative portfolio returns

---

## Methodology

### 1. Data Preparation
- Historical adjusted closing prices ingested and cleaned
- **Log returns** computed: `r_t = ln(P_t / P_{t-1})`
- Annualized expected returns and covariance matrix estimated

### 2. Monte Carlo Simulation
- Random portfolio weights generated under the constraint: `Σwᵢ = 1, wᵢ ≥ 0`
- For each portfolio: expected return, volatility, and Sharpe ratio computed
- Full risk-return scatter plotted across the feasible set

### 3. Analytical Optimization
- **Minimum Variance Portfolio**: `min wᵀΣw` subject to `Σwᵢ = 1`
- **Maximum Sharpe Ratio Portfolio**: `max (μₚ - rƒ) / σₚ` using `scipy.optimize`
- Risk-free rate assumed at a standard benchmark (e.g., 3-month T-bill)

### 4. Performance Backtesting
- Optimal portfolio weights applied to out-of-sample price data
- Cumulative returns computed and visualized over the evaluation period

---

## Project Structure

```
01_efficient_frontier/
├── 01_Efficient_Frontier_Portfolio_Optimization.ipynb   ← Main analysis notebook
├── Efficient_Frontier_Portfolio_Optimization_Showcase.pdf ← Polished PDF report
│
├── figures/
│   ├── efficient_frontier.png       ← Frontier curve + optimal portfolios
│   ├── cumulative_returns.png       ← Backtested cumulative performance
│   └── correlation_heatmap.png      ← Asset correlation matrix
│
├── tables/
│   ├── asset_prices.csv             ← Raw adjusted closing prices
│   ├── log_returns.csv              ← Computed log returns
│   ├── expected_returns.csv         ← Annualized expected returns per asset
│   ├── covariance_matrix.csv        ← Annualized covariance matrix
│   └── correlation_matrix.csv       ← Pearson correlation matrix
│
├── outputs/
│   └── run_summary.txt              ← Optimal weights & performance metrics
│
├── requirements.txt
└── README.md
```

---

## Key Results

| Portfolio | Expected Return | Volatility | Sharpe Ratio |
|-----------|----------------|------------|--------------|
| Minimum Variance Portfolio | — | Lowest feasible | — |
| Maximum Sharpe Ratio Portfolio | — | — | Highest |

> *Exact values are populated in `outputs/run_summary.txt` after running the notebook.*

**Optimal weight allocations** for each portfolio are saved to `outputs/run_summary.txt`, including per-asset breakdown.

---

## Figures

### Efficient Frontier
`figures/efficient_frontier.png`
Scatter plot of 10,000+ simulated portfolios colored by Sharpe ratio, with the efficient frontier curve overlaid. The MVP and MSP are marked with distinct markers.

### Cumulative Returns
`figures/cumulative_returns.png`
Backtested cumulative return comparison between the MVP, MSP, and an equal-weight benchmark over the evaluation window.

### Correlation Heatmap
`figures/correlation_heatmap.png`
Annotated heatmap of pairwise Pearson correlations between all assets, highlighting diversification potential.

---

## Data

| File | Description |
|------|-------------|
| `tables/asset_prices.csv` | Adjusted closing prices (date-indexed) |
| `tables/log_returns.csv` | Daily log returns per asset |
| `tables/expected_returns.csv` | Annualized mean returns |
| `tables/covariance_matrix.csv` | Annualized covariance matrix |
| `tables/correlation_matrix.csv` | Pearson correlation matrix |
| `outputs/run_summary.txt` | Optimal weights and performance summary |

---

## Installation & Usage

```bash
# From the repo root
cd 01_efficient_frontier

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Open notebook
jupyter notebook 01_Efficient_Frontier_Portfolio_Optimization.ipynb
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

Run all cells sequentially. All figures and tables are generated and saved automatically.

---

## Theoretical Background

**Portfolio Return:**
$$\mu_p = \mathbf{w}^\top \boldsymbol{\mu}$$

**Portfolio Variance:**
$$\sigma_p^2 = \mathbf{w}^\top \boldsymbol{\Sigma} \mathbf{w}$$

**Sharpe Ratio:**
$$S = \frac{\mu_p - r_f}{\sigma_p}$$

The **efficient frontier** is the upper boundary of the minimum variance set — representing portfolios that offer the highest expected return for each level of risk. No rational investor holds a portfolio below this boundary.

---

## 📎 Related Projects

- [02 — Financial Asset Return Analysis](../02_asset_return_analysis/README.md)
- [03 — Financial Econometrics & Time Series](../03_financial_econometrics/README.md)

---

*Part of the [Quantitative Finance Portfolio](../README.md)*
