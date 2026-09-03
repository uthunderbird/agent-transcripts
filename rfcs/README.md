# RFC process

RFCs are the only route for changing the normative files of Agent Transcripts:

- `SPEC.md` — transcript semantics;
- `rfcs/README.md` — this change process;
- `rfcs/0000-template.md` — the required RFC record.

The process is manual. It makes a proposal, review, decision, and effective
change inspectable in Git and GitHub. It does not claim to prevent bypasses.

## Authority

The deciding authority is the fixed identity `github:uthunderbird`. Repository
ownership or write access does not transfer that authority. Changing this rule
itself requires an RFC decided by the authority named here.

## Lifecycle

1. Copy `0000-template.md` to the next unused four-digit number and open a pull
   request containing the Draft RFC and its complete prospective normative
   diff.
2. Run between one and five cold review rounds. A round records the exact base
   and candidate commits reviewed, its verdict, and a committed summary of every
   P0/P1 finding and disposition. The prospective normative diff is
   `git diff <base>..<candidate> -- <normative files>`, where base must be an
   ancestor of candidate. Review by another instance of the same model is cold
   but not independent.
3. A P0/P1 is closed only when fixed with stated evidence, withdrawn by its
   author with a reason, or explicitly overridden by the deciding authority
   with a reason. An RFC with an unresolved P0/P1 cannot be accepted.
4. The final round reviews an exact base/candidate pair. Later commits may
   append only review and decision records or change RFC status. Any other
   change invalidates that round and requires another round within the
   five-round cap.
5. The deciding authority records `Accepted` or `Rejected` in the pull request
   for the same base/candidate pair reviewed by the final round. The RFC then
   records that decision and its status without changing the reviewed proposal
   or normative diff.
6. Acceptance becomes effective only when the RFC, the exact reviewed
   normative diff, and the review and decision records land together on
   `main`. Immediately before landing, the contents of all normative files must
   equal their contents at the reviewed base; after landing, they must equal
   their contents at the reviewed candidate, including absence when either tree
   deletes a path. A branch status, partial merge, or different result is not
   effective.

A Draft may be withdrawn by its author by recording the author identity, date,
pull-request or commit URL, and reason in the RFC. Withdrawal does not require a
decision by the deciding authority. Rejected and Withdrawn RFCs may land as
historical records but do not change normative files. If five rounds end with
an unresolved P0/P1, the RFC cannot be accepted; a replacement starts a new RFC
and a new review budget.

RFC 0003 is the one-time bootstrap for this process. It follows the same six
observable steps by explicit decision of `github:uthunderbird`; its rules become
effective only when its exact bundle lands on `main`. Later process changes are
decided under the version of this file already effective on `main`.

Acceptance means only that this repository adopts the documented change. It
does not claim that tooling or an external implementation exists.
