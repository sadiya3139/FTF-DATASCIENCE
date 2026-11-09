

# HASKE SAFETY LAB

## Project Title
**Robustness of Lightweight Machine-Learning Models for Scam SMS Detection in Hausa and English**

### Programme Information
- **Organisation:** FutureMAP Foundation
- **Programme:** Future Tech Fellowship
- **Track:** Data Science
- **Project Category:** Cybersecurity and Machine Learning
- **Research Focus:** SMS Scam Detection

## 1. Project Overview

Haske Safety Lab is a data science and cybersecurity research project that investigates the use of lightweight machine-learning models to identify suspicious SMS messages.

The project compares three machine-learning algorithms: Multinomial Naive Bayes, Logistic Regression, and Linear Support Vector Machine (Linear SVM).

It also explores model robustness under selected text variations, Hausa spelling changes, and the removal of common suspicious-message indicators.

A Streamlit prototype was developed to demonstrate SMS classification and supplementary warning signs.

Although the project focuses on Hausa and English in its research direction, the available combined dataset is English-heavy. The Hausa experiments are exploratory pilots and do not establish reliable bilingual detection performance.

## 2. Problem Statement

SMS scams and phishing messages are increasingly used to deceive mobile phone users through fake offers, suspicious links, urgent requests, and attempts to obtain sensitive information.

Many users may find it difficult to recognise these messages, especially when scammers change their wording or remove obvious warning signs.

This project investigates whether lightweight machine-learning models can help identify suspicious SMS messages and examines their limitations under different text conditions.

## 3. Project Aim

To investigate the robustness of lightweight machine-learning models for suspicious SMS detection, with particular attention to model comparison, spelling variation, warning signs, and the challenges of extending detection to Hausa and English messages.

## 4. Specific Objectives

1. To prepare and document a combined SMS dataset for the experimental evaluation of lightweight machine-learning models for suspicious message classification.
2. To compare Multinomial Naive Bayes, Logistic Regression, and Linear SVM using character-level TF-IDF features.
3. To conduct an exploratory synthetic-to-human message review.
4. To explore prediction stability under selected Hausa spelling and text variations.
5. To examine how removing selected warning cues affects model predictions.
6. To analyse five supplementary warning-sign rule groups (R1–R5).
7. To develop a Streamlit prototype for demonstrating suspicious SMS classification.

## 5. Research Questions

1. How do the three selected machine-learning models compare in suspicious SMS classification?
2. What can a small synthetic-to-human message pilot reveal about model generalisation?
3. How stable are model predictions when selected Hausa spelling variations are introduced?
4. How does removing suspicious-message indicators affect model detection?
5. How frequently do the R1–R5 warning signs occur in legitimate and suspicious messages?
6. How can the trained model be demonstrated through a lightweight application?

## 6. Dataset Description

The project combines data from two publicly available datasets:

- UCI SMS Spam Collection
- Mishra–Soni SMS Phishing Dataset

The processed dataset contains:

- Total messages: 6,055
- Ham messages: 4,993 (82.46%)
- Suspicious messages: 1,062 (17.54%)

The dataset contains message text, labels, and source information.

**Important dataset limitation:** The dataset is English-heavy and does not contain a verified language column. Its labels were inherited from the original sources and were not independently re-annotated for this project.

## 7. Tools and Technologies

- Python
- Pandas
- Scikit-learn
- TF-IDF Vectorisation
- Multinomial Naive Bayes
- Logistic Regression
- Linear Support Vector Machine
- Streamlit
- Joblib
- GitHub
- Jupyter Notebook / Google Colab

## 8. Methodology

The project followed an experimental machine-learning approach.

### Data Preparation
SMS datasets were combined, cleaned, and prepared for model development.

### Feature Extraction
Character-level TF-IDF was used with character n-grams ranging from 3 to 5 characters.

### Model Development
Three lightweight machine-learning models were trained and compared:

- Multinomial Naive Bayes
- Logistic Regression
- Linear SVM

### Model Evaluation
The comparative experiment used five random seeds and five folds per seed, producing 75 model-fold runs across the three models.

Evaluation metrics included:
- Accuracy
- Precision
- Recall
- F1-score

### Robustness Experiments
Additional exploratory tests examined:
- Synthetic-to-human message review
- Hausa spelling variations
- Removal of selected suspicious-message indicators
- R1–R5 warning-sign analysis

### Prototype Development
A Streamlit application was developed to demonstrate message classification and supplementary warning-sign checks.

## 9. Key Experimental Results

| Model | Mean Accuracy | Suspicious Precision | Suspicious Recall | Suspicious F1 |
|---|---:|---:|---:|---:|
| Linear SVM | 98.84% | 98.75% | 94.55% | 96.60% |
| Logistic Regression | 98.54% | 97.58% | 94.01% | 95.75% |
| Multinomial Naive Bayes | 94.77% | 99.86% | 70.29% | 82.48% |

Linear SVM achieved the strongest overall balance across the reported metrics.

Multinomial Naive Bayes achieved the highest suspicious-message precision but had lower recall.

These results describe the experimental dataset and evaluation procedure; they do not guarantee performance on real-world messages.

## 10. Hausa Spelling Variation Pilot

A small exploratory pilot examined 50 rows generated from 10 Hausa message templates.

Seventeen text-changing variants were tested. The model's predictions remained unchanged across the 17 variants, but all original and variant predictions were classified as ham.

This result does not demonstrate successful Hausa scam detection. It highlights the need for a larger Hausa-English dataset, fluent Hausa-speaker annotation, and independent evaluation.

## 11. Project Limitations

- The available dataset is English-heavy.
- Hausa-language evaluation is limited to a small pilot.
- The source labels were not independently verified.
- The synthetic-to-human review was small and involved one reviewer.
- Cue-removal tests used a single held-out split.
- The prototype is a research demonstration, not a production security system.

## 12. Future Improvements

- Develop a larger and more diverse Hausa-English SMS dataset.
- Collaborate with fluent Hausa speakers for message annotation.
- Include regional expressions, informal spelling, and code-switching.
- Conduct independent external model evaluation.
- Improve the prototype and its privacy safeguards.
- Carry out structured community testing with intended users.

## 13. Responsible Use

The prototype is intended for research and educational demonstration. A model prediction should not be treated as proof that a message is safe or fraudulent.

Users should avoid entering passwords, OTPs, banking information, or other sensitive personal details into the application.

## 14. Acknowledgement

This project was developed under the Future Tech Fellowship – Data Science Track, organised by FutureMAP Foundation.

The project acknowledges the value of the programme's practical data science training and learning activities.

## 15. Project Repository

GitHub: https://github.com/sadiya3139/FTF-DATASCIENCE

**Project Name:** Haske Safety Lab

**Research Theme:** Robustness of Lightweight Machine-Learning Models for Scam SMS Detection in Hausa and English.
