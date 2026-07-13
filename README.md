<div align="center">

<!-- Animated Typing Header -->
<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=32&pause=1000&color=1DB954&center=true&vCenter=true&multiline=true&width=900&height=100&lines=%F0%9F%A9%BA+Diabetes+Prediction;Logistic+Regression+%2B+SMOTE+%2B+Cross-Validation" alt="Typing SVG" /></a>

<br/>

<!-- Animated Wave Banner -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:0f2e1f,100:1db954&height=200&section=header&text=Diabetes%20Risk%20Classifier&fontSize=42&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Binary%20Classification%20on%20Routine%20Clinical%20Measurements&descSize=16&descAlignY=55&descColor=7ee8a0" width="100%"/>

![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-Model-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data-150458?style=for-the-badge&logo=pandas&logoColor=white)
![SMOTE](https://img.shields.io/badge/SMOTE-Imbalance%20Handling-9146FF?style=for-the-badge)
![ROC AUC](https://img.shields.io/badge/ROC--AUC-0.851-1DB954?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Documented%20Limitations-yellow?style=for-the-badge)

</div>

---

## 📌 Overview

A binary classifier that predicts whether a patient has diabetes based on **8 routine clinical measurements** — Glucose, BMI, Blood Pressure, Age, and more — trained on the classic **Pima Indians Diabetes dataset** (768 patients).

### Why This Project

Early diabetes detection from routine clinical data is a well-established healthcare ML problem, chosen deliberately to demonstrate an end-to-end pipeline that handles the things that actually make medical ML hard:

- 🔍 **Missing values disguised as zeros** — a common, easy-to-miss real-world data quality issue
- ⚖️ **Class imbalance** — meaningfully fewer diabetic than non-diabetic cases
- 📊 **Evaluation beyond accuracy** — precision, recall, ROC-AUC, and cross-validation, since a medical use case needs more than a single number to be trustworthy

---

## 🗂️ Dataset

| Property | Details |
|---|---|
| **Source** | Pima Indians Diabetes Dataset |
| **Rows** | 768 patients |
| **Features** | Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age |
| **Target** | `Outcome` (0 = Non-Diabetic, 1 = Diabetic) |

---

## 🔬 Pipeline

| Step | What Was Done |
|---|---|
| **1. EDA** | Correlation heatmap, distribution plots for all features |
| **2. Data Cleaning** | Biologically impossible zeros (e.g. 0 blood pressure) replaced with column median/mean |
| **3. Outlier Handling** | IQR-based filtering, plus a 95th-percentile cap on Insulin |
| **4. Feature Scaling** | `StandardScaler` applied to all features |
| **5. Class Imbalance** | SMOTE oversampling applied to the training set |
| **6. Modeling** | Logistic Regression |
| **7. Validation** | 5-fold stratified cross-validation (ROC-AUC) |
| **8. Evaluation** | Accuracy, ROC-AUC, confusion matrix, precision/recall |

---

## 📈 Results

<div align="center">

| Metric | Score |
|---|---|
| **Test Accuracy** | 74.8% |
| **Test ROC-AUC** | 0.851 |
| **Cross-Validated ROC-AUC (5-fold)** | 0.846 mean (range: 0.819 – 0.911) |
| **Diabetic-Class Recall** | 0.72 |

</div>

> **Recall was prioritized over raw accuracy** — in a medical screening context, missing a true diabetic case (false negative) is costlier than a false alarm (false positive). A false alarm means an extra test; a missed case means a missed diagnosis.

---

## ⚠️ Known Limitations / Next Steps

Documented honestly, not glossed over — these are real, specific issues found during review, along with the fix for each:

| Issue | Impact | Fix |
|---|---|---|
| **Data leakage** | Imputation (median/mean fill) and `StandardScaler` are currently fit on the *full* dataset before the train/test split — this can make test-set performance slightly optimistic | Split first, fit preprocessing only on training data, then transform the test set |
| **Outlier filtering bug** | The per-column IQR loop overwrites its filter mask each iteration, so in practice only the last column's bounds are applied. A properly combined filter across all columns is too aggressive for this dataset size (drops ~50% of rows) | Cap/winsorize extreme values instead of dropping rows |
| **No baseline comparison** | Only Logistic Regression was tried — without a benchmark, it's unclear if the linear model was a deliberate choice or a default one | Add a Random Forest or Gradient Boosting comparison to confirm the linear model holds up |

---

## 🛠️ Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
imbalanced-learn
```

---

## 🚀 How to Run

1. Place `diabetes.csv` in the same directory as the notebook (update the file path in the first cell if needed)
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
   ```
3. Run all cells in order

---

## 👤 Author

<div align="center">

**Tarun Maurya**
Final-year BCA (Artificial Intelligence), Invertis University
[GitHub](https://github.com/tarunmaurya13) · tarunmaurya016@gmail.com

</div>
