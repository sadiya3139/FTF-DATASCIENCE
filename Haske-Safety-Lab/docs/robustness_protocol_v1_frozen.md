# Haske Safety Lab — Frozen Robustness Experiment Protocol v1

**Research title:** Robustness of Lightweight Machine-Learning Models for Scam SMS Detection in Hausa and English  
**Protocol status:** Frozen v1.0; approved for the specified exploratory experiment, subject to the execution gates below.  
**Protocol version:** 1.0  
**Scope of current experiment:** Exploratory English SMS classification using the existing 6,055-row combined corpus. This experiment does **not** measure Hausa or mixed-language performance.

## 1. Purpose and boundaries

This protocol specifies a reproducible comparison of Multinomial Naive Bayes (MNB), Logistic Regression (LR), and Linear Support Vector Machine (Linear SVM) using character-level TF-IDF features. It is designed to reduce leakage from detected near-duplicate/template messages.

The existing corpus has 6,055 rows: 4,993 `ham` and 1,062 `suspicious`. The labels are inherited from public SMS spam/smishing datasets and do not establish that every `suspicious` message is a confirmed scam. Results must be described as **exploratory suspicious/spam-message classification**, not verified scam-detection performance.

The corpus has no verified language column. The current 15-message English/Hausa/Mixed synthetic pilot remains pending review and is not eligible for training, tuning, or evaluation. No Hausa-specific or bilingual performance claim may be made from this experiment.

## 2. Data inputs and immutable-source rule

Primary input: `data/processed/combined_unique_exploratory.csv`

Expected columns: `comparison_text`, `text`, `label`, `source`.

Before execution, verify the file exists and matches the audited counts. Do not modify or overwrite raw/processed data. Use `text` as model input and `label` as target. Fit all text transformations inside a scikit-learn pipeline so vectorizers are fitted only on each training fold.

Do not use `source` as a predictive feature. Keep source information only for post-hoc descriptive/sensitivity analyses.

## 3. Approximate template grouping

The prior audit used character TF-IDF (character 3–5 grams, `min_df=2`, `sublinear_tf=True`, `max_features=100000`), cosine nearest neighbours (`k=min(10, n)`), and similarity threshold `>=0.90`. Union-find connected components produced 5,731 approximate groups: 5,488 singleton groups and 243 non-singleton groups containing 567 messages; the largest component contained 6 messages. No non-singleton component had mixed binary labels.

This grouping is **approximate and not exhaustive**: only a limited number of nearest neighbours per message were inspected. It may miss related templates, and connected components can chain pairwise similarities. Record the grouping code, threshold, vectorizer settings, package versions, and resulting group assignments with the experiment outputs. Do not claim all related templates were identified.

If the graph construction or group counts differ from the audited results, stop and investigate before training.

## 4. Cross-validation design

Use `StratifiedGroupKFold(n_splits=5, shuffle=True, random_state=SEED)` on the full development corpus, with the same group assignments for all three models for each seed.

**Five fixed seeds:** `42`, `17`, `23`, `101`, `2026`.

For each seed:
1. Construct the five group-aware folds.
2. Confirm every row is validation exactly once across the five folds.
3. Confirm no group ID occurs in both training and validation within any fold.
4. Report each fold's row count and ham/suspicious counts.
5. If a fold lacks either class or the split fails, stop and document the issue; do not silently substitute ordinary stratification.

This yields 25 fold evaluations per model (5 folds × 5 seeds). The same fold assignments must be used for MNB, LR, and Linear SVM for fair comparisons.

These folds provide internal development estimates only. Because this corpus has already been used for exploratory training and threshold comparisons, it is not an untouched external or final test set. Do not call any source-exclusive subset an untouched final test set.

## 5. Fixed feature-extraction configuration

Use a single scikit-learn `Pipeline` per model so TF-IDF is fitted only on each fold's training portion.

`TfidfVectorizer`:
- `analyzer="char"`
- `ngram_range=(3, 5)`
- `min_df=2`
- `sublinear_tf=True`
- `max_features=100000`
- `lowercase=True`
- `strip_accents=None`
- all other settings left at documented scikit-learn defaults

The `max_features=100000` cap and character 3–5-gram range are fixed before comparison. Do not tune the vectorizer on validation folds in this protocol. If a later hyperparameter search is needed, create a new protocol version and use nested/group-aware model selection without using the held-out bilingual sets.

## 6. Fixed model configurations

Use the same TF-IDF configuration for all models.

### Model A — Multinomial Naive Bayes
`MultinomialNB(alpha=1.0, fit_prior=True)`

### Model B — Logistic Regression
`LogisticRegression(C=1.0, class_weight="balanced", max_iter=2000, solver="liblinear", random_state=SEED)`

### Model C — Linear SVM
`LinearSVC(C=1.0, class_weight="balanced", random_state=SEED, max_iter=5000)`

The classifier seed must be set to the same run seed where supported. Record any convergence warnings; do not silently ignore them. Do not change model parameters after seeing validation results without issuing a new protocol version.

No probability calibration is planned. Do not compare uncalibrated decision scores as if they were probabilities.

## 7. Prediction rules and metrics

Target labels are `ham` and `suspicious`. Treat `suspicious` as the positive class for class-specific precision, recall, and F1.

For each fold and seed, report:
- accuracy;
- suspicious precision, recall, and F1;
- ham precision, recall, and F1;
- confusion matrix in a fixed label order `[ham, suspicious]`;
- false alarms (ham predicted suspicious);
- missed suspicious messages (suspicious predicted ham);
- support for each class;
- fit warnings/errors and run metadata.

For MNB and LR, use the estimator's default class prediction (`predict`) without threshold tuning. For Linear SVM, use its default `predict` decision boundary. Do not apply the previously explored LR threshold of 0.55 to this comparison.

Report fold-level results and aggregated mean and standard deviation across the 25 fold evaluations, alongside per-seed summaries. Do not pool all repeated out-of-fold predictions as though each row had only one independent prediction: each row is validated once per seed. If confidence intervals are reported, state the method and unit of resampling; do not treat correlated folds or repeated-seed predictions as independent observations. The primary comparison should be descriptive, not a claim of independent external validation.

Prioritize suspicious-class recall, while reporting false alarms and missed suspicious messages. No single metric alone determines the best model.

## 8. Model selection rule

Use the predeclared metrics, with emphasis on suspicious recall and the associated false-alarm burden. Choose the preferred development model only after examining all folds and seeds. Report trade-offs rather than selecting solely by accuracy.

No threshold tuning, feature selection, or model selection may use the future human-written gold set or stress set. If the project later requires tuning, perform it using development data only and freeze the resulting settings before held-out evaluation.

## 9. Robustness experiments not covered by this run

These are separate future stages and must not be claimed as completed by the cross-validation experiment:

1. **Human-written generalization:** a reviewed human-written gold set and stress set, excluded from all training and tuning.
2. **Hausa spelling variation:** meaning-preserving, fluent-speaker-reviewed variants.
3. **Obvious-cue ablation:** controlled masking/removal of links, digits, phone numbers, and other cues; preserve originals and log each transformation.
4. **Warning-category analysis:** R1 prize/money; R2 urgency; R3 requests for authentication secrets; R4 suspicious links; R5 impersonation of a bank/official. Apply only after reviewed annotation rules and labels exist.
5. **Source/template generalization:** exploratory sensitivity analysis only, with explicit acknowledgment of heavy source overlap and prior use of the corpus.

The bilingual pilot's 15 messages are pending review and too small for reliable performance estimates. They must not be represented as the planned gold/stress set.

## 10. Reproducibility and output naming

Do not overwrite existing baseline, LR, threshold, error-analysis, or model files.

Write new outputs under a versioned directory, for example `results/robustness_v1/`.

Suggested artifacts:
- `protocol_snapshot.md`
- `environment_versions.txt`
- `dataset_audit.json`
- `approximate_group_assignments.csv`
- `fold_assignments_seed_42.csv` (and corresponding files for the other seeds)
- `fold_metrics.csv`
- `seed_summary.csv`
- `aggregate_summary.csv`
- `confusion_matrices.csv`
- `run_manifest.json`
- `warnings.log`

Save the exact code or notebook used, the fixed seeds, package versions, input file checksum, grouping parameters, fold assignments, and model configurations. Record timestamp and any deviations. If any setting or data changes, stop and create a new protocol version rather than silently changing this one.

## 11. Execution gates

Do not begin model fitting until:
- the frozen protocol is saved and its settings are verified;
- the data checksum and expected row/label counts are recorded;
- the approximate group graph is reconstructed and its counts match the audit;
- fold assignments are generated and checked for row coverage, class presence, and group leakage;
- output paths are confirmed not to overwrite existing artifacts.

After fitting, inspect convergence/errors and validate all metrics before interpretation.

## 12. Limitations to state in reporting

- Existing labels indicate public-dataset ham/spam/smishing-derived categories, not independently verified scams.
- The combined sources overlap heavily; they are not independent external datasets.
- Approximate near-duplicate grouping is limited to nearest-neighbour candidates and may miss related templates.
- The current combined dataset has no verified language column; the results apply to this corpus, not to measured Hausa or mixed-language performance.
- The existing corpus has already been used for exploratory development and threshold comparisons; cross-validation is not a new untouched final test.
- The synthetic bilingual pilot has 15 pending-review examples and is not a validated evaluation set.
- The proposal specifies a Streamlit prototype while an earlier prototype report describes Gradio; resolve this implementation difference separately.

## 13. Protocol freeze record

- **Approval/freeze date:** 2026-10-25 (UTC date)
- **Input dataset SHA-256:** `58b5482ef6afd0492310d61591344123198629e25a9d05091d4004835a6643b3`
- **Git commit at freeze:** `460d640415dd4645384d07b4c6c3d9e4df62ea8c`
- **Environment:** Python 3.13.16, pandas 2.2.3, NumPy 2.1.3, scikit-learn 1.6.1
- **Protocol approval:** User reviewed and approved Protocol v1.0 in chat.
- **Deviations at freeze:** None declared.
- **Training status:** No models trained by this freeze step.

**No new models are trained by preparing this protocol document.**
