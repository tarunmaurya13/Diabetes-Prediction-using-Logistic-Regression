# Diabetes-Prediction-using-Logistic-Regression
A binary classifier that predicts whether a patient has diabetes based on 8 routine clinical measurements (Glucose, BMI, Blood Pressure, Age, etc.), trained on the Pima Indians Diabetes dataset (768 patients).

Why This Project

Early diabetes detection from routine clinical data is a well-established healthcare
ML problem, chosen to demonstrate an end-to-end pipeline that handles:


Missing values disguised as zeros (a common real-world data quality issue)
Class imbalance (fewer diabetic than non-diabetic cases)
Evaluation beyond accuracy — precision, recall, ROC-AUC, and cross-validation,
since a medical use case needs more than a single number to be trustworthy


Dataset


Source: Pima Indians Diabetes dataset
Rows: 768 patients
Features: Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI,
DiabetesPedigreeFunction, Age
Target: Outcome (0 = Non-Diabetic, 1 = Diabetic)


Approach

StepWhat was done1. EDACorrelation heatmap, distribution plots for all features2. Data CleaningBiologically impossible zeros (e.g., 0 blood pressure) replaced with column median/mean3. Outlier HandlingIQR-based filtering, plus a 95th-percentile cap on Insulin4. Feature ScalingStandardScaler applied to all features5. Class ImbalanceSMOTE oversampling applied to the training set6. ModelingLogistic Regression7. Validation5-fold stratified cross-validation (ROC-AUC)8. EvaluationAccuracy, ROC-AUC, confusion matrix, precision/recall

Results


Test Accuracy: 74.8%
Test ROC-AUC: 0.851
Cross-validated ROC-AUC (5-fold): 0.846 (mean), range 0.819–0.911 across folds
Diabetic-class recall: 0.72 — prioritized over raw accuracy, since missing a
true diabetic case (false negative) is costlier than a false alarm in this context


Known Limitations / Next Steps


Data leakage: Imputation (median/mean fill) and StandardScaler are currently
fit on the full dataset before the train/test split, which can make test-set
performance slightly optimistic. Fix: split first, fit only on training data,
then transform the test set.
Outlier filtering bug: The per-column IQR loop overwrites its filter mask each
iteration, so in practice only the last column's bounds are applied. A combined
filter across all columns is too aggressive for this dataset size (drops ~50% of
rows) — capping/winsorizing extreme values is a better fix than dropping rows.
No baseline comparison: Only Logistic Regression was tried; a Random Forest or
similar benchmark would confirm the linear model is a deliberate choice, not a
default one.


Requirements

pandas
numpy
matplotlib
seaborn
scikit-learn
imbalanced-learn

How to Run


Place diabetes.csv in the same directory as the notebook (update the file path
in the first cell if needed)
Install dependencies: pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
Run all cells in order
