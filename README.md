# LLM-Powered ATT&CK Mapping

A lightweight reasoning-driven framework for MITRE ATT&CK technique mapping using Large Language Models (LLMs).

## Overview

Existing ATT&CK mapping approaches typically treat the task as a classification problem and assume a single correct label. Many rely on supervised learning, fine-tuning, or retrieval-augmented generation (RAG).

This project takes a different perspective: ATT&CK mapping is inherently ambiguous and interpretive. The same behavior may reasonably map to multiple techniques depending on analyst interpretation, abstraction level, or implementation details.

We propose a lightweight reasoning-driven framework that:
- decomposes ATT&CK mapping into interpretable reasoning steps,
- models analyst-style reasoning instead of strict classification,
- uses prompt engineering only (no fine-tuning or RAG),
- supports flexible and explainable mappings.

The framework achieves around **80% exact-match accuracy**. After post-evaluating mismatched predictions, many are found to be semantically reasonable, increasing the effective accuracy to approximately **90%**.

---

## Repository Structure

```text
attck-mapping-llm/
├── README.md
├── requirements.txt
├── data/
│   └── samples.json
├── scripts/
│   ├── run_mapping.py
│   └── evaluate.py
├── results/
```

---

## Installation

```bash
git clone https://github.com/yourusername/attck-mapping-llm.git
cd attck-mapping-llm
pip install -r requirements.txt
```

---

## Running

```bash
python3 scripts/run_mapping.py \
    --model gpt-5 \
    --temperature 0.3 \
    --input data/samples.json
```

---

## Example

Input behavior:

```text
can search for anti-virus products on the system
```

Output:

```json
{
  "technique": [
    "T1518.001"
  ],
  "reasoning": "The behavior explicitly searches for installed anti-virus products."
}
```

---

## Key Contributions

- Reasoning-driven ATT&CK mapping
- No fine-tuning or labeled training required
- Handles ambiguity and multiple valid interpretations
- Explainable mapping process
- LLM-based post-evaluation for reasonable mismatches

---

## License

MIT License
