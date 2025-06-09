# Fake Job Postings Detection Project

## Overview

This project aims to detect **fraudulent job postings** using classical machine learning techniques combined with strategic feature engineering. By analyzing job descriptions, metadata, and categorical signals, we trained a classification model capable of identifying suspicious listings with high accuracy.

---

## Problem Statement

Fake job postings waste time, scam applicants, and damage the credibility of job platforms. The goal is to detect fraudulent job listings using available features such as description, location, telecommuting flag, and more.

---

## Business Objective

Fake job listings are a growing concern on job platforms, wasting time and exposing users to scams.  
**Our goal**: Build a model that helps **automate the detection of fraudulent job postings**, aiding human moderators and reducing risk on job boards.

---

## Data Understanding

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

 ![image](https://github.com/user-attachments/assets/4ea2de65-baa0-4386-bb5a-3b85d6e086a6)

This helps us understand relationships between features and can guide feature selection for modeling.

2. **Feature Engineering**: Word counts, keyword flags, binary transforms

![image](https://github.com/user-attachments/assets/1f4d686b-4527-4108-817a-162246f3d377)

The initial Random Forest model identified several features as highly predictive of fraudulent job postings

3. **Balancing the Data**: Used **SMOTE** to handle class imbalance

4. **Modeling**: Final model = `RandomForestClassifier` with `class_weight='balanced'`

![image](https://github.com/user-attachments/assets/f63d5727-faba-499b-96fb-5cc409e03e71)

This shows how our fraud detection model assigns fraud probability scores to new job posts, and how these scores can guide automated moderation decisions.

5. **Evaluation**: ROC-AUC, Precision, Recall, F1-Score

 ![image](https://github.com/user-attachments/assets/8a743625-ea48-4b6b-8f6a-1ef192c0ea89)

To evaluate model performance, we trained and compared multiple classifiers, including Logistic Regression and Random Forest, using ROC curves and AUC scores. The ROC curve helps us understand how well each model distinguishes between fraudulent and legitimate job postings by plotting the trade-off between the true positive rate and false positive rate.

 ![image](https://github.com/user-attachments/assets/db2ce745-53fb-45d7-a695-4199ae525d87)

To understand which model performs better, we compared key metrics like precision, recall, and F1-score side by side. This helps identify which model balances identifying fraudulent jobs without misclassifying legitimate ones.

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

## Key Insights

1. **Content Signals Are Strong Predictors**
   - Features like `description_word_count`, use of certain keywords (e.g., "urgent", "click here"), and vague job titles were strong indicators of fraud.

2. **Class Imbalance Required Special Handling**
   - Without resampling (e.g., SMOTE), models failed to identify fraudulent listings.
   Applying SMOTE significantly improved recall and helped balance precision.

3. **Best Performing Model: Random Forest (with SMOTE)**
   - Precision: ~50%
   - Recall: ~70–75%
   - ROC AUC: ~0.95  
   - This model strikes a balance between identifying fraud and minimizing false alarms.

---

## **Recommendations**

1. **Integrate Model into Moderation Workflow**
   - Auto-approve job posts with predicted fraud probability < 0.3.
   - Flag posts with probability > 0.7 for human review.
   - Queue medium-risk posts (0.3–0.7) for further inspection.

2. **Establish Continuous Feedback & Retraining**
   - Use moderator decisions to relabel borderline cases.
   Retrain the model regularly (e.g., monthly or after 1,000 new posts) to ensure optimal performance.

3. **Enhance Feature Set**
   - Add TF-IDF features or keyword frequency vectors.
   - Explore integrating external metadata (e.g., domain age, geolocation, company reputation).

---

## Business Impact

This model can help:
- Flag fake job postings for manual review
- Improve trust in job platforms
- Reduce time spent moderating listings manually

---

## Future Improvements

1. **Optimize Thresholds**
   - Conduct a precision–recall analysis to fine-tune the classification thresholds based on business risk tolerance.

2. **Deploy Controlled Pilot (A/B Test)**
   - Deploy the model to a subset of new job postings and measure reduction in fraud, false positives, and moderator time saved.

3. **Add Explainability Tools**
   - Use SHAP values or feature importances to show why a job was flagged, helping moderators make informed decisions.

4. **Explore Advanced Models**
   - Test XGBoost, LightGBM, or even simple NLP transformer models (e.g., DistilBERT) for further gains in accuracy and robustness.

---

## Author

By automating early fraud detection and refining human moderation through model insights, the stakeholders can drastically reduce risk on the platform and improve user trust and operational efficiency.
**Aluoch Phanela**    
Presented as part of the final phase 3 project at **Moringa School**



