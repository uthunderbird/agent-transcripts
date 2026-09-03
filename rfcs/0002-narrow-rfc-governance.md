# RFC 0002: Narrow manual RFC governance

- Status: Withdrawn
- Authors: github:uthunderbird
- Created: 2026-09-03
- Decision date: 2026-09-03

## Summary

This proposal tried to define authority, review, compatibility, versioning,
supersession, and lifecycle in one manual RFC process. It was not accepted and
made no normative change.

## Decision

Withdrawn after the fifth and final local-polish round left one P1 finding:
the proposed `Compatible` and `Governance-only` classes were not disjoint.
Earlier rounds had already shown that combining lifecycle with compatibility
and supersession made the governance proposal larger than its central job.

The replacement should be narrower: govern only how an exact normative change
is proposed, reviewed, decided, and made effective. Compatibility and
supersession belong in the RFCs whose subject matter requires them.

## Local polish record

Five non-independent cold rounds were run. They examined lifecycle,
authority/bypasses, cross-file coherence, coverage, and final regression. The
first four rounds produced repairs. The fifth found the unresolved class
overlap above. Because the agreed cap was five rounds, the proposal was not
revised or accepted after that finding.
