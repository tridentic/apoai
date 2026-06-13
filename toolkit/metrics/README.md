# Metrics

## Rule
Train for what the contest measures.

## Classification
- Accuracy: balanced problems
- Macro F1: minority classes matter
- Weighted F1: class imbalance with support awareness
- ROC-AUC: ranking/probability quality
- PR-AUC: positive class rarity
- Top-k accuracy: multiple guesses allowed
- Balanced accuracy: class imbalance with equal class weighting
- Log loss: when probability calibration matters

## Regression
- MAE: robust to outliers
- RMSE: penalizes large errors
- R2: explanatory fit, not always contest-relevant
- MAPE/SMAPE: relative error when scale varies, but watch divide-by-zero cases

## Segmentation
- Dice / IoU / mIoU
- Track class-wise performance when classes are uneven
- Boundary-aware metrics if the challenge emphasizes edges

## Detection
- mAP and IoU thresholds
- Box regression quality matters as much as classification
- Per-class AP to detect failure modes in rare classes

## Similarity / retrieval
- Cosine similarity
- Recall@k
- MAP / NDCG when ranking is explicit
- Use the same embedding normalization at train and inference

## Loss alignment
- See `losses/README.md` for the exact loss recipes and combination rules.

## Practical habit
Always decide whether the metric is threshold-based, ranking-based, or pixel/box-based before choosing the model.
