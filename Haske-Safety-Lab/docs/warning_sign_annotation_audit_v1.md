# Haske Safety Lab — Warning-Sign Annotation Audit v1

## Purpose

This report records a review of the five warning-sign annotations
in the 20-message English/Hausa pilot dataset, using
`docs/warning_sign_annotation_guide_v1.md`.

## Structural audit

- Messages reviewed: 20
- Unique message IDs: 20
- Warning-sign fields: 5
- Warning-sign values: binary 0/1
- Missing warning-sign values: none

## Annotation review

The existing annotations were reviewed against the agreed definitions.
No obvious correction was identified from this review alone.

### R1 — Unexpected prize or money

EV001, EV003, EV011 and EV013 were considered reasonably flagged.
A grant or money mention alone should not trigger R1; the suspicious
context matters.

### R2 — Pressure or urgency

The six existing flags appear consistent with urgency, threats,
pressure, or fear in the message wording.

### R3 — Request for secret details

The seven existing flags cover explicit requests for PINs, OTPs,
one-time codes, or login credentials.

EV015 remains unflagged for R3 because “confirm your details” does
not explicitly request a secret credential in the supplied wording.

### R4 — Suspicious link or destination

The four existing flags appear consistent with link-based actions
in suspicious contexts. An instruction to use an official app is
not, by itself, evidence of a suspicious link.

### R5 — Potential impersonation

EV004 and EV014 claim to represent a bank while requesting a secret
code. Their existing R5 annotations appear justified.

## Uncertain messages

EV009 and EV019 remain labelled `uncertain`. Asking someone to use
their official banking app is not automatically suspicious. These
messages should not be treated as confirmed legitimate or confirmed
suspicious without further context.

## Limitations

- This is a preliminary review by one reviewer.
- The messages are fictional examples, not a representative real-world dataset.
- Annotation judgments are not independently verified ground truth.
- A second reviewer, especially for Hausa wording, would strengthen
  annotation quality.
- A valid binary value does not guarantee that its annotation is correct.

## Decision

No source annotations were changed as part of this audit.
The original pilot CSV, training dataset, and frozen model were preserved.
Any future corrections should be documented in a separately versioned file.
