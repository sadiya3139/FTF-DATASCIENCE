# Haske Safety Lab — Bilingual Pilot Findings (Corrected v2)

## Purpose
This is a small exploratory pilot using fictional English and Hausa messages.
It is not an independent or representative benchmark.

## Verified results

| Language | Matches | Disagreements | Compared |
|---|---:|---:|---:|
| English | 6 | 3 | 9 |
| Hausa | 4 | 5 | 9 |
| **Total** | **10** | **8** | **18** |

Two messages labelled uncertain were excluded from binary comparison.

## Interpretation and limitations
- The pilot contains only 20 fictional messages and one reviewer.
- Results describe this pilot only, not expected real-world accuracy.
- Hausa messages had 4 matches and 5 disagreements; further evaluation is needed.
- English messages had 6 matches and 3 disagreements.
- The observed errors may relate to language coverage, wording, training data, or other model limitations. This pilot cannot determine the cause.
- Warning-sign annotations are provisional and should be reviewed.

## Error review
The eight disagreements are recorded in `results/bilingual_pilot_error_review_v1.csv`.

## Preservation
The frozen model and original training dataset were not modified during this comparison.

## Next steps
1. Review the eight errors and warning-sign annotations.
2. Seek a second reviewer where possible, especially for Hausa messages.
3. Build a larger, carefully reviewed bilingual dataset.
4. Evaluate any revised model separately against a held-out test set.

This corrected report supersedes the earlier pilot summary where its comparison counts differ.
