# Delegation and review measurement candidates

Status: design only, 2026-10-01. None of these has been run. They follow from a
research pass on agent roles, fan-out, and review, and from read-only lookup
and review roles added to the author's live Claude Code and Codex
configuration. Those roles are not evaluated; M1 is their first check. The
partial probes behind them are recorded in the
[Claude Code](../claude-code-notes.md#bounded-subagents) and
[OpenAI](../openai-surfaces-notes.md#codex-delegation-and-adoption) notes. The
[evaluation protocol](README.md) owns validity and measurement; the
[evidence status](../evidence-status.md) records what has actually run.

Freeze the task and source revision, rubric, permission envelope, and model
versions. Record run order, context mode, actual model, effort and fallback,
child count and depth, tool calls, retries, elapsed and human time, accepted
and rejected findings, and rework, including failed or cancelled runs.
Predeclare which resource matters; a latency win doesn't excuse a quality
failure.

| ID / question | Smallest useful comparison | Pass condition | What it cannot prove |
| --- | --- | --- | --- |
| M1 Does a role load and respect its boundary? | One benign fixture per host and role: required marker, known local fact, unavailable-tool case, explicit cancellation; disposable, separately approved probe targets only | Correct identity; source-grounded fact; forbidden effects denied by the intended control; no activity after cancellation where observable. Missing action telemetry means unqualified, not pass | A finite probe isn't a security proof; marker compliance isn't enforcement or useful work |
| M2 Small-task delegation break-even | Known lookup, related lookup batch, noisy exploration: direct tools vs owner-only vs one batched lookup worker, starting with three frozen examples of each | Acceptance checks pass and the candidate improves the predeclared all-in resource on held-out cases, without more rework or unsupported claims; reported per task shape | Screens candidates; can't estimate rare failures or promise savings |
| M3 Does an instruction refactor keep its coverage? | Old vs modular reviewer contract on known instruction conflicts, stale model claims, a correct no-change artifact, and loading-vs-enforcement confusion | No missed critical seeded defect; nothing invented on the clean case; every recommendation sourced; no unrequested rewrite. Context savings count only after that | Seeded cases may favor the rewrite; a later real artifact is still needed |
| M4 Do schemas and graders hold? | A fixed extraction batch plus malformed, ambiguous, and incomplete inputs; a grader given wrong artifacts that pass superficial checks | Exact item coverage and schema; ambiguity kept; the grader rejects a semantically wrong result despite a correct file and format | Structural checks don't establish semantic completeness |
| M5 Does independent review add value? | Blinded correct and defective candidates: owner review, same-model fresh reviewer, cross-model reviewer, matched budgets, rubric frozen first | Seeded defects found; every final finding adjudicated; no false blocking finding on clean candidates; adopt only if marginal real defects or reduced human checking repay the cost | Vendor diversity isn't statistical independence |
| M6 Which review stages survive ablation? | Current workflow vs the same minus one reviewer or critic stage, candidate and acceptance held fixed | Keep a stage only for a repeatable unique accepted finding, less verification work, or explicitly required risk coverage | Rare-risk coverage may need expert judgment |
| M7 Model and effort allocation | On a frozen M2/M5 subset: strong model at low effort, strong at medium, cheaper at medium; both directions for an aggregation step | Critical criteria kept; the gain survives input, cache, output, retry, and human costs; an unknown effective model voids attribution | Holds for tested versions and tasks only |
| M8 Lifecycle and accounting | Offline fixture: worker failure, timeout, duplicate return, missing result, cancellation | Correct terminal state and partial evidence; no orphan worker in the trace; duplicates rejected; stage totals reconcile with available metering | Doesn't validate production load or billing |
| M9 Development and non-development pilot | Reuse an existing real-work pilot's review point plus a small research or document sample; retained roles vs a cheaper baseline | Acceptance evidence and human time for every case; no guardrail regression; the owner can name each role's repeated contribution and upkeep | Still n=1 and specific to that task mix |

Change one role or one contract per experiment. For an instruction change,
map the old requirements to the candidate first, so a shorter prompt can't
win by silently dropping work.
