# Kaggle Final Project

This repository holds an attempt to apply Random Forest classification to metastatic breast cancer diagnosis prediction using data from the WiDS Datathon 2024 Challenge #1 (https://www.kaggle.com/competitions/widsdatathon2024-challenge1).

## Overview

The task, is to predict whether a patient will receive a metastatic breast cancer diagnosis within 90 days of screening, using real-world healthcare data. The approach in this repository formulates the problem as a binary classification task, using a Random Forest classifier with tabular patient demographic, medical, and socioeconomic features as input. Our best model achieved an accuracy of 77.5% and a ROC-AUC score of 0.773 on the validation set.

## Summary of Workdone

### Data
- **Type:** Input: CSV file of patient features, Output: binary classification label (DiagPeriodL90D: 0 or 1)
- **Size:** 16.36 MB total
- **Instances:** 12,906 training samples, 1,936 validation samples, 1,936 test samples (from training split); 5,792 Kaggle test samples

### Preprocessing / Clean Up
- Dropped single-value columns: `patient_gender` and `metastatic_first_novel_treatment_type`
- Filled missing numerical values with the median
- Filled missing categorical values with 'Unknown'
- One-hot encoded all categorical features
- Aligned train and test columns after encoding

### Data Visualization
- Compared histograms of every numerical feature between Class 0 and Class 1
- Compared class proportions for every categorical feature in table format
- Notable finding: `breast_cancer_diagnosis_code` and `patient_state` showed the strongest variation between classes

## Problem Formulation
- **Input:** 292 features after cleaning and encoding
- **Output:** Binary label — 1 if diagnosed within 90 days, 0 otherwise
- **Model:** Random Forest Classifier (n_estimators=100, random_state=42)
- **No explicit loss function** — Random Forest uses Gini impurity for splitting

## Training
- Trained using scikit-learn on local CPU
- Training completed in under 2 minutes
- No training curves (Random Forest is not epoch-based)
- Used default hyperparameters as a baseline

## Performance Comparison

| Metric | Score |
|--------|-------|
| Accuracy | 0.775 |
| ROC-AUC | 0.773 |
| F1 (Class 0) | 0.67 |
| F1 (Class 1) | 0.83 |

ROC curve is included in the notebook.

## Conclusions
- Random Forest performed reasonably well on this tabular healthcare dataset
- Class imbalance (62.5% class 1 vs 37.5% class 0) affected recall for class 0
- `breast_cancer_diagnosis_code` and `patient_state` appear to be the most informative features

## Future Work
- Try XGBoost or LightGBM for potentially better performance
- Address class imbalance using SMOTE or class weights
- Perform feature selection to reduce dimensionality
- Tune hyperparameters using GridSearchCV

## How to Reproduce Results
1. Download data from https://www.kaggle.com/competitions/widsdatathon2024-challenge1/data
2. Place `training.csv.zip` and `test.csv.zip` in the project directory
3. Run the notebook `DATA 3402 FINAL PROJECT.ipynb` top to bottom
4. Submission file will be saved as `submission.csv`

## Overview of Files
- `DATA 3402 FINAL PROJECT.ipynb`: Main notebook containing all steps from data loading to submission
- `submission.csv`: Generated Kaggle submission file
- `sample_submission.csv`: Original sample submission from Kaggle

## Software Setup
Required packages:
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

## Citations
- WiDS Datathon 2024 Challenge #1: https://www.kaggle.com/competitions/widsdatathon2024-challenge1
- ChatGPT
- cLAUDE. ai 

