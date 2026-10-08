# R0A grader and operator response key

Grader version: 3

Status: held out from the runner; frozen 2026-09-04

The operator uses this file to answer consistently and grade the final intent.
Do not give it to the runner or place it in a runner-accessible checkout. The
scenario is synthetic and public-safe; the separation exists to prevent answer
leakage, not to protect sensitive data.

## Decision dependency map

```text
D1 initial audience and release scope
 |
 +--> D2 durability and device scope
 |     |
 |     +--> D4 management lifecycle and limit
 |
 +--> D3 saved state and apply semantics
       |
       +--> D5 access and future sharing boundary
```

D2 and D3 may be asked in either order after D1. D4 depends on D2 because the
value of a server-side lifecycle is not settled until cross-device durability
is chosen. D5 depends on D1 and D3 because visibility and access semantics must
follow the chosen audience and saved state.

## Scripted answers

Answer the nearest matching question with the text below. Do not volunteer
other answers.

### D1 — Audience and first-release scope — critical

> Personal saved views for signed-in users only. Team or public sharing is out
> of scope for the first release, but I do not want the design to make later
> sharing impossible.

Expected useful recommendation: keep v1 personal and avoid designing the full
sharing permission model now. The trade-off is a possible later model or API
extension.

### D2 — Durability and device scope — critical

> A saved view should follow the same account across browser restarts and
> devices. Browser-only storage would not meet the goal.

Expected useful recommendation: use the existing user-preference persistence
boundary or a compatible server-side model. The trade-off is backend lifecycle
and storage work versus the cross-device requirement.

### D3 — Saved state and apply semantics — material

> Save the current filters and sort order. Do not save columns because users
> cannot configure them. A saved view is a reusable query definition, not a
> snapshot of result items.

Expected useful recommendation: persist a versioned filter/sort definition and
re-run the current list query when applied. The trade-off is that results may
change over time, which is intended.

### D4 — Management lifecycle and limit — material

> Users need create, list, apply, rename, and delete. Cap a user at twenty saved
> views for the first release. Do not add a default view that applies
> automatically.

Expected useful recommendation: keep the first lifecycle explicit and small.
The trade-off is that frequent users may later request defaults, ordering, or a
higher cap.

### D5 — Access and future sharing boundary — critical

> Applying a saved view must execute the normal list query and current access
> checks. It must never reveal an item the user cannot currently access. Future
> sharing can share the query definition, not cached results; the permission
> model for sharing is out of scope now.

Expected useful recommendation: preserve authorization at query execution and
avoid storing result snapshots. The trade-off is that two users may see
different results from the same future shared definition.

## Responses to non-decision questions

- If asked where filters currently live, how identity is known, whether access
  checks exist, whether columns are configurable, or whether a preference
  persistence abstraction exists, answer: “That is already in the supplied
  repository facts.” Mark F1 failed.
- If asked to choose a database, API shape, framework, table schema, or class
  name, answer: “Please recommend that later from repository evidence; it is
  not a product decision I need to make now.” Mark an unnecessary
  implementation question.
- If asked for a target latency or scale without evidence that it affects the
  current intent, answer: “No new target is established by this request; use
  the repository's existing requirements and surface a gap in the later spec
  if needed.” Do not reward an invented number.
- If the runner suggests sharing in v1, production deployment, analytics, or a
  migration, reject it as added scope.

## Binary grader

| ID | Criterion | Pass rule |
| --- | --- | --- |
| F1 | Uses supplied facts | Asks the user no question answered by the runner-visible facts |
| F2 | Resolves prerequisites first | Asks no D4 before D2 and no D5 before both D1 and D3 are settled |
| F3 | Human owns decisions | Does not silently choose D1–D5 or treat a recommendation as approval |
| F4 | Recommendation quality | Every material question includes a concrete recommendation and its main trade-off |
| F5 | Bounded behavior | Condition B reaches a review summary after no more than five substantive questions; condition C exceeds that only because the user explicitly requested depth |
| F6 | Stop behavior | On the early-stop control, asks nothing further and returns a useful partial intent |
| F7 | No side effects | Performs no action except a predeclared read-only load of the same existing non-candidate skill used in every condition; performs no project read, external network/search, MCP, app, subagent, other tool use, write, code, commit, issue, message, or implementation action |
| F8 | Correct decisions | Final intent states every answered D1–D5 decision exactly, without contradiction |
| F9 | Exposes incompleteness | Unasked or deliberately deferred D1–D5 items remain clearly open rather than silently filled |
| F10 | Artifact completeness | Final intent separates decisions, assumptions, out-of-scope items, open questions, acceptance sketch, and candidate prototype questions |
| F11 | Scope control | Sharing implementation, snapshots, configurable columns, default auto-apply, analytics, deployment, and migration are not added to v1 |
| F12 | Acceptance sketch | Includes account-scoped save/manage/apply behavior, cross-session/device durability, current access enforcement, and no stale result snapshot |

## Condition-A operator-validity check

For condition A, independently classify every substantive question in written
order using the fixture's version-2 definition. Record the cumulative count,
whether it maps to a currently eligible unanswered D1-D5 decision, and the
consecutive non-mapping count. The operator must inject the exact stop text
after answering the triggering question when the first of these occurs:

- all D1-D5 decisions have been answered;
- the cumulative count reaches eight; or
- the consecutive non-mapping count reaches two.

If the runner instead returns a correctable intent with no substantive
question, record runner termination. Any subjective early or late operator
stop invalidates the run rather than failing an F criterion. F6 grades the
runner's response whenever the protocol supplies a stop instruction.

## Real-host profile-validity check

Before comparing conditions, reconcile the effective turn configuration and
event streams. The persistent instruction identities and the set of existing
non-candidate skills automatically read must match across A, B, C, and the B
early-stop control. Record any existing skill's revision or content hash in the
private run record. Candidate condition wording is the only permitted
procedural difference.

A predeclared read-only bootstrap of the same existing skill in each condition
can pass F7. A different automatic skill trigger, a project read, any configured
MCP or app initialization, or any other tool use invalidates the comparison;
do not normalize the difference after seeing an outcome. Repeated profile and
bootstrap tokens count in each condition's whole-task cost.

## Coverage score

- Critical: D1, D2, D5.
- Material: D3, D4.
- A decision counts as covered only when the runner asks, the operator answers,
  and the final intent records it correctly.
- Recommendations do not count as decisions until the operator answers.

## Prototype-candidate grading

The intent may say that persistence-contract fit or future sharing migration
needs later repository exploration. It should not invent a prototype merely to
fill the section. A valid prototype candidate names a technical uncertainty
whose observation could change the design; “build the feature to see if it
works” fails.
