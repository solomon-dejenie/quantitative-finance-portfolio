# 📊 Quantitative Finance Portfolio

> A curated collection of three end-to-end quantitative finance projects covering portfolio optimization, return analysis, and financial econometrics — built with Python, grounded in theory, and designed for professional presentation.

---

## 🗂️ Repository Structure

```
quantitative-finance-portfolio/
├── README.md                          ← You are here (Hub)
├── LICENSE
│
├── 01_efficient_frontier/             ← Project 1: Portfolio Optimization
│   ├── 01_Efficient_Frontier_Portfolio_Optimization.ipynb
│   ├── Efficient_Frontier_Portfolio_Optimization_Showcase.pdf
│   ├── figures/
│   ├── tables/
│   ├── outputs/
│   ├── requirements.txt
│   └── README.md
│
├── 02_asset_return_analysis/          ← Project 2: Return Analysis
│   ├── 02_Financial_Asset_Return_Analysis.ipynb
│   ├── Financial_Asset_Return_Analysis_Portfolio_Showcase.pdf
│   ├── figures/
│   ├── tables/
│   ├── requirements.txt
│   └── README.md
│
└── 03_financial_econometrics/         ← Project 3: Econometrics & Time Series
    ├── 03_Financial_Econometrics_TimeSeries.ipynb
    ├── Financial_Econometrics_TimeSeries_Portfolio_Showcase.pdf
    ├── figures/
    ├── tables/
    ├── outputs/
    ├── requirements.txt
    └── README.md
```

---

## 🚀 Projects at a Glance

### [📈 01 — Efficient Frontier & Portfolio Optimization](./01_efficient_frontier/README.md)

Constructs the Markowitz efficient frontier for a multi-asset portfolio using Monte Carlo simulation and analytical optimization. Identifies the **Minimum Variance Portfolio** and the **Maximum Sharpe Ratio Portfolio**, with full covariance decomposition and cumulative return backtesting.

**Key techniques:** Mean-variance optimization · Monte Carlo simulation · Sharpe ratio maximization · Correlation heatmaps

---

### [📉 02 — Financial Asset Return Analysis](./02_asset_return_analysis/README.md)

A deep-dive statistical study of asset return distributions across multiple securities. Examines normality assumptions, tail risk, and time-varying volatility through rolling window analysis and drawdown profiling.

**Key techniques:** Return distribution analysis · Q-Q plots · Rolling volatility · Maximum drawdown · Risk summary statistics

---

### [🔬 03 — Financial Econometrics & Time Series](./03_financial_econometrics/README.md)

Applies formal econometric methods to financial time series — including stationarity testing, ARIMA forecasting, and GARCH volatility modelling. Model performance is evaluated with RMSE benchmarks and diagnostic residual analysis.

**Key techniques:** ADF stationarity tests · ARIMA/SARIMA modelling · GARCH(1,1) · Volatility forecasting · RMSE evaluation

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.10+ | Core language |
| NumPy / Pandas | Data manipulation & matrix algebra |
| SciPy / statsmodels | Optimization & econometric modelling |
| arch | GARCH volatility models |
| Matplotlib / Seaborn | Visualization |
| Jupyter Notebook | Interactive analysis & reporting |

---

## ⚡ Getting Started

Each project is self-contained with its own `requirements.txt`. To run any project:

```bash
# Clone the repository
git clone https://github.com/your-username/quantitative-finance-portfolio.git
cd quantitative-finance-portfolio

# Navigate to a project
cd 01_efficient_frontier

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

---

## 📄 License

This repository is licensed under the terms of the [LICENSE](./LICENSE) file.

---

## 👤 Author

**Your Name**
Quantitative Finance | Data Science | Financial Modelling

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/your-profile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/your-username)

---

*Each project folder contains a standalone README with methodology details, visual outputs, and interpretation of results.*

