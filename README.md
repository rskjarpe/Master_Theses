# Predicting Swedish Trotter Yearling Auction Prices Using Machine Learning
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
        └── horse_pedigree_parser.html
```

---

## Data

### Auction Catalogues

Raw PDF catalogues from five Swedish yearling sales covering 2023–2025:

| File | Auction | Year |
|---|---|---|
| `Aby_YS_23.pdf` | Åby Yearling Sale | 2023 |
| `Solvalla_CS_23.pdf` | Solvalla Crème de la Crème | 2023 |
| `Solvalla_CS_24.pdf` | Solvalla Crème de la Crème | 2024 |
| `Elitauktionen 2024.pdf` | Elitauktionen | 2024 |
| `MOS_2023_Enkel.pdf` | MOS Enkel | 2023 |
| `Solvalla_CS_25.pdf` | Solvalla Crème de la Crème | 2025 |

Catalogue data was extracted using a combination of manual parsing and LLM-assisted structured extraction via `scripts/parsing/horse_pedigree_parser.html`.

### Processed Dataset

`Yearlingauctiondata.xlsx` — the final modelling dataset 

### Key Features

- `log_stud_fee` — log-transformed sire stud fee (dominant predictor)
- Sire and dam sire BLUP breeding values
- Dam's best race time and career earnings
- Full and half-sibling earnings
- Breeder (smoothed leave-one-out target encoded)
- Auction type indicators and year fixed effects
- Inbreeding coefficient

### Target Variable

Hammer price in SEK, log-transformed during modelling. Back-transformation applies a bias correction (σ²/2 adjustment).

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

## Reproducing the Results

### 1. Environment Setup

```bash
git clone https://github.com/rskjarpe/Master_Theses.git
cd Master_Theses
pip install -r requirements.txt
```

### 2. Run Notebooks in Order

```
notebooks/02_eda/EDA and Correlation_Analysis.ipynb   ← Exploratory analysis
notebooks/03_modelling/Linear_regression_horse_prices.ipynb
notebooks/03_modelling/GAM_horse_prices.ipynb
notebooks/03_modelling/RandomForest_horse_prices.ipynb
notebooks/03_modelling/XGBoost_horse_prices.ipynb
notebooks/03_modelling/BHM_horse_prices.ipynb
```

> The processed dataset (`data/processed/Yearlingauctiondata.xlsx`) is included, so modelling notebooks can be run directly without re-running data extraction.

### 3. LLM-Assisted Parsing

Auction catalogue HTML pages were processed using `scripts/parsing/horse_pedigree_parser.html` in combination with Claude.ai for structured data extraction. This step is documented for transparency and reproducibility but is not required to run the models.

---

## Results Summary

*(To be completed — placeholder for final thesis results)*

| Model | OOF MAE (SEK) | OOF R² | Test MAE (SEK) | Test R² |
|---|---|---|---|---|
| Linear Regression | | | | |
| GAM | | | | |
| Random Forest | | | | |
| XGBoost | | | | |
| Bayesian Hierarchical | | | | |

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

Raw auction catalogues are included where redistribution is permissible. The processed dataset `Yearlingauctiondata.xlsx` is provided to allow full replication of the modelling pipeline regardless of catalogue availability.

---

## Citation

If you use this code or dataset, please cite:

```
Skjærpe, R. (2025). Predicting Swedish Trotter Yearling Auction Prices Using Machine Learning.
Master's Thesis, [University Name].
```

---

## License

Code in this repository is released under the MIT License. Data derived from third-party sources (auction catalogues, blodbanken.nu) remains subject to the terms of those sources.
