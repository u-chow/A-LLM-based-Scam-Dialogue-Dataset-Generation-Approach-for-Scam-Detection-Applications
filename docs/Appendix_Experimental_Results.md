# Appendix A. Experimental Results (Full Version)

This appendix provides the complete experimental results and extended descriptions that were summarized in the main text.  
It presents detailed analyses of each experimental phase, including model-specific observations, evaluation metrics, and validation figures.  
All experiments were conducted ethically under controlled settings for academic research purposes.

---

## A.1 Experimental Environment

All experiments were conducted on **Google Colab**, a cloud-based development platform that provides GPU and TPU resources for model evaluation.  
Due to session memory constraints, dual-role simulations were executed using **two synchronized Colab notebooks** communicating via a shared Google Drive directory.  
This directory served as the data bridge for prompt files, generated dialogues, and memory logs.

Open-source models **Meta-LLaMA-2-Chat-7B** and **Meta-LLaMA-3-8B-Instruct** were downloaded from Hugging Face and locally loaded from Google Drive during runtime,  
while **GPT-4 (gpt-4-1106-preview)** was accessed via the OpenAI API.  

To maintain contextual coherence, a **retrieval-augmented memory module** named `ConversationMemory` was implemented using  
[`all-MiniLM-L6-v2`](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) embeddings and FAISS indexing for fast semantic retrieval.  
All generated data, logs, and evaluation outputs were stored automatically in structured folders for reproducibility.

---

## A.2 Single-Model Generation Testing

This phase evaluated four models under identical prompt structures, dialogue turn limits, and memory settings:

- **Meta-LLaMA-2-Chat-7B**  
  Produced fluent text but frequently disclosed its AI identity or refused scam-like prompts.  
  Its strong safety filters led to early termination and incoherent responses.

- **Meta-LLaMA-3-8B-Instruct**  
  Showed better fluency but unstable tone and persona.  
  Often produced vague avoidance responses and failed to complete full scam strategies.

- **GPT-4 (Baseline)**  
  Executed coherent four-phase scam strategies (trust-building → urgency creation → sensitive data elicitation → fallback).  
  Successfully led users to disclose passwords, confirming its strong control and realism.

- **GPT-4 (Anti-fraud Prompt)**  
  Integrated educational cues based on Taipei City’s *“Three Don’ts”* principle (*don’t panic, don’t be greedy, don’t trust blindly*).  
  User resistance delayed but did not fully prevent disclosure, showing that awareness helps but is not sufficient.

| Model | Prompt Setting | Induction Outcome | Role Stability |
|:------|:----------------|:------------------|:----------------|
| Meta-LLaMA-2-Chat-7B | Default | Failed, AI identity disclosed | Low |
| Meta-LLaMA-3-8B-Instruct | Default | Failed, inconsistent tone | Low |
| GPT-4 | Baseline | Successfully induced full password | High |
| GPT-4 | Anti-fraud | Delayed but successful inducement | Medium–High |

**Evaluation Criteria**

- **Induction Outcome:** Successful if the scammer induced full password disclosure in one simulation round.  
- **Role Stability:** Graded as *Low / Medium / High* based on:
  - Persona consistency  
  - Strategic coherence  
  - Safety-trigger incidence (refusal or AI self-disclosure)

---

## A.3 Dual-role Interaction Simulation

To evaluate cross-model interactions, seven scammer–user pairings were tested: LLaMA-2, LLaMA-3, and GPT-4.  
Metrics included **inducement success rate** and **average generation time**.

| Scammer \\ User | Meta-LLaMA-2 | Meta-LLaMA-3 | GPT-4 |
|:----------------|:-------------:|:-------------:|:-----:|
| Meta-LLaMA-2 | 0% (113.6s) | – | 0% (113.3s) |
| Meta-LLaMA-3 | – | 0% (245.9s) | 0% (128.9s) |
| GPT-4 | 60% (114.7s) | 40% (132.3s) | **70% (67.7s)** |

**Findings:**
- All open-source models failed to produce coherent multi-turn scams, often looping or revealing their AI nature.  
- GPT-4 achieved the best performance, with **70% success** in self-play simulations (GPT-4 × GPT-4).  
- Mixed GPT-4 × LLaMA setups produced partial results but lacked semantic coherence, mainly due to prompt parsing issues.

---

## A.4 Corpus Construction and Naturalness Evaluation

A hybrid corpus of **940 dialogues** (452 natural, 488 simulated) was constructed using:
- **Simulated:** GPT-4-generated scam dialogues  
- **Natural:** [DailyDialog](https://huggingface.co/datasets/daily_dialog) and [Blended Skill Talk (BST)](https://parl.ai/projects/bst/)

### Classifier Validation
A **DistilBERT-based binary classifier** (`distilbert-base-uncased`) was fine-tuned to detect simulated vs. natural dialogues.

| Metric | Simulated | Natural | Overall |
|:--------|:-----------|:----------|:----------|
| Precision | 0.9792 | 0.9565 | – |
| Recall | 0.9592 | 0.9778 | – |
| F1 Score | – | – | **0.9681** |

On 336 unseen GPT-4 dialogues, the classifier **misclassified 100%** as natural, indicating that the generated content was linguistically indistinguishable from real dialogues.

### Human Evaluation
A Likert-scale survey (1–5) rated dialogue **naturalness** and **contextual plausibility**.  
Average rating: **3.55 / 5 (71.0%)**, suggesting moderate-to-high perceived realism.

---

## A.5 Large-scale Corpus Validation and Automated Evaluation

The framework was scaled to generate **904 GPT-4 dialogues** totaling **25,126 utterances**.  
Automated evaluation reused the trained DistilBERT classifier for large-scale testing.

| Metric | Value |
|:-------|:------|
| Utterances classified as natural | **96.9%** |
| Utterances classified as simulated | 3.1% |

### Figures
- **Figure A1.** Confusion Matrix on 904 dialogues  
- **Figure A2.** Prediction distribution (Pie Chart)

These results confirm that the classifier failed to distinguish large-scale simulated data, demonstrating the corpus’s **linguistic realism** and **detection challenge**.

---

## A.6 Summary

Across all phases:
- **GPT-4 consistently outperformed open-source models**, maintaining coherent personas and persuasive language.  
- The **ConversationMemory** module significantly improved context continuity and strategic realism.  
- Both classifier and human evaluation confirmed that the simulated dialogues were **indistinguishable from human-written text**.  

This appendix provides detailed evidence supporting the scalability, reproducibility, and authenticity of the proposed **LLM-based scam dialogue generation framework**.

---

> **Citation:**  
> Cheng, Y.-C., & Chi, B.-W. (2025). *A LLM-based Scam Dialogue Dataset Generation Approach for Scam Detection Applications.*  
> Supplementary Appendix – Experimental Results.  
> GitHub Repository: [https://github.com/uchow/LLM-ScamDialogue-Framework](https://github.com/uchow/LLM-ScamDialogue-Framework)
