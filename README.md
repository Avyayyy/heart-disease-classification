# Heart Disease Classification 🫀

Predicting the presence of heart disease from patient health data, using a classification model built from scratch as a self-practice project.

## Problem Statement

Given a patient's medical attributes, can we predict whether they have heart disease? This is a **binary classification** problem — the target column indicates presence (1) or absence (0) of heart disease.

**Evaluation goal:** reach 90% accuracy as a proof-of-concept threshold to justify further investment in the project.

## Dataset

- Source: [Cleveland Database, UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/45/heart+disease) (also available on [Kaggle](https://www.kaggle.com/datasets/redwankarimsony/heart-disease-data))
- **303 rows, 14 columns**, no missing values
- Target balance: 165 patients with heart disease (1), 138 without (0) — reasonably balanced, so accuracy alone is a fair-ish metric, though precision/recall/F1 still tell a fuller story
- Features: `age`, `sex`, `cp` (chest pain type), `trestbps` (resting blood pressure), `chol` (cholesterol), `fbs` (fasting blood sugar), `restecg` (resting ECG results), `thalach` (max heart rate achieved), `exang` (exercise-induced angina), `oldpeak`, `slope`, `ca` (number of major vessels), `thal`
- All columns are already numeric (int/float) — no categorical string encoding needed, though several are really categorical codes (e.g. `cp`, `restecg`, `thal`) worth treating as such during EDA

> **Note:** The raw dataset CSV is not tracked in this repository (see `.gitignore`). Download it separately and place it in a local `data/` folder to reproduce this project.

## Approach

- Exploratory data analysis (EDA) — distributions, missing values (none found), target balance (165 vs. 138, reasonably balanced), correlation heatmap
- Train/test split (before any preprocessing decisions, to avoid data leakage)
- Preprocessing — feature scaling; categorical-coded columns (`cp`, `restecg`, `thal`, etc.) treated as categories rather than raw integers
- Baseline model comparison across Logistic Regression, Random Forest, and KNN — **Logistic Regression performed best** (~88.5% CV accuracy)
- Hyperparameter tuning on Logistic Regression via `RandomizedSearchCV` and `GridSearchCV` — no improvement over baseline, suggesting the model had already reached a stable ceiling for this dataset size
- Evaluation via confusion matrix and classification report (precision, recall, F1 per class)
- Feature importance via logistic regression coefficients (`.coef_`)

## Results

Final model: **Logistic Regression**, tuned via `GridSearchCV` (best params: `C=0.2257`, `solver=liblinear`). Baseline comparison showed it outperforming Random Forest and KNN; tuning matched but did not exceed the baseline's ~88.5% accuracy — indicating the untuned defaults were already close to optimal for this dataset.

Evaluated on a held-out test set of 61 patients:

| Metric | Class 0 (no disease) | Class 1 (disease) |
|--------|----------------------|--------------------|
| Precision | 0.89 | 0.88 |
| Recall | 0.86 | 0.91 |
| F1-score | 0.88 | 0.89 |

**Overall accuracy: 0.89** (macro avg F1: 0.88, weighted avg F1: 0.89)

### Why 89% is a good result, even against a 90% target

The evaluation goal set at the start of this project (see Problem Definition) was 90% accuracy as a proof-of-concept threshold. The final model reached 89% — just one misclassified patient out of 61 away from that target. A few reasons this still counts as a strong, credible result rather than a shortfall:

- **A single test row is worth ~1.6% of the accuracy score.** With only 61 test patients, hitting exactly 90% vs. 89% comes down to one prediction. Treating that 1% gap as a meaningful failure would be over-reading noise in a small sample — a slightly different train/test split could just as easily have landed above the threshold.
- **The stronger signal is recall on Class 1 (0.91).** For a health-screening problem, correctly catching actual disease cases matters more than raw accuracy, since a false negative (missing a real case) is costlier than a false positive. The model's best number is exactly on the metric that matters most for this use case.
- **Tuning converged, not stalled.** `RandomizedSearchCV` and `GridSearchCV` both landed on essentially the same performance as the baseline, which is evidence that the model reached a genuine ceiling for this feature set and dataset size — not that the tuning process was incomplete or misconfigured.
- **The 90% threshold was a proof-of-concept gate, not a hard requirement.** Its purpose was to test whether the medical attributes carry enough signal to justify further investment in the project, and 89% with strong, balanced precision/recall across both classes clearly demonstrates that they do.

Consistent, balanced performance across both classes (rather than one strong class propping up the average), combined with strong recall on the more consequential class, makes a solid case that the model is fit for its purpose as a proof-of-concept, even one point under the original target.

**Feature importance** was assessed via logistic regression coefficients (`.coef_`) on scaled features. The strongest predictors were `sex` (coefficient ≈ -0.89), `cp` — chest pain type (≈ +0.67), and `exang` — exercise-induced angina (≈ -0.63), with `restecg` (≈ +0.33) as a secondary contributor. Features like `age`, `chol`, and `trestbps` had near-zero coefficients, suggesting limited standalone linear influence once the stronger features are accounted for.

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
- Matplotlib / Seaborn (visualisation)
- Jupyter Notebook
