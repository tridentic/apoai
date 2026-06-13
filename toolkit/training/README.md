# Training

## What this section is for
The habits that make a model actually work in a contest setting.

## Core checklist
- Fix seeds.
- Verify a tiny overfit on a small batch.
- Confirm train/val split logic.
- Monitor the exact metric used for selection.
- Save checkpoints by validation score.
- Keep a clear experiment log.
- Make baseline, ablation, and final-run notebooks separate.

## Reproducibility
- Seed Python, NumPy, PyTorch, and any dataloader workers.
- Freeze preprocessing and augmentation versions.
- Record model config, metric, fold, and random seed.
- Keep notebook cells runnable from top to bottom.
- Store the exact library versions if the environment is mutable.

## GPU optimization
- Move tensors to device once.
- Use mixed precision when stable.
- Use dataloading workers when I/O is the bottleneck.
- Reduce input resolution only if the metric survives it.
- Profile before adding complexity.
- Prefer a smaller clean model over an unmaintainable giant one.

## Validation strategy
- Stratified folds for classification.
- Group-based folds when samples are related.
- Time-based splits for temporal data.
- Never use the test set for threshold tuning.
- Use OOF predictions when ensembling or calibrating.
- If the contest uses a public/private split, avoid overfitting to the public leaderboard.

## Experiment tracking
- Log config, seed, data split, feature set, model, loss, optimizer, scheduler, and metric.
- Save failure cases and examples from the worst errors.
- Keep a short postmortem after each run.
- Write one-line conclusions after each experiment so you can compare later.

## Common failures
- Training only on one split and assuming the result generalizes
- Not isolating leakage
- Changing too many things at once
- Forgetting to track the exact version of the notebook used for submission
- No sanity check for label leakage
- No baseline comparison after architecture changes
