```markdown
# NeurIPS 2025 Open Polymer Prediction Challenge

This repo contains my solution for the **NeurIPS 2025 Open Polymer Prediction Kaggle Competition**.  

🏆 **Public LB wMAE:** `0.154`

---

## 🚀 Problem

Predict 5 polymer properties from SMILES strings:

- Tg
- FFV
- Tc
- Density
- Rg

---

## ✅ Approach

### RDKit Features

- Computed 12 RDKit descriptors:
  - MolWt, HeavyAtomCount, TPSA, MolLogP, NumRotatableBonds, FractionCSP3, RingCount, NHOHCount, NOCount, MaxPartialCharge, MinPartialCharge, LabuteASA
- Dropped `MaxPartialCharge` and `MinPartialCharge` due to missing values.

Saved as:
- `rdkit_train_features_clean.csv`
- `rdkit_test_features_clean.csv`

---

### Modeling

- Used **XGBoost regressors** (one per property)
- Handled missing values:
  - Fill NaNs in features with 0
  - Fill NaNs in targets with mean
- Competition metric:
```

Weighted MAE (wMAE) = (1/N) \* sum( MAE(y\_i) / count(y\_i) )

```
- Test predictions saved as `submission.csv`

---

## 🔧 How to Run

1. **Generate RDKit Features**

 Run:
```

RDKIT_Dataset_Creation.ipynb

```

2. **Upload Clean Features to Kaggle**

Upload CSVs as Kaggle Datasets and link them to your notebook.

3. **Train Model & Submit**

Run:
```

xgboost-for-polymer.ipynb

```

---

## 📁 Repo Structure

```

data/
train.csv
test.csv
rdkit\_train\_features\_clean.csv
rdkit\_test\_features\_clean.csv
notebooks/
01\_generate\_rdkit\_features.ipynb
02\_train\_xgboost\_model.ipynb
submission/
submission.csv

```

---

## 🙌 Acknowledgments

Thanks to the NeurIPS Polymer Challenge team and Kaggle community!

MIT License
```
