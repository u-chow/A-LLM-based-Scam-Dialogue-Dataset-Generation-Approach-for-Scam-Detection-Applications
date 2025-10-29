# LLM-based Scam Dialogue Dataset Generation Framework

**Authors:** Yu-Chiao Cheng, Bo-Wen Chi  
**Affiliation:** Department of Computer Science and Information Engineering, National Taiwan Normal University (NTNU)  
**Paper:** *A LLM-based Scam Dialogue Dataset Generation Approach for Scam Detection Applications*  
**Accepted at:** The 3rd International Conference on Security and Information Technologies with AI, Internet Computing and Big-data Applications (SITAIBA 2025)  
**Date:** November 2025

---

## Overview

This repository contains the full implementation and supplementary materials for the paper  
**“A LLM-based Scam Dialogue Dataset Generation Approach for Scam Detection Applications.”**  
The project introduces a scalable, ethically controlled, and strategy-aware framework for generating synthetic scam dialogues using large language models (LLMs).  
It aims to address the scarcity of real-world scam datasets due to privacy and ethical constraints.

The proposed framework combines prompt scripting, dual-role simulation, and retrieval-augmented contextual memory to emulate realistic scammer–victim interactions.  
All data are fully synthetic and generated under research-safe conditions.

---
## Experimental Highlights

| Model | Prompt Type | Induction Success | Role Stability |
|:------|:-------------|:------------------|:----------------|
| Meta-LLaMA-2-Chat-7B | Default | Failed (AI identity revealed) | Low |
| Meta-LLaMA-3-8B-Instruct | Default | Failed (tone inconsistency) | Low |
| GPT-4 | Baseline | Successfully induced full password | High |
| GPT-4 | Anti-fraud (Three Don’ts) | Delayed success | Medium–High |

- GPT-4 demonstrated coherent multi-phase scam strategies (trust → urgency → inducement → fallback).  
- Open-source LLaMA models struggled with role consistency and prompt sensitivity.  
- Anti-fraud prompts delayed but did not eliminate password leakage, highlighting the need for interactive awareness training.

### Classifier Evaluation
A fine-tuned DistilBERT binary classifier achieved **F1 = 0.9681** when distinguishing simulated vs. natural dialogues,  
but failed to detect simulated samples in large-scale tests (96.9 % misclassified as natural).

### Human Evaluation
Anonymous evaluators rated dialogue realism at **3.55 / 5 (71.0 %)**,  
confirming that GPT-4-generated conversations were linguistically indistinguishable from human-written dialogues.

---

## Key Findings

- Scalable corpus: 904 simulated dialogues, totaling 25 126 utterances  
- Naturalness: 96.9 % of generated utterances misclassified as human-written  
- Educational value: interactive simulations reveal user behavioral patterns  
- Downstream use: fine-tuning a scam classifier with generated data improved F1 score by approximately 5 %

For detailed results, see  
[Appendix A – Experimental Results (Full Version)](./docs/Appendix_Experimental_Results.md)

---

## Citation

If you use this repository or reference this research, please cite:

@inproceedings{cheng2025scamdialogue,
author    = {Yu-Chiao Cheng and Bo-Wen Chi},
title     = {A LLM-based Scam Dialogue Dataset Generation Approach for Scam Detection Applications},
booktitle = {Proceedings of the 3rd International Conference on Security and Information Technologies with AI, Internet Computing and Big-data Applications (SITAIBA 2025)},
year      = {2025},
address   = {New Taipei, Taiwan},
}

---

## Ethical Statement

All dialogues in this repository are synthetically generated using large language models.  
No real personal or sensitive data are used.  
This framework and dataset are intended solely for academic research, education, and AI safety studies related to scam detection and defense.

---

## Supplementary Resources

- [Appendix A – Full Experimental Results](./Appendix_Experimental_Results.md)  
- [Conference Website – SITAIBA 2025](https://sitaiba-2025.esam.io/submission_format.html)  
- [Hugging Face Models: LLaMA-2, LLaMA-3, MiniLM-L6-v2](https://huggingface.co/)  
- [FAISS Library](https://github.com/facebookresearch/faiss)

---

© 2025 Yu-Chiao Cheng and Bo-Wen Chi. Licensed for academic and non-commercial research use only.
