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

Prior state-of-the-art ATT&CK mapping approaches generally report exact-match accuracies in the range of 60%–70% [1]. In contrast, our framework achieves around **80% match accuracy** on MITRE CTI dataset. After post-evaluating mismatched predictions, many are found to be semantically reasonable, increasing the effective accuracy to approximately **90%**. 

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
git clone https://github.com/zsjstart/LLM-Powered-ATTACK-Mapping.git
cd LLM-Powered-ATTACK-Mapping
pip install -r requirements.txt
```

---

## Running


```bash
python3 scripts/llm_mapping.py \
    --model openai/gpt-oss-120b \
    --temper 0.3 \
    --input Data/MITRE_CTI_Data.csv \
    --limit 10 \
    --output Results/llm_mapping_gpt_test.json
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
  "reasoning": "Searching for anti-virus products matches Security Software Discovery, a sub‑technique of Software Discovery."
}
```

  ---
  
## Key Insights

- ATT&CK mapping is inherently ambiguous, and many behaviors may reasonably correspond to multiple techniques depending on interpretation granularity and analyst perspective.

- Exact-match evaluation alone may underestimate mapping quality, as many mismatched predictions remain semantically reasonable. Many disagreements arise from differences in abstraction level (e.g., parent technique vs. sub-technique) rather than incorrect reasoning, suggesting that ATT&CK mapping should not be treated as a strict single-label classification problem.

- Prompt engineering alone can enable competitive ATT&CK mapping performance without fine-tuning, supervised training, or retrieval augmentation.

- Larger models appear to possess stronger implicit domain knowledge and reasoning capabilities for ATT&CK mapping, reducing reliance on external retrieval systems.

- In contrast, smaller models still exhibit relatively weaker ATT&CK mapping performance. For example, Llama-3.1-Nemotron-70B-Instruct achieves around 65% accuracy, while Qwen2.5-72B-Instruct reaches approximately 71%.

---

## References

[1] Filippo Morbiato, Markus Keller, Priya Nair, and Luca Romano.  
*Hierarchical Retrieval Augmented Generation for Adversarial Technique Annotation in Cyber Threat Intelligence Text*. 2026. 


## Other
In another project, I open-sourced a lightweight LLM-powered CTI-to-ATT&CK pipeline that extracts adversary behaviors from Cyber Threat Intelligence (CTI) reports and maps them to MITRE ATT&CK techniques: https://github.com/zsjstart/LLM-Powered-CTI-ATTACK-Pipeline

## License

MIT License
