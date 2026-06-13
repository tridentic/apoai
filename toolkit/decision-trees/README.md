
# Decision Trees

## 1. What is the data?
- Tabular -> pandas + sklearn
- Image -> PyTorch + pretrained backbone
- Text -> TF-IDF baseline or transformer
- Multimodal -> split each modality first
- Time series -> lag features, windows, or sequence models

## 2. What is the target?
- Classification -> accuracy, F1, AUC, top-k
- Regression -> MAE, RMSE, R2
- Matching/assignment -> `linear_sum_assignment`
- Curve fitting -> `curve_fit`
- Clustering -> KMeans/PCA/NMF

## 3. What is the best first baseline?
- Tabular: imputer + encoder + linear/tree model
- Image: pretrained CNN
- Text: TF-IDF + logistic regression
- Time series: lag features + tree/linear model
- Multimodal: separate encoders, then fusion

## 4. What architecture family matches the problem?
- Local spatial patterns -> CNN
- Global dependencies -> transformer/attention
- Small structured tabular data -> tree ensemble
- Similarity/retrieval -> embedding model
- Pixel-wise prediction -> U-Net/DeepLab/SegFormer
- Multi-object localization -> detector

## 5. What loss should I start with?
- Classification -> cross entropy
- Imbalanced classification -> weighted CE or focal loss
- Segmentation -> CE + Dice
- Retrieval/similarity -> contrastive or triplet
- Multilabel -> BCEWithLogitsLoss
- Regression -> MAE or MSE depending on outliers
- Ranking -> pairwise/listwise/ranking loss if the metric is ranking-based

## 6. When to upgrade
- If baseline underfits: add better features or a stronger model
- If validation is unstable: simplify and use stronger CV
- If labels are scarce: transfer learning or pretrained embeddings
- If the task is structure-heavy: use SciPy or custom math
- If train loss keeps dropping but validation stalls: regularize, simplify, or improve validation
- If the metric is threshold-sensitive: tune the threshold after validation only

## 7. Fast routing
- Unknown continuous parameters -> `curve_fit`
- One-to-one minimum cost pairing -> `linear_sum_assignment`
- Categorical tabular data -> one-hot + model
- Many sparse text features -> linear model
- Images with enough data -> CNN / ViT
- Need to improve low-contrast images -> CLAHE or stronger normalization
- Need to model text similarity -> sentence embeddings + cosine similarity