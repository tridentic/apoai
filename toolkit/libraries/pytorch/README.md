
# PyTorch

## Use when
- You need neural nets, custom training loops, GPU tensors, or flexible data pipelines.

## Must-know
- Tensors and broadcasting
- Autograd and `.backward()`
- `nn.Module`, losses, layers
- `optim`, schedulers
- `Dataset`, `DataLoader`
- `train()` vs `eval()`
- `torch.no_grad()`
- `state_dict` / checkpointing
- mixed precision (`autocast`, `GradScaler`)
- device moves (`to(device)`)
- tensor reshaping (`view`, `reshape`, `flatten`)
- common layers (`Linear`, `Conv2d`, `BatchNorm`, `Dropout`, `Embedding`)
- common activations (`ReLU`, `GELU`, `SiLU`)

## Contest heuristics
- Start with a minimal training loop and verify shape flow first.
- Use pretrained models when the contest allows.
- Keep data transforms and normalization consistent.
- Save the best checkpoint by validation metric, not training loss.
- Keep the forward pass simple until the baseline works.
- Check device placement and tensor dtypes early.
- Build one clean custom `Dataset` instead of hacking preprocessing into the loop.
- Make the batch dimension explicit at every stage.

## Model definition pattern
```python
class Model(nn.Module):
    def __init__(self):
        super().__init__()
        self.backbone = nn.Sequential(...)
        self.head = nn.Linear(...)

    def forward(self, x):
        x = self.backbone(x)
        return self.head(x)
```

## Data pattern
- `Dataset` returns one sample at a time with final dtypes already fixed.
- `DataLoader` handles batching, shuffling, workers, and collate.
- Keep transforms separate from the dataset logic when possible.

## Optimization pattern
- Optimizer: AdamW for most deep learning baselines, SGD+momentum for some vision setups.
- Scheduler: cosine or step decay are common strong defaults.
- Regularization: weight decay, dropout, early stopping, label smoothing.
- Gradient clipping can help unstable sequence or generative setups.

## Gotchas
- Forgetting zero_grad
- Leaving dropout/batchnorm in training mode at inference
- Mixing NumPy arrays and tensors without checking device/dtype
- Not pinning down batch shapes early
- Hidden shape bugs in flattening/reshaping
- Accidentally detaching tensors needed for gradients
- Passing the wrong shape to losses such as CE/BCE
- Forgetting to move targets to device

## Practical training loop pattern
```python
for epoch in range(num_epochs):
    model.train()
    for x, y in train_loader:
        x, y = x.to(device), y.to(device)
        optimizer.zero_grad()
        with torch.autocast(device_type=device.type, enabled=use_amp):
            logits = model(x)
            loss = criterion(logits, y)
        scaler.scale(loss).backward()
        scaler.step(optimizer)
        scaler.update()

    model.eval()
    with torch.no_grad():
        ...
```

## Sources
- PyTorch basics tutorial
- Tensors
- Datasets/DataLoaders
- Autograd
- Optimization