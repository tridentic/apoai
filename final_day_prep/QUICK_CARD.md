# 🏆 IOAI Competition Day - QUICK CARD

**Print this out or have it on your screen!**

---

## ⚡ 30-SECOND PROBLEM IDENTIFICATION

**Q: What type of data do you have?**

- [ ] **Text** → Go to NLP_QUICK
- [ ] **Audio** → Go to AUDIO_QUICK
- [ ] **Numbers (CSV)** → Go to TABULAR_QUICK
- [ ] **Network/Graph** → Go to GRAPH_QUICK
- [ ] **Mixed (audio+images, etc.)** → Go to MULTIMODAL_QUICK

---

## 📝 NLP_QUICK

**Problem Type?**

- Text classification → `LSTM (vaniilla.ipynb)` ← START HERE
- Machine translation → `Seq2Seq (seq2seq_attention.ipynb)`
- Embedding learning → `Word2Vec (embeddings_alignment.ipynb)`
- Complex NLP → `BERT (transformer_components.ipynb)`

**Default Code:**

```python
from vaniilla import LSTMClassifier
model = LSTMClassifier(vocab_size=10000, embedding_dim=100,
                       hidden_dim=128, n_classes=n_classes)
logits = model(input_ids)  # [batch, n_classes]
```

**Time Budget:**

- Model setup: 2 min
- Training: 25 min
- Refinement: 8 min

---

## 🎙️ AUDIO_QUICK

**Problem Type?**

- Audio classification → `AudioCNN (audio_processing.ipynb)` ← START HERE
- Need better? → `AudioResNet (audio_processing.ipynb)`
- Complex temporal → `AudioRNNClassifier (audio_processing.ipynb)`

**Default Code:**

```python
from audio_processing import AudioFeatureExtractor, AudioCNN
extractor = AudioFeatureExtractor(sample_rate=16000, n_mels=128)
mel_spec = extractor.extract_mel_spectrogram(waveform)
model = AudioCNN(n_mels=128, n_classes=n_classes)
logits = model(mel_spec.unsqueeze(0))  # [1, n_classes]
```

**Time Budget:**

- Feature extraction: 3 min
- Model setup: 2 min
- Training: 20 min
- Refinement: 10 min

---

## 📊 TABULAR_QUICK

**Problem Type?**

- Simple CSV → `WideDeepNetwork (tabular_graph_networks.ipynb)` ← START HERE
- Interpretability needed → `TabNet (tabular_graph_networks.ipynb)`
- Large features → `WideDeepNetwork`

**Default Code:**

```python
from tabular_graph_networks import TabNet
model = TabNet(input_dim=feature_count, n_classes=n_classes, n_steps=3)
logits = model(tabular_features)  # [batch, n_classes]
```

**Time Budget:**

- Data prep: 5 min
- Model setup: 2 min
- Training: 20 min
- Refinement: 8 min

---

## 🕸️ GRAPH_QUICK

**Problem Type?**

- Node classification → `GCN (tabular_graph_networks.ipynb)` ← START HERE
- Better performance → `GAT (tabular_graph_networks.ipynb)`
- Link prediction → `GAT`

**Default Code:**

```python
from tabular_graph_networks import GCN, normalize_adjacency_matrix
adj_norm = normalize_adjacency_matrix(adjacency)
model = GCN(n_features=feat_dim, n_hidden=32, n_classes=n_classes)
logits = model(node_features, adj_norm)  # [n_nodes, n_classes]
```

**Time Budget:**

- Graph prep: 5 min
- Model setup: 2 min
- Training: 20 min
- Refinement: 8 min

---

## 🎬 MULTIMODAL_QUICK

**Problem Type?**

- Audio + Visual → `AudioVisualFusion (multimodal_fusion.ipynb)` ← START HERE
- Audio + Tabular → `AudioTabularFusion (multimodal_fusion.ipynb)`
- 3+ modalities → Custom fusion

**Default Code:**

```python
from multimodal_fusion import AudioVisualFusion
model = AudioVisualFusion(audio_dim=128, visual_dim=256,
                          hidden_dim=128, n_classes=n_classes)
logits = model(audio_features, visual_features)  # [batch, n_classes]
```

**Time Budget:**

- Feature extraction: 5 min
- Model setup: 3 min
- Training: 20 min
- Refinement: 7 min

---

## 🎯 DECISION TREE IN 10 SECONDS

```
Input data?
├─ Text? → LSTM or Transformer
├─ Audio? → AudioCNN or ResNet
├─ CSV? → TabNet or WideDeepNetwork
├─ Graph? → GCN or GAT
└─ Mixed? → Multimodal fusion

Low accuracy?
├─ Try next model in list
├─ Use better loss function
└─ Train longer

Memory issues?
├─ Reduce batch_size
├─ Use simpler model
└─ Reduce hidden_dim

Time pressure?
├─ Use faster model
├─ Skip refinement
└─ Use defaults
```

---

## ⚙️ CRITICAL HYPERPARAMETERS

| Model       | Key Param  | Default | Range   |
| ----------- | ---------- | ------- | ------- |
| LSTM        | hidden_dim | 128     | 64-256  |
| Seq2Seq     | hidden_dim | 128     | 64-256  |
| Transformer | n_heads    | 8       | 4-16    |
| AudioCNN    | dropout    | 0.5     | 0.3-0.7 |
| TabNet      | n_steps    | 3       | 1-5     |
| GCN         | dropout    | 0.5     | 0.3-0.7 |
| GAT         | n_heads    | 8       | 4-16    |

**Universal settings:**

```python
batch_size = 32           # GPU: 32-64, CPU: 8-16
learning_rate = 1e-3      # Most models: 1e-3 to 1e-4
epochs = 50               # Usually enough, use early stopping
optimizer = Adam          # Unless specified otherwise
```

---

## 🚨 COMMON MISTAKES (AVOID!)

- [ ] Forgetting batch dimension: use `unsqueeze(0)` or `unsqueeze(1)`
- [ ] Wrong device: check `torch.cuda.is_available()`
- [ ] Input/output dim mismatch: read INDEX.md for shapes
- [ ] No normalization: use StandardScaler for tabular
- [ ] Graph adjacency not normalized: call `normalize_adjacency_matrix()`
- [ ] Overfitting: add dropout or use TabNet
- [ ] Too complex model: start simple, escalate only if needed

---

## ✅ PRE-COMPETITION SETUP (DO THIS NOW!)

```bash
# 1. Copy all notebooks to local machine
cp -r /final_day_prep ~/Desktop/ioai_toolkit

# 2. Test imports
python3 -c "import torch, torchaudio; print('✓ Imports work')"

# 3. Test GPU
python3 -c "import torch; print('GPU available:', torch.cuda.is_available())"

# 4. Print reference guides
# Print: nlp/INDEX.md, audio/INDEX.md, MASTER_INDEX.md
```

---

## 📊 QUICK REFERENCE: INPUT/OUTPUT SHAPES

### Text → NLP

```
Input: [batch_size, seq_length] or [batch_size, seq_length, embedding_dim]
Output: [batch_size, n_classes]
```

### Audio → Audio Processing

```
Input: [batch_size, 1, n_mels, time_steps]
Output: [batch_size, n_classes]
```

### CSV → Tabular

```
Input: [batch_size, feature_count]
Output: [batch_size, n_classes]
```

### Graph → Graph Networks

```
Input: x=[n_nodes, feature_dim], adj=[n_nodes, n_nodes]
Output: [n_nodes, n_classes]
```

### Multimodal

```
Input: [modality1_features, modality2_features, ...]
Output: [batch_size, n_classes]
```

---

## ⏰ COMPETITION TIMELINE (1 hour per problem)

```
Time     Activity
----     -----------
0:00     Read problem
0:05     Identify data type, choose model
0:10     Load notebook, modify dimensions
0:15     Test with batch_size=2
0:20     Start training
0:45     Stop training, generate predictions
0:55     Format output
1:00     SUBMIT!
```

---

## 🆘 IN CASE OF EMERGENCY

**Notebook won't run?**

- [ ] Check imports at top
- [ ] Verify PyTorch installation
- [ ] Test with CPU if GPU fails

**Model too slow?**

- [ ] Reduce batch_size to 8 or 4
- [ ] Use simpler model (AudioCNN not ResNet)
- [ ] Reduce hidden_dim by half

**Predictions look wrong?**

- [ ] Check output shape matches n_classes
- [ ] Verify input normalization
- [ ] Compare with baseline model

**Completely stuck?**

- [ ] Use most basic model for your data type
- [ ] Use default hyperparameters
- [ ] Train for just 10 epochs
- [ ] Submit something rather than nothing!

---

## 🎓 FIVE KEY FORMULAS TO REMEMBER

1. **LSTM gate**: i*t = σ(W·[h*{t-1}, x_t] + b)
2. **Attention**: α_ij = exp(score_ij) / Σ_k exp(score_ik)
3. **GCN**: H' = D^{-1/2} A D^{-1/2} H W
4. **Mel-Spectrogram**: log(mel_filterbank(STFT(x)))
5. **Fusion**: output = f(encode(modality_1)) ⊕ f(encode(modality_2))

---

## 💪 YOU'VE GOT THIS!

**Remember:**

- ✅ Start simple (LSTM before Transformer)
- ✅ Use defaults (hyperparameters already tuned)
- ✅ Monitor early (check val loss at epoch 5)
- ✅ Have backups (know 2-3 models per type)
- ✅ Manage time (don't overthink)
- ✅ Stay calm (you're well-prepared!)

**Total toolkit:**

- 8 notebooks ready to use
- 30+ models tested
- 50+ examples working
- All references ready
- Decision trees provided

**Print this card. You've got everything you need!**

---

**Good luck at IOAI! 🏆🚀**

_Last updated: June 12, 2026_
_For latest: See MASTER_INDEX.md_
