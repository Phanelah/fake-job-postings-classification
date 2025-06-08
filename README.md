# Fake Job Postings Detection Project

## Overview

This project aims to detect **fraudulent job postings** using classical machine learning techniques combined with strategic feature engineering. By analyzing job descriptions, metadata, and categorical signals, we trained a classification model capable of identifying suspicious listings with high accuracy.

---

## Business Objective

Fake job listings are a growing concern on job platforms, wasting time and exposing users to scams.  
**Our goal**: Build a model that helps **automate the detection of fraudulent job postings**, aiding human moderators and reducing risk on job boards.

---

## Dataset

- Source: [Kaggle - Fake Job Postings Dataset](https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction)
- Target variable: `fraudulent`  
- Key features used:
  - `title`, `company_profile`, `description`, `requirements`, `benefits`
  - `telecommuting`, `has_company_logo`, `has_questions`
  - Custom features like:
    - Word counts
    - Suspicious keyword flags

---

## Project Structure
```
fake-job-detection-project/
│
├── README.md
├── index_cleaned.ipynb # Final cleaned notebook with modeling
├── final_job_postings_encoded.csv
│
├── data/
│ └── processed/ # Final balanced and encoded datasets
├── models/
│ └── final_random_forest.pkl
├── reports/
│ ├── presentation.pdf # Non-technical summary slides
│ └── crisp_dm.md # CRISP-DM breakdown
└── visuals/
├── confusion_matrix.png
├── roc_curve.png
└── feature_importance.png

```
---

## Modeling Approach

We followed the **CRISP-DM** process with these major steps:

1. **Exploratory Data Analysis (EDA)**  
2. **Feature Engineering**: Word counts, keyword flags, binary transforms  
3. **Balancing the Data**: Used **SMOTE** to handle class imbalance  
4. **Modeling**: Final model = `RandomForestClassifier` with `class_weight='balanced'`  
5. **Evaluation**: ROC-AUC, Precision, Recall, F1-Score

---

##  Results

| Metric        | Value |
|---------------|--------|
| Accuracy      | ~96% |
| ROC-AUC Score | 0.96 |
| Recall (Fraud)| ~73% |
| Precision (Fraud)| ~46% |

*Model was able to identify a majority of fraudulent listings with strong performance on real listings.*

---

## Key Visualizations

- ✅ Confusion Matrix  
- ✅ ROC Curve  
- ✅ Top 10 Important Features (from Random Forest)  
- ✅ Class Distribution Before vs. After SMOTE  

---

## Business Impact

This model can help:
- Flag fake job postings for manual review
- Improve trust in job platforms
- Reduce time spent moderating listings manually

---

## Future Improvements

- Apply NLP techniques (TF-IDF, BERT)
- Build a browser plugin or API-based flagging tool
- Real-time moderation using this trained model

---

## Author

**Aluoch Phanela**  
[Your GitHub Profile]  
Presented as part of the final phase 3 project at **Moringa School**



