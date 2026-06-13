
# NLP

## First move
- Decide whether the task is classification, retrieval, deduplication, sequence labeling, generation, or multimodal alignment.

## Default playbook
1. Start with text cleaning only if the contest clearly benefits.
2. Build a TF-IDF + linear model baseline for classification.
3. Move to pretrained transformers when semantics matter.
4. Use proper tokenization and max-length control.
5. Check whether the task benefits from sentence-level or token-level supervision.
6. Overfit a small subset before scaling up.

## Model choice
- Fast baseline: TF-IDF + logistic regression / linear SVM
- Small labeled data: pretrained transformer + careful CV
- Deduplication/paraphrase: sentence embeddings or cross-encoder
- Sequence tasks: token classification head
- Long documents: chunking, pooling, hierarchical encoding, or long-context transformers
- Retrieval-style tasks: bi-encoder for fast search, cross-encoder for reranking
- Generative tasks: encoder-decoder or decoder-only model depending on the prompt format

## Architecture notes
- RNN/LSTM/GRU still matter when sequence length is small and compute is tight
- Word2Vec/GloVe/FastText are useful for lightweight representation baselines
- BERT/RoBERTa/DistilBERT are strong starting points for classification and NER
- Seq2Seq is the baseline for translation, summarization, and controlled generation
- Sentence embeddings are often the cleanest route for similarity, clustering, and deduplication
- POS/NER: token classifier on top of contextual encoder
- Long-context tasks: chunk + pool or long-context model if available

## Loss and objective recipes
- Classification: cross entropy
- Imbalanced classification: weighted CE or focal loss
- Token labeling: token-wise cross entropy, ignoring padded positions
- Similarity: contrastive/triplet loss or cosine-based objectives
- Retrieval: in-batch negatives or ranking losses
- Generation: teacher forcing with token-level CE; use label masking carefully
- Multi-label text: BCEWithLogitsLoss
- Sequence-to-sequence: cross entropy with teacher forcing and padding mask

## Tokenization notes
- Word-level tokenization is simple but weak for OOV handling.
- Subword tokenization is the default for modern transformers.
- Character-level models can help in noisy or morphology-heavy settings.
- Always inspect what the tokenizer does to emojis, punctuation, and special symbols.

## Augmentation recipes
- Synonym replacement
- Random deletion
- Back translation
- Token masking
- Sentence shuffling
- Noise injection
- Only augment when semantics survive the transformation

## Practical code habits
- Keep tokenizer, max length, truncation, and padding consistent across train/val/test
- Use attention masks correctly
- For transformers, always verify shapes of input IDs, attention masks, and labels
- For sequence labeling, align labels with subword tokenization rules
- For retrieval, cache embeddings and normalize vectors before similarity search
- For classification, compare a sparse baseline against a transformer before committing to complexity
- For generation, decode with a fixed strategy first and tune only if the metric requires it

## Strong baseline ladder
1. TF-IDF + linear classifier
2. FastText / shallow embeddings
3. DistilBERT / RoBERTa / BERT fine-tune
4. Ensemble or cross-validation if the contest rewards stability

## Common architecture pairings
- Intent or sentiment classification -> transformer encoder
- NER / POS -> token classification head
- Duplicate detection -> sentence embedding or cross-encoder
- Retrieval -> bi-encoder + nearest neighbor search
- Translation / summarization -> encoder-decoder

## Common contest traps
- Leaking labels through preprocessing
- Over-cleaning text and removing useful signal
- Ignoring class imbalance or threshold tuning
- Using a heavy model when a sparse baseline is enough
- Forgetting subword alignment in NER/POS
- Incorrect truncation on long text
- Measuring with the wrong averaging scheme
- Treating token-level and sentence-level tasks the same