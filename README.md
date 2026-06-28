# Clinical and Treatment Predictors of Survival in Breast Cancer
### Time-to-Event Analysis Using The Cancer Genome Atlas (TCGA-BRCA)

**Authors:** Abby Chen, Abdelrahman Badawy, Lindsey Kwon, Tara Allred  
**Course:** Data Science — University of Utah  
**Dataset:** [TCGA Breast Invasive Carcinoma (BRCA)](https://www.cancer.gov/ccg/research/genome-sequencing/tcga)

---

## Overview

This project applies survival analysis methods to TCGA clinical and treatment data for 1,095 breast cancer patients. Using Kaplan–Meier estimation and Cox proportional hazards regression, we identify the strongest independent predictors of patient survival and stratify patients into clinically meaningful risk groups.

---

## Key Findings

- **Tumor stage** is the dominant predictor of survival. Stage IV patients have >8× the mortality hazard of Stage I patients (HR = 8.25, p < 0.001).
- **Drug therapy** is significantly associated with reduced mortality risk (HR = 0.42, 95% CI: 0.25–0.71), with a more pronounced benefit in early-stage disease.
- **Age at diagnosis** contributes a modest but significant effect (~3% increase in hazard per year, HR = 1.03, p < 0.001).
- **HER2 status** shows significant survival differences; ER and PR effects are attenuated after adjusting for stage and treatment.
- The final multivariable Cox model achieves a **concordance index of 0.76** and effectively stratifies patients into high- and low-risk groups (log-rank p < 0.001).

---

## Repository Structure

| File | Description |
|------|-------------|
| `Data_Processing_and_EDA.ipynb` | Data cleaning, integration, and exploratory analysis |
| `Modeling_Script.ipynb` | Kaplan–Meier, Cox models, and risk stratification |
| `analysis_ready_complete.csv` | Preprocessed patient-level dataset (1,095 patients, 51 features) |
| `README.md` | Project overview and documentation |
---

## Methods

| Step | Details |
|------|---------|
| **Data integration** | Merged clinical, follow-up, radiation, and drug treatment datasets using patient barcode |
| **Preprocessing** | Median imputation for numerics, "Unknown" category for categoricals, missingness indicators, one-hot encoding |
| **Survival outcome** | Time to death or last follow-up; 12.8% event rate (140 deaths / 955 censored) |
| **EDA** | Distribution analysis, Cramér's V for categorical associations, Spearman correlation, VIF for multicollinearity |
| **Survival modeling** | Kaplan–Meier curves, log-rank tests, univariable and multivariable Cox PH models |
| **Risk stratification** | Patients classified into high/low risk based on predicted Cox hazard scores |

---

## Data Source

Raw data from the [TCGA BRCA cohort](https://portal.gdc.cancer.gov/) (public access).  
Four files used: clinical patient data, follow-up records, radiation treatment data, and drug treatment data.

---

## Requirements

```bash
pip install pandas numpy matplotlib seaborn lifelines scikit-learn statsmodels
```

The primary survival modeling library is [`lifelines`](https://lifelines.readthedocs.io/).

---

## Limitations
- Observational data — treatment assignment is not randomized, so associations between drug therapy and survival should not be interpreted causally.
- Demographic imbalance (69% White) limits generalizability to underrepresented populations.
- Biomarker data contains substantial missingness, handled via imputation and missingness indicators.
