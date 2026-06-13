
# CV

## First move
- Identify whether the task is classification, detection, segmentation, restoration, metric learning, or generation/editing.

## Default playbook
1. Resize and normalize consistently.
2. Use augmentations only if they preserve the label semantics.
3. Start with a pretrained backbone if the contest allows it.
4. Freeze first, then unfreeze if time permits.
5. Inspect one batch visually before training.
6. Match the loss to the task and the metric to the actual leaderboard scoring rule.

## Model choice
- Image classification: pretrained ResNet/EfficientNet/ConvNeXt/ViT
- Small data: transfer learning beats training from scratch
- Segmentation: U-Net/DeepLabV3+/SegFormer
- Detection: YOLO/Faster R-CNN/DETR depending on metric, data size, and speed constraints
- Restoration/editing: task-specific losses and careful visualization
- Fine-grained or multimodal vision: CLIP-style encoders and metric learning
- Limited data with spatial focus: CBAM/channel attention/spatial attention modules can help

## Architecture notes
- ResNet: residual connections help optimization and make deeper CNNs trainable
- EfficientNet: compound scaling is useful when you need balanced depth/width/resolution
- ConvNeXt: modern CNN baseline with transformer-era training ideas
- ViT: works well when data and augmentation are strong
- U-Net: encoder-decoder with skip connections; good for segmentation and pixel tasks
- DeepLabV3+: strong when you need multi-scale context
- SegFormer: lightweight modern segmentation baseline
- YOLO: fast detector; useful when the contest rewards speed or simple implementation
- Faster R-CNN: strong region-based detector when accuracy matters more than speed
- DETR: transformer-based detection with set prediction; useful when the task is conceptually novel

## Loss and objective recipes
- Classification: cross entropy; label smoothing if classes are noisy
- Imbalanced classification: weighted CE or focal loss
- Segmentation: CE + Dice is a common strong pair
- Detection: classification loss + box regression loss; follow the model's default recipe first
- Metric learning: contrastive, triplet, or supervised contrastive loss
- Multilabel: BCEWithLogitsLoss with per-class weighting if needed
- Multi-task: weighted sum of task losses, then normalize by scale and gradient magnitude

## Augmentation recipes
- Flip, rotation, random crop, resize, color jitter, Gaussian noise, blur, random erasing
- MixUp/CutMix for classification when labels support interpolation
- Mosaic for detection when object scale diversity matters
- CLAHE for low-contrast medical or satellite-like data
- Perspective transform when viewpoint variance is real
- Do not use augmentations that destroy the label semantics

## Training recipe
1. Fit a tiny overfitting sanity check first.
2. Train a frozen backbone baseline.
3. Unfreeze gradually.
4. Add scheduler, weight decay, and early stopping.
5. Track validation metrics and inspect failure cases.
6. Add TTA/ensemble only after the single-model baseline is solid.

## Common contest traps
- Augmentations that break the label
- Forgetting train/eval mode
- Mismatched normalization between train and inference
- Treating a restoration or generation task like plain classification
- Ignoring input resolution effects on the metric
- Choosing a model because it is fashionable rather than because it fits the data regime