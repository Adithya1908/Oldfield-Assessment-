# Post-Trade Performance Analysis
**Historical Trade Performance Review | 556 Completed Trades | 2005–2025**

---

## What You Will Find Here

In this report, you will find a comprehensive post-trade performance analysis using Jupyter Notebook, Python, and statistical methods to answer the question:

> ***What drove trade performance across 556 historical trades, and which fundamental factors best predict success?***

The analysis covers 54 sectors and 40+ countries over 2005–2025, examining sector allocation, geographic exposure, temporal cycles, and company fundamentals (valuation, growth, profitability) at the time of purchase.

---

## How I Approached The Question

**Objective:** Identify performance drivers across Oldfield's historical trade book and develop actionable, statistically grounded recommendations for improving future trade selection.

**Methodology:**
1. Load and clean the raw trade dataset (556 trades), removing 29 Error-classified observations.
2. Aggregate sector-level performance and test significance using one-sample t-tests.
3. Map Bloomberg country codes to regions and test geographic differences using ANOVA and Mann-Whitney U.
4. Construct rolling 1-year performance curves and detect outperformance/underperformance regimes.
5. Screen 11 candidate fundamental metrics for multicollinearity using Variance Inflation Factors (VIF).
6. Fit a logistic regression (HC3 robust SEs) on VIF-cleaned features to identify the top predictive factors.
7. Visualise all findings in 4 charts following JP Morgan *Guide to the Markets* formatting.

**Key Analyses:**
- **Sector Alpha** (Chart 1): Top 10 vs Bottom 10 sectors by mean annualised relative return
- **Performance Cycles** (Chart 2): Rolling 1-year returns with regime detection (2005–2025)
- **Geographic Decomposition** (Chart 3): Regional alpha with ANOVA and Mann-Whitney U tests
- **Multi-Factor Model** (Chart 4): Logistic regression marginal effects across valuation, growth, and profitability

---

## Requirements

To reproduce this analysis, you will need:
- **Python 3.12+** with Jupyter Notebook or JupyterLab installed
- **`Raw data set (2).xlsx`** — the source data file must be placed in the **same folder** as the notebook. The code reads from a relative path, so no file path editing is needed
- **`requirements.txt`** — included in the submission. Run `pip install -r requirements.txt` before launching the notebook to install all dependencies with pinned versions

Once the above are in place, open the notebook and run all cells top-to-bottom. The first cell automatically verifies that the data file exists and that all dependencies are installed.

---

## Libraries Imported

| # | Library | Purpose |
|---|---------|---------|
| 1 | `pandas` | Clean, transform, and analyse the trade dataset |
| 2 | `numpy` | Numerical computation, array operations, missing value handling |
| 3 | `matplotlib` | Static visualisations with precise layout control |
| 4 | `seaborn` | Additional plotting utilities and colour palette support |
| 5 | `scipy.stats` | Hypothesis testing — t-tests, Pearson correlation, ANOVA, Mann-Whitney U |
| 6 | `scipy.interpolate` | Cubic spline smoothing of the temporal performance curve |
| 7 | `statsmodels` | Logistic regression with HC3 robust SEs, marginal effects, Wald tests |
| 8 | `statsmodels.stats` | Variance Inflation Factor (VIF) multicollinearity diagnostics |
| 9 | `sklearn.preprocessing` | StandardScaler to z-score features before regression |

---

## Files In This Repository

| File | Description |
|------|-------------|
| `oldfield_revised_code.ipynb` | Main Jupyter Notebook containing all analysis code |
| `Raw data set (2).xlsx` | Source dataset (556 trades — place in same folder as notebook) |
| `requirements.txt` | Pinned dependency versions for exact reproducibility |
| `Post_Trade_Analysis_Report.pdf` | Written report addressing all assessment questions |
| `sector_performance_institutional.png` | Chart 1: Sector alpha |
| `performance_cycles_schroder_style.png` | Chart 2: Temporal performance cycles |
| `geographic_performance_institutional.png` | Chart 3: Geographic alpha decomposition |
| `chart4_multifactor_institutional.png` | Chart 4: Multi-factor marginal effects |

---

## Jupyter Notebook To Reference For Code

To refer to the analysis code, refer to the following notebook:
1. **Jupyter Notebook For Post-Trade Analysis** → `./oldfield_revised_code.ipynb`

---

## Key Statistical Methods Used

| Method | Where Used | Purpose |
|--------|-----------|---------|
| One-sample t-test | Sectors, Regions | Test if mean alpha differs from zero |
| One-way ANOVA | Regions | Test joint equality of regional means |
| Mann-Whitney U | Regions | Non-parametric distributional comparison |
| Pearson correlation | Sectors | Trade frequency vs performance relationship |
| VIF screening | Multi-factor | Remove multicollinear features before regression |
| Logistic regression (HC3) | Multi-factor | Model P(Hit) as function of standardised fundamentals |
| Wald test | Multi-factor | Joint significance of variable categories |
| Avg. marginal effects | Multi-factor | Translate log-odds into probability changes |

---

## Notes

- All analysis is point-in-time at purchase to avoid look-ahead bias
- The multi-factor model uses 159 of 527 trades due to missing fundamental data across all metrics
- VIF screening removed P/B Ratio (VIF = 15.1) and ROIC (VIF = 6.3) before the regression was fitted
- Significance is assessed at the 5% level throughout, with 10% flagged where relevant
- Use of AI tools was employed as appropriate for code generation and analytical support
