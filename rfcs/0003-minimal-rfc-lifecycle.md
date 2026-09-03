# RFC 0003: Minimal RFC lifecycle

- Status: Draft
- Authors: github:uthunderbird
- Created: 2026-09-03
- Pull request: —
- Reviewed base: —
- Reviewed candidate: —
- Local review: 0/5 qualifying rounds; 4 preliminary cold critiques

## Summary

Define only the manual lifecycle by which normative changes are proposed,
reviewed, decided, and made effective. Subject-specific concerns such as format
compatibility, versioning, profiles, and supersession remain the responsibility
of the RFC that changes those semantics.

## Problem

The initial process does not bind an acceptance decision to an exact reviewed
change. RFCs 0001 and 0002 attempted to solve this together with broader
governance and compatibility machinery; both exhausted their five-round review
budgets without converging.

The repository needs a smaller invariant: an accepted normative change is the
same change that received bounded cold review and an explicit owner decision.

## Proposed normative change

Replace `rfcs/README.md` and `rfcs/0000-template.md` with the prospective files
in this pull request. They define:

- the three normative files;
- one fixed deciding authority;
- a Draft containing the complete prospective normative diff;
- one to five base-and-candidate-bound cold review rounds;
- explicit, attributable P0/P1 dispositions;
- an owner decision bound to the same final base/candidate pair as review;
- effectiveness only when the exact bundle lands on `main`;
- an explicit manual-auditability ceiling.

No editorial exception, compatibility taxonomy, supersession protocol,
automation, signature, or branch-protection claim is part of this RFC.

## Examples

Accepted:

```text
Draft + complete normative diff from base B to candidate A
  -> final cold review of B..A with no unresolved P0/P1
  -> github:uthunderbird accepts B..A
  -> review/decision-only record commit
  -> A's normative diff and records land together on main
```

Not accepted:

```text
commit A is reviewed
  -> proposal text changes in commit B
  -> B lands without another cold round
```

## Consequences

Every change to a normative file, including editorial repairs, uses an RFC.
This trades a small amount of ceremony for a boundary with no classification
loophole. Individual format RFCs must explain their own compatibility and
version consequences; this lifecycle does not pre-judge them.

No authored transcript changes validity or meaning through RFC 0003 itself.

## Alternatives considered

RFC 0001's mechanized acceptance model was rejected as larger than the format
it governed. RFC 0002's manual model was still too broad because it combined
lifecycle with compatibility and supersession. Allowing editorial exceptions
was rejected because it creates a second decision path.

## Local review

Four non-independent cold critiques examined evolving, uncommitted working
trees. Because they were not bound to exact commits, they are preliminary
design evidence rather than qualifying lifecycle rounds:

1. `PRE-1-P1` found that a candidate commit alone did not identify its
   comparison base. Fixed by recording an ancestor base and defining the
   prospective normative diff as `base..candidate`.
2. `PRE-2-P0` found that review and decision could name different bases. Fixed
   by requiring the same base/candidate pair. `PRE-2-P1` found that checking
   only changed paths admitted concurrent normative changes. Fixed by comparing
   all normative-file contents before and after landing.
3. `PRE-3-P1` found that author withdrawal could not satisfy the owner-only
   Decision schema. Fixed by giving `Withdrawn` a separate author record.
4. Coverage review returned zero P0/P1 across the lifecycle states and stated
   manual guarantee.

One final cold review must examine an exact committed base/candidate pair. It
is the fifth and last local-polish iteration for this RFC and the first round
that can qualify under the proposed lifecycle.

## Decision

Pending.
