# Haske Safety Lab

## Project Title
Robustness of Lightweight Machine-Learning Models for Scam SMS Detection in Hausa and English.

## Project Overview
Haske Safety Lab investigates lightweight machine-learning approaches for identifying potentially suspicious SMS messages. The project compares Multinomial Naive Bayes, Logistic Regression, and Linear Support Vector Machine using character-level TF-IDF features.

The project also examines synthetic-to-human generalisation, Hausa spelling variation, warning-sign indicators, and the effect of removing selected message cues.

## Dataset Overview
The exploratory combined dataset contains 6,055 SMS records:
- Ham: 4,993 (82.46%)
- Suspicious: 1,062 (17.54%)

The dataset combines the UCI SMS Spam Collection and the Mishra–Soni dataset. It is English-heavy, and labels were inherited from source datasets rather than independently verified.

The original datasets and processed message-level data are not included in this public repository pending licence and redistribution checks.

## Model Comparison
Three models were evaluated using character n-gram TF-IDF features and a repeated group-aware evaluation protocol (5 seeds × 5 folds).

| Model | Mean accuracy | Suspicious precision | Suspicious recall | Suspicious F1 |
|---|---:|---:|---:|---:|
| Linear SVM | 98.84% | 98.75% | 94.55% | 96.60% |
| Logistic Regression | 98.54% | 97.58% | 94.01% | 95.75% |
| Multinomial Naive Bayes | 94.77% | 99.86% | 70.29% | 82.48% |

Linear SVM achieved the strongest overall balance. Multinomial Naive Bayes had the highest suspicious-message precision but lower recall.

## Robustness Experiments

### Cue Removal
On one held-out split:
- Link removal: 31 affected messages; detections decreased from 31 to 27.
- Long-number removal: 135 affected messages; detections decreased from 135 to 128.
- Urgency removal: 27 affected messages; detections remained at 27.
- Credential-request removal: no matching test messages were available.

These findings apply only to the affected subsets and this single split.

### Hausa Spelling Variation
Seventeen text-changing spelling variants were examined. Predictions remained unchanged, but all original and variant messages were predicted as ham. This is prediction stability, not evidence of successful scam detection. The pilot had one reviewer and requires further validation by Hausa speakers.

### R1–R5 Warning-Sign Analysis
At least one warning-sign rule was triggered for:
- 79 of 216 suspicious messages (36.57%).
- 18 of 999 ham messages (1.80%).

The rules are supplementary indicators and should not be used as a standalone classifier.

## Prototype
The Streamlit prototype is in `app.py`.

The deployment model is stored at:
`results/linear_svm_sms_model_final.joblib`

This model was trained on the full available dataset for demonstration. It is not an independent evaluation model.

## Run the Application
Install dependencies:

```bash
pip install -r requirements.txt
```

Start the application:

```bash
streamlit run app.py
```

## Project Limitations
- The dataset is English-heavy and does not establish robust bilingual performance.
- Source labels were not independently verified.
- The Hausa spelling pilot is small and was not independently adjudicated.
- No completed community review with women and young adults in Kano is claimed.
- Cue-removal results use one held-out split.
- Warning-sign rules are supplementary and may miss messages that use different wording.
- The source datasets and message-level records are excluded pending licence and privacy review.

## Responsible Use
This prototype is an educational research tool. Its predictions may be wrong. Users should not rely on it as the sole basis for financial, security, or other important decisions. Avoid submitting private or sensitive messages.

## Project Structure
- `app.py` — Streamlit prototype.
- `requirements.txt` — Python dependencies.
- `docs/` — methodology, protocols, and research documentation.
- `results/` — aggregate experiment results and model artefacts.

## Author
Sadiya Muhammad Rabiu

Haske Safety Lab
