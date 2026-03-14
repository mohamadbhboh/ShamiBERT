---
language:
- ar
license: cc-by-nc-4.0
tags:
- bert
- Arabic BERT
- Levantine Dialect
- Shami
- Syrian Arabic
- Lebanese Arabic
- Jordanian Arabic
- Palestinian Arabic
- Masked Language Model
- Arabic NLP
datasets:
- QCRI/arabic_pos_dialect
- guymorlan/levanti
base_model: aubmindlab/bert-base-arabertv02-twitter
pipeline_tag: fill-mask
---

# ShamiBERT 🇸🇾🇱🇧🇯🇴🇵🇸

**ShamiBERT** is a BERT-based language model specialized for **Levantine Arabic (اللهجة الشامية)** — the dialect spoken across **Syria, Lebanon, Jordan, and Palestine**.

The model was created using **continual pre-training** of AraBERT-Twitter on Levantine Arabic text datasets to better understand **colloquial Shami expressions commonly used in social media and everyday conversations**.

---

# Model Description

ShamiBERT adapts an existing Arabic transformer model to better represent **Levantine dialect language patterns**, vocabulary, and informal expressions.

### Architecture

- **Base Model:** `aubmindlab/bert-base-arabertv02-twitter`
- **Model Type:** BERT-base
- **Layers:** 12 Transformer layers
- **Attention Heads:** 12
- **Hidden Size:** 768
- **Task:** Masked Language Modeling (MLM)

### Training Strategy

The model was trained using **continual pre-training** rather than training from scratch.  
This allows the model to preserve the strong Arabic linguistic knowledge of AraBERT while adapting to **Levantine dialect usage**.

---

# Why AraBERT-Twitter?

The base model was chosen because it already handles **dialectal Arabic and social media text** effectively.

Key advantages:

- Pre-trained on **77GB of Arabic text**
- Includes **60M Arabic tweets**
- Handles **informal Arabic writing**
- Supports **emojis in vocabulary**
- Strong baseline for **dialect adaptation**

---

# Training Data

ShamiBERT was trained on a combination of Levantine Arabic datasets:

| Dataset | Source | Description |
|-------|------|-------------|
| QCRI Arabic POS (LEV) | HuggingFace | Levantine tweets annotated with POS tags |
| Levanti | HuggingFace | Sentences from Syrian, Lebanese, Jordanian and Palestinian dialects |
| Curated Shami | Manual | Manually collected Levantine expressions |

These datasets contain **dialectal text commonly used in social media and conversational Arabic**.

---

# Training Details

| Parameter | Value |
|---|---|
| Epochs | 5 |
| Learning Rate | 2e-5 |
| Batch Size | 128 (effective) |
| Max Sequence Length | 128 |
| MLM Probability | 0.15 |
| Optimizer | AdamW |
| Weight Decay | 0.01 |
| Warmup | 10% |
| Evaluation Perplexity | 5.04 |

---

# Usage

## Fill Mask (Masked Language Modeling)

```python
from transformers import pipeline

fill_mask = pipeline(
    "fill-mask",
    model="mabahboh/ShamiBERT"
)

results = fill_mask("كيفك [MASK] الحمدلله")

for r in results[:3]:
    print(f"{r['token_str']} ({r['score']:.4f})")
