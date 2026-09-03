# RFC 0002: Adopt narrow manual RFC governance

- Status: Draft
- Authors: github:uthunderbird
- Created: 2026-09-03
- Compatibility: Governance-only
- Supersedes: RFC 0001 as a proposal only; RFC 0001 was never accepted
- Superseded by: —
- Pull request: —
- Local polish: 4/5 rounds
- Review relationship: non-independent cold review

## Summary

Replace the underspecified initial RFC instructions with a narrow manual
process. A proposal, its prospective normative diff, cold review, owner
decision, and effective merge remain visibly distinct. The process makes no
claim that GitHub authority or commit topology is mechanically verified.

## Problem

The initial process does not say who accepts an RFC, when acceptance becomes
effective, or how the process changes itself. RFC 0001 tried to close those
questions with a machine-like acceptance protocol. Its five-pass local polish
did not converge: the mechanism accumulated its own event, manifest, topology,
and review-set ambiguities and was withdrawn.

The repository needs a smaller promise: a human can inspect the Draft, its
actual prospective diff, the bounded review record, the owner's decision, and
the files that landed together.

## Proposed normative change

This pull request replaces exactly:

- `rfcs/README.md`;
- `rfcs/0000-template.md`.

The replacement defines:

- the three normative files and their subject authority;
- a conservative semantic/editorial boundary;
- `github:uthunderbird` as fixed deciding authority;
- revision-bound Draft review on the actual prospective diff;
- a mandatory local polish of 1–5 cold rounds;
- no acceptance with unresolved P0/P1;
- effective acceptance only when RFC and target changes land together;
- disjoint compatibility classes and non-reinterpretation of issued versions;
- prospective supersession and pre-merge RFC-number collision handling;
- an explicit ceiling: manual auditability, not cryptographic or automated
  enforcement.

## Examples

Accepted lifecycle:

```text
Draft RFC + prospective target diff in one PR
  -> 1–5 cold rounds, zero unresolved P0/P1
  -> explicit owner acceptance of the exact candidate commit
  -> disposition-only status/decision commit
  -> reviewed target diff and RFC land together on main
```

Not accepted:

```text
owner likes the proposal
  -> only the RFC lands, while the target file remains unchanged
```

The second case leaves the proposal ineffective regardless of its prose status.

## Compatibility

`Governance-only`: no authored or observed artifact changes validity or meaning.
The contribution process changes prospectively. RFC 0001 remains a historical
Withdrawn proposal and gains no normative force.

## Core and profiles

Governance only. This RFC does not decide core grammar, profile identity, or
evaluation semantics.

## Alternatives considered

### Keep the initial process

Rejected because authority and effective acceptance remain ambiguous.

### Repair RFC 0001

Rejected after its fifth local-polish pass retained five P1 findings. Continuing
would violate the agreed five-round ceiling and preserve an unnecessarily large
governance state machine.

### Add automated or cryptographic enforcement

Rejected for this phase. It would make governance machinery larger than the
documentation it governs. A future RFC may add a check after a concrete failure
demonstrates the need.

## Future tooling impact

A future repository check could verify RFC metadata and co-change of declared
targets, but this RFC neither requires nor claims such a check.

## Local polish

All reviewers were non-independent cold agents. Rounds 1–4 reviewed evolving
working trees based on commit `85854ad`; they are design evidence, not the final
candidate review. Finding authors are the named cold round; disposition actor
is `github:uthunderbird` unless stated otherwise.

1. **Central lifecycle.** Result: repair. `R1-P1-1` found an impossible
   Draft-to-Accepted merge transition; fixed by separating recorded decision
   from effectiveness on `main`. `R1-P1-2` found stale-review risk; fixed by
   binding the final round to an exact candidate and invalidating it after a
   semantic change. Evidence: the Authority and lifecycle section.
2. **Authority and bypasses.** Result: repair. `R2-P1-1` dynamic-owner authority,
   `R2-P1-2` mutable reviewed target, `R2-P1-3` unrecorded editorial escape,
   `R2-P1-4` unauditable finding closure, and `R2-P1-5` circular
   self-amendment were fixed respectively by a literal authority identity,
   commit-bound review and decision, an owner editorial record, closed finding
   dispositions, and the RFC 0002 bootstrap rule. Evidence: When an RFC is
   required, Authority and lifecycle, and the bootstrap paragraph.
3. **Cross-file coherence.** Result: repair. `R3-P1-1` impossible acceptance
   transition and `R3-P1-2` mutable review target duplicate R1 and are fixed as
   above. `R3-P1-3` issued-version reinterpretation was fixed by prohibiting
   reinterpretation, not merely silent reinterpretation. `R3-P1-4` dynamic
   authority duplicates R2 and is fixed as above. `R3-P1-5` ambiguous partial
   supersession was fixed by reserving `Superseded` for full replacement and
   requiring exact reciprocal scope for partial replacement. Evidence:
   Compatibility and Supersession and numbering.
4. **Coverage.** Result: repair. `R4-P1-1` circular bootstrap was fixed by an
   independent four-step adoption rule. `R4-P1-2` missing rejection transition
   was fixed by a disposition-only `Rejected` record. `R4-P1-3` overlapping
   compatibility classes was fixed by defining them relative to processing
   under the proposed version. `R4-P1-4` supersession/immutability conflict was
   fixed by admitting reciprocal edits only in the superseding RFC bundle.
   `R4-P1-5` unattributed finding withdrawal was fixed with stable finding and
   actor fields. `R4-P1-6` mutable audit evidence was fixed by committed
   summaries and a closed correction boundary. Evidence: the corresponding
   process and template clauses.

Round 5 must review the exact candidate commit and return zero unresolved
P0/P1 before this RFC can be accepted.

## Decision

Pending.
