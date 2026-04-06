# Individual Homework 3 — Disparate Impact Audit

**Dataset:** COMPAS (Correctional Offender Management Profiling for Alternative Sanctions)

---

## Overview

This project performs a full disparate impact audit on a logistic regression model
trained to predict two-year recidivism risk using the cleaned ProPublica COMPAS dataset.

The audit examines whether the model produces discriminatory outcomes across **race** and
**sex**, using a combination of the `solas-ai` Python library and manual statistical methods.

---

## Assignment Tasks

| # | Task | Methods Used |
|---|------|-------------|
| 1 | Compute AIR, ME, and SMD for race and sex separately | `solas-ai`, manual verification |
| 2 | Intersectional analysis (race × sex) — report worst-group AIR | Cross-tabulation |
| 3 | Compute FPR and FNR disparities by race; test statistical significance | Two-proportion z-test |
| 4 | Publication-quality grouped bar chart of FPR and FNR by race | `matplotlib` |
| 5 | 300-word compliance memo to a hypothetical regulator | Written analysis |

---

## Key Metrics:

| Metric | Definition |
|--------|-----------|
| **AIR** | Adverse Impact Ratio — selection rate of group ÷ selection rate of reference group. Fails the 4/5ths rule if < 0.80 |
| **ME** | Marginal Effect — absolute difference in selection rates between group and reference group |
| **SMD** | Standardized Mean Difference (Cohen's d) — effect size on continuous risk score |
| **FPR** | False Positive Rate — % of non-recidivists incorrectly flagged as high-risk |
| **FNR** | False Negative Rate — % of actual recidivists incorrectly flagged as low-risk |


| Package | Purpose |
|---------|---------|
| `pandas`, `numpy` | Data manipulation |
| `scikit-learn` | Logistic regression model |
| `solas-ai` | Fairness metrics (AIR, ME, SMD) |
| `statsmodels` | Two-proportion z-tests |
| `matplotlib` | Publication-quality figures |
| `scipy` | Statistical utilities |

---

## How to Run

1. Open **Google Colab** 
2. Create a new notebook and paste each cell block from the homework script in order
3. Run all cells top to bottom (`Runtime → Run all`)
4. The COMPAS dataset is loaded automatically from the ProPublica GitHub URL. No file upload needed
5. The bar chart is saved as `fpr_fnr_by_race.png` in the working directory


---

## Key Findings Summary

- **Race (AIR):** African-American defendants receive high-risk classifications at a rate
  that falls below the 4/5ths rule threshold relative to Caucasian defendants, indicating
  statistically significant adverse impact.
- **Sex (AIR):** Female defendants are classified as high-risk at a lower rate than males.
- **Intersectional:** The worst subgroup (race × sex) faces compounded disparity that would
  be invisible in a single-axis analysis.
- **FPR:** African-American non-recidivists are flagged as high-risk at a significantly
  higher rate than Caucasian non-recidivists (p < 0.05, two-proportion z-test).
- **FNR:** Runs in the opposite direction — Caucasian recidivists are more often
  under-predicted — consistent with prior ProPublica reporting.


---

## AI Acknowledgement

For this assignment, Claude (Anthropic) was used to help structure the Python code for
computing fairness metrics, running statistical tests, and generating the publication-quality
figure. The AI assisted with code organization and error handling. All analytical
interpretations, the compliance memo, and final review of results are my own work.
