# Augmentations

## Principle
Use augmentations to create realistic variability, not random corruption.

## Computer vision
- Flip: when left-right symmetry is valid
- Rotation: only within semantic limits
- Random crop: preserves object identity
- Resize: maintain aspect ratio when geometry matters
- Color jitter: when lighting variation is realistic
- Gaussian noise: when sensor noise is plausible
- Blur: when focus variation is part of the domain
- CutMix: useful for classification
- MixUp: useful for classification and calibration
- Mosaic: useful for detection
- Random erasing: helpful for robustness
- CLAHE: useful for low-contrast imagery
- Perspective transform: only when viewpoint shifts are real
- Use stronger augmentation for larger datasets and weaker augmentation when data is scarce.
- A safe default chain is resize -> crop -> color/intensity perturbation -> regularization augmentation.
- For pixel tasks, ensure masks are transformed identically to images.

## NLP
- Synonym replacement: only if meaning survives
- Random deletion: useful for robustness in some classification settings
- Back translation: strong but expensive
- Token masking: good for denoising and MLM-style setups
- Sentence shuffling: only if order is not essential
- Noise injection: use carefully
- Token dropout/masking: good for denoising or regularizing embeddings
- Augmentation should never flip the label semantics.
- For token-level labels, preserve alignment after augmentation or avoid it.

## Rules of thumb
- Augmentations must match the test-time distribution or make the model robust to a known shift.
- Do not stack every augmentation by default.
- Validate ablations one at a time.
- If an augmentation hurts CV more than it helps training, reduce it or remove it.
- Keep geometry-preserving augmentations separate from color/intensity augmentations.
- If the task is already tiny, augmentation may hurt more than help.

## Good contest pattern
Start with no augmentation, then add one safe augmentation at a time, then add stronger composition only after the baseline is stable.
