# RFC 0005: Authored envelope and profile binding

- Status: Withdrawn
- Authors: github:uthunderbird
- Created: 2026-09-03
- Pull request: https://github.com/uthunderbird/agent-transcripts/pull/2
- Reviewed base: 931230659986128da600dbc389225c23e5339210
- Reviewed candidate: 9862378dcec7625dbce7ad6adb40eb8282d42c54
- Local review: 0/5 qualifying rounds; 5 cold critiques

## Summary

Introduce `draft-1`, a closed product-neutral authored envelope, exact profile
binding, deterministic Unicode and JSON parsing, and byte-level authored
identity. Runtime evidence and evaluation remain separate future schemas.

## Problem

`draft-0` closes neither its nested YAML-like grammar nor profile authority and
cannot support cross-implementation conformance. RFC 0004 closed most of this
surface but its last permitted cold review proved that an unversioned NFC rule
still yields different validity decisions under different Unicode releases.
RFC 0004 was therefore withdrawn.

## Proposed normative change

Replace `SPEC.md` with the prospective version in this pull request. Relative
to the withdrawn RFC 0004 proposal, RFC 0005 additionally binds all source and
decoded-JSON assignment and normalization checks to Unicode 15.1.0 and rejects
code points unassigned in that version.

The complete proposal:

- preserves `draft-0` as documentation-only history;
- introduces exact source-byte and contract-comment framing;
- uses strict JSON with duplicate rejection, lexical bounded integers,
  Unicode-scalar checks, `General_Category != Cn` assignment, and
  Unicode-15.1.0 NFC;
- closes block envelopes, cardinality, IDs, and visible-source projection;
- keeps `expect`/`forbid` polarity and conjunction in the core;
- requires normative registration and digest verification of profile contracts;
- defines deterministic authored identity;
- explicitly makes no bundle, result, runtime, or eval conformance claim.

## Examples

The ASCII JSON examples in `SPEC.md` are unaffected by Unicode-version choice.
The escaped string `"a\u0315\u1acf"` is rejected because U+1ACF has
`General_Category=Cn` in Unicode 15.1.0, even if a host runtime with newer
Unicode data would normalize it. Literal or escaped U+FDD0 is likewise rejected
as `Cn`, so noncharacter handling does not depend on a host library's notion of
the broader `Assigned` or `Age` properties.

A matching digest for arbitrary profile bytes is insufficient: the exact
profile triple must also be registered by an accepted RFC before a
profile-valid or compilable claim is available.

## Consequences

Existing examples remain historical `draft-0`. No `draft-1` profile is yet
registered, so a file may establish core validity but not profile validity or
compilability. Implementations need Unicode 15.1.0 assignment and normalization
data to validate `draft-1`.

The next RFC must define a closed runtime evidence envelope. A later RFC must
define deterministic predicates, judge inputs/outputs, scoring, and combined
verdict semantics.

## Alternatives considered

### Use each host runtime's current Unicode data

Rejected because identical bytes already produced different NFC verdicts in
the RFC 0004 final review.

### Remove normalization

Rejected because canonically equivalent identifiers and profile-owned strings
would remain byte-distinct after JSON escape decoding and would force every
downstream registry to choose its own policy.

### Permit unassigned code points

Rejected because a later Unicode release can assign combining behavior to a
previously unassigned scalar and retroactively change the NFC verdict.

## Local review

Four non-independent cold critiques examined evolving, uncommitted working
trees and therefore do not qualify as commit-bound lifecycle rounds:

1. `PRE-1-P1` found that “assigned” did not select one UCD predicate and made
   noncharacter handling ambiguous. Fixed by defining assignment as Unicode
   15.1.0 `General_Category != Cn` and stating literal/escaped U+FDD0 and
   U+1ACF boundaries.
2. `PRE-2-P1` found duplicate-key equality ambiguous for `a` versus `\u0061`.
   Fixed by comparing names after escape and surrogate-pair decoding by exact
   Unicode scalar sequence.
3. `PRE-3-P1` found no explicit relation between the profile triple and the
   scenario's format version. Fixed by requiring registered version support for
   profile validity and compiler support for the exact pair.
4. Coverage review returned zero P0/P1 across the complete authored-layer scope
   and all preceding repairs.

5. The final regression found no technical P0/P1, but found two lifecycle P1s:
   `PRE-5-P1-1` the pull request was opened after rather than before review, so
   the round could not qualify; `PRE-5-P1-2` RFC 0004's withdrawal record used a
   placeholder instead of the URL required by RFC 0003. The local-polish budget
   was exhausted, so RFC 0005 was not revised or accepted.

## Decision

- Withdrawing author: `github:uthunderbird`
- Date: 2026-09-03
- URL: https://github.com/uthunderbird/agent-transcripts/pull/2#issuecomment-5525296313
- Reason: the fifth local-polish iteration left the two lifecycle P1s above
  unresolved. The technically reviewed content may be proposed again only in a
  fresh RFC whose complete Draft PR exists before its qualifying review.

RFC 0005 made no normative change.
