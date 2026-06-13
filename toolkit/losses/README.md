# Losses

## Rule
Pick the loss that matches the output geometry, then combine only when the task really needs multiple signals.

## Core losses
- Cross entropy: single-label classification
- BCEWithLogitsLoss: multilabel or binary outputs
- MSE / MAE / Huber: regression
- Dice loss: segmentation overlap
- Focal loss: hard examples or imbalance
- Contrastive / triplet / supervised contrastive: embedding and retrieval tasks
- KL divergence: distillation or probability matching

## Common combinations
- Classification with noisy labels: cross entropy + label smoothing
- Segmentation: CE + Dice
- Detection: classification loss + box regression loss
- Multitask: weighted sum of task losses
- Retrieval: contrastive + ranking-aware term if needed
- Distillation: student CE + KL to teacher logits

## Combination rules
- Normalize loss magnitudes before weighting.
- Start with one loss and add the second only when the baseline shows the failure mode.
- If one term dominates gradients, rescale or reduce it.
- Match the loss to the metric whenever possible.
- Use masks for padded sequence losses.

## Practical hints
- Label smoothing helps when labels are noisy or classes are similar.
- Focal loss helps when easy negatives overwhelm positives.
- Huber can be safer than MSE under outliers.
- Dice is especially useful when foreground is sparse.
- KL is useful when matching probability distributions, not hard labels.

## Common mistakes
- Combining losses without understanding what each term changes
- Using MSE for a classification target
- Ignoring masking on padded sequence losses
- Choosing a fancy loss before checking the baseline
