# NeurIPS 2025 Open Polymer Prediction Challenge

This repository contains my solution for the **NeurIPS 2025 Open Polymer Prediction Kaggle Competition**.  

🏆 **Public LB wMAE:** `0.154`

---

## 🚀 Problem

The goal is to predict 5 polymer properties from molecular structures (SMILES):

- Tg
- FFV
- Tc
- Density
- Rg

These properties are critical for designing polymers with desired characteristics.

---

## ✅ Approach

### RDKit Feature Engineering

- Extracted 12 molecular descriptors from SMILES:
  - MolWt, HeavyAtomCount, TPSA, MolLogP, NumRotatableBonds, FractionCSP3, RingCount, NHOHCount, NOCount, MaxPartialCharge, MinPartialCharge, LabuteASA
- Dropped `MaxPartialCharge` and `MinPartialCharge` due to excessive missing values.
- Saved computed features into CSV files for Kaggle usage.

---

### Modeling

- Used separate **XGBoost regressors** for each target property.
- Handled missing values:
  - Filled missing feature values with 0.
  - Filled missing target values with the mean.
- Evaluated with the competition metric:

    ```
    Weighted MAE (wMAE) = (1/N) * sum_i( MAE(target_i) / count(target_i) )
    ```

- Prepared final submission in required Kaggle format:
    - CSV file with columns: id, Tg, FFV, Tc, Density, Rg

---

## 🔧 How to Run

### 1. Generate RDKit Features

Run:

notebooks/RDKIT_Dataset_Creation.ipynb


This generates:

- `data/rdkit_train_features_clean.csv`
- `data/rdkit_test_features_clean.csv`

Upload these CSVs to Kaggle as datasets (because the competition notebook cannot use internet).

---

### 2. Train Models & Create Submission

Run:

notebooks/xgboost-for-polymer.ipynb


Outputs:

- `submission/submission.csv`

---

## 📁 Project Structure

data/
train.csv
test.csv
rdkit_train_features_clean.csv
rdkit_test_features_clean.csv

notebooks/
01_generate_rdkit_features.ipynb
02_train_xgboost_model.ipynb

submission/
submission.csv

README.md


---

## 🙌 Acknowledgments

Thanks to the NeurIPS Polymer Challenge team and the Kaggle community!
