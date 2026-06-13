# Architectures

## CNN family
- Conv -> normalization -> activation -> pooling is the classic backbone pattern
- ResNet: residual blocks, strong default
- DenseNet: feature reuse, useful when data is limited
- EfficientNet: good accuracy/compute tradeoff
- ConvNeXt: strong modern CNN baseline
- Use pretrained CNNs first unless the contest explicitly forbids them.

## Attention family
- Self-attention: global interaction
- Multi-head attention: multiple relationship subspaces
- CBAM: channel + spatial attention for CNNs

## Vision transformers
- ViT: patch embeddings + transformer encoder
- Works best with strong data, pretraining, and augmentation
- Fine-tuning a pretrained ViT is usually easier than training from scratch.

## Segmentation
- U-Net: encoder-decoder with skip connections
- DeepLabV3+: multi-scale context
- SegFormer: modern transformer-based segmentation baseline

## Detection
- YOLO: one-stage speed-focused detector
- Faster R-CNN: two-stage accuracy-focused detector
- DETR: set prediction, transformer-based detector
- Choose the detector whose training and inference complexity fits the contest time budget.

## NLP architectures
- RNN / LSTM / GRU for lightweight sequence baselines
- Transformer encoder for classification and tagging
- Encoder-decoder for generation and translation
- Decoder-only for open-ended generation

## Multimodal
- CLIP-style image-text encoders
- Cross-encoders for reranking
- Bi-encoders for retrieval
- Multimodal tasks often start as retrieval, then become classification after fusion.

## Selection rule
- Small data: transfer learning
- Strong spatial structure: CNN/U-Net
- Strong global context: attention/transformers
- Ranking or retrieval: embeddings and similarity models
- Need speed and simplicity: smaller pretrained CNN or linear text baseline
- Need interpretability: simpler architecture plus stronger validation
