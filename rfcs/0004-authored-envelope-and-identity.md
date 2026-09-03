# RFC 0004: Authored envelope and profile binding

- Status: Withdrawn
- Authors: github:uthunderbird
- Created: 2026-09-03
- Pull request: —
- Reviewed base: 931230659986128da600dbc389225c23e5339210
- Reviewed candidate: 0aceeccdced2c5d11feb168e054ce8cbddae5f71
- Local review: 1/5 qualifying rounds; 4 preliminary cold critiques

## Summary

Introduce `draft-1`, a closed product-neutral envelope for authored transcript
blocks, explicit profile binding, and byte-level authored identity. Keep
compiled-run identity, profile semantics, and eval algebra out of the core until
later RFCs define closed schemas for them.

## Problem

`draft-0` closes only four discriminator names and four identity fields. Its
nested YAML-like values, defaults, profile identity, comment framing, duplicate
handling, and digest inputs are unspecified. A future validator could therefore
accept a file that another compiler interprets differently. The specification
also names scenario bundles and result artifacts without defining closed
schemas for them.

That ambiguity blocks a strict eval framework before scoring begins: two
implementations cannot first agree on what scenario or run they are scoring.

## Proposed normative change

Replace `SPEC.md` with the prospective version in this pull request. It:

- preserves `draft-0` as historical documentation-only input;
- introduces `draft-1` source-byte and contract-comment framing rules;
- uses strict JSON with duplicate rejection and bounded integers;
- closes the core block envelopes and cardinality;
- binds every profile-owned value to an immutable profile triple;
- distinguishes core-valid, profile-valid, and compilable;
- defines authored identity and an explicit non-claim boundary for downstream
  bundle and result formats;
- makes visible assistant text explicitly exemplar rather than observation;
- reserves predicate syntax and eval algebra for a later RFC.

## Examples

A `draft-1` scenario begins with exactly one block shaped as:

```json
{"kind":"scenario","value":{"format_version":"draft-1","profile":{"id":"chiplog","version":1,"sha256":"0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"},"id":"example","version":1,"inputs":{}}}
```

This can be core-valid. It is not profile-valid merely because the profile says
`chiplog`: a compiler must receive bytes with the declared digest and validate
`inputs` against that contract.

Rejected core-validity boundary: two JSON members named `version`, an unknown
envelope member, or an HTML comment not framed as an Agent Transcript block.
An `expect` block whose profile contract cannot be loaded may remain core-valid,
but must be rejected as profile-valid or compilable.

## Consequences

Existing examples remain `draft-0` and lose no historical meaning, but they
cannot support conformance claims. `draft-1` is intentionally not executable
until a later RFC registers a profile contract. Implementations gain a stable
parse and authored-identity boundary before runtime or eval semantics are
introduced.

A future validator can implement core validity without Chiplog. A future
compiler additionally needs a verified profile artifact. A separate RFC must
define the closed bundle/result evidence envelope before a runner or evaluator
can make a strict binding claim.

## Alternatives considered

### Close the existing YAML-like grammar

Rejected because YAML schema/version choices, implicit scalar typing, aliases,
and duplicate-key behavior would become extra interoperability decisions with
no demonstrated benefit for the hidden contract.

### Put all Chiplog and eval semantics in the core

Rejected because product-specific boundaries and scoring registries would make
the supposedly reusable protocol a Chiplog schema in disguise.

### Define scoring in the same RFC

Rejected because authored parsing, runtime evidence, and evaluation are three
independent failure boundaries. The latter two will be separate RFCs. A score
is not meaningful until all evaluators bind the same authored scenario,
compiled inputs, and observed run.

## Local review

Four non-independent cold critiques examined evolving, uncommitted working
trees. They are preliminary evidence rather than commit-bound lifecycle rounds:

1. `PRE-1-P1-1` found Markdown-dependent comment discovery;
   `PRE-1-P1-2` ambiguous integer tokens; `PRE-1-P1-3` unpaired surrogate
   disagreement; and `PRE-1-P1-4` ambiguous NFC scope. They were fixed with a
   byte scanner, lexical integer grammar, Unicode-scalar rejection, and separate
   source/decoded-string NFC checks. A supporting core/profile example mismatch
   was also corrected.
2. `PRE-2-P1-1` and `PRE-2-P1-2` found that bundle identity and runtime-input
   completeness were open prose; `PRE-2-P1-4` found the same for result identity.
   They were fixed by removing those conformance claims from this RFC and
   reserving closed downstream schemas for another RFC. `PRE-2-P1-3` found an
   unverifiable semantic-version claim; fixed by defining `scenario.version` as
   a bounded author assertion at this layer.
3. `PRE-3-P0-1` found profile-redefinable `expect`/`forbid` polarity; fixed by
   core-owned conjunction and polarity. `PRE-3-P0-2` found self-authorizing
   profile artifacts; fixed by normative registration through an accepted RFC.
   `PRE-3-P1-1` found undefined visible input; fixed by an exact byte projection.
4. Coverage review returned zero P0/P1 across the narrowed authored-envelope,
   profile-binding, modality, and identity scope.

The fifth and last local-polish iteration reviewed
`931230659986128da600dbc389225c23e5339210..0aceeccdced2c5d11feb168e054ce8cbddae5f71`.
Relationship: non-independent cold review. Verdict: zero P0 and one unresolved
P1, `FINAL-P1-1`: NFC validity depended on the implementation's Unicode data
version. Python Unicode 16 and Node Unicode 17 disagreed on a string containing
U+1ACF. With the five-iteration budget exhausted, the finding was not repaired
in RFC 0004.

## Decision

- Withdrawing author: `github:uthunderbird`
- Date: 2026-09-03
- URL: https://github.com/uthunderbird/agent-transcripts/commit/9862378dcec7625dbce7ad6adb40eb8282d42c54
- Reason: the final permitted review left `FINAL-P1-1` unresolved. RFC 0005
  replaces the proposal with explicit Unicode-version binding.

RFC 0004 made no normative change.
