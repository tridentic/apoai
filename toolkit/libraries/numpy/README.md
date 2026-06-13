
# NumPy

## Use when
- You need fast array math, shape transforms, indexing, or vectorized preprocessing.

## Must-know
- `ndarray`, `shape`, `ndim`, `dtype`
- Broadcasting rules
- Boolean masks and advanced indexing
- `reshape`, `transpose`, `stack`, `concatenate`
- `argsort`, `unique`, `bincount`, `where`
- `@` / `matmul`, `dot`, `linalg`
- `einsum` for compact tensor algebra when it clarifies intent

## Contest heuristics
- Prefer vectorized code over Python loops.
- Use broadcasting for per-row/per-column transforms.
- Use `np.unique(..., return_counts=True)` for frequency work.
- Use `np.argsort` for rankings and top-k style logic.
- Use `np.bincount` for fast integer histograms.
- Use `np.clip` and stable normalization when building numeric features.
- Use `np.random.default_rng` for reproducibility.

## Gotchas
- `*` is elementwise, not matrix multiply
- Shapes must broadcast from the right
- dtype casting can silently hurt results

## Sources
- NumPy quickstart
- Broadcasting guide
- Linear algebra reference