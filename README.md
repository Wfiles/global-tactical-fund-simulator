# 🌐 Global Tactical Fund Simulator

> **International Portfolio Diversification & Dynamic Asset Allocation**
>
> Reproducible research code & data for constructing and evaluating an international multi‑asset fund that targets **15 % annual volatility** while combining **diversification** and **tactical overlays** (momentum, reversal, carry & dollar).

---

## 📑 Table of Contents

1. [Project Overview](#project-overview)
2. [Quick Start](#quick-start)
3. [Project Structure](#project-structure)
4. [Research Objectives](#research-objectives)
5. [Data Sources](#data-sources)
6. [Methodology Summary](#methodology-summary)
7. [Reproducing the Results](#reproducing-the-results)
8. [Dependencies](#dependencies)
9. [Citation](#citation)
10. [License](#license)
11. [Disclaimer](#disclaimer)

---

## Project Overview

This repository accompanies the **FIN‑405 – Investments** group project (Spring 2025, EPFL). It demonstrates how a U.S.‑based investor can:

* **Quantify** the benefits of international equity & currency diversification.
* **Design** dynamic long–short overlay strategies driven by well‑documented risk premia (momentum, long‑term reversal, currency carry, dollar factor).
* **Blend** the base diversification portfolio with tactical overlays to reach a target risk level and maximise the **risk‑adjusted return**.
* **Benchmark** the resulting fund against classic factor models (CAPM, Fama–French 5) and evaluate statistical significance.

All results reported in the companion paper `project_report.pdf` are fully reproducible from this repository.

---

## Quick Start

```bash
# 1. Clone the repo
$ git clone https://github.com/<user>/global-tactical-fund-simulator.git
$ cd global-tactical-fund-simulator

# 2. Create & activate a dedicated environment (conda example)
$ conda create -n envi python=3.12.8 -y
$ conda activate envi

# 3. Install required packages
$ pip install -r requirements.txt

# 4. Fetch / place the raw data into the data/ folder (see below)

# 5. Run the notebook to reproduce every figure & table
$ jupyter notebook project.ipynb
```

> **Note:** Access to **WRDS** (World Indices) and **FRED** (macro rates & FX) is necessary for the automated data‑download cells. If you do not have active credentials, place the pre‑downloaded CSV files in the `/data` directory instead.

---

## Project Structure

```
├── project_report.pdf   # 10‑page academic report
├── project.ipynb        # Executable notebook (analysis & visualisations)
├── requirements.txt     # Precise Python dependencies
├── /data/               # Raw datasets (CSV)
├── /pdf/               # Key academic references in PDF format
└── README.md            # You are here
```

---

## Research Objectives

1. **International Diversification**
   Construct equal‑weight, risk‑parity & mean‑variance portfolios across seven developed equity markets (2002‑04 → 2024‑12). Evaluate both **unhedged** and **currency‑hedged** USD returns.
2. **Dynamic Overlay Strategies**
   Implement and back‑test:

   * **Momentum (MOM)** – 11‑month look‑back minus 1‑month skip.
   * **Reversal (REV)** – 5‑year lagged performance.
   * **Currency Carry (CARRY)** – 3‑month interest‑rate differential.
   * **Dollar (DOLLAR)** – Long USD vs. equally‑weighted foreign FX basket.
3. **Optimal Fund Allocation**
   Combine a **T‑Bill + Diversification (DIV)** core with the overlay composite (STRAT) to maintain 15 % annualised volatility using risk‑parity **and** mean‑variance optimisation.
4. **Performance Attribution**
   Diagnose alpha & betas via OLS on the Fama–French 5 factors; discuss consistency with EMH, CAPM & APT.

---

## Data Sources

| Asset Class     | Provider                         | Series                                                                       |
| --------------- | -------------------------------- | ---------------------------------------------------------------------------- |
| Equity Indices  | **WRDS – Monthly World Indices** | Australia, France, Germany, Japan, Switzerland, UK, US (CRSP value‑weighted) |
| Risk‑Free Rates | **WRDS** & **FRED**              | 1‑month T‑Bill (US), 3‑month interbank rates (AUD, EUR, JPY, CHF, GBP)       |
| FX Rates        | **FRED**                         | AUD/USD, EUR/USD, JPY/USD, CHF/USD, GBP/USD                                  |

All time series are aligned to **month‑end** and span **April 2002 – December 2024**.

---

## Methodology Summary

<details>
<summary>Click to expand</summary>

* **Returns in USD:** Convert local equity returns via spot FX; compute hedged returns using the covered‑interest‑parity framework.
* **Risk‑Parity:** 60‑month rolling volatility estimates to derive weights.
* **Mean‑Variance:** 60‑month rolling µ and Σ; γ = 1.
* **Overlay Signals:** Cross‑sectional ranking; dollar‑neutral long–short construction with scaling `Z` ensuring +1 / −1 notionals.
* **Fund Optimisation:** Solve for weights `b` and `c` in $R_{FUND}=R_{TBill}+b(R_{DIV}-R_{TBill})+c R_{STRAT}$ s.t. annual σ ≈ 15 %.
* **Statistical Tests:** Sharpe ratios, t‑tests on mean returns, regression alphas/betas.

</details>

---

## Reproducing the Results

| Step                                 | Output                                                                            |
| ------------------------------------ | --------------------------------------------------------------------------------- |
| **Run all cells** in `project.ipynb` | Cleans data, builds strategies, saves intermediate artefacts to `/data/processed` |



---

## Dependencies

* Python ≥ 3.12.8
* Core: `numpy`, `pandas`, `scipy`, `statsmodels`, `matplotlib`, `seaborn`, `jupyter`
* Optional: `ipykernel`, `tqdm`, `pyarrow`

Install everything via:

```bash
pip install -r requirements.txt
```

---

## Citation

If you build upon this work, please cite the accompanying report:

```text
Jallot, W., Abbassi, N., Le Dur, A., & Simonnet, L. (2025). International Portfolio Diversification and Dynamic Asset Allocation. FIN‑405 Investments Project, EPFL.
```

---

## License

Distributed under the **MIT License**. See `LICENSE` for details.

---

## Disclaimer

This repository is for **academic & educational purposes only**. It does **not** constitute financial advice or an offer to invest. Past performance is not indicative of future results. Use at your own risk.
