# RFC 0006: Authored envelope and profile binding

- Status: Draft
- Authors: github:uthunderbird
- Created: 2026-09-03
- Pull request: https://github.com/uthunderbird/agent-transcripts/pull/3
- Reviewed base: 931230659986128da600dbc389225c23e5339210
- Reviewed candidate: 6630380ddec6c23203f9f52e8385fcb539855fa8
- Local review: 1/5 rounds

## Summary

Adopt the Unicode-bound `draft-1` authored envelope developed in withdrawn RFCs
0004 and 0005. This fresh proposal exists because their technical content
converged but their lifecycles did not.

## Problem

`draft-0` is useful design prose but not an interoperable format: nested values,
comment discovery, Unicode behavior, profile authority, and authored identity
are open. RFC 0004 left Unicode normalization dependent on host library data.
RFC 0005 repaired that defect, but its pull request was created only after its
final review, so the review could not qualify under RFC 0003.

## Proposed normative change

Replace `SPEC.md` with the complete prospective file in this pull request. It:

- preserves `draft-0` as documentation-only history;
- defines UTF-8/LF/NFC source bytes using Unicode 15.1.0 and rejects
  `General_Category=Cn` scalars;
- defines byte-scanned contract comments and strict RFC-8259 JSON with closed
  envelopes, decoded duplicate-name comparison, lexical integers, and scalar
  checks;
- defines block cardinality, IDs, deterministic visible-source projection, and
  authored SHA-256 identity;
- assigns `expect`/`forbid` polarity and conjunction to the core while keeping
  their predicate values profile-owned;
- requires an accepted-RFC registration, exact digest, and explicit
  format-version support for profile-valid and compilable claims;
- defines `scenario.version` as a bounded author assertion at this layer;
- explicitly declines bundle, result, runtime, reproducibility, and eval
  conformance until later RFCs provide closed schemas.

The pull request also lands RFCs 0004 and 0005 as historical Withdrawn records;
they have no normative effect.

## Examples

`{"a":1,"\u0061":2}` is rejected because member names are compared after
escape decoding. Literal or escaped U+FDD0 and U+1ACF are rejected because their
Unicode-15.1.0 general category is `Cn`. A profile artifact with a matching
digest remains unregistered unless an accepted RFC normatively registers its
exact triple and interpretation.

The three repository examples remain `draft-0`; none is presented as a
`draft-1` conformance fixture.

## Consequences

Independent core validators gain a deterministic authored-source boundary. No
`draft-1` document is profile-valid yet because no profile triple is registered.
This is intentional: the next RFC must define a closed runtime evidence
envelope and a subsequent RFC must define profile predicates and eval algebra.

Implementations require Unicode 15.1.0 assignment and normalization data.
Existing `draft-0` examples remain readable but are not silently reinterpreted.

## Alternatives considered

- Host-current Unicode was rejected after Python and Node produced different
  NFC decisions for the same bytes.
- YAML was rejected because schema, implicit typing, alias, and duplicate-key
  choices add interoperability decisions without helping the hidden contract.
- Defining runtime evidence and scoring here was rejected because authored
  parsing, run capture, and evaluation are separate failure boundaries.
- Reopening RFC 0005 was rejected because its five-iteration budget was
  exhausted and its final review did not satisfy the PR-before-review rule.

## Local review

Round 1 reviewed
`931230659986128da600dbc389225c23e5339210..6630380ddec6c23203f9f52e8385fcb539855fa8`
after the complete Draft and prospective diff were published in pull request
#3. Relationship: non-independent cold review. Verdict: zero P0 and zero P1.

The review covered deterministic authored parsing and identity, Unicode 15.1.0,
JSON/comment scanning and visible projection, profile authority/version/modality,
downstream non-claims, the two historical withdrawal records, and lifecycle
ordering. No finding disposition was required.

## Decision

Pending.
