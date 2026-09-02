# RFC process

RFCs are the change mechanism for the Agent Transcripts format draft. They make
the reason, compatibility cost, and rejected alternatives visible before the
normative text changes.

## When an RFC is required

An RFC is required for any change that affects how an authored transcript is
interpreted, including:

- syntax, discriminators, fields, or defaults;
- normative meaning or authority of a section;
- versioning, identity, compatibility, or result separation;
- the boundary between the generic core and a product profile;
- requirements placed on a future validator, compiler, runner, or adapter.

Spelling, formatting, broken-link, and explanatory changes that provably do not
alter meaning do not require an RFC.

## Lifecycle

1. Copy `0000-template.md` to the next unused four-digit number and choose a
   descriptive slug, for example `0001-outcome-semantics.md`.
2. Open it as `Draft`. State the problem, proposed normative change, examples,
   compatibility impact, and alternatives.
3. Discuss it in a pull request. Revise the RFC rather than hiding decisions in
   the review thread.
4. A maintainer marks it `Accepted` or `Rejected` and records the decision.
5. A normative accepted RFC and its corresponding `SPEC.md` change land
   together. Only non-normative tooling described by the RFC may be deferred.

Allowed statuses are `Draft`, `Accepted`, `Rejected`, and `Superseded`. An RFC
is immutable after acceptance except for clearly labelled editorial fixes. A
replacement RFC marks the old one `Superseded` and links both directions.

Acceptance means “this repository adopts the documented design.” It does not
claim that a validator, compiler, runtime, or external implementation exists.
