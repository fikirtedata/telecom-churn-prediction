# Telecom Customer Churn Prediction

Final assignment for the Data Science and AI program (GCI World, Matsuo-Iwasawa Laboratory, University of Tokyo).

## Problem
Predict which telecom customers will churn (leave) and find which factors are linked to churn.

## Data
- Two tables, `Client.csv` and `Record.csv`, provided by the course (not included in this repo).
- Merged on `Customer_ID`: 100,000 customers, 100 columns.
- Classes are almost balanced: 50.44% retained, 49.56% churned.

## Method
1. Merge the two tables and drop rows with a missing target.
2. Stratified split: 70% train, 30% test (`random_state=42`).
3. Numerical features (77): median imputation, then standard scaling.
4. Categorical features (21): constant imputation ("Unknown"), then one-hot encoding. Final matrix: 247 features.
5. Model: Random Forest (150 trees, max depth 12, `class_weight='balanced'`).
6. EDA plots: churn distribution, handset age vs. churn, dropped voice calls vs. revenue change.

## Results
- ROC-AUC: 0.669 on the test set.
- Accuracy 0.62; F1 about 0.60 (retained) and 0.63 (churned).
- Top features by importance: `eqpdays` (handset age), `months` (time as customer), `change_mou`, `mou_Mean`, `adjrev`.

## Limitations
- Performance is modest. The features carry only limited signal about churn.
- No hyperparameter tuning or cross-validation yet.
- Feature importance shows association, not cause.

## How to run
1. Put `Client.csv` and `Record.csv` in a folder and set `DATA_PATH` at the top of the notebook.
2. `pip install -r requirements.txt`
3. Run the notebook from top to bottom. Plots are saved to `figures/`.
