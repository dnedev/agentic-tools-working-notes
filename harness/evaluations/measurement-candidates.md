# Delegation and review measurement candidates

Status: design only, 2026-10-01. None of these has been run; the delegation
skill recorded [below](#candidate-a-delegation-skill-for-chat-and-cowork) on
2026-10-11 has its own status. They follow from a
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

## Candidate: a delegation skill for chat and Cowork

Status: recorded 2026-10-11 as a candidate projection for chat and Cowork,
not added to the [shared skills](../README.md#samples-by-tool). Unlike the
rows above, it has had two runs, neither of them a comparison.

The author drafted a skill, in the claude.ai project, that carries the
[Claude Code sample](../CLAUDE.example.md)'s delegation rules into chat and
Cowork: the fan-out gate, a model named on every call, a brief that carries
the rules because subagents there didn't get the profile (see the
[Cowork notes](../cowork-notes.md#delegation-as-observed-2026-10-11)), scout
and critic contracts, and checking what comes back. It had one critique by a
Fable-class agent before use, then two runs on 2026-10-11, one inside a
project and one outside any project, each checked against five criteria fixed
before the first run:

1. The skill loads before the first agent call.
2. The model is named, and the independent check runs on a model other than
   the writer's.
3. The brief carries scope, a budget and stop rule, an anchored return, and
   the refusal line.
4. The agent count, models, and rough cost are stated before launch.
5. The results are checked.

Both runs loaded the skill from its description alone, did the lookups in the
main session, and gated delegation to one blind verifier on a different
model, with a brief that carried scope, evidence rules, a budget, a stop rule,
and the refusal line; both checked the result against its anchors. Cost
estimates ran several times low or were given in calls rather than tokens,
and in one run the verifier overran its stated call ceiling. The Sonnet-class
lookup route was never exercised. The second run was graded from its
transcript in the claude.ai project the skill came from; neither is recorded
as graded independently.

As a shared skill, it doesn't meet the bar of the
[selective-derivation decision](../decisions/0001-selective-skill-derivation.md).
Neither run had a baseline arm, so the runs show the skill loading and being
followed, not doing better than the profile and sample alone, and the skill
puts host model classes and surface mechanics into what the decision keeps
as a neutral contract. The decision's own shape fits it better: the neutral
rules stay with the workflow's
[gate](../agentic-development-workflow.md#fan-out-gate) and
[packet](../agentic-development-workflow.md#worker-packet-and-return), the
Claude Code sample stays their Claude Code projection, and the skill becomes
a tested projection for chat and Cowork that carries only what differs there
(no effort setting, no profile in a subagent, roles held read-only by
instruction) and points to the workflow for the rest. As drafted, it
restates rules the workflow and the sample already state, so adding it would
make another home for them.

No surface switch keeps it to chat and Cowork. claude.ai turns a skill on or
off for the whole account, and an account skill also loads in Claude Code's
cloud and signed-in terminal sessions; in a cloud session, this one was
listed next to the user file's own delegation rules
([Claude Code notes](../claude-code-notes.md#cloud-sessions)). Keeping it out
of Claude Code is a setting on the Claude Code side. The author means it for
chat and Cowork only: in Claude Code, the sample's delegation section, a
plugin workflow (superpowers, for one), and the host's workflow mode already
cover fan-out, so a synced copy there would be one more trigger for the same
moment.

The smallest useful comparison: the same frozen prompts in chat and in a
Cowork task, with and without the skill, graded blind on the five criteria
plus cost-estimate accuracy and budget adherence, with a task that needs a
lookup agent. Cowork's skill-creator is documented to run the same prompts
without the skill as a baseline, which could supply the missing arm for the
Cowork runs, though not in chat; blind grading would still need arranging.
[Create custom skills](https://claude.com/docs/skills/how-to)
