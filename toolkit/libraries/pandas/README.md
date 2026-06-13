
# Pandas

## Use when
- You need table cleaning, joins, feature prep, or fast EDA.

## Must-know
- `read_csv`, `info`, `describe`, `value_counts`
- Missing values: `isna`, `fillna`, `dropna`
- `groupby`, `agg`, named aggregation
- `merge`, `join`, `concat`
- `pivot_table`, `melt`, reshaping
- Datetime conversion and resampling
- Categorical dtype management
- Window operations for time series features

## Contest heuristics
- Use pandas for inspection and feature prep, then move to NumPy/sklearn/PyTorch for modeling.
- Check train/test schema alignment early.
- Convert categorical columns intentionally.
- Prefer vectorized operations and `.loc`.
- Profile memory and dtypes before building expensive features.
- Use named aggregations and clear column naming in feature pipelines.

## Gotchas
- Chained indexing
- Merge explosions from duplicate keys
- Silent dtype drift
- Train/test column mismatch

## Sources
- pandas user guide
- Missing data
- GroupBy
- Merge/join
- Reshaping and time series