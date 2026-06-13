# NLP Toolkit for IOAI Competition 🚀

**Last Updated:** 2026-06-12  
**Prepared for:** Asia Pacific Olympiad in Artificial Intelligence

## Quick Navigation

### 📚 Core NLP Notebooks

#### 1. **vanilla.ipynb** - Baseline RNNs

- Vanilla RNN (Tanh activation)
- LSTM (Long Short-Term Memory)
- GRU (Gated Recurrent Unit)
- Best for: Sequential classification tasks

#### 2. **seq2seq_attention.ipynb** - Sequence-to-Sequence Models

- **Bahdanau (Additive) Attention**: `score(s_t, h_i) = v^T * tanh(W_q * s_t + W_k * h_i)`
- **Luong (Dot-Product) Attention**: `score(s_t, h_i) = s_t^T * W * h_i`
- Encoder-Decoder LSTM with bidirectional encoder
- Teacher forcing support
- Best for: Machine translation, text summarization, Q&A

#### 3. **transformer_components.ipynb** - Modern Architectures

- **Multi-Head Self-Attention** from scratch
- **Vision Transformer (ViT)**:
  - Patch embedding (stride=patch_size Conv2d)
  - Class token + Positional embedding
  - Transformer encoder stack
- **BERT/RoBERTa Backbones**:
  - Token embeddings + Positional embeddings + Segment embeddings
  - Pure TransformerEncoder stacks
  - Masked Language Model (MLM) head for pretraining
- Best for: Classification, NLU, vision tasks

#### 4. **embeddings_alignment.ipynb** - Vector Space Models

- **Word2Vec Skip-gram**: Center word → Context words
- **Word2Vec CBOW**: Context words → Center word
- **GloVe**: Co-occurrence matrix factorization
- **FastText**: Subword-aware embeddings
- **CLIP-style Dual Encoder**:
  - Text encoder (LSTM-based)
  - Vision encoder (CNN-based)
  - InfoNCE contrastive loss
- **Contextual Token Regression**: Map contextual embeddings to token space
- Best for: Semantic similarity, image-text matching, zero-shot learning

---

## 🎯 Quick Reference: Model Dimensions

```python
# Typical configurations for different tasks

# Small models (quick testing)
BATCH_SIZE = 16
HIDDEN_DIM = 128
EMBED_DIM = 256

# Medium models (balanced)
BATCH_SIZE = 32
HIDDEN_DIM = 256
EMBED_DIM = 512

# Large models (SOTA)
BATCH_SIZE = 64
HIDDEN_DIM = 512-768
EMBED_DIM = 768-1024
```

---

## 💡 When to Use Each Model

| Task                   | Model                  | Why                      |
| ---------------------- | ---------------------- | ------------------------ |
| Text Classification    | Vanilla RNN/LSTM/GRU   | Simple, fast             |
| Machine Translation    | Seq2Seq with Attention | Handles variable lengths |
| Image Classification   | ViT                    | Patch-based processing   |
| Language Understanding | BERT                   | Bidirectional context    |
| Image-Text Matching    | CLIP                   | Shared embedding space   |
| Word Similarity        | Word2Vec/GloVe         | Pre-trained efficiency   |

---

## 🔑 Key Hyperparameters

### Attention Mechanisms

- **Bahdanau**: More learnable parameters, better for longer sequences
- **Luong**: Simpler, faster computation (dot product)

### Transformer

- **num_heads**: 8, 12, 16 (must divide d_model)
- **d_ff**: Usually 4× d_model
- **num_layers**: 2-12 depending on task complexity

### Embeddings

- **Word2Vec context_size**: 2-5 (smaller = faster)
- **GloVe x_max**: Weight cutoff for rare pairs
- **CLIP temperature**: 0.07 (default), lower = sharper distribution

---

## ⚡ Speed Comparison

| Model       | Parameters | Speed       | Memory    |
| ----------- | ---------- | ----------- | --------- |
| Vanilla RNN | Small      | 🟢 Fast     | Low       |
| LSTM        | Medium     | 🟡 Moderate | Medium    |
| Transformer | Large      | 🔴 Slow     | High      |
| CLIP        | Very Large | 🔴 Slow     | Very High |

**Recommendation**: Start with LSTM/GRU for quick prototyping, then scale to Transformers if needed.

---

## 🛠️ Common Issues & Solutions

### Issue: Vanishing/Exploding Gradients

- **Solution**: Use LSTM/GRU instead of Vanilla RNN, add layer normalization

### Issue: Attention weights not focused

- **Solution**: Decrease temperature in softmax, check gradient flow

### Issue: CLIP embeddings not aligning

- **Solution**: Increase contrastive loss weight, use higher temperature initially

### Issue: ViT overfitting on small datasets

- **Solution**: Use pretrained ViT, increase regularization/dropout

---

## 📊 Training Tips

```python
# Standard training loop
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
scheduler = torch.optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=100)

for epoch in range(num_epochs):
    for batch in dataloader:
        outputs = model(batch)
        loss = criterion(outputs, targets)

        optimizer.zero_grad()
        loss.backward()
        torch.nn.utils.clip_grad_norm_(model.parameters(), 1.0)  # Gradient clipping
        optimizer.step()

    scheduler.step()
```

---

## 🚀 Quick Start Template

```python
import torch
import torch.nn as nn

# Device setup
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

# Model initialization
model = YourModel(...).to(device)

# Forward pass
output = model(input_data)

# Loss & optimization
loss = criterion(output, target)
optimizer.zero_grad()
loss.backward()
optimizer.step()
```

---

## 📝 Notes for Competition

- **Time management**: Transformers train slower; start with LSTM if time is tight
- **Memory management**: Reduce batch size or use gradient checkpointing for large models
- **Debugging**: Always test with small batch first (batch_size=2)
- **Reproducibility**: Set random seeds: `torch.manual_seed(42)`

---

## 🔗 Architecture Cheat Sheet

### Seq2Seq Flow

```
Input → Encoder LSTM → Context Vectors
Context + Decoder Hidden → Attention → Context
Context + Hidden → Output Layer → Predictions
```

### Vision Transformer Flow

```
Image → Patch Embedding → Class Token
Patches + Pos Embedding → Transformer Stack
Extract Class Token → Classification Head
```

### CLIP Flow

```
Image → Vision Encoder → Normalized Embedding
Text → Text Encoder → Normalized Embedding
Similarity Matrix → InfoNCE Loss
```

---

Good luck with IOAI! 🎯

For detailed implementations, refer to the respective notebooks.
