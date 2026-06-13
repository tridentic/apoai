# Audio & Multimodal Processing Quick Index

**Quick Reference for IOAI Competition**

---

## 🎙️ Audio Processing Cheat Sheet

### Feature Extraction (30 seconds)

```python
from audio_processing import AudioFeatureExtractor
extractor = AudioFeatureExtractor(sample_rate=16000, n_mels=128)

# For general audio classification
mel_spec = extractor.extract_mel_spectrogram(waveform)

# For speech recognition
mfcc = extractor.extract_mfcc(waveform)

# Add temporal context (optional)
delta = extractor.extract_delta(mel_spec)
```

### Audio Model Selection

```
Quick:      AudioCNN           (2D conv on spectrogram)
Balanced:   AudioResNet        (residual connections)
Temporal:   AudioRNNClassifier (CNN + LSTM)
```

---

## 📊 Tabular Data Cheat Sheet

### Quick Baseline

```python
from tabular_graph_networks import WideDeepNetwork
model = WideDeepNetwork(input_dim=feature_count, n_classes=output_count)
```

### Interpretability Needed

```python
from tabular_graph_networks import TabNet
model = TabNet(input_dim=feature_count, n_classes=output_count, n_steps=3)
```

---

## 🕸️ Graph Data Cheat Sheet

### Standard Graph Problem

```python
from tabular_graph_networks import GCN, normalize_adjacency_matrix
adj_norm = normalize_adjacency_matrix(adjacency)
model = GCN(n_features=feat_dim, n_hidden=32, n_classes=n_classes)
logits = model(node_features, adj_norm)
```

### Need Better Performance

```python
from tabular_graph_networks import GAT
model = GAT(n_features=feat_dim, n_hidden=32, n_classes=n_classes, n_heads=4)
logits = model(node_features, adjacency_binary)
```

---

## 📏 Input Shapes at a Glance

### Audio Models

```
AudioCNN, AudioResNet:
  Input:  [batch_size, 1, n_mels, time_steps]
  Output: [batch_size, n_classes]

AudioRNNClassifier:
  Input:  [batch_size, 1, n_mels, time_steps]
  Output: [batch_size, n_classes]
```

### Tabular Models

```
WideDeepNetwork, TabNet:
  Input:  [batch_size, feature_count]
  Output: [batch_size, n_classes]
```

### Graph Models

```
GCN, GAT:
  Input:  x=[n_nodes, feature_dim], adj=[n_nodes, n_nodes]
  Output: [n_nodes, n_classes]
```

---

## 🎯 Problem-Solution Quick Map

| Data             | Task                | Solution                  |
| ---------------- | ------------------- | ------------------------- |
| Audio file       | Classify            | AudioCNN + MelSpectrogram |
| Speech           | Speech recognition  | AudioRNNClassifier + MFCC |
| Tabular CSV      | Classification      | TabNet                    |
| Tabular + clicks | Click behavior      | WideDeepNetwork           |
| Graph + nodes    | Node classification | GCN → if bad: GAT         |
| Multimodal       | Audio+features      | AudioRNN + concatenate    |

---

## ⚡ One-Liners

```python
# Full audio pipeline
mel = AudioFeatureExtractor(16000, 128).extract_mel_spectrogram(wav)
pred = AudioCNN(128, 10)(mel.unsqueeze(0))

# Full tabular pipeline
pred = TabNet(50, 10)(tabular_features)

# Full graph pipeline
adj_norm = normalize_adjacency_matrix(adj)
pred = GCN(16, 32, 4)(node_features, adj_norm)
```

---

## 🚨 Common Mistakes to Avoid

1. **Audio**: Forgetting to squeeze/unsqueeze batch dimension
2. **Audio**: Using wrong sample_rate in feature extraction
3. **Tabular**: Not normalizing features (use StandardScaler)
4. **Graph**: Forgetting to normalize adjacency matrix
5. **Graph**: Passing float adjacency to GAT (should be binary)

---

## 📊 Complexity Quick Rank

**Fastest to Slowest:**

1. AudioCNN / WideDeepNetwork
2. AudioResNet / TabNet / GCN
3. AudioRNNClassifier / GAT

**Memory Usage (Low to High):**

1. WideDeepNetwork / TabNet
2. AudioCNN / GCN
3. AudioResNet / GAT / AudioRNNClassifier

---

## 🔧 Default Hyperparameters

```python
# Audio
sample_rate=16000, n_mels=128, n_fft=400, hop_length=160

# Audio Models
AudioCNN: dropout=0.5
AudioResNet: depth=18
AudioRNNClassifier: hidden_dim=256, n_layers=2

# Tabular
TabNet: n_steps=3, dim=64
WideDeepNetwork: hidden_dims=[256, 128]

# Graph
GCN: n_hidden=32, dropout=0.5, n_layers=2
GAT: n_hidden=32, n_heads=8, dropout=0.6
```

---

## ✅ Pre-Competition Setup

```bash
# Install dependencies
pip install torch torchaudio scipy

# Test import
python -c "import torchaudio; from torch_geometric.nn import GCNConv"
```

---

## 📚 Which Notebook for Which Problem?

**Use `audio_processing.ipynb` if:**

- [ ] Audio file classification
- [ ] Speech recognition
- [ ] Sound event detection
- [ ] Music genre classification

**Use `tabular_graph_networks.ipynb` if:**

- [ ] Tabular/structured data (CSV, features)
- [ ] Graph with nodes/edges
- [ ] Network data
- [ ] Complex relationships between entities

---

## 🎓 Learning Path (5 minutes each)

1. Read audio_processing.ipynb → Understand feature extraction
2. Read tabular_graph_networks.ipynb → Understand GCN vs GAT
3. Modify input dimensions to match your data
4. Run on small batch (batch_size=2) to verify
5. Train on full data

---

## 🆘 During Competition

**Memory error?**

- Reduce batch_size
- Use AudioCNN instead of AudioResNet
- Use GCN instead of GAT

**Time pressure?**

- Use AudioCNN (fast)
- Use WideDeepNetwork (simple)
- Use GCN (standard)

**Overfitting?**

- Increase dropout
- Use TabNet (has built-in regularization)
- Use more data

**Underfitting?**

- Use AudioResNet (deeper)
- Use GAT (better features)
- Train longer

---

**Reference compiled for maximum competition speed! 🚀**
