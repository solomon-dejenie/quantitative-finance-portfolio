<div align="center">

<br>

# Efficient Frontier & Portfolio Optimization

### Project 01 of 3 — Quantitative Finance Portfolio

<br>

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)
[![SciPy](https://img.shields.io/badge/SciPy-%E2%89%A51.10-8CAAE6?style=flat-square&logo=scipy&logoColor=white)]()
[![NumPy](https://img.shields.io/badge/NumPy-%E2%89%A51.24-013243?style=flat-square&logo=numpy&logoColor=white)]()
[![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)]()

<br>

[← Back to Portfolio Hub](../README.md)

<br>

</div>

---

## Overview

A complete, ground-up implementation of **Markowitz Mean-Variance Portfolio Theory** — the mathematical foundation of modern portfolio management since its introduction by Harry Markowitz in 1952. This project constructs the efficient frontier using two complementary approaches: Monte Carlo simulation to map the full feasible investment set, and analytical quadratic programming to identify the two canonical benchmark portfolios.

The **Minimum Variance Portfolio (MVP)** is the portfolio achieving the lowest attainable volatility across all feasible allocations — the leftmost point on the efficient frontier. The **Maximum Sharpe Ratio Portfolio (MSP)**, also called the tangency portfolio, is the single risky portfolio that maximizes risk-adjusted return per unit of volatility relative to a risk-free rate. It is the point where the Capital Market Line is tangent to the efficient frontier, and represents the optimal portfolio for any investor who can combine risky assets with a risk-free asset.

All intermediate outputs are exported for full transparency: raw prices, log return series, expected return vector, covariance and correlation matrices, optimal portfolio weight allocations, and a complete performance summary.

**What this project demonstrates:**

- Construction of the Markowitz efficient frontier from raw price data to final visualization
- Application of SLSQP constrained quadratic programming to solve the MVP and MSP
- How asset correlation structure determines the shape of the feasible set and the magnitude of diversification benefit
- The distinction between variance minimization and Sharpe ratio maximization as optimization objectives
- Out-of-sample performance backtesting of optimal portfolios against a naive equal-weight benchmark

---

## 📄 PDF Portfolio Showcase

<div align="center">

### [`Efficient_Frontier_Portfolio_Optimization_Showcase.pdf`](./Efficient_Frontier_Portfolio_Optimization_Showcase.pdf)

*A complete, professional-quality presentation of this project — no code or Python environment required*

</div>

<br>

The PDF showcase is the recommended starting point for reviewers, recruiters, and professional contacts. It is a fully self-contained, print-ready document covering every aspect of the project — from data preparation through to final results — with all figures, tables, equations, and written interpretation included.

**Complete contents of the PDF:**

| # | Section | What Is Included |
|---|---------|-----------------|
| 1 | **Executive Summary** | Project scope, asset universe, analytical approach, and headline portfolio results in one page |
| 2 | **Data & Return Preparation** | Asset selection rationale, data source, log return computation, annualization conventions, and data quality notes |
| 3 | **Monte Carlo Simulation** | Dirichlet weight sampling methodology, constraint enforcement, per-portfolio metric computation (return, volatility, Sharpe), full feasible set description |
| 4 | **Efficient Frontier Chart** | Full annotated chart — 10,000+ simulated portfolios colored by Sharpe ratio, efficient frontier curve, MVP and MSP markers, Capital Market Line from risk-free rate through MSP |
| 5 | **Analytical Optimization** | SLSQP quadratic programming formulation for both MVP and MSP, convergence diagnostics, constraint verification |
| 6 | **Optimal Weight Allocations** | Per-asset weight table for both MVP and MSP — all numeric values fully populated, with commentary on concentration and diversification |
| 7 | **Performance Metrics Table** | Annualized expected return, annualized volatility, and Sharpe ratio for MVP, MSP, and equal-weight benchmark — side-by-side comparison, all values populated |
| 8 | **Cumulative Return Backtest** | Out-of-sample backtesting chart — $1 invested at start, terminal cumulative values annotated, MVP vs MSP vs equal-weight comparison across the full evaluation window |
| 9 | **Correlation Heatmap** | Fully annotated Pearson correlation matrix with hierarchical asset clustering, color-scaled from −1 to +1, with written diversification commentary per asset pair group |
| 10 | **Theoretical Background** | Portfolio return and variance formulas, Sharpe ratio derivation, efficient frontier definition, CML equation, mutual fund separation theorem, diversification inequality |

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
01_efficient_frontier/
│
├── 01_Efficient_Frontier_Portfolio_Optimization.ipynb      ← Full reproducible analysis notebook
├── Efficient_Frontier_Portfolio_Optimization_Showcase.pdf  ← ★ PDF Portfolio Showcase
│
├── figures/
│   ├── efficient_frontier.png      ← Feasible set scatter + frontier curve + CML (Sharpe-colored)
│   ├── cumulative_returns.png      ← Out-of-sample cumulative returns: MVP vs MSP vs equal-weight
│   └── correlation_heatmap.png     ← Annotated Pearson correlation matrix (hierarchically clustered)
│
├── tables/
│   ├── asset_prices.csv            ← Adjusted closing prices (date-indexed, one column per asset)
│   ├── log_returns.csv             ← Daily log returns (date-indexed, one column per asset)
│   ├── expected_returns.csv        ← Annualized expected return per asset (vector)
│   ├── covariance_matrix.csv       ← Annualized covariance matrix Σ (n × n)
│   └── correlation_matrix.csv      ← Pearson correlation matrix (n × n)
│
├── outputs/
│   └── run_summary.txt             ← MVP and MSP weights, performance metrics, optimization log
│
├── requirements.txt
└── README.md
```

---

## Methodology

### Step 1 — Data Ingestion & Log Return Computation

Historical **adjusted closing prices** are retrieved for a multi-asset universe via `yfinance`. Prices are cleaned (forward-fill for isolated missing values, alignment on common trading dates) and stored in `tables/asset_prices.csv`.

**Daily log returns** are computed for each asset:

```
r_t = ln(P_t / P_{t-1})
```

Log returns are preferred over simple arithmetic returns for three reasons: they are time-additive (multiperiod log returns sum to the total log return); they are more symmetric and better approximate normality over short horizons; and they are consistent with the geometric Brownian motion models underlying continuous-time finance.

**Annualized parameters** are estimated from the full in-sample period and exported to `tables/`:
- **Expected return vector μ** — annualized: daily mean log return × 252
- **Covariance matrix Σ** — annualized: daily covariance × 252

### Step 2 — Monte Carlo Simulation

Over 10,000 random portfolios are generated by sampling weight vectors from a **Dirichlet distribution**, which produces compositions that naturally sum to 1 with all non-negative entries — simultaneously satisfying both the full investment and long-only constraints:

```
Σ wᵢ = 1     (full investment)
wᵢ ≥ 0       (long-only)
```

For each simulated portfolio, three metrics are computed and stored:

| Metric | Computation |
|--------|------------|
| Expected annual return | `μₚ = wᵀμ` |
| Annual volatility | `σₚ = √(wᵀΣw)` |
| Sharpe ratio | `S = (μₚ − rƒ) / σₚ` |

The cloud of (σₚ, μₚ) pairs is plotted on the risk-return plane and colored by Sharpe ratio. This scatter simultaneously reveals the feasible set and makes the efficient frontier visible as the upper-left envelope — the set of portfolios for which no dominating alternative exists.

### Step 3 — Analytical Optimization

**Minimum Variance Portfolio (MVP)** — solves the quadratic program:

```
minimize    wᵀΣw
subject to  Σwᵢ = 1,   wᵢ ≥ 0
```

This is a strictly convex quadratic objective with linear constraints, guaranteeing a unique global minimum. Solved using `scipy.optimize.minimize` with the SLSQP solver.

**Maximum Sharpe Ratio Portfolio (MSP)** — maximizes the Sharpe ratio equivalently by minimizing its negative:

```
minimize    −(wᵀμ − rƒ) / √(wᵀΣw)
subject to  Σwᵢ = 1,   wᵢ ≥ 0
```

The MSP is the **tangency portfolio** — the unique risky portfolio lying on the Capital Market Line. The risk-free rate `rƒ` is set to the prevailing 3-month Treasury bill yield at the time of analysis.

Optimal weights and performance metrics for both portfolios are written to `outputs/run_summary.txt` and fully tabulated in the PDF showcase.

### Step 4 — Efficient Frontier Construction

The efficient frontier is traced by solving the parametric minimum-variance problem across a fine grid of target return levels μ*, from the MVP return (lower bound) up to the maximum achievable return:

```
minimize    wᵀΣw
subject to  wᵀμ = μ*,  Σwᵢ = 1,   wᵢ ≥ 0
```

Each solution is a frontier portfolio. Plotting the (σ*, μ*) pairs across the grid traces the efficient frontier — the Pareto-optimal boundary above which no feasible portfolio exists and below which every portfolio is dominated.

### Step 5 — Performance Backtesting

MVP and MSP weights are applied to the **out-of-sample** price series (hold-out period not used in estimation). Realized cumulative returns are computed alongside an equal-weight (1/N) benchmark:

```
CR_T = ∏(1 + rₜ) − 1     where rₜ = Σ wᵢ · rᵢ,ₜ
```

Results are plotted in `figures/cumulative_returns.png` with all terminal values annotated, and presented in full in the PDF showcase.

---

## Figures

### `figures/efficient_frontier.png`

The central visualization of this project, composed of three overlaid elements:

**Scatter cloud** — all 10,000+ simulated portfolios at their (σₚ, μₚ) coordinates, colored by Sharpe ratio using a perceptually uniform colormap (deep purple = low Sharpe, bright yellow = high Sharpe), with a colorbar displayed alongside.

**Efficient frontier curve** — the analytically traced upper-left envelope of the feasible set, plotted as a smooth line. Begins at the MVP and extends to the maximum achievable return portfolio.

**Optimal portfolio markers** — the MVP (star marker, labeled "Minimum Variance") and MSP (diamond marker, labeled "Maximum Sharpe / Tangency") are plotted at their exact (σ, μ) coordinates. The **Capital Market Line (CML)** is drawn as a dashed line from the risk-free rate intercept on the y-axis through the MSP, extending beyond the frontier. Axes show annualized volatility (%) and annualized expected return (%).

---

### `figures/cumulative_returns.png`

A time series line chart comparing three strategies over the out-of-sample backtesting window:

- **MVP** — Minimum Variance Portfolio weights applied to hold-out period
- **MSP** — Maximum Sharpe Ratio Portfolio weights applied to hold-out period
- **Equal-Weight (1/N)** — naive benchmark, equal allocation across all assets

All series start indexed at 1.00. Terminal values are annotated at the right edge. A vertical dashed line marks the in-sample / out-of-sample boundary.

---

### `figures/correlation_heatmap.png`

An annotated heatmap of the full Pearson correlation matrix between all assets:

- **Cell values** — exact correlation coefficients displayed in each cell
- **Color scale** — diverging palette: deep blue (ρ = −1) through white (ρ = 0) to deep red (ρ = +1)
- **Asset ordering** — rows and columns reordered by hierarchical clustering, grouping correlated assets together and revealing the block correlation structure of the universe at a glance
- **Diversification insight** — asset pairs with low or negative correlations are the primary drivers of risk reduction; the heatmap makes these pairs immediately identifiable

---

## Data & Outputs

| File | Format | Description |
|------|--------|-------------|
| `tables/asset_prices.csv` | CSV | Adjusted closing prices — date-indexed, one column per asset ticker |
| `tables/log_returns.csv` | CSV | Daily log returns — date-indexed, one column per asset ticker |
| `tables/expected_returns.csv` | CSV | Annualized expected return per asset (single-row vector) |
| `tables/covariance_matrix.csv` | CSV | Annualized covariance matrix Σ — (n × n), asset-labeled rows and columns |
| `tables/correlation_matrix.csv` | CSV | Pearson correlation matrix — (n × n), asset-labeled rows and columns |
| `outputs/run_summary.txt` | TXT | MVP weights · MSP weights · annualized return, volatility, Sharpe for all portfolios · optimization diagnostics |

---

## Key Results

Results are computed at notebook runtime and written to `outputs/run_summary.txt`. The schema below shows the output structure; specific values are fully populated in the file after running the notebook and are also presented in the **PDF Portfolio Showcase** without requiring any execution.

**Portfolio Performance Summary:**

| Portfolio | Annualized Return | Annualized Volatility | Sharpe Ratio |
|-----------|:-----------------:|:--------------------:|:------------:|
| Minimum Variance Portfolio (MVP) | — | Minimum feasible | — |
| Maximum Sharpe Ratio Portfolio (MSP) | — | — | Maximum |
| Equal-Weight Benchmark | — | — | — |

**Per-asset weight allocations** for both the MVP and MSP are included in `run_summary.txt` and presented in a fully populated table in the PDF showcase.

---

## Theoretical Background

**Portfolio Expected Return:**

$$\mu_p = \mathbf{w}^\top \boldsymbol{\mu} = \sum_{i=1}^{n} w_i \mu_i$$

**Portfolio Variance:**

$$\sigma_p^2 = \mathbf{w}^\top \boldsymbol{\Sigma} \mathbf{w} = \sum_{i=1}^{n}\sum_{j=1}^{n} w_i w_j \sigma_{ij}$$

Portfolio variance depends on individual asset variances (diagonal of **Σ**) and all pairwise covariances (off-diagonal). When assets are imperfectly correlated (ρ < 1), portfolio variance is strictly less than the weighted average of individual variances — the mathematical basis of diversification.

**Sharpe Ratio:**

$$S = \frac{\mu_p - r_f}{\sigma_p}$$

**Efficient Frontier** — the locus of minimum-variance portfolios across all target return levels:

$$\min_{\mathbf{w}} \; \mathbf{w}^\top \boldsymbol{\Sigma} \mathbf{w} \quad \text{s.t.} \quad \mathbf{w}^\top \boldsymbol{\mu} = \mu^*, \;\; \mathbf{1}^\top \mathbf{w} = 1, \;\; \mathbf{w} \geq 0$$

Portfolios below the frontier are **dominated** — a superior alternative (higher return for the same risk, or lower risk for the same return) always exists on the frontier. No rational risk-averse investor should hold a sub-frontier portfolio.

**Capital Market Line (CML):**

$$\mu_C = r_f + \frac{\mu_{MSP} - r_f}{\sigma_{MSP}} \cdot \sigma_C$$

When a risk-free asset is available, all mean-variance investors hold the MSP as their risky portfolio, combined with the risk-free asset in proportions that reflect individual risk tolerance. This is the **mutual fund separation theorem** — the MSP is the universal risky portfolio.

**Diversification benefit:**

$$\sigma_p^2 < \sum_i w_i^2 \sigma_i^2 \quad \text{when} \quad \rho_{ij} < 1 \; \text{for some } i \neq j$$

---

## Installation & Usage

```bash
# Navigate to this project from the repository root
cd 01_efficient_frontier

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# Install all dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook 01_Efficient_Frontier_Portfolio_Optimization.ipynb
```

**`requirements.txt`:**
```
numpy>=1.24
pandas>=2.0
scipy>=1.10
matplotlib>=3.7
seaborn>=0.12
yfinance>=0.2
jupyter>=1.0
```

Run all cells sequentially. The notebook will: download and process price data → compute returns and covariance statistics → run Monte Carlo simulation and optimization → generate and save all figures → export all tables → write the run summary to `outputs/`.

> **No code required.** Open [`Efficient_Frontier_Portfolio_Optimization_Showcase.pdf`](./Efficient_Frontier_Portfolio_Optimization_Showcase.pdf) for the complete results in a fully self-contained document.

---

## Related Projects

| Project | Relationship to This Work |
|---------|--------------------------|
| [02 — Financial Asset Return Analysis](../02_asset_return_analysis/README.md) | Provides the distributional and risk analysis of the individual assets used to build this portfolio — the empirical foundation that motivates asset selection and diversification decisions |
| [03 — Financial Econometrics & Time Series](../03_financial_econometrics/README.md) | Applies ARIMA and GARCH models to the return series of these assets — extends the volatility analysis beyond the constant-variance assumption used in Markowitz theory |

<br>

[← Back to Portfolio Hub](../README.md)

