# R3 — Blended versus two-ledger review

Fixture version: 1

Status: frozen protocol, 2026-09-04

Operator grader: [R3 grader](../graders/R3-two-axis-review.md). The exact
candidate, source anchors, prompts, and held-out key belong in the ignored
private overlay.

## Question

Does visibly separating specification conformance from engineering risk help
one reviewer catch and classify material defects without buying parallel-agent
cost?

This fixture evaluates review structure. It does not compare models or effort,
authorize edits, or establish that two agents are useful.

## Conditions

| Condition | Review structure |
| --- | --- |
| A — blended | Current concise reviewer contract: inspect intent, rules, and reachable risk; return actionable evidence-backed findings and a scoped gate recommendation |
| B — two ledgers | The same contract plus independently reported conformance and engineering-risk ledgers; neither axis can compensate for the other |

Use one fresh owner per condition with the same self-contained candidate,
model, effort, global instructions, read-only/no-tool boundary, output schema,
and wall/output ceiling. Condition B changes only the review-structure prefix.
Do not delegate either condition.

## Target selection

Freeze a small complete change packet containing:

- explicit behavioral requirements and out-of-scope items;
- documented repository rules;
- a candidate diff with at least one conformance-only defect, one
  standards/risk-only defect, one hunk relevant to both for distinct reasons,
  and one tempting unsupported finding;
- stable source identifiers that do not require repository access; and
- a held-out operator key with acceptable classifications and severities.

The packet must be understandable without domain credentials, external
sources, execution, or author reasoning.

## Shared output contract

Return at most 900 words. Each finding must include severity, exact source
anchor, violated requirement/rule or risk invariant, reachable impact, and the
smallest correction direction. Finish with coverage gaps, checks/not checked,
and a scoped gate recommendation. Do not propose unrelated refactors, report
style preference as a defect, or claim execution.

Condition B additionally keeps the two ledgers visibly separate, reports the
count and worst finding within each, and derives the gate mechanically from
blocking findings. It does not rank one axis above the other.

## Budgets and safety

- One owner, zero tools, zero delegates, at most five wall-clock minutes.
- Chat output only; no file, repository, network, app, MCP, credential,
  tracker, commit, or external action.
- A missing source is reported as missing rather than replaced with an
  invented rule.

## Predeclared comparison rule

The two-ledger treatment advances only when it passes every critical
conformance, engineering-risk, classification, grounding, route, and output
criterion; repairs at least one material baseline miss or misclassification;
and stays within 1.25 times baseline wall time and total exposed tokens. A tie
keeps the blended reviewer contract. One synthetic win permits a real-task
pilot; it does not install a skill or authorize parallel reviewers.

## Measures

Record per-axis fact coverage, classifications, duplicated findings,
unsupported claims, source anchors, output words, wall time, exposed token
classes, effective model/effort/context, tools/delegates, retries, operator
review time when available, and cleanup.
