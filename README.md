# Project Information

**Name:** Tiwari Kanak Suraj
**ID:** 23F2005464

## Project Structure

```text
project-name
├── notebooks
│   ├── milestone-1.ipynb
│   ├── milestone-2.ipynb
│   └── final_notebook.ipynb
├── src
│   ├── train.py
│   ├── inference.py
│   └── utils.py
├── reports
│   ├── milestone-1-report.pdf
│   ├── milestone-2-report.pdf
│   └── final-report.pdf
|
├── requirements.txt
└── README.md
```
# Smart MCQ Solver Challenge

## Overview

This project was developed for the **Smart MCQ Solver Challenge**, an NLP-based Kaggle competition. The objective is to build AI models capable of predicting the correct answer for multiple-choice questions. Various traditional machine learning, deep learning, transformer-based, and retrieval-augmented approaches were implemented and compared using the official Kaggle evaluation metric (MAP@3).

---

## Problem Statement

Given a multiple-choice question consisting of a question prompt and five answer options (A–E), the objective is to rank the most probable answers. The final performance is evaluated using **Mean Average Precision at 3 (MAP@3)**.

---

## Dataset

The dataset contains:

- Question prompt
- Five candidate answers (A, B, C, D, E)
- Correct answer label

For transformer-based models, the dataset was converted into **question–answer pairs** with binary labels (Correct = 1, Incorrect = 0), allowing sequence classification using pre-trained language models.

---

## Methodology

The project explores several NLP approaches:

### 1. Baseline Models

- Dummy Classifier
- TF-IDF + Cosine Similarity

### 2. Traditional Machine Learning

- TF-IDF Feature Extraction
- Logistic Regression

### 3. Transformer Model

- BertTokenizerFast (WordPiece Tokenization)
- Fine-tuned BERT (BertForSequenceClassification)
- Distil bert 
- Hyperparameter Tuning

### 4. Custom Deep Learning Model

- Custom Word Tokenizer
- Embedding Layer
- TextCNN
- Multiple Convolution Filters
- Max Pooling
- Fully Connected Layer

An attention mechanism was also evaluated but did not improve performance.

### 5. Retrieval-Augmented Generation (RAG)

A retrieval-based pipeline was implemented using:

- Sentence Transformer
- FAISS Vector Database
- Wikipedia as External Knowledge
- Qwen Large Language Model (Inference Only) (7B Parameter model)

The retrieved Wikipedia passages were provided as additional context to improve answer ranking.

---

## Exploratory Data Analysis

The dataset was analyzed to understand:

- Class distribution
- Question length
- Answer length
- Vocabulary distribution
- Validation overlap between similar questions

A major observation was that many validation questions were highly similar to training questions, leading to optimistic validation scores. Group-based validation was explored to reduce data leakage.

---

## Results & Comparison

| Model | MAP@3 |
|------|-------:|
| Dummy Baseline | 0.35245 |
| TF-IDF + Cosine Similarity | 0.35203 |
| **TF-IDF + Logistic Regression** | **0.75477** |
| BERT (LR = 2e-5) | 0.75103 |
| BERT (LR = 3e-5) | 0.73000 |
| TextCNN | 0.70199 |
| TextCNN + Attention | 0.69210 |

---

## Key Findings

- TF-IDF with Logistic Regression achieved the highest Kaggle MAP@3 score.
- Fine-tuned BERT produced competitive results by learning contextual relationships between questions and answers.
- TextCNN demonstrated the ability to learn from scratch but could not outperform pre-trained transformers.
- Adding an attention mechanism to TextCNN did not improve performance.
- Validation strategy had a significant impact on measured performance because of highly similar questions within the dataset.

---

## Future Work

- Evaluate the complete RAG pipeline on the Kaggle hidden test dataset.
- Explore larger transformer and LLM architectures such as RoBERTa, DeBERTa, and larger Qwen models.
- Investigate improved validation strategies that reduce data leakage while preserving sufficient training data.
- Apply ensemble techniques combining traditional machine learning and transformer-based models.
- Perform more extensive hyperparameter optimization.

---

## Technologies Used

- Python
- PyTorch
- Hugging Face Transformers
- Sentence Transformers
- FAISS
- Scikit-learn
- Weights & Biases (WandB)
- Pandas
- NumPy
- Matplotlib

---

## References

- BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding (Devlin et al., 2019)
- Convolutional Neural Networks for Sentence Classification (Kim, 2014)
- Sentence-BERT (Reimers & Gurevych, 2019)
- Retrieval-Augmented Generation (Lewis et al., 2020)
- Hugging Face Transformers Documentation
- PyTorch Documentation