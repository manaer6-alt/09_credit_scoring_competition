**English** | [Русский](README_RU.md)

# Credit Risk Scoring

End-to-end credit risk project focused on predicting the probability of a serious payment delinquency within 90 days after loan origination.

## Results

| Result | Value |
|---|---:|
| Best documented competition position | **9th place** |
| Final validation ROC-AUC | **0.8326** |
| Final ensemble | **60% Logistic Regression + 40% CatBoost** |

The final solution uses a rank-based blend. It improved over the tuned logistic regression on both local validation and the competition leaderboard while remaining comparatively simple and stable.

## Why this project matters

Credit scoring is not only a classification problem. A useful solution must combine predictive quality, leakage control, explainability and stable validation. This project demonstrates:

- aggregation of application, transaction, credit bureau and previous-loan data;
- identification and removal of target leakage;
- reproducible preprocessing for numerical and categorical features;
- comparison of an interpretable linear model with a nonlinear boosting model;
- hyperparameter tuning and rank-based ensembling;
- probability-based evaluation with ROC-AUC.

## Modeling approach

1. Audit the datasets and define the prediction moment.
2. Aggregate customer history from multiple source tables.
3. Build a leakage-safe validation split.
4. Establish Decision Tree and Logistic Regression baselines.
5. Train and tune CatBoost.
6. Blend model ranks to improve robustness under an ROC-AUC objective.
7. Generate the final competition submission.

## Repository guide

- [Final end-to-end notebook](notebooks/competition.ipynb)
- [Compact baseline](notebooks/simple_baseline.ipynb)
- `notebooks/` — additional feature-engineering and model experiments
- `requirements.txt` — Python dependencies

Competition data is intentionally not stored in the repository.

## Reproduction

```bash
python -m venv .venv
python -m pip install -r requirements.txt
```

Place the competition files in the paths referenced by the final notebook, then run `notebooks/competition.ipynb` from top to bottom.

## Technology

Python · pandas · NumPy · scikit-learn · CatBoost · SciPy · Matplotlib

## Limitations and next steps

- The project uses anonymized competition data and is not a production lending system.
- The reported leaderboard result should not be treated as evidence of performance on a new lending portfolio.
- A production continuation would add probability calibration, temporal stability monitoring, reject inference, fairness checks and a cost-based approval policy.
