# Similarity-Group and Fold-Assignment Validation

## Purpose

This validation checks whether messages belonging to the same
approximate similarity group were distributed across different
validation folds.

## Dataset and Grouping Summary

- Dataset size: 6,055 messages
- Approximate similarity groups: 5,731
- Similarity threshold: 0.90
- Largest approximate group: 6 messages
- Groups with mixed labels: 0

## Validation Procedure

The approximate group assignments were compared with the
five-fold validation assignments for five random seeds:

17, 23, 42, 101 and 2026.

Each dataset row was matched using its row index. The check
examined whether any approximate similarity group appeared
in more than one validation fold within a seed.

## Results

No approximate similarity group was found across multiple
validation folds for any of the five seeds.

All 6,055 rows had group assignments for each seed.

## Interpretation and Limitations

The check found no cross-fold separation of messages belonging
to the same identified approximate similarity group.

This provides evidence that the validation procedure accounted
for the similarity groups identified by the grouping process.

However, it does not establish that every semantically similar
message was identified or rule out every possible source of
data leakage.

## Evidence Files

- fold_assignments_all_seeds.csv
- approximate_group_assignments.csv
- dataset_audit.json
