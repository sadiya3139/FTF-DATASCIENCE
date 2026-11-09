# Haske Safety Lab: Warning-Sign Annotation Guide v1

## Purpose

This guide standardizes the annotation of five potential warning signs
in English and Hausa messages. A warning sign indicates a reason to
investigate; it does not, by itself, prove that a message is a scam.

## General annotation rules

- Use `1` when the message text supports the warning sign.
- Use `0` when the warning sign is not supported by the available text.
- Do not infer details that are not present in the message.
- A message may have more than one warning sign.
- Legitimate messages can mention banks, money, links, or urgency.
- Consider the full message and its context, not isolated keywords.
- Apply the same meaning consistently in English and Hausa.
- If the wording or context is genuinely unclear, record uncertainty
  in the review notes rather than inventing evidence.
- Keep message classification (legitimate/suspicious) separate from
  the five warning-sign annotations.

## R1 — Unexpected prize or money

Mark `1` when the message presents an unexpected prize, grant,
financial benefit, or money offer in a suspicious context.

Do not mark every mention of money. A routine payment notification,
salary notice, or legitimate financial announcement does not qualify
solely because it mentions money.

Example: "You have won a grant. Pay a fee to receive it."

## R2 — Pressure or urgency

Mark `1` when the message uses urgency, threats, pressure, or fear
to push the recipient into immediate action.

Example: "Your account will be blocked today unless you act now."

A normal appointment time or ordinary reminder is not sufficient
by itself.

## R3 — Request for secret details

Mark `1` when the message requests sensitive secrets or credentials,
including a PIN, OTP, password, login credentials, or comparable
confidential authentication information.

Example: "Tell me the code sent to your phone."

A general request to check an account does not automatically qualify.

## R4 — Suspicious link or destination

Mark `1` when the message directs the recipient to a suspicious
or unverified link or destination in a potentially deceptive context.

Example: "Click this link to verify your account."

Do not mark every instruction to open an app. An instruction to use
the recipient's usual official app is not, by itself, evidence of
a suspicious link. If the destination cannot be assessed, record
the uncertainty in the review notes.

## R5 — Potential impersonation

Mark `1` when the message appears to claim the identity or authority
of a trusted institution, organisation, or person in a potentially
deceptive way.

Example: "I am calling from your bank. Give me your OTP."

Merely mentioning a bank or organisation is not enough. Consider
the wording and the action being requested.

## Review and quality control

1. Read the complete message before annotating it.
2. Assign each of the five warning signs independently.
3. Record a short reason for each disputed annotation.
4. Seek a second reviewer where possible, particularly for Hausa
   wording and culturally specific expressions.
5. Resolve disagreements through documented review rather than
   silently changing labels.
6. Keep original annotations and model predictions available for
   comparison; do not treat model predictions as ground truth.
7. Version revised annotation files and document the changes.

## Limitations

These warning signs are a practical project-specific annotation
framework, not a complete definition of scams. Absence of these
signs does not guarantee that a message is safe, and their presence
does not automatically prove malicious intent.
