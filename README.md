# LLM-Powered ATT&CK Mapping

A lightweight reasoning-driven framework based on open-source models (e.g., gpt-oss-120b) for MITRE ATT&CK technique mapping using Large Language Models (LLMs).

## Overview

Existing ATT&CK mapping approaches typically treat the task as a classification problem and assume a single correct label. Many rely on supervised learning, fine-tuning, or retrieval-augmented generation (RAG).

This project takes a different perspective: ATT&CK mapping is inherently ambiguous and interpretive. The same behavior may reasonably map to multiple techniques depending on analyst interpretation, abstraction level, or implementation details.

We propose a lightweight reasoning-driven framework that:
- decomposes ATT&CK mapping into interpretable reasoning steps,
- models analyst-style reasoning instead of strict classification,
- uses prompt engineering only (no fine-tuning or RAG),
- supports flexible and explainable mappings.

Prior state-of-the-art ATT&CK mapping approaches generally report exact-match accuracies in the range of 60%–70% [1]. However, our framework achieves around **80% match accuracy** on MITRE CTI dataset. After post-evaluating mismatched predictions, many are found to be semantically reasonable, increasing the effective accuracy to approximately **90%**. 

---

## Repository Structure

```text
LLM-Powered-ATTACK-Mapping/
├── README.md
├── requirements.txt
├── data/
│   └── MITRE_CTI_Data.csv
├── scripts/
│   ├── llm_mapping.py
│   └── llm_mismatch_eva.py

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
## Key Insights

- Smaller models achieve a relatively poor performance in ATT&CK mapping due to their internal limited domain knowledge, such as, nvidia/Llama-3.1-Nemotron-70B-Instruct-HF achieves 65% accuracy while Qwen/Qwen2.5-72B-Instruct exhibits 71% accuracy.
- In contrast, larger models has sufficient inherent capability in handling this task without the reliance on external information, with openai/gpt-oss-120b achieves 80% accuracy (without including cases where its predictions are actually reasonable as well).

---

## References

```bibtex
@article{morbiato2026hierarchical,
  author = {Morbiato, Filippo and Keller, Markus and Nair, Priya and Romano, Luca},
  title = {Hierarchical Retrieval Augmented Generation for Adversarial Technique Annotation in Cyber Threat Intelligence Text},
  year = {2026},
  doi = {10.48550/arXiv.2604.14166}
}
```

## License

MIT License
