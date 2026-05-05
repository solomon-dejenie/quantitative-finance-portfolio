# 📈 Efficient Frontier Portfolio Optimization

📄 [View Executive Report](./Efficient_Frontier_Portfolio_Optimization_Showcase.pdf)

## 📓 View Notebook

👉 [Open Notebook on GitHub](./01_Efficient_Frontier_Portfolio_Optimization.ipynb)

---

## 🎯 Objective

Develop an optimal portfolio allocation strategy that maximizes return for a given level of risk using Modern Portfolio Theory.

---

## 🧠 Approach

- Computed log returns from asset prices  
- Estimated expected returns and covariance matrix  
- Simulated portfolios via Monte Carlo  
- Identified:
  - Minimum variance portfolio  
  - Maximum Sharpe ratio portfolio  

---

## 📊 Results

- Generated Efficient Frontier curve  
- Demonstrated diversification reduces risk  
- Identified optimal asset allocation  

---

## 📉 Visual Evidence

- Efficient Frontier → `figures/efficient_frontier.png`  
- Cumulative Returns → `figures/cumulative_returns.png`  
- Correlation Heatmap → `figures/correlation_heatmap.png`  

---

## ⚙️ Methods

- Mean-Variance Optimization  
- Sharpe Ratio Maximization  
- Portfolio Simulation  

---

## 🚀 Reproducibility

```bash
pip install -r requirements.txt
## Run:

01_Efficient_Frontier_Portfolio_Optimization.ipynb
## Insight

Portfolio performance depends heavily on correlation structure, not just individual asset returns.
