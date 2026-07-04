# Clinical Decision Making & Pattern Recognition in Healthcare
### Cotiviti Intern Assessment — Topic 2

> **Focus:** Payment Integrity — Detecting Outlier Insurance Claims using Isolation Forest & SHAP Explainability

---

## Overview

This repository contains all deliverables for the Cotiviti Intern Assessment. The project addresses a core challenge in healthcare payment integrity: identifying statistically anomalous insurance claims before they result in erroneous reimbursements — without requiring labeled fraud examples.

The central insight is that a claim's dollar value is only meaningful in context. A billing of $15,000 is routine for a surgical procedure and anomalous for a routine consultation. The system captures that context through engineered features, applies Isolation Forest to surface outliers, and uses SHAP to explain why each claim was flagged — producing findings that are both actionable and auditable.

---

## Repository Structure

```
cotiviti-intern-assessment/
│
├── Cotiviti_Report.pdf                ← Written report (2 pages + APA bibliography)
├── outlier_claims_insurer.ipynb       ← Hackathon proof-of-concept notebook
├── Cotiviti_Presentation.pptx         ← Slide deck with embedded presenter script
├── demo_recording.mp4                 ← Video presentation and POC screenshare
└── README.md
```

---

## Deliverables

### Written Report
`Cotiviti_Report_Humanized.docx`

A 2-page analytical report defining the topic, analyzing relevant industry trends, identifying opportunities and threats, and proposing three strategic recommendations for Cotiviti. APA-formatted bibliography included on page 3.

---

### Proof of Concept
`outlier_claims_insurer.ipynb`

An end-to-end anomaly detection pipeline built in Jupyter Notebook. The notebook loads a real healthcare dataset, engineers contextual billing features, trains an Isolation Forest model, generates SHAP explanations for each flagged claim, and produces interactive Plotly visualizations.

**Dataset:** [Kaggle Healthcare Dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset) — ~10,000 synthetic patient admission records. Downloaded automatically via `kagglehub` on first run.

**Tech Stack**

| Library | Purpose |
|---|---|
| `scikit-learn` | Isolation Forest anomaly detection and feature scaling |
| `shap` | Model explainability — feature importance and per-claim waterfall plots |
| `plotly` | Interactive visualizations |
| `pandas` / `numpy` | Data manipulation and feature engineering |
| `kagglehub` | Automated dataset download |

**Setup**

```bash
# 1. Clone the repository
git clone https://github.com/[your-username]/cotiviti-intern-assessment.git
cd cotiviti-intern-assessment

# 2. Install dependencies
pip install kagglehub pandas numpy scikit-learn shap plotly ipywidgets jupyter

# 3. Configure Kaggle credentials
# Download kaggle.json from kaggle.com → Account → API → Create New Token
# Place at ~/.kaggle/kaggle.json (Mac/Linux) or C:\Users\[username]\.kaggle\kaggle.json (Windows)

# 4. Launch the notebook
jupyter notebook outlier_claims_insurer.ipynb
```

Run all cells top to bottom. The dataset downloads automatically on the first run.

**Design Rationale**

*Why Isolation Forest?* Confirmed fraud labels in healthcare are rare and heavily lagged. Isolation Forest is unsupervised — it learns the statistical distribution of normal claims and flags deviations without requiring prior examples of fraud.

*Why feature engineering over model tuning?* Raw billing amounts are a weak signal. A billing z-score — measuring deviation from the mean for a specific insurer-condition combination — provides the contextual signal the model needs. The most consequential decisions in this project were in feature construction, not hyperparameter selection.

*Why SHAP?* A flag without an explanation creates more work for reviewers, not less. SHAP values quantify exactly which features drove each anomaly score, turning a black-box alert into a documented audit finding.

---

### Slide Presentation
`Cotiviti_Presentation.pptx`

A 10-slide deck providing an overview of the report findings and POC demonstration. A full presenter script is embedded in the Speaker Notes of every slide. Open in PowerPoint → View → Presenter View to access.

---

### Video Recording
`demo_recording.mp4`

A recorded walkthrough of the slide deck and live POC screenshare, presented on camera.

---

## Key Findings

- Approximately **5% of claims** were flagged as anomalous, consistent with realistic healthcare fraud prevalence estimates of 3–10%
- Anomaly rates were **not uniform across insurers** — certain payer-condition combinations carried significantly higher risk, indicating that blanket review thresholds systematically underperform targeted stratification
- **Billing z-score** (contextual deviation from insurer-condition norms) was the top SHAP driver, validating the feature engineering approach over raw dollar thresholds

---

## References

- Department of Justice. (2024). *False Claims Act settlements exceed $2.9 billion in FY2023.* https://www.justice.gov/opa/pr/false-claims-act-settlements-and-judgments-exceed-29-billion-fiscal-year-2023
- Federal Bureau of Investigation. (2024). *Health care fraud.* https://www.fbi.gov/investigate/white-collar-crime/health-care-fraud
- Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). Isolation Forest. *Proceedings of the 2008 IEEE ICDM* (pp. 413–422). https://doi.org/10.1109/ICDM.2008.17
- Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. *Advances in Neural Information Processing Systems, 30.* https://arxiv.org/abs/1705.07874
- Prasad, P. (2023). *Healthcare dataset* [Data set]. Kaggle. https://www.kaggle.com/datasets/prasad22/healthcare-dataset
- Shafqat, W., Byun, Y.-C., & Shafqat, S. (2020). Unsupervised ML approaches for anomaly detection in healthcare claims. *Healthcare, 8*(4), 404. https://doi.org/10.3390/healthcare8040404

