# 📋 NLP Toolkit Index for IOAI Competition

**Competition**: Asia Pacific Olympiad in Artificial Intelligence (IOAI)  
**Created**: June 12, 2026  
**Total Notebooks**: 5  
**Total Components**: 30+ architectures

---

## 🚀 Quick Start (5 minutes)

```python
# For classification
from vanilla import LSTMClassifier  # Fast & reliable

# For sequence-to-sequence
from seq2seq_attention import Seq2Seq  # Translation/Summarization

# For vision tasks
from transformer_components import VisionTransformer  # ViT from scratch

# For embeddings
from embeddings_alignment import CLIPModel  # Image-text matching
```

---

## 📚 Notebook Organization

### **Tier 1: Fundamentals** (`vanilla.ipynb`)

Essential baseline models for quick prototyping:

- RNN, LSTM, GRU
- Training & inference patterns
- **When to use**: First approach for any sequential data

### **Tier 2: Sequence Processing** (`seq2seq_attention.ipynb`)

Advanced sequence-to-sequence models:

- Bahdanau Attention (additive)
- Luong Attention (dot-product)
- Bidirectional encoder + attention decoder
- **When to use**: Translation, summarization, paraphrasing

### **Tier 3: Transformer Stack** (`transformer_components.ipynb`)

Modern architectures built from scratch:

- Multi-head self-attention
- Vision Transformer (ViT)
- BERT/RoBERTa backbones with MLM
- **When to use**: SOTA performance needed, more compute available

### **Tier 4: Embeddings** (`embeddings_alignment.ipynb`)

Vector space models and contrastive learning:

- Word2Vec (Skip-gram + CBOW)
- GloVe (co-occurrence matrix)
- FastText (subword embeddings)
- CLIP-style dual encoder
- **When to use**: Semantic matching, transfer learning, zero-shot tasks

### **Tier 5: Advanced Patterns** (`advanced_patterns.ipynb`)

Practical optimizations & combined techniques:

- Custom loss functions (Focal, Label Smoothing, Contrastive)
- Attention visualization
- Beam search
- Model quantization & pruning
- Knowledge distillation
- Complete training loop with best practices
- **When to use**: Fine-tuning, production deployment, memory constraints

---

## 🎯 Problem-to-Solution Mapping

| Problem Type             | Notebook    | Models                  |
| ------------------------ | ----------- | ----------------------- |
| Text Classification      | Tier 1 or 3 | LSTM or BERT            |
| Machine Translation      | Tier 2      | Seq2Seq with Attention  |
| Image Classification     | Tier 3      | ViT                     |
| Semantic Similarity      | Tier 4      | CLIP or Word2Vec        |
| Sentiment Analysis       | Tier 1 or 3 | RNN/LSTM or Transformer |
| Named Entity Recognition | Tier 3      | BERT or Transformer     |
| Question Answering       | Tier 2 or 3 | Seq2Seq or Transformer  |
| Paraphrase Generation    | Tier 2      | Seq2Seq with Attention  |
| Zero-shot Classification | Tier 4      | CLIP                    |

---

## ⏱️ Model Speed Ranking (Inference)

1. **Fastest** 🟢: Word embeddings (Word2Vec, GloVe)
2. **Fast** 🟡: RNN/LSTM/GRU
3. **Moderate** 🟠: Seq2Seq with Attention
4. **Slow** 🔴: Transformer/ViT
5. **Very Slow** 🔴🔴: Large BERT/CLIP models

**Competition Tip**: Start with Tier 1, scale up if time permits.

---

## 📊 Model Complexity (Training Parameters)

| Model     | Parameters | Memory      |
| --------- | ---------- | ----------- |
| Word2Vec  | 10M        | Very Low    |
| RNN       | 50M        | Low         |
| LSTM/GRU  | 100M       | Low-Medium  |
| Seq2Seq   | 200M       | Medium      |
| ViT-Base  | 86M        | Medium-High |
| BERT-Base | 110M       | High        |
| CLIP-Base | 150M       | Very High   |

---

## 🔑 Key Formulas Cheat Sheet

### Attention

```
Bahdanau: score = v^T * tanh(W_q * q + W_k * k)
Luong:    score = q^T * W * k  (or just q^T * k for dot product)
```

### Loss Functions

```
Focal Loss:         -α * (1 - p_t)^γ * log(p_t)
Label Smoothing:    (1-ε)y + ε/K
Contrastive (Triplet): max(0, d(a,p) - d(a,n) + margin)
InfoNCE (CLIP):     -log(exp(sim(i,t)/τ) / Σ exp(sim(i,t')/τ))
```

### Positional Encoding

```
PE(pos, 2i)   = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

---

## 💾 Memory Optimization Tricks

1. **Gradient Checkpointing**: Trade compute for memory

```python
from torch.utils.checkpoint import checkpoint
output = checkpoint(model, input)  # Recomputes forward on backward
```

2. **Quantization**: Reduce precision

```python
quantized_model = torch.quantization.quantize_dynamic(model, {nn.Linear}, dtype=torch.qint8)
```

3. **Pruning**: Remove unnecessary weights

```python
from advanced_patterns import prune_weights
pruned_model = prune_weights(model, pruning_ratio=0.3)
```

4. **Knowledge Distillation**: Train smaller model

```python
from advanced_patterns import knowledge_distillation_loss
loss = knowledge_distillation_loss(teacher_logits, student_logits)
```

---

## ⚡ Training Tips for Competition

### Quick Prototyping (Tier 1)

```
- Batch size: 64-128
- Learning rate: 1e-3
- Epochs: 5-10
- Time: ~5 minutes
```

### Balanced Approach (Tier 2)

```
- Batch size: 32-64
- Learning rate: 5e-4 (with warmup)
- Epochs: 10-15
- Time: ~30 minutes
```

### Maximum Performance (Tier 3-4)

```
- Batch size: 16-32 (memory limited)
- Learning rate: 1e-4 (with scheduler)
- Epochs: 20-30 or until convergence
- Time: ~2+ hours
```

---

## 🔍 Common Competition Problem Patterns

### Pattern 1: Classification with Imbalanced Classes

**Solution**: Use FocalLoss from `advanced_patterns.ipynb`

### Pattern 2: Limited Training Data

**Solution**: Use pretrained embeddings (Word2Vec) or CLIP

### Pattern 3: Generate Sequences (Translation, Summarization)

**Solution**: Use Seq2Seq with Attention (beam search optional)

### Pattern 4: Need Very Fast Inference

**Solution**: Use Word embeddings → Simple MLP (no RNN)

### Pattern 5: Multimodal (Image + Text)

**Solution**: Use CLIP from `embeddings_alignment.ipynb`

---

## 📖 How to Use Each Notebook During Competition

### During Problem Reading (5 min)

- Identify problem type using table above
- Pick notebook from "Problem-to-Solution Mapping"

### During Solution Design (10 min)

- Read relevant notebook's architecture explanation
- Check hyperparameters in README

### During Implementation (20-30 min)

- Copy model architecture from notebook
- Modify input/output dimensions to match problem
- Add data loading + training loop

### During Debugging (as needed)

- Use test cells in notebooks
- Check tensor shapes at each layer
- Use `advanced_patterns.ipynb` for loss debugging

---

## 🎓 Learning Order (for practice)

1. **Day 1**: `vanilla.ipynb` - Understand RNN/LSTM/GRU
2. **Day 2**: `seq2seq_attention.ipynb` - Learn attention mechanisms
3. **Day 3**: `transformer_components.ipynb` - Understand Transformers
4. **Day 4**: `embeddings_alignment.ipynb` - Study embeddings
5. **Day 5**: `advanced_patterns.ipynb` - Master optimizations

---

## ✅ Pre-Competition Checklist

- [ ] Run all notebooks successfully
- [ ] Understand model forward pass for each architecture
- [ ] Know which loss function to use for your problem
- [ ] Practice modifying hyperparameters
- [ ] Test inference speed on small batches
- [ ] Bookmark common formulas

---

## 🆘 During Competition - Decision Tree

```
Is my prediction
├─ Classification?
│  ├─ Single label → LSTM (fast) or BERT (accurate)
│  └─ Multi-label → Sigmoid output, BCE loss
├─ Regression?
│  ├─ Continuous → MSE loss with RNN/Transformer
│  └─ Ranking → Use ranking loss
└─ Generation?
   ├─ Fixed output → Seq2Seq
   ├─ Variable length → Seq2Seq with beam search
   └─ Image caption → CLIP + decoder

Memory issues?
├─ Yes → Quantize + Prune (from advanced_patterns)
└─ No → Proceed with full model

Time pressure?
├─ < 10 min → Use vanilla RNN
├─ 10-30 min → Use LSTM + simple attention
└─ 30+ min → Try full Transformer stack
```

---

## 🚀 Final Advice

> **Focus on getting _something_ working first**, then optimize.
> Better to have a working LSTM than a broken Transformer!

**Time allocation suggestion:**

- 5% Problem understanding
- 30% Data preprocessing
- 40% Model implementation
- 15% Training & tuning
- 10% Evaluation & submission

---

**Good luck with IOAI! 🎯**

For detailed code, refer to individual notebooks.
All models are tested and ready to use.
