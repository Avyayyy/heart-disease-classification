# Heart Disease Classification 🫀

Predicting the presence of heart disease from patient health data, using a classification model built from scratch as a self-practice project.

## Problem Statement

Given a set of clinical measurements for a patient, predict whether they have heart disease. This is a **binary classification** problem — the target column indicates presence (1) or absence (0) of heart disease.

## Dataset

- Source: UCI Heart Disease dataset (also hosted on Kaggle)
- **303 rows, 14 columns**, no missing values
- Target balance: 165 patients with heart disease (1), 138 without (0) — reasonably balanced, so accuracy alone is a fair-ish metric, though precision/recall/F1 still tell a fuller story
- Features: `age`, `sex`, `cp` (chest pain type), `trestbps` (resting blood pressure), `chol` (cholesterol), `fbs` (fasting blood sugar), `restecg` (resting ECG results), `thalach` (max heart rate achieved), `exang` (exercise-induced angina), `oldpeak`, `slope`, `ca` (number of major vessels), `thal`
- All columns are already numeric (int/float) — no categorical string encoding needed, though several are really categorical codes (e.g. `cp`, `restecg`, `thal`) worth treating as such during EDA

> **Note:** The raw dataset CSV is not tracked in this repository (see `.gitignore`). Download it separately and place it in a local `data/` folder to reproduce this project.

## Approach

<!-- TODO: fill in as you build this out, e.g.: -->
- Exploratory data analysis (EDA) — distributions, missing values, target balance, correlation heatmap
- Train/test split (before any preprocessing decisions, to avoid data leakage)
- Preprocessing — handling missing values, encoding categorical features
- Baseline model comparison (Logistic Regression, Random Forest, KNN, etc.)
- Hyperparameter tuning on the best-performing baseline
- Evaluation using accuracy, precision, recall, F1, and ROC-AUC
- Feature importance analysis

## Results

<!-- TODO: fill in once the model is trained -->
| Metric | Score |
|--------|-------|
| Accuracy | _fill in_ |
| Precision | _fill in_ |
| Recall | _fill in_ |
| F1 | _fill in_ |
| ROC-AUC | _fill in_ |

## Project Structure

```
.
├── README.md
├── .gitignore
├── heart-disease-classification.ipynb   # main notebook
└── data/                                 # (not tracked in git — download separately)
```

## Setup & Installation

This project uses **Miniconda** for dependency management.

```bash
# Clone the repository
git clone https://github.com/yourusername/heart-disease-classification.git
cd heart-disease-classification

# Create and activate a conda environment
conda create -n heart-disease-classification python=3.10
conda activate heart-disease-classification

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

<!-- TODO: generate a requirements.txt with: conda list -e > requirements.txt (or pip freeze > requirements.txt) -->

## Tools & Libraries

- Python
- pandas, NumPy
- scikit-learn (classification models)
- Matplotlib / Seaborn (visualization)
- Jupyter Notebook

## Notes

This project was built as a self-practice exercise to strengthen end-to-end classification workflow skills — problem framing, EDA, preprocessing, baseline modelling, tuning, and evaluation — without following a guided tutorial step-by-step.
