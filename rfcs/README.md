# RFC process

RFCs are the only route for semantic changes to the Agent Transcripts format
and for changes to this process. The process is deliberately manual: it makes
decisions inspectable in Git and GitHub, but does not claim cryptographic or
automated enforcement.

## Normative files

- `SPEC.md` defines transcript-format semantics.
- `rfcs/README.md` defines the change process.
- `rfcs/0000-template.md` defines the required RFC record.

An accepted RFC records why these files changed; it is not a second source of
live format semantics. If an RFC and a normative file disagree, the normative
file governs and the disagreement is a defect.

## When an RFC is required

An RFC is required when a change can alter:

- whether an authored artifact is valid;
- what an artifact, identity, version, profile, observation, score, or verdict
  means;
- compatibility or migration behavior;
- who may change a normative file or how that decision becomes effective.

Spelling, formatting, and link repairs may land without an RFC only when they
preserve every answer above. Their pull request must contain a brief decision
by the deciding authority naming the changed normative files and why the
change is editorial. If that classification is disputed, use an RFC.

## Authority and lifecycle

The deciding authority is the fixed identity `github:uthunderbird`. A transfer
of the repository does not transfer this authority. Naming a successor requires
an accepted RFC decided under the process and authority effective before that
RFC.

1. Create the next unused four-digit RFC as `Draft` on a branch and include all
   prospective normative-file changes in the same pull request.
2. Run 1–5 cold local-polish rounds against the RFC and prospective normative
   diff. Every round records the reviewed commit SHA, result, and a committed
   summary of every P0/P1 finding: stable ID, author, severity, disposition
   actor, reason, and evidence. External report links are supplementary. A
   finding closes only when it is fixed with evidence, withdrawn by its author
   with a reason, or overridden by the deciding authority with a reason. Record
   when reviewer, author, or decider are the same person. Cold agents are not
   independent certification.
3. A Draft with any unresolved P0/P1 cannot be accepted. The author may revise
   it within the five-round limit, withdraw it, or replace it with a new RFC.
4. The last round must cover the exact candidate commit. Later commits may only
   append review and decision records or apply the status transition described
   below. Any change to the proposal or prospective normative diff invalidates
   the round and requires another round within the limit.
5. The deciding authority records an explicit decision in the pull request,
   naming the exact candidate commit. After that decision, a disposition-only
   commit may change only the RFC's status and Decision record from pending to
   `Accepted` or `Rejected`.
6. `Accepted` in a pull-request branch records the decision but has no effect
   by itself. Acceptance becomes effective only when that RFC, its reviewed
   normative diff, and the decision record land together on `main`. A partial
   or semantically different merge is not acceptance.

Rejected proposals do not require zero P0/P1 or a final cold round. Their
Decision record must still identify what was rejected and why.

Allowed statuses are `Draft`, `Accepted`, `Rejected`, `Withdrawn`, and
`Superseded`. Authors may revise or withdraw Drafts. The deciding authority may
accept or reject them. Rejected and Withdrawn RFCs do not change normative
files. An Accepted RFC is immutable except for non-semantic corrections and
supersession links.

A correction to an Accepted RFC is limited to spelling, formatting, a repaired
link, or an appended audit fact; it must not alter the proposal, decision, or
meaning. Its pull request records the deciding authority's editorial decision.
Supersession status and reciprocal links are permitted only as part of the
reviewed candidate and effective merge bundle of the superseding RFC.

## Compatibility

Every RFC selects exactly one class:

- `Breaking`: when processed under the proposed new format/profile version, at
  least one artifact valid under the immediately preceding version becomes
  invalid or changes meaning.
- `Compatible`: when processed under the proposed version, every artifact valid
  under the immediately preceding version remains valid with the same meaning.
- `Governance-only`: artifact validity and meaning do not change.

A Breaking change introduces a new format or profile version. No RFC may
reinterpret an artifact under an already issued version. Migration
and continued execution support may be declined, but historical meaning must
remain identifiable.

## Supersession and numbering

RFC numbers are provisional until merge; collisions are renumbered before
acceptance, including filenames, titles, links, metadata, and review records.
A later accepted RFC may supersede an earlier Accepted RFC fully or by named
decision/section. Full supersession changes the earlier RFC's status to
`Superseded`; partial supersession leaves it `Accepted` and records the exact
scope in both RFCs. A Draft, Rejected, or Withdrawn proposal may be replaced but
is not normatively superseded. Supersession is prospective and does not rewrite
historical artifact meaning.

RFC 0002 is a one-time bootstrap independent of the process it proposes. It is
adopted only if `github:uthunderbird`: (1) reviews a candidate containing RFC
0002 and its complete normative diff; (2) records all cold-round findings and
dispositions, including the exact final candidate commit; (3) records an
explicit decision for that commit in its pull request; and (4) merges that exact
bundle, plus review/decision-only records, to `main`. After it becomes
effective, amendments to this process are proposed and decided under the
process already effective on `main`; new rules apply only after their own
accepted merge becomes effective.

Acceptance claims adoption of documentation only. Tooling exists only when it
is separately implemented and evidenced.
