
# GenAI

## First move
- Identify whether the task is prompting, editing, steering, ranking, or constrained generation.

## Default playbook
1. Make a strong prompt baseline before changing the model.
2. Test with fixed seeds and short loops.
3. Search for the smallest change that shifts output in the right direction.
4. Measure with the contest metric, not visual intuition alone.
5. Track prompt variants and outputs systematically.

## Common patterns
- Prompt rewriting
- Controlled generation
- Image/text steering
- Model behavior editing
- Diffusion guidance and prompt control
- Retrieval-augmented generation baselines
- Multimodal prompting with CLIP-style alignment

## Common contest traps
- Overfitting prompts to one example
- Forgetting prompt sensitivity
- Changing too many knobs at once
- Judging quality by aesthetics instead of the evaluation rule