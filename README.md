# Clinical Decision Making & Pattern Recognition in Healthcare
### Cotiviti Intern Assessment — Topic 2

> **Focus:** Payment Integrity — Detecting Outlier Insurance Claims using Isolation Forest & SHAP Explainability

---

## Overview

This repository contains all deliverables for the Cotiviti Intern Assessment. The project tackles a real-world problem in healthcare payment integrity: identifying statistically anomalous insurance claims before they result in erroneous reimbursements — without requiring a single labeled fraud example.

The core insight driving this work is that a claim's dollar amount only becomes suspicious in context. A $15,000 billing is perfectly normal for a surgical procedure and deeply anomalous for a routine office visit. The system built here captures that context through engineered features, then uses Isolation Forest to surface outliers and SHAP to explain exactly why each one was flagged.

---

## Repository Structure

```
cotiviti-intern-assessment/
│
├── Cotiviti_Report_Humanized.docx     ← Written report (2 pages + bibliography)
├── outlier_claims_insurer.ipynb       ← Hackathon proof-of-concept notebook
├── Cotiviti_Presentation.pptx         ← PowerPoint slide deck (10 slides)
├── demo_recording.mp4                 ← Video presentation + POC screenshare
└── README.md                          ← This file
```

---

## Deliverable 1 — Written Report

**File:** `Cotiviti_Report_Humanized.docx`

A 2-page report covering:
- Topic definition — what Clinical Decision Making & Pattern Recognition means in practice, and where it creates value within the TPO framework
- Relevant trends — $300B annual fraud cost, DOJ enforcement activity, and the rise of Explainable AI
- Opportunities and threats — prepayment screening, insurer-level risk stratification, SHAP audit narratives, and the regulatory/adversarial risks
- Three strategic recommendations for Cotiviti — prepayment scoring layer, SHAP-driven audit report generation, and an insurer risk intelligence dashboard

Bibliography on page 3 in APA format with 6 cited sources.

---

## Deliverable 2 — Hackathon Proof of Concept

**File:** `outlier_claims_insurer.ipynb`

### What it does

An end-to-end anomaly detection pipeline built in Jupyter Notebook that loads a real healthcare dataset, engineers contextual billing features, trains an Isolation Forest model, explains the results with SHAP, and visualizes findings through interactive Plotly charts.

### Dataset

[Kaggle Healthcare Dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset) by prasad22 — ~10,000 synthetic patient admission records covering billing amounts, medical conditions, insurance providers, admission types, medications, and hospital stay durations.

Downloaded automatically via `kagglehub` on first run.

### Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `scikit-learn` | Isolation Forest anomaly detection, feature scaling |
| `shap` | Model explainability — feature importance and waterfall plots |
| `plotly` | Interactive visualizations |
| `kagglehub` | Dataset download |

### Setup & Running

**Prerequisites:** Python 3.8+, Jupyter Notebook or JupyterLab, Kaggle account

**1. Clone the repository**
```bash
git clone https://github.com/[your-username]/cotiviti-intern-assessment.git
cd cotiviti-intern-assessment
```

**2. Install dependencies**
```bash
pip install kagglehub pandas numpy scikit-learn shap plotly ipywidgets jupyter
```

**3. Set up Kaggle credentials**

Log into [kaggle.com](https://www.kaggle.com) → Account → API → Create New Token. This downloads a `kaggle.json` file. Place it at:
- Mac/Linux: `~/.kaggle/kaggle.json`
- Windows: `C:\Users\[username]\.kaggle\kaggle.json`

**4. Launch the notebook**
```bash
jupyter notebook outlier_claims_insurer.ipynb
```

**5. Run all cells top to bottom** — the dataset downloads automatically on Cell 2.

### Notebook Structure

| Cell | What it does |
|---|---|
| Cell 1 | Package installation check |
| Cell 2 | Load Kaggle dataset via `kagglehub` |
| Cell 3 | Exploratory data analysis — shape, stats, insurer breakdown |
| Cell 4 | Feature engineering — billing z-score, insurer ratio, length of stay |
| Cell 5 | Isolation Forest — fit, predict, anomaly scoring |
| Cell 6 | Plotly scatter — billing vs z-score, normal vs anomalous |
| Cell 7 | Audit table — top 20 most anomalous claims |
| Cell 8 | SHAP explainability — feature importance + waterfall chart |
| Cell 9 | Summary statistics |
| Cells 10–14 | Add-ons — heatmap, time-series, financial impact, deep-dive |
| Final cell | Combined summary dashboard — all findings in one chart |

### Key Design Decisions

**Why Isolation Forest?** Healthcare fraud labels are rare, heavily lagged, and represent only confirmed cases. Isolation Forest is unsupervised — it learns the statistical shape of normal claims and flags anything that deviates, with no fraud labels required.

**Why feature engineering matters more than model choice?** A raw billing amount is a weak signal. A billing z-score — how many standard deviations a claim sits from the average for that specific insurer-condition combination — is a strong one. The most important work in this project was building those contextual features, not tuning the model.

**Why SHAP?** A flag with no explanation creates more work, not less. SHAP values show exactly which features drove each anomaly score, transforming a black-box alert into an auditable finding a reviewer can act on immediately.

---

## Deliverable 3 — Slide Presentation

**File:** `Cotiviti_Presentation.pptx`

10-slide PowerPoint deck covering:

| Slide | Content |
|---|---|
| 1 | Title slide |
| 2 | Agenda |
| 3 | Topic definition — TPO framework and project focus |
| 4 | Relevant trends — 3 stat callouts ($300B, $2.9B, XAI) |
| 5 | POC methodology — 4-step pipeline |
| 6 | Key findings — anomaly counts, insurer bar chart, financial impact |
| 7 | Opportunities and threats |
| 8 | Three strategic recommendations for Cotiviti |
| 9 | POC demo preview — notebook cell walkthrough |
| 10 | Conclusion |

Full presenter script is embedded in Speaker Notes on every slide. Open in PowerPoint → View → Presenter View to access during recording or live presentation.

---

## Deliverable 4 — Video Recording

**File:** `demo_recording.mp4`

Recorded presentation covering:
- Slide deck walkthrough using the PowerPoint above
- Live screenshare of the Jupyter notebook with cells running
- Summary dashboard demonstration

---

## Topic Context

This project sits within **Topic 2 — Clinical Decision Making and Pattern Recognition in Healthcare**, specifically the **Payment** lane of Cotiviti's TPO framework.

Healthcare fraud, waste, and abuse costs the U.S. system an estimated $300 billion annually (FBI, 2024). Traditional detection relies on rule-based systems and post-payment audits — both reactive by design and easily gamed. This POC demonstrates that an unsupervised ML approach can identify statistically anomalous claims in real time, with SHAP-powered explanations that make every flag actionable and auditable without requiring prior fraud examples.

---

## References

- Department of Justice. (2024). *False Claims Act settlements exceed $2.9 billion in FY2023.* https://www.justice.gov/opa/pr/false-claims-act-settlements-and-judgments-exceed-29-billion-fiscal-year-2023
- Federal Bureau of Investigation. (2024). *Health care fraud.* https://www.fbi.gov/investigate/white-collar-crime/health-care-fraud
- Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). Isolation Forest. *Proceedings of the 2008 IEEE International Conference on Data Mining*, 413–422. https://doi.org/10.1109/ICDM.2008.17
- Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. *Advances in Neural Information Processing Systems, 30.* https://arxiv.org/abs/1705.07874
- Prasad, P. (2023). *Healthcare dataset* [Data set]. Kaggle. https://www.kaggle.com/datasets/prasad22/healthcare-dataset
- Shafqat, W., Byun, Y.-C., & Shafqat, S. (2020). Unsupervised machine learning approaches for anomaly detection in healthcare claims data. *Healthcare, 8*(4), 404. https://doi.org/10.3390/healthcare8040404

---

*Submitted to Cotiviti — jesus.hurtado@cotiviti.com*
