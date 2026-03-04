# Botnet Detection using Machine Learning

**Authors:** Timurmalik Djuraev (8562763) fileciteturn5file0  
**Topic:** Cybersecurity / Machine Learning (Supervised Classification)

## Overview
This project implements a **supervised ML pipeline** to detect **botnet traffic** from **network-flow telemetry**. Each network flow is represented by statistical features (duration, packet/byte counts, rates, etc.) and classified as:

- **0 — Normal traffic**
- **1 — Botnet / anomalous traffic** fileciteturn5file0

## Dataset
- CSV dataset derived from **CTU-13**, where each row represents a **bidirectional network flow** (e.g., CICFlowMeter-style features). fileciteturn5file0  
- After merging and minimal cleaning, the final dataset contains **18,443 flows** with a binary label column. fileciteturn5file0

## Method (Pipeline)
1. **Preprocessing**
   - Drop identifiers (IPs, ports, timestamps, flow IDs) to avoid environment-specific overfitting. fileciteturn5file0  
   - One-hot encode categorical features (if present). fileciteturn5file0  
   - Train/test split: `test_size=0.2`, `stratify=y`, `random_state=42`. fileciteturn5file0  
   - Standardization with `StandardScaler` fit on training data only. fileciteturn5file0

2. **Model**
   - **RandomForestClassifier** (100 estimators, `random_state=42`, `n_jobs=-1`, no fixed max depth). fileciteturn5file0

3. **Evaluation**
   - Accuracy, Precision, Recall, F1-score, Confusion Matrix. fileciteturn5file0  
   - **UMAP** visualization of high-dimensional feature space in 2D (`n_neighbors=15`, `min_dist=0.1`, `random_state=42`). fileciteturn5file0

## Results (from the report)
Confusion matrix (test set): fileciteturn5file0  
- TN: 10,646  
- FP: 17  
- FN: 12  
- TP: 7,768  

Metrics (approx.): fileciteturn5file0  
- Accuracy: ~99.84%  
- Precision (botnet): ~99.78%  
- Recall (botnet): ~99.85%  
- F1-score (botnet): ~99.81%

## Files
- `botnet_detection.ipynb` — the full pipeline (preprocessing → training → evaluation → plots). fileciteturn5file0  
- `CTU13_Attack_Traffic.csv` — botnet/malicious flows. fileciteturn5file0  
- `CTU13_Normal_Traffic.csv` — normal/benign flows. fileciteturn5file0  
- `docs/Botnet Detection using Machine Learning.docx` — report.

## Requirements
Python 3.x. Recommended packages: fileciteturn5file0  
- `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `umap-learn`

Install (example):
```bash
pip install pandas numpy scikit-learn matplotlib umap-learn
```

## How to run (Jupyter / Kernel)
Yes — `.ipynb` is opened in **Jupyter Notebook** or **JupyterLab** using a **Python kernel**.

1. Install Jupyter:
```bash
pip install jupyterlab
```
2. Start JupyterLab:
```bash
jupyter lab
```
3. Open `botnet_detection.ipynb`
4. Make sure CSV files are in the **same folder** (or update paths in the first cells). fileciteturn5file0  
5. Run cells **top-to-bottom**:
   - data load + preprocessing
   - train/test split + scaling
   - Random Forest training
   - evaluation metrics + confusion matrix + UMAP plot fileciteturn5file0

## Repository structure
```
.
├── botnet_detection.ipynb
├── CTU13_Attack_Traffic.csv
├── CTU13_Normal_Traffic.csv
├── docs/
│   └── Botnet Detection using Machine Learning.docx
└── README.md
```

## References (as used in the report)
- Egor Zakharenko (2024). Bagging and Random Forest… (Habr). fileciteturn5file0  
- Faisal Malik (2022). CTU13-CSV-Dataset (GitHub). fileciteturn5file0  
- scikit-learn documentation: RandomForest* API. fileciteturn5file0
