# Multilingual Health Question Answering in Low-Resource African Languages

**ALU Final Project — Zindi Competition**
**Student:** David Akachi Nwanze
**Competition:** [Multilingual Health Question Answering in Low-Resource African Languages Challenge](https://zindi.africa)

---

## Overview

This repository contains all code and experiments for the Zindi competition on multilingual health question answering across five African languages: **Akan, Amharic, Luganda, Swahili, and English** (across multiple African countries).

The task is to generate accurate answers to health questions in the same language as the question. Models are evaluated using ROUGE-1 F1, ROUGE-L F1, and an LLM-as-a-Judge score.

---

## Notebooks

| Notebook | Description | Open in Colab |
|----------|-------------|---------------|
| [summative_eda.ipynb](notebooks/summative_eda.ipynb) | Exploratory Data Analysis | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_eda.ipynb) |
| [summative_exp1.ipynb](notebooks/summative_exp1.ipynb) | Exp 1: mT5-small baseline fine-tuning (full data) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp1.ipynb) |
| [summative_exp2.ipynb](notebooks/summative_exp2.ipynb) | Exp 2: mT0-small baseline fine-tuning (full data) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp2.ipynb) |
| [summative_exp3.ipynb](notebooks/summative_exp3.ipynb) | Exp 3: mT5-small + language tag prompt | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp3.ipynb) |
| [summative_exp4.ipynb](notebooks/summative_exp4.ipynb) | Exp 4: mT5-small + 5 epochs | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp4.ipynb) |
| [summative_exp5.ipynb](notebooks/summative_exp5.ipynb) | Exp 5: mT5-small + lower learning rate (5e-5) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp5.ipynb) |
| [summative_exp6.ipynb](notebooks/summative_exp6.ipynb) | Exp 6: mT5-small + language tag prompt (30% data) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp6.ipynb) |
| [summative_exp7.ipynb](notebooks/summative_exp7.ipynb) | Exp 7: Semantic retrieval (MiniLM embeddings) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp7.ipynb) |
| [summative_exp8.ipynb](notebooks/summative_exp8.ipynb) | Exp 8: mT5-small + LoRA fine-tuning | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp8.ipynb) |
| [summative_exp9.ipynb](notebooks/summative_exp9.ipynb) | Exp 9: mT0-small full data fine-tuning | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp9.ipynb) |
| [summative_exp10.ipynb](notebooks/summative_exp10.ipynb) | Exp 10: Hybrid semantic + TF-IDF retrieval | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/S1rDavid9/multilingual_health_summative/blob/main/notebooks/summative_exp10.ipynb) |

---

## Experiment Results

| Exp | Model/Approach | Data | Epochs | Key Config | Val ROUGE-1 | Zindi Score |
|-----|---------------|------|--------|------------|-------------|-------------|
| 1 | mT5-small | Full (~28k) | 3 | Baseline fine-tune | — | 0.1986 |
| 2 | mT0-small | Full (~28k) | 3 | Baseline fine-tune | 0.1870 | 0.1477 |
| 3 | mT5-small | Full (~28k) | 3 | Language tag prompt | ~0.10 | 0.2292 |
| 4 | mT5-small | 30% (~8.5k) | 5 | More epochs | ~0.15 | 0.2148 |
| 5 | mT5-small | 30% (~8.5k) | 2 | Lower lr (5e-5) | 0.0970 | 0.1732 |
| 6 | mT5-small | 30% (~8.5k) | 3 | Language tag prompt | 0.1029 | 0.1905 |
| **7** | **Semantic Retrieval** | **N/A** | **N/A** | **MiniLM embeddings** | **0.3846** | **0.4977** |
| 8 | mT5-small + LoRA | 30% (~8.5k) | 2 | r=16, lora_alpha=32 | 0.0453 | 0.0529 |
| 9 | mT0-small | Full (~28k) | 2 | Full data, lr=1e-4 | 0.1875 | 0.2219 |
| 10 | Hybrid Semantic+TF-IDF | N/A | N/A | Per-language weights | 0.4088 | 0.4836 |

**Best Zindi Score: 0.4977 (Experiment 7 — Semantic Retrieval)**

---

## Key Findings

- **Retrieval-based approaches outperformed generative fine-tuning** significantly. Semantic retrieval (Exp 7) and hybrid retrieval (Exp 10) both scored ~0.49 on Zindi, far above the best fine-tuned model (Exp 3: 0.229).
- **TF-IDF baseline scored 0.4926**, suggesting the task rewards exact answer retrieval more than generation.
- **Language tag prompting** improved mT5-small performance (Exp 3 > Exp 1).
- **LoRA fine-tuning (Exp 8)** underperformed due to repetition loops from removed generation constraints.
- **mT0-small vs mT5-small**: mT5-small consistently outperformed mT0-small on this task.

---

## How to Run

1. Upload `Train.csv`, `Test.csv`, `Val.csv`, and `SampleSubmission.csv` to your Colab/Kaggle environment
2. Open the desired experiment notebook
3. Update data paths if needed (default: `/content/` for Colab, `/kaggle/working/` for Kaggle)
4. Run all cells

**Dependencies:**
```
scikit-learn pandas numpy rouge-score transformers sentencepiece accelerate torch datasets sentence-transformers peft
```

---

## Languages Covered

| Code | Language | Country |
|------|----------|---------|
| Aka_Gha | Akan | Ghana |
| Amh_Eth | Amharic | Ethiopia |
| Eng_Eth | English | Ethiopia |
| Eng_Gha | English | Ghana |
| Eng_Ken | English | Kenya |
| Eng_Uga | English | Uganda |
| Lug_Uga | Luganda | Uganda |
| Swa_Ken | Swahili | Kenya |
