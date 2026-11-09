# Haske Safety Lab
## Methodology

**Prepared by:** Sadiya Muhammad Rabiu
**Date:** 2026-10-24
**Status:** Current implementation and exploratory evaluation

## 1. Research Approach

This project uses an applied machine-learning approach to develop
an experimental SMS screening prototype. The work includes dataset
preparation, text classification, model comparison, error analysis,
threshold exploration and development of an interactive interface.

The prototype is intended to flag messages for further review. It
has not been established as a reliable real-world phishing detector.

## 2. Dataset

The processed dataset is:
`data/processed/combined_unique_exploratory.csv`

It contains 6,055 SMS records:

| Label | Records | Percentage |
|---|---:|---:|
| ham | 4,993 | 82.46% |
| suspicious | 1,062 | 17.54% |
| Total | 6,055 | 100% |

The dataset combines records from UCI SMS Spam Collection and a
Mishra–Soni dataset. Data preparation included checks for missing
values, normalized duplicates and label disagreements among
overlapping records. The processed dataset had no missing values
or normalized duplicates, and the overlap check found no binary
label disagreements among 4,933 overlapping messages.

The suspicious class may include spam, promotions, adult-oriented
messages and other unsolicited content. It does not consist
exclusively of confirmed phishing messages.

## 3. Data Preparation and Splitting

The recorded stratified split used an approximately 80:20 ratio
and random state 42.

- Training set: 4,844 records
- Test set: 1,211 records
- Training labels: 3,994 ham and 850 suspicious
- Test labels: 999 ham and 212 suspicious

This test set has already been used in model exploration and
threshold comparisons. It should not be treated as a completely
untouched final evaluation set.

## 4. Text Feature Extraction

TF-IDF (Term Frequency–Inverse Document Frequency) was used to
represent message text numerically for classification. The fitted
Logistic Regression model is stored in a pipeline containing the
TF-IDF transformer and classifier.

## 5. Models Compared

### 5.1 Multinomial Naive Bayes

This lightweight classifier was used as a baseline for SMS text
classification.

### 5.2 Class-weighted Logistic Regression

A class-weighted Logistic Regression model was trained with
`max_iter=1000` and `random_state=42`. Class weighting was used
to account for the unequal number of ham and suspicious records.

## 6. Warning-Category Definitions

The bilingual synthetic SMS dataset uses the following warning categories.
Categories describe observable message features; they do not independently
prove that a message is fraudulent.

- **R1 — Unexpected prize or money:** An unexpected prize, grant, refund,
  or payment claim involving an upfront fee or unusual claiming action.
- **R2 — Pressure or urgency:** Artificial deadlines, immediate-action
  pressure, or threats such as account closure.
- **R3 — Request for secret details:** Requests for an OTP, PIN, password,
  recovery code, or another authentication secret.
- **R4 — Suspicious link:** An unverified or deceptive link, particularly
  one used to solicit sensitive information or payment.
- **R5 — Impersonation of a bank or official:** A message that presents
  itself as a trusted organization or official without adequate basis.

A message may have multiple categories separated by semicolons, such as
`R2;R3`. Use `none` when no defined warning category is evident from the
message text. A `none` category or a legitimate label does not guarantee
that a message is safe. Category assignments and labels remain subject to
human review, including fluent-speaker review of Hausa examples.

## 7. Evaluation Metrics

Evaluation included accuracy, suspicious-class precision, recall,
F1-score and the confusion matrix. Error analysis also recorded
false alarms (ham predicted as suspicious) and missed suspicious
examples (suspicious predicted as ham).

These metrics measure agreement with the dataset labels, not
independent confirmation that messages are fraudulent.

## 8. Exploratory Model Comparison

Results from the previously used test split were:

| Metric | Naive Bayes | Logistic Regression |
|---|---:|---:|
| Accuracy | 95.71% | 98.02% |
| Suspicious precision | 99.38% | 92.73% |
| Suspicious recall | 75.94% | 96.23% |
| Suspicious F1-score | Approximately 86% | 94.44% |
| False alarms | 1 | 16 |
| Missed suspicious examples | 51 | 8 |

In this experiment, Logistic Regression identified more
suspicious-labelled messages but generated more false alarms.
These exploratory results do not guarantee real-world performance.

## 9. Error Analysis

Twenty-four Logistic Regression errors were selected for review:
16 false alarms and 8 missed suspicious examples.

A manual review recorded provisional judgements for 22 examples,
with 2 unresolved. These judgements were not independently
verified ground truth. Because the examples were selected from
model errors, this review is diagnostic rather than an unbiased
performance evaluation.

The errors illustrate that legitimate personal messages and
notifications can be flagged incorrectly.

## 10. Decision Threshold Exploration

A decision threshold was explored for the interactive prototype.
The threshold comparison remains exploratory and has not established
an optimal operating point.

The threshold results are being reconciled before detailed figures
are published because evaluation records currently contain
inconsistent results. The same test split has also been examined
during model and threshold exploration.

The threshold should therefore be treated as provisional. The
model's score is not a calibrated probability that a message is
harmful. Independent evaluation is required before making claims
about threshold effectiveness or real-world performance.

## 11. Interactive Prototype

The trained pipeline was connected to a Gradio interface that
accepts a message and displays its predicted class, suspicious-class
score and a safety reminder.

Live tests showed that the interface could process messages.
They also demonstrated sensitivity to wording: a short personal
message received a much higher suspicious-class score than a
longer, similar personal message.

These examples are functional checks, not comprehensive testing.
The public demo link is temporary. Only non-sensitive sample
messages should be entered into a publicly shared interface.

## 12. Ethical and Safety Considerations

A ham result does not guarantee safety, and a suspicious result
does not prove phishing. Users should verify requests through
independently obtained official channels and never disclose
passwords or one-time passcodes in response to unsolicited messages.

Any future community study involving participants should include
appropriate consent, privacy safeguards and relevant supervisor
or institutional approval.

## 13. Limitations and Future Work

The current documented workflow does not establish representative
Hausa-language performance or completed community learning
outcomes.

Future work should include:

1. Independent testing on data not used for model selection.
2. More reliable labels distinguishing phishing, spam and legitimate
   messages.
3. Source-aware evaluation and further false-alarm analysis.
4. Separate English and Hausa evaluation where suitable labelled
   data and fluent-speaker review are available.
5. Usability and learning-outcome assessment if feasible and
   appropriately approved.
6. Model versioning and continued privacy and safety improvements.

## 14. Conclusion

The current work demonstrates an experimental workflow involving
SMS dataset preparation, baseline model comparison, error analysis,
threshold exploration and an interactive prototype. Further
independent and representative evaluation is required before
claiming reliable real-world phishing detection.

## Related Project Documents

- [Prototype Test Report](prototype_test_report.md)
- [Dataset Register](dataset_register.csv)

The processed dataset, trained model pipeline, and detailed review
records are maintained separately and are not included in this
public repository. The literature review will be added when it is
ready for publication.
