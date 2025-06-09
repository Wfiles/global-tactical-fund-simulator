# global-tactical-fund-simulator

# 📈 International Portfolio Diversification and Dynamic Asset Allocation  


## 📂 Project Structure

This repository contains:
- `report.pdf` — Main report (max. 10 pages excluding tables/figures) detailing methodology, results, and justifications.
- `main.py` or `notebook.ipynb` — Executable Python code to reproduce all results.
- `/data` — Folder containing all downloaded and preprocessed datasets.
- `/figures` — All plots and tables used in the report (optional, can be generated via code).

---

## 📋 Project Objectives

The main objective is to construct, analyze, and optimize an international investment portfolio by:

1. Quantifying the benefits of international equity and currency diversification.
2. Constructing various dynamic strategies (momentum, reversal, carry, dollar).
3. Evaluating performance improvements over a benchmark diversification strategy.
4. Analyzing the performance of a combined strategy through both statistical and asset pricing models.

---

## 🔍 Sections Overview

### 1. Data Acquisition
- Monthly stock returns (2002–2024) for:
  - Australia, France, Germany, Japan, Switzerland, UK, and US (CRSP value-weighted index)
- Exchange rates vs. USD for: AUD, EUR, JPY, CHF, GBP
- 3-month interbank rates and 1-month T-Bill rates from FRED

### 2. International Diversification Strategy (DIV)
- Compute USD returns (hedged and unhedged)
- Evaluate equal-weighted, risk-parity, and mean-variance portfolios
- Define DIV as the currency-hedged, risk-parity portfolio

### 3. Dynamic Strategies
- **Momentum (MOM)**: Based on 11-month past returns
- **Reversal (REV)**: Based on 5-year lagged return
- **Currency Carry (CARRY)**: Based on interest rate differential
- **Dollar (DOLLAR)**: Short equal-weighted foreign currencies vs. USD

For each:
- Construct long-short portfolio
- Compute risk-return metrics and test significance
- Run OLS regression against DIV strategy

### 4. Optimal Fund Allocation (STRAT)
- Construct a baseline fund using T-Bill + DIV (target annual vol = 15%)
- Combine MOM, REV, CARRY, DOLLAR overlays using:
  - Risk parity
  - Mean-variance optimization
- Solve for optimal `b` and `c` in:  
  `R_FUND = R_TBill + b * (R_DIV - R_TBill) + c * R_STRAT`

### 5. Performance Attribution
- Regress fund return on Fama-French 5 factors
- Interpret explanatory power, α, β coefficients, and R²
- Discuss in light of EMH, CAPM, APT

---

## 🛠️ Dependencies

Install required Python packages:

```bash
pip install numpy pandas matplotlib scipy statsmodels yfinance fredapi
```

Access to WRDS and FRED is required for full data retrieval.

---

## 🚀 How to Run

1. Download and place all required data files in the `/data` folder
2. Run `main.py` or open `notebook.ipynb`
3. Generated figures and tables will appear in `/figures`
4. The report can be reproduced from these outputs

---

## ⚠️ Notes

- All results must be fully reproducible via the code
- All numerical and graphical results must be explained in the report
- Code must be written in Python

---

