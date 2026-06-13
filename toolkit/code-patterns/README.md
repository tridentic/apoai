# Code Patterns

## PyTorch contest notebook skeleton
1. Imports and seed setup
2. Data loading
3. Visual sanity checks
4. Model definition
5. Loss, optimizer, scheduler
6. Train/eval loop
7. Save best checkpoint
8. Inference and submission

## Debug-first habits
- Confirm one batch end-to-end before training.
- Print sample inputs, labels, and predictions.
- Overfit a tiny batch before doing full training.
- Write assertions for shape and dtype at the edges of the pipeline.
- Keep a single notebook cell for quick visual sanity checks.

## Clean module habits
- Keep config in one place.
- Separate dataset, model, train loop, and inference.
- Print tensor shapes in the first run.
- Assert shape assumptions early.
- Keep notebook cells idempotent when possible.

## Common reusable patterns
- Freeze/unfreeze transfer learning
- One-batch overfit test
- Early stopping on validation metric
- TTA loop
- K-fold training
- Ensemble averaging
- Threshold tuning on validation predictions
- Stacking or blending after strong single-model baselines
- EMA / SWA when the baseline is already stable
- Freeze backbone then fine-tune head for transfer learning
- Save best and last checkpoints separately
- Store validation predictions for post-analysis

## scikit-learn pattern
- `Pipeline` for preprocessing + model
- `ColumnTransformer` for mixed tabular data
- `GridSearchCV` / `RandomizedSearchCV` for tuning
- Fold-safe encoding and imputation
- Proper `predict_proba` handling when the metric uses probabilities
- Use `set_output(transform="pandas")` only if it helps debugging and the environment supports it

## Anti-patterns
- Huge notebook with mixed responsibilities
- Manual preprocessing duplicated in train and test
- Silent dtype changes
- No validation baseline before fancy tricks
- No versioned save of the final submission notebook
- Trial-and-error without a recorded hypothesis

## Minimal checklist for every run
- Does the batch shape look right?
- Does one training step reduce loss?
- Does the model overfit a tiny subset?
- Does validation reflect the final metric?
- Do saved predictions match submission format?
