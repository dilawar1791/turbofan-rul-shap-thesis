# Remaining Useful Life Prediction of Aircraft Turbofan Engines Using Machine Learning and SHAP

This repository contains the code, data, and supporting prototype artifacts developed for my Master's thesis at Hochschule Trier.

The study investigates Remaining Useful Life (RUL) prediction for aircraft turbofan engines using the NASA C-MAPSS FD001 dataset. Four regression approaches are evaluated: Linear Regression, Random Forest, XGBoost, and Support Vector Regression (SVR). The work additionally investigates model explainability using SHAP, explanation stability, correlated features, robustness to input perturbations, prediction uncertainty, near-failure classification, and asymmetric prognostic error using the PHM08 scoring function.

The repository also contains the ERMDSF (Explainable Remaining Useful Life & Maintenance Decision-Support Framework), a research prototype demonstrating how RUL predictions, uncertainty estimates, SHAP explanations, near-failure probabilities, and maintenance-oriented information can be integrated into an interactive interface.

## Repository Structure

```text
turbofan-rul-shap-thesis/
│
├── README.md
├── requirements.txt
├── 01_main_analysis.ipynb
├── 02_revision_experiments.ipynb
├── 03_ermdsf_prototype.ipynb
│
├── data/
│   ├── train_FD001.txt
│   ├── test_FD001.txt
│   └── RUL_FD001.txt
│
└── ermdsf_artifacts/
    ├── dashboard_config.pkl
    ├── fleet_maintenance_prioritization.csv
    ├── operational_case_studies.csv
    ├── train_processed.csv
    ├── X_full.csv
    ├── xgb_classifier.pkl
    └── xgb_rul_model.pkl
```

## Notebooks

### 01_main_analysis.ipynb

Contains the main thesis analysis, including data preprocessing, RUL target construction, machine-learning model development and evaluation, and SHAP-based model interpretation.

### 02_revision_experiments.ipynb

Contains the additional experiments and analyses performed during the final thesis revision. These include analyses addressing feature informativeness, SHAP ranking agreement, random-ranking baselines, feature–RUL correlations, correlated-feature sensitivity, KernelSHAP sensitivity, robustness experiments, official NASA FD001 test evaluation, uncertainty analysis, and PHM08 asymmetric prognostic scoring.

### 03_ermdsf_prototype.ipynb

Contains the interactive ERMDSF research prototype. The prototype integrates previously generated prediction, uncertainty, explainability, classification, and maintenance-prioritization artifacts into an interactive dashboard.

Some ERMDSF saved artifacts originate from an earlier stage of the study and therefore correspond to the earlier 24-feature analysis rather than the final revised 16-feature experimental pipeline. They are retained to reproduce the prototype interface and functionality presented in the thesis and should not be interpreted as the authoritative final experimental results.

## Dataset

The experiments use the NASA C-MAPSS FD001 turbofan-engine degradation dataset.

The repository contains:

- `train_FD001.txt` — training trajectories
- `test_FD001.txt` — official test trajectories
- `RUL_FD001.txt` — NASA-provided Remaining Useful Life labels for the official test-engine endpoints

The main experiments use a piecewise RUL target capped at 125 cycles during training.

## Final Predictor Set

Following feature screening, the final revised experimental pipeline uses 16 predictors:

```text
op1, op2,
s2, s3, s4, s7, s8, s9,
s11, s12, s13, s14, s15,
s17, s20, s21
```

## Models

Four regression model families are evaluated:

- Linear Regression
- Random Forest
- XGBoost
- Support Vector Regression (RBF kernel)

A separate calibrated binary classifier is used to estimate the probability associated with the modelling event `RUL < 30 cycles`.

The 30-cycle threshold is a modelling threshold used for the research experiments. It should not be interpreted as a certified aviation maintenance threshold.

## Reproducibility

The notebooks are designed for execution in Google Colab.

The analysis notebooks use the FD001 files contained in the `data/` directory.

The ERMDSF notebook uses the supporting files contained in `ermdsf_artifacts/`.

The final experimental software environment used:

```text
Python        3.13.15
NumPy         2.1.3
pandas        2.2.3
scikit-learn  1.6.1
XGBoost       3.4.1
SHAP          0.52.0
Gradio        6.27.0
Plotly        5.24.1
```

Additional dependencies are listed in `requirements.txt`.

## ERMDSF Prototype Disclaimer

ERMDSF is a research prototype developed to demonstrate the integration of prognostic and explainability outputs.

It is not a certified or validated aircraft maintenance, airworthiness, or operational decision-making system. Recommendations and risk categories displayed by the prototype are research demonstrations and should not be interpreted as operational maintenance instructions.

## Thesis

**Title:** Remaining Useful Life Prediction of Aircraft Turbofan Engines Using Machine Learning and SHAP

**Author:** Muhammad Dilawar  
**Institution:** Hochschule Trier  
**Supervisor:** Prof. Dr. Maik Weber

## Purpose

This repository accompanies the Master's thesis and is provided to improve transparency and reproducibility of the reported experiments.
