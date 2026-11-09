# Haske Safety Lab: Robustness Experiment Plan

**Research title:** Robustness of Lightweight Machine-Learning Models
for Scam SMS Detection in Hausa and English

**Status:** Experimental design — not yet executed

## 1. Research objective

Evaluate how lightweight text classifiers generalize beyond familiar
message patterns, including spelling variation, removal of obvious
scam cues, and human-written bilingual messages.

The existing English dataset is an exploratory benchmark. Its labels
represent `ham` and `suspicious`, not independently verified legitimate
and confirmed scam messages.

## 2. Models to compare

1. Multinomial Naive Bayes
2. Logistic Regression
3. Linear Support Vector Machine (Linear SVM)

All three models will use character-level TF-IDF features for the
primary comparison. Model configurations will be recorded explicitly.

## 3. Development data and preprocessing

- Begin with the existing 6,055-message exploratory dataset.
- Use the `text` column as the primary input.
- Preserve the original source and label fields.
- Audit exact and near-duplicate messages before splitting.
- Investigate source overlap and possible source-specific patterns.
- Do not assume that `suspicious` means confirmed scam.
- Fit all learned preprocessing steps within each training fold.

## 4. Model selection

- Use stratified five-fold cross-validation on eligible development data.
- Keep all messages from identified duplicate/template groups together
  in the same fold.
- Compare character n-gram TF-IDF configurations using a predefined,
  documented search space.
- Select models and settings using development data only.
- Record random seeds, package versions, parameters, and fold results.
- Do not use the final held-out evaluation sets for tuning.

If duplicate groups or source structure make ordinary stratification
inappropriate, document and use a group-aware split where feasible.

## 5. Metrics

Report accuracy, precision, recall, and F1-score, with class-specific
results and confusion matrices. Prioritize recall for the suspicious
class while also reporting false alarms. Include uncertainty intervals
where sample sizes support them.

Metrics on the existing dataset must be described as exploratory spam/
suspicious-message results, not confirmed scam-detection performance.

## 6. Bilingual data requirements

The current 15-message synthetic pilot is pending review and is not
validated training or test data.

Before bilingual claims are made:

- Have fluent Hausa reviewers assess wording and meaning.
- Review English, Hausa, and mixed-language labels independently.
- Define annotation guidance for R1-R5 warning categories.
- Resolve disagreements and document review decisions.
- Create a separate human-written gold set and stress set.
- Keep the gold and stress sets out of model selection and tuning.
- Document consent, privacy, and required approvals before collecting
  any real messages or conducting community testing.

The planned 3,000-message synthetic training corpus is not yet complete.
Do not represent the 15-message pilot as that corpus.

## 7. Robustness experiments

### A. Human-written generalization
Evaluate on reviewed human-written messages that were never used for
training, feature selection, threshold selection, or tuning.

### B. Hausa spelling variation
Create controlled variants reviewed for meaning preservation, including
relevant spelling variation and missing or altered Hausa characters.
Compare predictions against the original messages.

### C. Obvious-cue ablation
Test controlled versions with links, digits, phone numbers, and other
obvious cues removed or masked. Preserve the original examples and
record exactly which transformation was applied.

### D. Warning-category analysis
Report results for R1 unexpected prize/money, R2 urgency, R3 requests
for authentication secrets, R4 suspicious links, and R5 impersonation
of a bank or official. Categories may overlap when justified.

### E. Source and template generalization
Where source and duplicate information allow, test whether performance
drops on sources or templates not represented in training.

## 8. Existing results and leakage safeguards

The existing random 80:20 split and threshold comparisons have already
been used for exploration. They must not be presented as a new,
untouched final evaluation.

Keep existing model files and results unchanged. Save new experiments
under distinct filenames and record their dataset versions, splits,
parameters, and evaluation status.

## 9. Prototype and community evaluation

The proposal specifies Streamlit, while the experimental prototype
report describes Gradio. Resolve this difference before final delivery
or document an approved scope change.

Conduct community usability work only after required approvals and
consent arrangements are confirmed. Do not submit real personal or
sensitive messages without appropriate authorization and safeguards.

## 10. Execution gates

1. Complete dataset and label audit.
2. Confirm duplicate/source-aware split strategy.
3. Review and validate bilingual annotations.
4. Finalize development and held-out set definitions.
5. Run cross-validation and model selection.
6. Freeze selected configurations.
7. Run held-out robustness tests once.
8. Document errors, uncertainty, limitations, and reproducibility.

**Current status:** Planning and audits only. No new models trained.


## 11. Verified provenance audit findings

Read-only audits of the original source archives and combined dataset
established the following:

- The Mishra–Soni source contains 5,971 rows and 5,831 unique messages
  after lowercasing, trimming, and collapsing whitespace.
- The UCI SMS Spam Collection contains 5,572 rows and 5,157 unique
  messages under the same normalization.
- There are 4,933 shared normalized messages, 898 Mishra–Soni-only
  messages, and 224 UCI-only messages in the combined dataset.
- All 6,055 combined rows have source tags consistent with membership
  in the original datasets, and their binary labels match the originals.
- No shared messages have differing binary-label sets across the two
  sources.
- In the original Mishra–Soni data, 34 duplicate-message groups have
  `spam` versus `smishing` label disagreements. These disagreements
  disappear under the current binary mapping because both map to
  `suspicious`. Preserve this distinction in reporting.
- Recreating the documented stratified 80:20 split produced zero exact
  normalized-message overlap between training and test. This does not
  rule out near-duplicate, template, or other dependence.
- The combined dataset has no verified language column. It cannot, by
  itself, support a claim of measured Hausa-specific performance.
- The 15 synthetic bilingual pilot messages remain pending review and
  have not been validated for model training or evaluation.

## 12. Split strategy decision gate

Before new model training:

1. Build normalized-message groups and identify duplicate and plausible
   template relationships without using evaluation outcomes.
2. Determine whether groups are sufficiently reliable and numerous for
   group-aware stratified cross-validation.
3. Report class counts and group-size distributions for every proposed
   split. If group-aware stratification is infeasible, document the
   compromise and its consequences rather than silently using ordinary
   stratification.
4. Keep identical or related messages together across folds whenever
   identified reliably.
5. Do not describe either source-exclusive subset as an untouched final
   test set: the existing combined corpus has already been used in
   exploratory model development and threshold comparisons.
6. Define and freeze a new evaluation protocol before fitting new models.
   Save assignments and outputs under new, versioned filenames.
7. Treat source-exclusive analysis as a sensitivity analysis, not as
   independent external validation, unless the data-use history and
   independence requirements can be demonstrated.

No new models have been trained as part of these audits.
