# cybersecurity_attacks
# Cybersecurity Attacks ML Project
# Cybersecurity Attacks ML Project

## 🚀 Overview
This project builds and compares seven supervised classifiers to predict whether a given network event will trigger a security action (block/log/ignore). It demonstrates an end-to-end ML pipeline—from raw data exploration and preprocessing, through model training and hyperparameter tuning, to evaluation and visualization.

---

## 📊 Dataset
- Name: Cybersecurity Attacks Dataset  
- Source: Incribo’s synthetic dataset on Kaggle  
- Link: https://www.kaggle.com/datasets/incribo/cybersecurity-attacks  
- Samples: 40,000  
- Features: Originally 25 mixed numerical & categorical; ~15 used after dropping non-informative columns  
- Target: Action Taken (0 = No Action, 1 = Action Taken)

---

## 🛠 Key Steps

### 1. Data Exploration (EDA)
- Distributions: Attack types by year/month/day of week  
- Device/OS breakdown: Windows vs. Linux vs. macOS vs. mobile  
- Correlations: Feature heatmap to spot collinear numerical fields  

### 2. Preprocessing
- Impute missing values in:  
  - Alerts/Warnings → "None"  
  - IDS/IPS Alerts → "No Data"  
  - Malware Indicators → "No Detection"  
  - Firewall Logs → "No Data"  
  - Proxy Information → "No Proxy Data"  
- Drop timestamps, IPs, raw payload text, geo-logs, proxies, firewall/IDS log columns  
- Label-encode all remaining categoricals  
- Train/test split: 80/20 stratified on the target  
- Resample: SMOTE to balance the minority class in training set  
- Scale: StandardScaler on all numeric features

### 3. Modeling
We train, tune (where appropriate), and save predictions for:
1. Artificial Neural Network (ANN)
2. Support Vector Machine (SVM)  
3. Naive Bayes (GaussianNB)  
4. K-Nearest Neighbors (KNN)  
5. Decision Tree  
6. Random Forest  
7. Logistic Regression  

> Each script under src/ outputs:
> - predictions_<MODEL>_model.csv  
> - A saved confusion-matrix plot in figures/

### 4. Hyperparameter Tuning
- SVM: RandomizedSearchCV over C, gamma, kernel  
- Random Forest: RandomizedSearchCV over n_estimators, max_depth, etc.  
- KNN: Grid search for optimal n_neighbors  
- ANN: Tuning number of hidden layers, units, and learning rate via simple cross-val

### 5. Evaluation
- Primary metric: Accuracy  
- Secondary metrics: Precision, Recall, F1-score  
- Best model: Random Forest (~ 65% accuracy)  
- Worst model: Naive Bayes (~ 48% accuracy)  

---

## 📈 Visualization
- EDA plots: histograms, countplots, correlation heatmaps  
- Model results:  
  - Distribution of Predictions (annotated bar charts)  
  - Confusion Matrices (heatmaps)  
  - Accuracy Comparison (grouped bar chart)  

All figures live in figures/ for easy report inclusion.

---

## 💾 Results & Structure

```text
├── data/
│   ├── raw/                       ← original CSV
│   ├── preprocessed/              ← X.csv, Y.csv, X_test.csv, Y_test.csv
│   └── results/                   ← predictions_<MODEL>_model.csv
├── src/
│   ├── preprocess.py              ← data cleaning & feature engineering
│   ├── train_*.py                 ← one per model
│   └── tune_*.py                  ← hyperparameter scripts
├── figures/                       ← all PNG plots
├── README.md
└── requirements.txt
