# Predicting Swedish Trotter Yearling Auction Prices Using Machine Learning

**Master's Thesis** | International University of Applied Sciences] | 2026 
**Author:** Runar Skjærpe  


---

## Overview

This repository contains all code, data, and documentation for my master's thesis investigating the use of machine learning to predict hammer prices of Swedish Standardbred (trotter) yearlings at auction. Five models are developed and compared: Linear Regression, Generalised Additive Model (GAM), Random Forest, XGBoost, and a Bayesian Hierarchical Model (BHM).


---

## Repository Structure

```
Master_Theses/
│
├── README.md
│
├── data/
│   ├── raw/
│   │   └── auction_catalogues/
│   │       ├── Aby_YS_23.pdf
│   │       ├── Elitauktionen 2024.pdf
│   │       ├── MOS_2023_Enkel.pdf
│   │       ├── Solvalla_CS_23.pdf
│   │       ├── Solvalla_CS_24.pdf
│   │       └── Solvalla_CS_25.pdf
│   ├── processed/
│   │   └── Yearlingauctiondata.xlsx
│   └── predictions/
│       ├── BHM_horse_predictions.xlsx
│       ├── GAM_2025_PREDICTIONS.xlsx
│       ├── LINEAR_REGRESSION_2025.xlsx
│       ├── XGB_Predictions_2025.xlsx
│       └── rf_tuned_predictions.xlsx
│
├── notebooks/
│   ├── 01_data_extraction/
│   │   ├── Solvalla_CS_2024.ipynb
│   │   └── ÅBY_YS_2024_4.ipynb
│   ├── 02_eda/
│   │   └── EDA and Correlation_Analysis.ipynb
│   └── 03_modelling/
│       ├── Linear_regression_horse_prices.ipynb
│       ├── GAM_horse_prices.ipynb
│       ├── RandomForest_horse_prices.ipynb
│       ├── XGBoost_horse_prices.ipynb
│       └── BHM_horse_prices.ipynb
│
└── scripts/
    └── parsing/
        ├── horse_pedigree_parser.html
        └── BLodbank_scraper.ipynb
```

---

## Data

### Auction Catalogues

Raw PDF catalogues from Swedish yearling sales covering 2023–2025:

| File | Auction | Year |
|---|---|---|
| `Aby_YS_23.pdf` | Åby Yearling Sale | 2023 |
| `Solvalla_CS_23.pdf` | Solvalla Criterium Sale | 2023 |
| `Solvalla_CS_24.pdf` | Solvalla  Criterium Sale | 2024 |
| `Elitauktionen 2024.pdf` | Elitauktionen | 2024 |
| `MOS_2023_Enkel.pdf` | MOS Enkel | 2023 |
| `Solvalla_CS_25.pdf` | Solvalla  Criterium Sale | 2025 |

Catalogue data was extracted using a combination of manual parsing and LLM-assisted structured extraction. See `scripts/parsing/` for the tools used.

### Processed Dataset

`Yearlingauctiondata.xlsx` — the final modelling dataset containing features per yearling including pedigree, earnings, BLUP scores, stud fees, and auction metadata.


### Target Variable

Hammer price in SEK, log-transformed during modelling. 

### Train/Test Split

- **Training:** Auction years 2023–2024 (GroupKFold cross-validation grouped by year)
- **Test set:** 2025 auction cohort


---

## Models

| Model | Notebook | Key Library |
|---|---|---|
| Linear Regression | `Linear_regression_horse_prices.ipynb` | scikit-learn |
| GAM | `GAM_horse_prices.ipynb` | pyGAM |
| Random Forest | `RandomForest_horse_prices.ipynb` | scikit-learn |
| XGBoost | `XGBoost_horse_prices.ipynb` | xgboost |
| Bayesian Hierarchical | `BHM_horse_prices.ipynb` | PyMC |

All models use a consistent preprocessing pipeline including median imputation for missing numeric features and informative missingness flags where appropriate. Tree-based models use MAE as the loss function.

---


---

## Requirements

Key dependencies:

```
numpy
pandas
scikit-learn
pygam
xgboost
pymc
arviz
shap
matplotlib
seaborn
openpyxl
```

Python version: **3.10+**

---

## Notes on Data Availability

The processed dataset `Yearlingauctiondata.xlsx` is provided to allow full replication of the modelling pipeline




