# Preprocessing

## Tabular
- Impute missing numeric values with median or domain-specific values.
- Impute categorical missing values with a dedicated category.
- Encode categoricals with one-hot when the feature cardinality is manageable.
- Consider ordinal encoding only when order is real.
- Normalize or standardize when the model is scale-sensitive.
- Build target-aware features only inside CV folds.
- Use log transforms on heavy-tailed positive variables when appropriate.

## Image
- Resize to the backbone's expected shape.
- Normalize with the pretrained model's stats if using transfer learning.
- Preserve label semantics when augmenting.
- Check channel order and pixel value range.
- Ensure resizing does not destroy small objects or critical boundaries.

## Text
- Choose tokenizer before cleaning.
- Lowercasing and punctuation stripping are task-dependent.
- Keep special tokens intact for transformer models.
- Truncation policy should match the evaluation metric and document length.
- Preserve entities and numeric patterns if they matter.

## Time series
- Sort by time.
- Check missingness and irregular sampling.
- Use rolling windows, lags, and aggregates.
- Split chronologically.
- Avoid future leakage in window features and normalization.

## Leakage rules
- Fit preprocessors on train only.
- Compute feature statistics inside CV when possible.
- Never let future data influence current features.
- If a preprocessing step touches labels, keep it inside the training fold only.

## Practical checks
- Confirm the transformed shape.
- Confirm dtype after each major preprocessing stage.
- Compare one sample before and after preprocessing.
- Validate on a tiny subset before scaling to the full dataset.
