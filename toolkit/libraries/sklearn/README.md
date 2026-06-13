# scikit-learn

## Use when
- You need a reliable contest baseline for tabular ML, classical NLP, clustering, or evaluation.

## Must-know
- `Pipeline`
- `train_test_split`, `cross_val_score`, `StratifiedKFold`
- `GroupKFold`, `TimeSeriesSplit`
- `GridSearchCV`, `RandomizedSearchCV`
- `SimpleImputer`, `StandardScaler`, `OneHotEncoder`, `OrdinalEncoder`
- `ColumnTransformer`
- `metrics` and averaging modes
- `PCA`, `NMF`, `KMeans`
- `CalibratedClassifierCV`

## Contest heuristics
- Put preprocessing inside a pipeline.
- Use stratified CV for classification.
- Tune only the knobs that matter.
- Use `macro` scores when minority classes matter.
- Use `top-k` metrics when the task allows multiple guesses.
- Use `ColumnTransformer` for mixed-type tabular data.
- Use calibration when probabilities matter.

## Good defaults
- Tabular classification: imputer + one-hot + tree/linear model
- Tabular regression: imputer + scaler + Ridge/ElasticNet/GBM
- Sparse text: TF-IDF + linear classifier
- Unsupervised: PCA before KMeans if dimensionality is high
- Mixed numeric/categorical: `ColumnTransformer` + `Pipeline`
- Sparse high-dimensional classification: linear SVM or logistic regression
- Small labeled data: simple model plus strong CV beats fancy defaults

## Code pattern
```python
num_pipe = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
])

cat_pipe = Pipeline([
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("onehot", OneHotEncoder(handle_unknown="ignore")),
])

preprocess = ColumnTransformer([
    ("num", num_pipe, num_cols),
    ("cat", cat_pipe, cat_cols),
])

model = Pipeline([
    ("preprocess", preprocess),
    ("clf", LogisticRegression(max_iter=1000)),
])
```

## Gotchas
- Test leakage from preprocessing outside CV
- Misreading class imbalance
- Ignoring `handle_unknown` for categoricals
- Using the wrong metric average
- Forgetting that `fit_transform` must happen inside the train fold
- Treating `cross_val_score` as a substitute for careful metric analysis

## Sources
- Preprocessing guide
- Cross-validation guide
- Pipeline guide
- Model evaluation guide
- Grid search guide
