
<div align="center">

<br>

# Financial Asset Return Analysis

### Project 02 of 3 — Quantitative Finance Portfolio

<br>

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)
[![SciPy](https://img.shields.io/badge/SciPy-%E2%89%A51.10-8CAAE6?style=flat-square&logo=scipy&logoColor=white)]()
[![pandas](https://img.shields.io/badge/pandas-%E2%89%A52.0-150458?style=flat-square&logo=pandas&logoColor=white)]()
[![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)]()

<br>

[← Back to Portfolio Hub](../README.md)

<br>

</div>

---

## Overview

A rigorous **statistical examination of financial asset return distributions** applied to a multi-asset universe. The dominant assumption in classical portfolio theory, derivatives pricing, and risk management — that asset returns are independently and identically distributed according to a normal distribution — is tested directly and in depth. This project documents precisely how, by how much, and in what direction real return distributions deviate from normality, and draws out the practical consequences for risk measurement.

The analysis moves through four interconnected analytical stages: descriptive statistics and graphical distribution analysis; formal normality testing using the Jarque-Bera framework; rolling volatility estimation to reveal time-varying risk structure; and peak-to-trough drawdown profiling to capture worst-case loss experience in a way that variance alone cannot.

The findings carry real practical weight. **Gaussian-based Value-at-Risk (VaR)** models systematically underestimate tail losses when return distributions are leptokurtic and negatively skewed. **Volatility clustering** — large moves following large moves in persistent regimes — means risk is not constant and motivates the conditional variance models developed in Project 03. **Drawdown profiling** captures how painful a loss experience actually is: magnitude, duration, and time to recovery are all dimensions invisible to a standard deviation statistic.

**What this project demonstrates:**

- Why the normality assumption fails for financial returns and the direct consequences for risk management
- How to construct a complete, multi-dimensional statistical risk profile for any financial asset
- The empirical presence and magnitude of excess kurtosis, negative skewness, and tail risk across asset classes
- Volatility clustering and regime structure through rolling window analysis
- Historical worst-case loss experience — magnitude, duration, and recovery — through drawdown profiling

---

## 📄 PDF Portfolio Showcase

<div align="center">

### [`Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf`](./Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf)

*A complete, professional-quality presentation of this project — no code or Python environment required*

</div>

<br>

The PDF showcase is the recommended starting point for reviewers, recruiters, and professional contacts. It is a fully self-contained, print-ready document presenting every stage of the analysis — all statistical tests, every chart, the complete risk summary table, and written interpretation — without requiring Python, Jupyter, or any technical setup.

**Complete contents of the PDF:**

| # | Section | What Is Included |
|---|---------|-----------------|
| 1 | **Executive Summary** | Research motivation, asset universe, analytical scope, and key distributional findings across all assets |
| 2 | **The Non-Normality Problem** | Why the Gaussian assumption is embedded in classical finance theory, why it fails empirically, and the direct risk management consequences — illustrated with the contrast between Gaussian VaR and historical VaR |
| 3 | **Risk Summary Table** | Annualized return, annualized volatility, skewness, excess kurtosis, 5% historical VaR, and maximum drawdown — **fully populated for every asset in the universe** |
| 4 | **Return Distribution Charts** | One histogram panel per asset — empirical return distribution bars with fitted Gaussian curve overlaid, annotated directly with skewness coefficient, excess kurtosis, and Jarque-Bera p-value |
| 5 | **Jarque-Bera Test Results** | Formal normality test — test statistic and p-value per asset, with clear normality verdict; interpretation of what rejection means in practice |
| 6 | **Q-Q Normality Plots** | One Q-Q plot per asset — sorted empirical return quantiles plotted against theoretical normal quantiles, with 45° reference line; tail deviation and S-curve analysis |
| 7 | **Rolling Volatility Charts** | 21-day and 63-day annualized rolling volatility across the full sample; regime commentary identifying periods of persistently elevated and suppressed volatility |
| 8 | **Drawdown Profile Charts** | Drawdown curves per asset — percentage below running peak over the full sample; maximum drawdown level annotated with dashed reference line; recovery duration visible from chart geometry |
| 9 | **Implications for Practice** | What the combined distributional findings mean for portfolio construction, risk model choice, volatility forecasting, and position sizing in practice |

<br>

> **Tip for reviewers:** The PDF is entirely self-contained. Open it directly to evaluate this project without running any code.

---

## Table of Contents

- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Figures](#figures)
- [Data](#data)
- [Key Results](#key-results)
- [Theoretical Background](#theoretical-background)
- [Installation & Usage](#installation--usage)
- [Related Projects](#related-projects)

---

## Project Structure

```
02_asset_return_analysis/
│
├── 02_Financial_Asset_Return_Analysis.ipynb               ← Full reproducible analysis notebook
├── Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf ← ★ PDF Portfolio Showcase
│
├── figures/
│   ├── return_distribution.png    ← Return histograms with fitted Gaussian overlay (per asset)
│   ├── qq_plot_returns.png        ← Q-Q plots: empirical vs theoretical normal quantiles (per asset)
│   ├── rolling_volatility.png     ← 21-day and 63-day annualized rolling volatility (all assets)
│   └── drawdown_profile.png       ← Peak-to-trough drawdown curves, MDD annotated (per asset)
│
├── tables/
│   ├── returns_data.csv           ← Full daily log return series (date × asset)
│   └── risk_summary.csv           ← Complete risk statistics table (asset × metric)
│
├── requirements.txt
└── README.md
```

---

## Methodology

### Step 1 — Return Computation

Adjusted closing prices are sourced for all assets in the universe and **daily log returns** computed:

```
r_t = ln(P_t / P_{t-1})
```

Log returns are used throughout this project rather than simple arithmetic returns because they are time-additive (making multi-period aggregation correct by summation), are more symmetric and better approximate normality at short horizons, and are theoretically grounded in continuous compounding and geometric Brownian motion frameworks.

The full return series for all assets is stored in `tables/returns_data.csv` and is the single input to all subsequent analysis steps.

---

### Step 2 — Descriptive Statistics

A complete set of risk statistics is computed for each asset and assembled into `tables/risk_summary.csv`. This table is the core quantitative output of this project and is reproduced in full — with all values populated — in the PDF showcase.

| Statistic | Definition | Annualization |
|-----------|-----------|:-------------:|
| **Mean return** | Average daily log return | × 252 |
| **Volatility (σ)** | Standard deviation of daily log returns | × √252 |
| **Skewness** | Third standardized central moment | — |
| **Excess Kurtosis** | Fourth standardized central moment − 3 | — |
| **5% Historical VaR** | 5th percentile of the empirical return distribution | — |
| **Maximum Drawdown** | Largest peak-to-trough percentage loss over the full sample | — |

**Interpreting skewness:** Zero indicates perfect symmetry. Negative skewness — the typical signature of equity returns — means the left tail is heavier: extreme negative returns occur more frequently and with greater magnitude than extreme positive returns of the same probability. A portfolio of negatively skewed assets has more crash risk than symmetry-based risk measures imply.

**Interpreting excess kurtosis:** Zero corresponds to the normal distribution. Positive excess kurtosis (leptokurtosis) means fatter tails than Gaussian — extreme events of both signs are more common. Most equity return series exhibit excess kurtosis of 2 to 10, meaning the normal distribution dramatically underestimates the probability of large daily moves.

---

### Step 3 — Distribution Analysis & Normality Testing

**Graphical — Return Histograms:**
Return histograms are plotted for each asset with automatically calibrated bin widths. A fitted Gaussian curve — parameterized by the empirical mean and standard deviation of the return series — is overlaid on each panel. Departures between the bars and the curve directly reveal the nature and location of non-normality: sharper peaks (excess kurtosis), fatter tails, asymmetric shoulders (skewness).

**Graphical — Q-Q Plots:**
Quantile-Quantile plots provide a precise diagnostic of distributional shape. The sorted empirical return quantiles are plotted against the corresponding quantiles of a theoretical standard normal. If returns were exactly normally distributed, all points would fall on the 45° reference line. Departures follow characteristic patterns:

| Pattern | Meaning |
|---------|---------|
| **S-shaped curve** (points above line in right tail, below in left tail) | Fat tails — leptokurtosis |
| **Systematic upward bowing** | Positive skewness |
| **Systematic downward bowing** | Negative skewness |
| **Both S-shape and bowing** | The typical signature of equity returns — fat-tailed and negatively skewed simultaneously |

**Statistical — Jarque-Bera Test:**
The Jarque-Bera test provides a formal, quantitative test of the normality null hypothesis by jointly testing whether skewness and excess kurtosis are simultaneously zero:

$$JB = \frac{n}{6}\left[S^2 + \frac{(K-3)^2}{4}\right] \sim \chi^2(2) \quad \text{under } H_0$$

- **H₀:** Returns are normally distributed (S = 0, K − 3 = 0)
- **H₁:** Returns are not normally distributed

For financial return series with adequate sample size, normality is typically rejected at the 1% significance level for virtually all assets. Test statistics and p-values per asset are printed inline in the notebook and presented in a dedicated results table in the PDF showcase.

---

### Step 4 — Rolling Volatility Analysis

Volatility is not constant over time — a fact immediately apparent in any financial return series. The phenomenon of **volatility clustering** (Mandelbrot 1963; Engle 1982) describes how periods of large return magnitudes tend to cluster together, followed by quieter periods. Risk is persistent and regime-dependent.

Rolling standard deviation is computed over two window lengths:

| Window | Calendar Equivalent | Interpretation |
|--------|:-----------------:|----------------|
| **21-day** | ~1 calendar month | Reactive to recent shocks; captures short-term regime shifts and volatility spikes |
| **63-day** | ~1 calendar quarter | Smoother and slower-moving; highlights persistent medium-term volatility regimes |

Rolling volatility is annualized at each date: `σ_annual = σ_daily_rolling × √252`

Plotting both window lengths simultaneously reveals: (1) the visual structure of volatility clustering — extended calm periods punctuated by sharp spikes; (2) the trade-off between responsiveness and smoothness in risk estimation; (3) how quickly elevated volatility subsides following a shock. This evidence directly motivates the GARCH(1,1) conditional variance modelling in Project 03.

---

### Step 5 — Drawdown Profiling

The **drawdown** at time t measures the percentage decline from the most recent running historical peak:

$$D_t = \frac{P_t - \max_{s \leq t} P_s}{\max_{s \leq t} P_s}$$

The drawdown series is always non-positive (D_t ≤ 0) and equals zero precisely when the price is at a new all-time high. The **Maximum Drawdown (MDD)** is the single worst trough-to-peak loss over the full sample:

$$MDD = \min_{t \in [0,T]} D_t$$

Drawdown profiling captures three dimensions of loss experience that variance and VaR cannot fully express:

- **Magnitude** — how severe was the largest historical loss?
- **Duration** — how long did the asset remain below its prior peak?
- **Recovery time** — how long did it take to return to the prior peak after the trough?

Assets with nearly identical annualized standard deviations can have dramatically different drawdown profiles, making this a critical complementary risk measure alongside variance-based statistics.

---

## Figures

### `figures/return_distribution.png`

A grid of panels — one per asset in the universe. Each panel shows:
- **Histogram bars** representing the empirical frequency distribution of daily log returns
- **Fitted Gaussian curve** overlaid in a contrasting color, parameterized by the empirical mean and standard deviation
- **Annotations** for skewness coefficient, excess kurtosis, and Jarque-Bera p-value displayed directly on each panel

The gap between bars and normal curve in the tails is the most direct visual illustration of fat-tail risk. The asymmetry of the distribution reveals skewness. Panels use a consistent axis scale for cross-asset comparability.

---

### `figures/qq_plot_returns.png`

A grid of Q-Q plots — one per asset. Each panel shows:
- **Empirical quantile points** (sorted return data vs corresponding theoretical normal quantiles)
- **45° reference line** — perfect normality would place all points exactly on this line
- **Shaded confidence band** — the region where points would fall under normality with specified confidence
- **Tail deviations** — points pulling away from the reference line in both tails confirm fat-tailed, leptokurtic distributions; systematic asymmetric deviation reveals skewness

The characteristic S-shaped departure from the reference line — points above the line in the right tail and below in the left tail — is visible across all assets and is the signature of leptokurtosis.

---

### `figures/rolling_volatility.png`

A time series line chart displaying rolling annualized volatility across the full sample period for all assets:
- **Solid lines** — 21-day rolling volatility (short-term, reactive)
- **Dashed lines** — 63-day rolling volatility (medium-term, smoothed)
- **Color-coding** — one consistent color per asset
- **Volatility spikes** — sharp upward movements during identifiable market stress periods are visible as prominent peaks
- **Regime structure** — extended calm periods (flat, low-volatility sections) contrast with turbulent regimes (high, elevated sections)

This chart provides direct visual evidence for volatility clustering and the heteroskedasticity that motivates GARCH modelling in Project 03.

---

### `figures/drawdown_profile.png`

A time series line chart showing the drawdown series for each asset across the full sample:
- **Drawdown series** — solid line per asset showing the continuous percentage loss from the running peak (all values ≤ 0%)
- **Maximum drawdown level** — horizontal dashed reference line per asset, marking the single worst historical loss, labeled with the exact MDD percentage
- **Recovery dynamics** — the geometric shape of each trough region reveals how quickly the asset recovered to its prior peak; flat or slowly climbing trough floors indicate prolonged underwater periods
- **Cross-asset comparison** — different assets reaching similar MDD levels from different durations reveals qualitatively different loss structures despite similar headline risk numbers

---

## Data

| File | Format | Row Index | Columns | Description |
|------|--------|-----------|---------|-------------|
| `tables/returns_data.csv` | CSV | Trading date | Asset tickers | Daily log returns for all assets |
| `tables/risk_summary.csv` | CSV | Asset ticker | Risk metrics | Mean return, vol, skewness, kurtosis, 5% VaR, MDD per asset |

---

## Key Results

Full computed results are available in `tables/risk_summary.csv` after running the notebook, and are presented with all values populated in the **PDF Portfolio Showcase** without requiring any execution. The schema below shows the output structure:

| Asset | Ann. Return | Ann. Volatility | Skewness | Excess Kurtosis | 5% VaR (daily) | Max Drawdown |
|-------|:-----------:|:--------------:|:--------:|:--------------:|:--------------:|:------------:|
| Asset A | —% | —% | — | — | —% | —% |
| Asset B | —% | —% | — | — | —% | —% |
| ... | | | | | | |

**What to expect for typical equity return series:**

- Excess kurtosis of 2 to 8 — fat tails, more extreme daily moves than normality implies
- Negative skewness of −0.2 to −0.8 — heavier left tail; crash risk structurally exceeds equivalent upside
- Jarque-Bera p-value < 0.001 — normality rejected with very high confidence for all assets
- Volatility clustering clearly visible in all 21-day rolling windows
- Historical 5% VaR materially worse than what a Gaussian model would estimate at the same confidence level
- Maximum drawdown larger than the drawdown implied by a constant-volatility Gaussian process

---

## Theoretical Background

**Log Returns:**

$$r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)$$

**Skewness** — third standardized central moment, measures distributional asymmetry:

$$S = \frac{E\!\left[(r - \mu)^3\right]}{\sigma^3}$$

For a symmetric distribution S = 0. Negative S implies a longer, heavier left tail — the distribution generates larger losses than gains at the same probability level. Combined with leverage or concentrated positions, negative skewness materially increases the probability of severe loss.

**Excess Kurtosis** — fourth standardized moment minus 3, measures tail heaviness relative to the normal:

$$K - 3 = \frac{E\!\left[(r - \mu)^4\right]}{\sigma^4} - 3$$

The normal distribution has K − 3 = 0 by construction. Positive excess kurtosis (leptokurtosis) means more probability mass in the tails and the center than the normal, with less in the shoulders. Equity returns typically exhibit K − 3 ranging from 2 to 10.

**Jarque-Bera Test:**

$$JB = \frac{n}{6}\!\left[S^2 + \frac{(K-3)^2}{4}\right] \sim \chi^2(2) \;\; \text{under} \; H_0$$

Rejection of H₀ confirms the Gaussian model is misspecified. Under normality the test statistic follows a chi-squared distribution with 2 degrees of freedom; observed values for financial return series are typically orders of magnitude above the 1% critical value.

**Historical Value-at-Risk (5%):**
$$VaR_{5\%} = F^{-1}(0.05)$$

The 5th percentile of the empirical return distribution. Unlike parametric Gaussian VaR, historical VaR makes no distributional assumption and directly reflects fat-tail behavior present in observed data. The gap between historical VaR and Gaussian VaR is a direct measure of how much the normality assumption underestimates downside risk.

**Maximum Drawdown:**

$$MDD = \min_{t \in [0,T]} \frac{P_t - \max_{s \leq t} P_s}{\max_{s \leq t} P_s}$$

**Risk management implications:** Standard deviation-based risk measures systematically underestimate the frequency and magnitude of extreme losses for leptokurtic, negatively skewed return distributions. This project provides the empirical case for fat-tailed risk models and is the distributional foundation that motivates the GARCH conditional variance modelling in Project 03.

---

## Installation & Usage

```bash
# Navigate to this project from the repository root
cd 02_asset_return_analysis

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# Install all dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook 02_Financial_Asset_Return_Analysis.ipynb
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

Run all cells sequentially. The notebook will: download and process price data → compute log returns → calculate all risk statistics and export to `tables/risk_summary.csv` → generate and save all four figures to `figures/` → print all Jarque-Bera test results inline.

> **No code required.** Open [`Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf`](./Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf) for the complete results in a fully self-contained document.

---

## Related Projects

| Project | Relationship to This Work |
|---------|--------------------------|
| [01 — Efficient Frontier & Portfolio Optimization](../01_efficient_frontier/README.md) | Uses the covariance structure and expected return estimates documented here as inputs to portfolio construction; the correlation heatmap directly informs diversification decisions |
| [03 — Financial Econometrics & Time Series](../03_financial_econometrics/README.md) | Extends the rolling volatility evidence from this project with formal GARCH(1,1) conditional variance modelling — providing a rigorous framework for the volatility clustering observed here |

<br>

[← Back to Portfolio Hub](../README.md)
