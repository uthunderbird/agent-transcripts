# RFC 0001: Make RFC governance self-applicable and auditable

- Status: Withdrawn
- Authors: uthunderbird
- Created: 2026-09-03
- Decision ID: RFC-0001-D1
- Decision date: 2026-09-03
- Deciding authority: github:uthunderbird
- Review: local polish, five cold passes, not converged

## Summary

This docs-only bootstrap proposed the exact replacements below. It was
withdrawn after its fifth and final allowed local-polish pass retained five P1
findings. It changed no normative rule and implemented no tooling.

## Bootstrap and acceptance

The sole bootstrap authority is `github:uthunderbird` for canonical repository
`github.com/uthunderbird/agent-transcripts` and branch `main`. Approval is a
public PR comment in exactly this form, with the full candidate SHA substituted:

```text
I, uthunderbird, accept RFC-0001-D1 at candidate commit <full-40-hex-SHA> with the closed normative manifest [rfcs/README.md, rfcs/0000-template.md].
```

The named candidate contains this Draft and a prospective diff producing the
exact replacements below. The acceptance commit has that candidate as first
parent and becomes canonical `main` without cherry-pick, rebase, or a
content-changing merge. In the candidate, `Status` is exactly `Draft`; `Decision date`,
`Deciding authority`, and `Review` are exactly `—`; and `Decision` is exactly the
pending text at the end of this RFC. Relative to that candidate, the acceptance
commit may change only those four metadata values and replace the `Decision`
section with an acceptance receipt containing the decision ID, outcome, full
candidate SHA, authority identity, decision date, approval-comment URL, the
closed manifest, `Governance-only`, no exceptions, and every P0/P1 disposition.
It must also materialize both exact replacements. No other path, including a
non-normative path, or RFC text may change in that commit. The comment is
authority evidence and disclosed self-approval, not
independent review. A mismatch is ineffective and cannot be cured retroactively;
a new candidate and approval are required.

For RFC 0001, the closed ordered normative path manifest is exactly:

1. `rfcs/README.md`
2. `rfcs/0000-template.md`

These are its only normative targets. `SPEC.md` is in the repository registry
but is not changed by this governance-only decision. A changed normative file
outside this manifest, an incomplete replacement, or any non-enumerated change
voids the attempted acceptance.

## Exact replacement: `rfcs/README.md`

````markdown
# RFC process

RFCs change the Agent Transcripts format and this process. Accepted RFCs are
decision records, not live normative text.

## Closed normative-target registry and precedence

Only `SPEC.md` (format semantics), `rfcs/README.md` (governance), and
`rfcs/0000-template.md` (record shape) are normative. Adding, removing,
renaming, or changing an entry's role or precedence requires an accepted RFC.
A file cannot declare itself normative. Registered targets govern current
interpretation; RFCs and acceptance commits establish whether they were validly
changed. `rfcs/README.md` governs RFC procedure and authority,
`rfcs/0000-template.md` governs the required shape of an RFC record, and
`SPEC.md` governs transcript format semantics. If statements overlap, the
target governing that subject controls; if two targets govern the same subject
and disagree, neither RFC history nor an exception chooses between them: the
inconsistency is a defect requiring an RFC and atomic corrective target edits.

## Required changes and authority

Every semantic change to a registered target requires an RFC. Editorial changes
are spelling, formatting, immutable-link repair, or wording preserving validity,
meaning, identity/version, authority, evidence, and procedure; dispute makes a
change normative.

The deciding authority is `github:uthunderbird` until an accepted RFC changes
it. Actor identities are structured as `github:<login>` or
`local:<declared-name>`. Dates are UTC calendar dates in `YYYY-MM-DD`. A review
record contains reviewer identity, candidate full SHA, public immutable commit
URL and public PR/review URL, date, findings, dispositions, and one
honesty class: `independent`, `self-review`, or `cold-local-audit`. The
`independent` class is permitted only when reviewer and decider are distinct
people. `cold-local-audit` means a no-parent-context audit whose report is
recorded in the PR; it is local polish, not independent certification.

## Lifecycle

Events are creation (none→Draft), revision (Draft→Draft), acceptance
(Draft→Accepted), rejection (Draft→Rejected), withdrawal (Draft→Withdrawn),
supersession (Accepted→Superseded), and editorial correction (status unchanged).
Every event record contains exactly event, actor, date, prior state, resulting
state, and evidence. An author may create, revise, or withdraw a Draft. The current deciding authority
may reject or accept a Draft, approve an editorial correction, and accept the
later RFC that supersedes an Accepted RFC. The later RFC's effective acceptance
performs the supersession event; neither an author nor an edit to the older RFC
alone can do so. Each event records actor identity, date, prior/resulting state,
and evidence. Rejected, Withdrawn, and Superseded are terminal. Accepted content
is immutable except labelled editorial corrections and reciprocal supersession
metadata. Any unlisted transition, wrong actor, missing record, or attempted
mutation of terminal content is void and leaves the prior state governing. An
invalid attempted transition is repaired only by a new legal event from that
prior state; later metadata cannot retroactively validate it.

## Acceptance

Approval names the stable Decision ID, full candidate SHA, and closed ordered
manifest. The reviewed candidate has Draft status and normalized pending
placeholders. The acceptance commit has that candidate as first parent and may
change only Status, Decision date, Deciding authority, Review, and the fixed
Decision receipt in the RFC, plus complete manifested targets and, when the
manifest expressly includes them, reciprocal supersession metadata. It
atomically lands complete metadata and approved target text. A missing target,
partial target edit, different target text, unmanifested normative edit, or any
other non-enumerated mutation voids acceptance and needs a new candidate and
approval. It must become canonical `main` without rewriting the candidate. The
record identifies every linked cold-review finding classified P0 or P1 and its
disposition; `none` is allowed only when every linked report contains zero such
findings.

## Compatibility and historical meaning

Apply the first matching class: (1) `Breaking`: a previously valid artifact
becomes invalid or its backward semantic meaning changes; (2) `Compatible`:
prior artifacts retain validity and backward semantic meaning though additions
are allowed; (3) `Governance-only`: artifact validity and meaning are
unchanged. Backward semantic meaning is interpretation under the artifact's
original identity/version and rules effective when authored, not parseability.
These classes describe authored/observed artifact semantics only;
`Governance-only` does not claim that contribution procedure is unchanged.

No exception, migration, supersession, correction, or authority decision may
silently reinterpret an old artifact. Later rules may reject, migrate, or
decline execution only while identifying its historical regime. Classification
and historical interpretation are non-waivable: an exception cannot downgrade a
change that first matches `Breaking`, or reinterpret any issued version. Other
exceptions record the exact invariant, artifacts, reason, and bounded
consequence.

## Supersession

Accepted decisions have stable IDs `RFC-NNNN-DN`. Supersession is prospective
from the newer acceptance commit. Full supersession retires all future effect;
Partial names exact decision IDs and sections/rules replaced. Both records gain
reciprocal links atomically; outside scope, the older decision continues.

Acceptance claims no tooling, implementation, or independent review.

## Identifiers and corrections

RFC filenames use a four-digit number unique on canonical `main`; numbers are
provisional before acceptance and collision is checked against the candidate's
parent. Decision IDs are `RFC-NNNN-DN`, unique within that RFC and never reused.
An editorial correction records date, actor, commit URL, exact affected text,
and why validity, meaning, identity/version, authority, evidence, and procedure
are unchanged. A disputed classification requires a new RFC.
````

## Exact replacement: `rfcs/0000-template.md`

````markdown
# RFC 0000: Title

- Status: Draft
- Authors: github:login or local:name
- Created: YYYY-MM-DD
- Supersedes: — or Full/Partial with Decision IDs and exact scope
- Superseded by: —
- Decision ID: RFC-0000-D1
- Decision date: —
- Deciding authority: —
- Review: —
- Reviewer: —
- Review relationship: —

## Summary
What changes?
## Problem
What concrete ambiguity or defect exists?
## Proposed normative change
Give complete replacement text or exact diff and the closed ordered manifest.
## Lifecycle event
- Event: creation | revision | acceptance | rejection | withdrawal | supersession | editorial correction
- Actor: github:login or local:name
- Date: YYYY-MM-DD
- Prior state: —
- Resulting state: Draft
- Evidence: public commit URL and public PR/review URL

Authors may create, revise, or withdraw Drafts. The deciding authority may
reject or accept Drafts and approve editorial corrections. Only acceptance of a
later RFC may supersede an Accepted RFC. Unlisted transitions, wrong actors,
missing records, and terminal-content mutations are void.
## Examples
Give accepted and relevant rejected examples.
## Compatibility
Apply the first match: Breaking (invalidity or changed backward meaning);
Compatible (same validity and backward meaning, additions allowed);
Governance-only (artifact validity and meaning unchanged). Identify historical
regimes. Classification and historical interpretation cannot be waived.
An exception cannot downgrade Breaking or reinterpret an issued version.
## Core and profiles
Name every affected registered target.
## Supersession
Write None, or Full/Partial with stable Decision IDs and exact scope; explain
prospective precedence and reciprocal links.
## Alternatives considered
Record rejected alternatives.
## Future tooling impact
Describe possible impact without authorizing or claiming tooling.
## Decision
Pending while Draft. On disposition record outcome, Decision ID/date, structured
authority, review, full candidate SHA, closed ordered manifest, every P0/P1
disposition, compatibility class, and exceptions (exact invariant, artifacts,
reason, bounded consequence). Review records name reviewer identity, candidate
SHA, evidence, date, findings, dispositions, and exactly one relationship:
independent, self-review, or cold-local-audit. Cold-local-audit means a
no-parent-context report recorded in the PR, not independent certification.

For acceptance, list every linked P0/P1 finding and disposition; write `none`
only when every linked report has zero P0/P1. Dates use UTC `YYYY-MM-DD`.
RFC numbers are unique four-digit values on canonical `main`; Decision IDs are
unique within one RFC and never reused. An editorial correction records date,
actor, commit URL, affected text, and the preserved normative answers.
````

## Compatibility

`Governance-only` by the ordered test. Artifact meaning is unchanged.

## Decision

Withdrawn by the author on 2026-09-03 following the repository owner's explicit
choice to replace it with narrower governance. The RFC completed five cold
local-polish passes and did not converge. Residual P1 findings were:

1. `Governance-only` was unreachable under the proposed classification order.
2. The permitted acceptance diff could not make RFC 0001 satisfy its own new
   record schema.
3. Concurrent candidates were not serialized against the canonical branch tip.
4. The required set of review reports remained selectable rather than closed.
5. Lifecycle-event history and supersession manifests lacked one unambiguous
   record model.

No target text from this RFC is adopted. A narrower replacement must receive a
new RFC number and its own local polish.
