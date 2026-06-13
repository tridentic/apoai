
# Contest Patterns

## What past IOAI/APOAI-style tasks look like
- Feature generation for a fixed model
- Updating a classifier to handle new classes
- Deduplication or paraphrase detection
- Vision tasks that require editing or steering model behavior
- Tabular classification/regression with a hidden metric
- Clustering, assignment, and curve fitting as hidden subproblems
- Image restoration, segmentation, and detection with a score-driven metric
- Multimodal alignment or CLIP-like matching
- Prompt/control tasks for generative models
- Theoretical questions about selecting the right method, not just coding

## Recurrent instincts
- Read the metric first.
- Separate data inspection from model training.
- Build a baseline in the simplest possible framework.
- Use official docs when a library helper can replace custom math.
- Treat validation as part of the solution, not a final checkpoint.
- Search for hidden structure: class imbalance, grouping, time order, or geometry.
- When in doubt, prototype the smallest thing that can fail quickly.

## Historical sources
- IOAI official task repositories for 2024 and 2025
- `open-cu/awesome-ioai-tasks`
- other national selection task archives linked from the IOAI resources page
- regional olympiad training camps and selection task repositories

## What this means in practice
- If the task looks tabular, reach for pandas + sklearn first.
- If the task looks like matching or fitting, check SciPy before inventing an algorithm.
- If the task is visual, start with transfer learning.
- If the task is text-heavy, compare TF-IDF baseline vs transformer quickly.
- If the task is an olympiad-style edit/generate task, look for the minimal change that fixes the specific failure mode.
- If the task has a weird evaluation rule, reverse-engineer the metric before optimizing the model.

## Common recurring olympiad motifs
- “Improve a fixed model” tasks
- “Add missing classes” tasks
- “Repair this model’s behavior” tasks
- “Classify under severe data scarcity” tasks
- “Find the best feature set for a locked model” tasks
- “Match or align outputs under a constrained objective” tasks

## Competition mindset
- Search docs aggressively.
- Keep a library cheat sheet open.
- Always ask: "What exact object or function already solves this?"