
# ML

## First move
- Inspect target type, metric, missingness, categorical columns, leakage risk, sample count, and whether the target is imbalanced or ordinal.

## Default playbook
1. Build a pandas profile: `info()`, `describe()`, `value_counts()`, missingness rates.
2. Use a `sklearn.pipeline.Pipeline`.
3. Impute missing values, encode categoricals, scale only when the model needs it.
4. Start with a strong baseline: logistic/linear model, random forest, gradient boosting, or a small MLP if the data is dense and clean.
5. Validate with stratified CV for classification, GroupKFold when samples are grouped, TimeSeriesSplit for temporal data, and KFold for regression.
6. Compare metric stability, not just mean score.

## Model choice
- Small tabular data: linear model, tree ensemble
- Nonlinear tabular: gradient boosting, random forest, XGBoost/LightGBM if allowed
- Sparse high-dimensional: linear model, Naive Bayes, linear SVM
- Few samples: simpler models, strong CV discipline
- Mixed numeric/categorical: one-hot + tree ensemble or target-encoded variant if leakage is controlled
- Monotonic structure: boosted trees with monotonic constraints if allowed
- Strong interaction effects: tree ensembles or shallow neural nets with careful regularization

## Common contest traps
- Fitting preprocessing outside CV
- Using the test set to tune thresholds
- Ignoring class imbalance
- Overusing deep nets on tiny tabular data
- Not stratifying folds
- Not checking that the train/test schema matches exactly
- Forgetting that leakage can happen through feature engineering, not only through model fitting

## Practical recipes
- Classification baseline: imputer -> one-hot -> logistic regression / random forest
- Regression baseline: imputer -> scaler -> Ridge / ElasticNet / gradient boosting
- Imbalanced classification: class weights, threshold tuning, macro F1, PR-AUC if relevant
- Ordinal target: ordinal-aware loss or regression framing if metric allows