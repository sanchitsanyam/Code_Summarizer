
````markdown
# Code Summarization using Seq2Seq LSTM with Attention

## Project Overview
This project implements a Sequence-to-Sequence (Seq2Seq) Encoder–Decoder architecture using LSTMs to automatically generate natural language summaries from Python code snippets.

The task is formulated similar to machine translation:
- Source sequence: code tokens  
- Target sequence: summary tokens  

---

## Problem Statement
Given a Python code snippet, generate a concise and meaningful textual description of what the code does.

### Example
**Input (Code):**
```python
ax.set_xlabel("temperature")
````

**Output (Summary):**

```
set x axis label to temperature
```

---

## Model Architecture

The model follows a Seq2Seq with Attention design:

```
Code Text
  ↓
Tokenizer → Integer Sequences
  ↓
Embedding Layer
  ↓
Encoder LSTM (return_sequences=True)
  ↓
Attention Mechanism
  ↓
Decoder LSTM
  ↓
Dense + Softmax
  ↓
Generated Summary
```

### Key Components

* Encoder: Multi-layer LSTM to encode code semantics
* Attention: Aligns decoder steps with relevant encoder states
* Decoder: LSTM generating summaries token-by-token
* Teacher Forcing during training
* Greedy Decoding during inference

---

## Data Preprocessing

* CamelCase splitting (setXLabel → set x label)
* Lowercasing
* Removing punctuation, numbers, and symbols
* Tokenization using spaCy
* Length filtering for stable training
* Special tokens:

  * `sostok`: start of summary
  * `eostok`: end of summary

---

## Dataset

* Python code snippets paired with docstrings
* Filtered to:

  * `max_code_len = 40`
  * `max_summary_len = 40`

---

## Training Configuration

* Embedding Dimension: 128
* LSTM Hidden Units: 256
* Optimizer: RMSprop
* Loss Function: Sparse Categorical Crossentropy
* Batch Size: 128
* Early Stopping enabled

---

## Evaluation

* Metric: BLEU Score
* BLEU evaluates n-gram overlap between generated and reference summaries
* Greedy decoding used during inference

---

## Limitations

* LSTM bottleneck for long sequences
* Greedy decoding may miss globally optimal summaries
* No beam search implemented
* Limited handling of out-of-vocabulary identifiers

---

## Future Work

* Replace LSTM with Transformer-based models (CodeT5, T5, BERT variants)
* Implement beam search decoding
* Add copy mechanism for variable and function names
* Train on larger and more diverse datasets
* Evaluate using ROUGE metrics

---

## Technologies Used

* Python
* TensorFlow / Keras
* spaCy
* NumPy
* Pandas
* NLTK (BLEU Score)

---

## References

* Sutskever et al., "Sequence to Sequence Learning with Neural Networks"
* Bahdanau et al., "Neural Machine Translation by Jointly Learning to Align and Translate"
* Google Neural Machine Translation (GNMT)

---

## Author

Sanchit Sanyam
Mathematics & Computing | Data Science
BIT Mesra | IIT Madras (BS Data Science)


