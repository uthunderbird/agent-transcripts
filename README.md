# Agent Transcripts

`agent-transcripts` documents a draft, human-readable format for describing
agent interactions as versioned Markdown. The same document can show a coherent
user story and carry hidden, machine-oriented expectations without pretending
that the illustrated dialogue is the only valid execution path.

This repository has a new, unrelated Git history. The former research project
is preserved at
[`uthunderbird/agent-transcripts-archive`](https://github.com/uthunderbird/agent-transcripts-archive).
If you cloned `agent-transcripts` before 2026-09-03, make a fresh clone; do not
push an old clone to this repository.

## Status

The format is an **authored-format draft**, not an implemented standard. Today
this repository provides documentation, examples, and an RFC process. It does
not provide a validator, compiler, runner, eval framework, or ACP integration,
and it makes no interoperability or conformance claim.

The core model is intended to be product-neutral. The current examples come
from Chiplog and should be read as a motivating **Chiplog profile**, not as
generic vocabulary required by the core format.

## Read this first

- [`SPEC.md`](SPEC.md) — current format draft and semantic model.
- [`examples/`](examples/) — Chiplog-authored examples.
- [`rfcs/README.md`](rfcs/README.md) — how proposed format changes are made.
- [`rfcs/0000-template.md`](rfcs/0000-template.md) — RFC template.

## Scope

The initial release is documentation-only and uses format identifier
`draft-0`:

- define the authored transcript and its relationship to observed results;
- distinguish examples, design notes, scenarios, expectations, and forbids;
- evolve normative decisions through reviewable RFCs;
- keep product-specific concepts in profiles and examples.

Possible later layers, in order, are a structural validator, a compiler to a
canonical scenario bundle, and an independent eval framework. ACP may become an
adapter boundary for that future framework. None of those layers is part of the
current repository contract.

## Changing the format

Normative changes to `SPEC.md` require an accepted RFC. Editorial corrections
that do not change meaning may be made directly, but the pull request must say
why the change is non-normative. See [`rfcs/README.md`](rfcs/README.md).
