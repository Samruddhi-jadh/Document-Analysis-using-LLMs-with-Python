# 📄 Document QA using Hybrid LLMs

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/Samruddhi-jadh/Document-Analysis-using-LLMs-with-Python/blob/main/Document_Analysis.ipynb)
![Python Version](https://img.shields.io/badge/python-3.10-blue)

## 🔹 Overview

This project implements a **hybrid Question-Answering system for documents**.
It combines **extractive QA** (for factual questions) with **abstractive QA using RAG + LLM** (for reasoning-based questions). The system ensures answers are **clean, grounded, and confidence-scored**, minimizing hallucinations while providing meaningful insights.

> Inspired by: [Document Analysis using LLMs with Python](https://amanxai.com/2024/10/21/document-analysis-using-llms-with-python/)

---

## 🧰 Features

* PDF/Text extraction and preprocessing using `pdfplumber`
* Passage chunking and Top-K important passage selection
* LLM-based question generation (T5 QG) with deduplication
* **Hybrid QA pipeline**:

  * Extractive QA (RoBERTa SQuAD2)
  * Abstractive QA with context guard (Flan-T5 + RAG)
* Confidence scoring & fallback mechanism
* Clean, normalized, human-readable answers

---

## ⚙️ System Pipeline

**Workflow:**

```mermaid
flowchart TD
    A["PDF / Document"] --> B["Text Extraction (pdfplumber)"]
    B --> C["Text Cleaning + Normalization"]
    C --> D["Sentence Tokenization"]
    D --> E["Passage Chunking"]
    E --> F["Passage Selection (Cluster → Select → Top-K Important Passages)"]
    F --> G["Question Generation (T5 QG)"]
    G --> H["Question Deduplication"]
    H --> I["Question Classifier (Factual vs Reasoning)"]
    
    I --> J1["Extractive QA (RoBERTa SQuAD2)"]
    I --> J2["Abstractive QA (RAG + Flan-T5 + Context Guard)"]
    
    J1 --> K1["Answer + Score"]
    J2 --> K2["Answer + Evidence"]
    
    K1 --> L["Fallback Mechanism (Low Confidence Handling)"]
    K2 --> L
    L --> M["Final Answer Output (Answer + Mode + Confidence)"]
```

---

## 📂 Repository Structure

```
.
├── Sample Data/               # Sample PDFs or documents
├── notebook/          # Jupyter / Colab notebooks
├── requirements.txt    # Python dependencies
└── README.md           # Project overview and instructions
```

---

## 🚀 How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Run notebook
jupyter notebook notebooks/Document Analysis.ipynb

```

---

## 📌 Notes

* Designed to handle **large documents efficiently**
* **Hybrid QA** reduces hallucinations while maintaining reasoning
* **Confidence scores** indicate reliability of answers
* Supports **extensible modular code** for future improvements
