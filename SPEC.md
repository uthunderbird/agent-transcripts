# Agent Transcripts — authored format

Status: documentation specification. No validator, compiler, runner, or eval
framework is implemented yet. Normative words describe required behavior of
future implementations, not present enforcement.

## 1. Purpose and boundary

An Agent Transcript is a versioned Markdown scenario for designing and
evaluating an interaction with an agent system. One file carries two authored
layers:

1. a **visible story** for a human reader;
2. a **hidden contract** in machine-readable HTML comments.

A third layer, the **observed result**, is produced by a run and is never
written back into the authored transcript. An authored assistant reply is an
experience exemplar, not evidence that a model produced it and not a golden
string unless a contract explicitly says otherwise.

The format describes stimuli, controlled external boundaries, allowed outcomes,
expectations, and prohibitions. It does not prescribe an agent loop. A runner
must exercise the production loop selected by its run configuration.

## 2. Conformance levels

The specification separates three claims:

- **core-valid**: the file satisfies the byte, Markdown-envelope, block, and
  identity rules in this document;
- **profile-valid**: it is core-valid, the registered profile triple explicitly
  supports the scenario's exact `format_version`, and every profile-owned value
  satisfies that contract's interpretation for that version;
- **compilable**: it is profile-valid and a compiler supports the exact
  `(format_version, profile triple)` pair and every referenced registry entry.

Core validity alone never implies that a scenario can run or be scored. A tool
must state which level it established and must fail closed when it cannot load
or verify a required profile contract.

## 3. Format versions

`draft-0` names the historical examples in this repository. Its nested hidden
grammar was never closed, so it supports documentation reading only and cannot
receive a conformance or compilation claim.

`draft-1` is the format defined below. A later RFC may register profiles for it.
Until an exact profile contract exists, a `draft-1` document may be core-valid
but cannot be profile-valid or compilable.

A future change that alters the validity or meaning of an already valid file
must introduce a new `format_version`. Implementations must select semantics by
the declared version; a later specification must not reinterpret earlier files.

## 4. Source bytes and authored digest

`draft-1` fixes Unicode semantics to Unicode 15.1.0. A `draft-1` source file
must:

- be UTF-8 without a byte-order mark;
- use LF line endings;
- contain no NUL byte;
- encode all text in Unicode Normalization Form C;
- contain only scalar values assigned in Unicode 15.1.0;
- end with exactly one LF.

The assignment and NFC checks use the Unicode 15.1.0 Character Database and
Normalization Forms in Unicode Standard Annex #15 for that version. Here,
**assigned** means that the scalar's `General_Category` in Unicode 15.1.0 is not
`Cn`. Noncharacters such as U+FDD0 therefore fail this predicate. The checks
apply to the Unicode scalar sequence obtained by decoding the complete source
as UTF-8. Independently, every JSON member name and string value, after JSON
escape decoding, must contain only scalars satisfying the same predicate and
must itself be NFC under the same data. Unpaired surrogate escapes are errors.

Consequently, both a literal U+FDD0 and `\uFDD0` are errors. U+1ACF is also an
error because it was unassigned in Unicode 15.1.0, regardless of its assignment
or combining behavior in a later Unicode version.

`authored_sha256` is lowercase hexadecimal SHA-256 of the complete source bytes.
It is computed externally and is not stored inside the source. Every byte,
including visible prose, whitespace, and `design` blocks, contributes to it.

## 5. Document envelope

A source is Markdown prose plus contract comments. Contract discovery is a byte
scan and does not invoke a Markdown parser: code spans and fenced code blocks
have no special status. Scanning from the first byte, every occurrence of
`<!--` must begin at column 1 and be the exact opening delimiter below. Its next
occurrence of `-->` must be the exact closing delimiter below at column 1. A
stray closer, nested opener, or other HTML comment is an error. Consequently,
visible Markdown cannot quote literal HTML-comment syntax directly.

A contract comment has this exact framing:

```text
<!-- agent-transcript
<one JSON object>
-->
```

The opening and closing delimiters occupy lines by themselves. The JSON body
starts on the next line, ends on the line before `-->`, and may span lines.
Leading or trailing whitespace outside the JSON value is insignificant. The
comment body may not contain `--`.

The JSON value follows RFC 8259 with these additional rules:

- duplicate object member names are errors; equality is tested after JSON
  escape and surrogate-pair decoding by exact Unicode scalar sequence, so `a`
  and `\u0061` are the same member name;
- every number token must match `-?(0|[1-9][0-9]*)` and its value must be in
  `[-9007199254740991, 9007199254740991]`; fractions and exponents are errors
  even when their mathematical value is integral;
- every decoded member name and string value must contain only Unicode scalar
  values and be NFC, as required by the source-byte rules;
- unknown members are errors wherever this core specification defines a closed
  object;
- a profile contract must state whether each profile-owned object is closed and
  must reject anything it does not explicitly admit.

There is exactly one `scenario` block. It must precede every other contract
block. There may be zero or more `design`, `expect`, and `forbid` blocks in any
order after it. Block order is authored order and contributes to the digest; it
does not itself impose runtime ordering.

## 6. Core block grammar

The `scenario` block is a closed object with exactly `kind` and `value`:

```json
{
  "kind": "scenario",
  "value": {
    "format_version": "draft-1",
    "profile": {
      "id": "chiplog",
      "version": 1,
      "sha256": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"
    },
    "id": "calendar-proposal-confirmation",
    "version": 1,
    "inputs": {}
  }
}
```

Its `value` is closed and contains exactly:

- `format_version`: the literal `draft-1`;
- `profile`: the closed profile reference below;
- `id`: a stable scenario identifier matching
  `^[a-z][a-z0-9]*(?:-[a-z0-9]+)*$`, 1–80 ASCII characters;
- `version`: an integer from 1 through 2,147,483,647;
- `inputs`: a JSON object owned and validated by the named profile contract.

The profile reference contains exactly:

- `id`: matching the scenario-ID grammar;
- `version`: an integer from 1 through 2,147,483,647;
- `sha256`: 64 lowercase hexadecimal characters naming the exact bytes of the
  profile contract supplied to the compiler.

Every other block is a closed envelope with exactly `kind`, `id`, and `value`:

```json
{
  "kind": "expect",
  "id": "proposal-is-grounded",
  "value": {}
}
```

- `kind` is exactly `design`, `expect`, or `forbid`;
- `id` uses the scenario-ID grammar and is unique across all non-scenario blocks
  in the file;
- `value` is a JSON object owned by the named profile contract for that kind.

`design` is non-executable rationale. A compiler must not translate it into a
stimulus, fixture, runtime setting, check, score, or verdict input; it may retain
it only as non-executable metadata. The authored digest still covers it.

The core owns block modality even though a profile owns predicate syntax and
evidence interpretation. Every `expect` denotes a required condition. Every
`forbid` denotes a condition that must remain unsatisfied. All blocks of both
kinds apply conjunctively: every `expect` must be satisfied and no `forbid` may
be satisfied. A profile may define how a condition is evaluated but may not
invert, ignore, waive, or change this composition. If any block cannot be
compiled to a registered condition, the document is not compilable.

## 7. Profiles and extension boundary

A profile contract is a separate immutable byte artifact identified by the
triple `(id, version, sha256)`. The triple is registered only when an accepted
RFC adds it and its interpretation to this specification or to another
normative profile registry named by the RFC process. Possessing bytes with a
matching digest, or locating them through runner configuration, does not confer
registration or semantic authority. An unregistered triple can be core-valid
only; it cannot support a profile-valid or compilable claim.

How a registered artifact is located is runner configuration, not authored
input. A compiler must verify its bytes before interpreting any profile-owned
value and must record the triple in any downstream binding.

A profile contract must enumerate the exact `format_version` strings it
supports and define separately for each supported version:

- closed schemas for `scenario.inputs` and each block kind's `value`;
- speaker/stimulus extraction from visible Markdown, if used;
- fixture boundary and matcher registries;
- expectation, prohibition, event, observation, and outcome registries;
- compilation of profile-owned values into the product adapter's inputs;
- which checks are deterministic and which, if any, require a judge.

Core implementations must not infer semantics from an unknown profile member,
speaker label, prose phrase, or example. Cross-profile comparison is undefined
unless another normative contract defines the mapping.

## 8. Visible story

The **visible source** is derived after core validation by removing each
complete contract span: all bytes from the `<!-- agent-transcript` opening line
through the LF immediately following its `-->` closing line. The remaining
bytes are concatenated without a placeholder or further normalization. Profile
stimulus extraction may consume only these bytes, never hidden contract bytes.

The visible source is for people and is otherwise unconstrained by the core. A
profile may define exact stimulus extraction directly over it. Rendering-based
extraction is valid only if the profile contract fixes the renderer semantics
and identity. Unless it defines extraction, visible dialogue is illustrative
and cannot be executed or scored.

An authored assistant response is never an observed response. Exact wording may
become a contract only through a registered profile expectation. A scenario may
allow several outcomes; the visible story demonstrates one and does not exclude
the others.

## 9. Fixtures and execution

Fixtures are profile-owned inputs that bind a public injected boundary, a
request matcher, and a controlled response. A fixture does not call a tool and
does not dictate that the production loop use it. A runner supplies a fixture
response only after the production loop independently makes a matching request.

Unmatched calls, unused fixtures, ambiguity, cardinality, consumption, and
ordering are errors or behaviors only as explicitly defined by the exact
profile contract. There are no core defaults for them.

## 10. Identity chain

The authored scenario identity is:

```text
(format_version,
 profile.id, profile.version, profile.sha256,
 scenario.id, scenario.version,
 authored_sha256)
```

Changing visible story, contract blocks, whitespace, or profile reference
changes `authored_sha256`. `scenario.version` is an author-supplied label scoped
by `(profile.id, scenario.id)`; core validity checks only its type and range.
This version defines no machine-verifiable claim that it is monotonic or that a
change is semantic. Such claims require a future predecessor/change contract.

This specification deliberately defines no conformant compiled-bundle or
observed-result serialization yet. A downstream artifact may claim association
with a source only if it reproduces the complete authored identity above, but
that statement alone is not a bundle, run, reproducibility, or evaluation
conformance claim. Closed downstream schemas must define their own identity,
canonicalization, runtime-input boundary, references, absence rules, and
digests before such claims are possible.

An observed result remains a separate record of one run, never a new authored
expectation and never a replacement for the source. This is a layer boundary,
not a result-schema definition.

## 11. Ordering and evaluation boundary

Authored block order is not a scheduler. Runtime ordering requirements must be
expressed through profile-registered events and relations. Deterministic hard
gates and judge-scored qualities are different evidence classes: a judge cannot
waive a failed hard gate.

This version deliberately does not yet define predicate syntax, trace event
shape, scoring, judge prompts, aggregation, or verdict algebra. Those rules
must arrive through an RFC and a bound profile contract before any strict eval
claim is possible.

## 12. Historical examples

The files under [`examples/`](examples/) are `draft-0` design examples. They
illustrate proposal confirmation, separation of fact from plan, and honest
unknown external outcomes. They are not `draft-1` conformance fixtures and do
not prove compiler or eval support.
