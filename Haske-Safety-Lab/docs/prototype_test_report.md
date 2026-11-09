# Haske Safety Lab
## SMS Screening Prototype Test Report

**Report date:** 2026-10-24
**Project:** Haske Safety Lab
**Purpose:** Initial evaluation of an experimental SMS screening prototype.

---

## 1. Project Overview

Haske Safety Lab is an experimental machine-learning project designed
to screen SMS messages for patterns associated with a dataset's
suspicious class. It is intended to support awareness and further
review, not to make definitive security decisions.

The prototype uses TF-IDF text features and a Logistic Regression
classifier. The interface was built using Gradio and tested through
a temporary public demo link.

## 2. Dataset and Model

- Total processed SMS records: 6,055
- Ham records: 4,993
- Suspicious records: 1,062
- Selected model: Class-weighted Logistic Regression
- Decision threshold: provisional; threshold selection remains exploratory

The dataset's suspicious class may include spam, promotional,
adult-oriented, or other unsolicited messages. It should not be
interpreted as a collection of confirmed phishing messages only.

## 3. Initial Model Evaluation

On the exploratory held-out test split, the Logistic Regression
model achieved:

- Accuracy: 98.02%
- Suspicious-class precision: 92.73%
- Suspicious-class recall: 96.23%
- Suspicious-class F1-score: 94.44%
- False alarms: 16
- Missed suspicious-class examples: 8

These figures describe the current exploratory evaluation, not
guaranteed performance in real-world use. The test split has already
been used during model exploration, so an independent evaluation
is still required. Detailed threshold comparisons are being withheld
from publication while inconsistent evaluation records are reconciled.

## 4. Live Prototype Tests

### Test A: Prize message

**Input:** "Congratulations! You won a free prize. Reply now to claim."

- Predicted class: Suspicious
- Suspicious-class score: 96.50%
- Observation: The message was flagged for further review.

### Test B: Ordinary personal message

**Input:** "I'm at home. Please call me when you arrive."

- Predicted class: Ham
- Suspicious-class score: 22.78%
- Observation: The message was classified below the 55% threshold.

### Related earlier exploratory test

**Input:** "I'm at home. Please call"

- Predicted class: Suspicious
- Suspicious-class score: 71.75%
- Observation: The shorter wording received a substantially higher
  score than the longer personal message.

These tests show that model output can vary considerably with wording.
They are illustrative examples, not a comprehensive performance test.

## 5. Limitations and Risks

1. A ham result does not guarantee that a message is safe.
2. A suspicious result does not prove that a message is phishing.
3. The model may flag legitimate personal messages or notifications.
4. The dataset labels may represent unsolicited messages beyond phishing.
5. The suspicious-class score is not a calibrated probability of harm.
6. The dataset and test results may not represent current SMS threats,
   Hausa messages, or the full range of Nigerian communication styles.
7. Independent, source-aware testing and more representative data
   are required before any real-world security use.
8. The public Gradio share link is temporary and should only be used
   with non-sensitive sample messages.

## 6. Recommended Next Steps

- Preserve the current model and record its version.
- Expand testing with legitimate and suspicious examples.
- Review false positives and false negatives.
- Evaluate Hausa and English messages separately when suitable data
  and reliable labels are available.
- Conduct independent evaluation on data not used during model
  selection or threshold tuning.
- Improve user guidance and privacy safeguards.
- Avoid presenting the prototype as a definitive phishing detector.

## 7. Conclusion

The initial prototype demonstrates that an SMS text-classification
model can be connected to an interactive interface and used to flag
messages for further review. The tests also reveal wording sensitivity
and potential false alarms. Further validation is necessary before
drawing conclusions about real-world effectiveness.

**Responsible-use statement:** Haske Safety Lab is an experimental
research prototype for awareness and screening. Users should verify
suspicious requests through official channels and should not rely on
the model alone to determine whether a message is safe.
