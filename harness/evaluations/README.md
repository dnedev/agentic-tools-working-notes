# Agentic-development evaluations

These are small, frozen instruments for one engineer's agentic-development
pilot. They compare one mechanism at a time against a cheaper baseline. Passing
a fixture is evidence to continue testing, not proof of general productivity or
permission to install a skill.

## Evidence status

The [evidence status](../evidence-status.md) is the one place that interprets
the dated observations: valid results, invalid treatments, marker-only
preflights, and unrun candidates. There is no qualified useful-delegation
winner or completed model/effort tuning stage. Trials were sparse, with
incomplete human/phase timing and without established blinded independent
grading; on material host or model drift, rerun both arms under current matched
conditions.

## Current instruments

- [Source intake and overlap](source-intake-and-overlap.md) — frozen record of
  pinned public sources, local baselines, mechanism contracts, and outcomes.
- [Run-record template](run-record-template.md) — pre-registration, effective
  configuration, cost, grading, side-effect, cleanup, and decision fields.
- [R1P Codex role isolation](fixtures/R1P-codex-role-isolation.md) and its
  [grader](graders/R1P-codex-role-isolation.md) — a cheap marker-only preflight
  for a newly projected role; it does not test useful work.
- [R2 code intelligence](fixtures/R2-code-intelligence.md) and its
  [grader](graders/R2-code-intelligence.md) — local search against the existing
  IDE route on one path trace.
- [R3 two-axis review](fixtures/R3-two-axis-review.md) and its
  [grader](graders/R3-two-axis-review.md) — ordinary review against a
  two-ledger treatment.
- Candidate role contracts — [owner](roles/owner.md), [explorer](roles/explorer.md),
  [reviewer](roles/reviewer.md), and [classifier](roles/classifier.md). They
  are evaluation inputs that specialize the workflow's worker packet, not
  installed agents or evidence that fan-out helps.
- [Measurement candidates](measurement-candidates.md) — delegation and review
  comparisons, design only (2026-10-01); none has run.

Retired fixtures (R0A–R0D) are [archived](../../archive/README.md) as dated
history; the R1 operator template and the unrun R5 fixture are held privately.

## Reproducibility boundary

A method can be reusable without supplying a complete experiment package. R2
and R3 need operator-owned private inputs, and R0D describes a temporary
checker whose source is not retained here. Preserve or create authorized,
sanitized inputs and any required checker before claiming replayability, and
freeze a new version when they change. Do not expose a held-out key to a runner
just because the grader is tracked in this repository.

## Run protocol

1. Copy the run-record template and complete its pre-registration before the
   run starts.
2. Predeclare repetitions, arm order, common stopping rules, a cost ceiling,
   and a rule using actually observable measures. Record who authored and who
   grades the treatment and any blinding or independence limitation. A small
   repeated pilot still does not establish broad statistical validity.
3. Freeze the fixture version, prompt packet, repository revision when used,
   host, model, effort, topology, tools, and permissions. Change only the named
   independent variable.
4. Give the runner only the fixture's **Runner-visible packet**. The operator
   keeps the grader and any held-out answer key out of the runner context.
5. Preflight the execution envelope cheaply: directory, instruction/skill
   loading, tool initialization, permission mode, and measurable cost fields.
   Startup network activity counts even if the model never invokes a tool.
   Keep preflight costs separate and included in full setup cost.
   Use a fresh context. If that is impossible, mark the run invalid rather than
   comparing it as though it were fresh. For a resumable CLI run, launch the
   initial command and every resume from the same declared working directory,
   then verify the effective directory in every turn record; an initial
   directory flag is not evidence that later resume processes preserved it.
6. Record actual effective configuration. A requested model, effort, tool, or
   instruction is not evidence that the host applied it.
7. For a delegated condition, record whether the child received a fresh packet,
   selected context, or a full fork. Before substantive work, use a cheap
   marker-only role preflight when identity or permissions matter. Afterward,
   inspect actual child actions; its summary is not proof of compliance.
   A marker pass is not enforced tool denial. If required action evidence is
   unavailable, do not certify that boundary.
8. Execute the declared checks and cleanup before grading. Record accidental
   side effects even if cleanup succeeds.
9. Grade every binary criterion. Resolve evidence, not majority votes or an
   agent's confidence statement.
10. Apply the predeclared keep/change/retire threshold. A changed threshold
   requires a new run.

## Comparison rules

- Do not expose a baseline result or grader answer to a treatment runner.
- Do not compare different prompts, revisions, permissions, or retrieval
  routes as though only the skill changed.
- Run more than one trial before attributing a small difference to the model.
  Choose repetitions and order before the run; interleave arms and blind the
  decisive grading where feasible. Report single trials as observations.
- Invalid or never-started runs remain visible but are excluded from valid
  comparative averages. A safety breach can retire a candidate immediately;
  it cannot estimate a compliant alternative's economics.
- A win rule requiring unavailable telemetry cannot pass. Record `more evidence`
  or redesign and version the next comparison before execution.
- Separate wall time, active agent time, and human interaction/review time.
  Include approvals, setup, preflights, validation, integration, failed attempts,
  and rework. Do not add overlapping wall intervals as end-to-end latency.
- Document whether cached input is a subset of input and reasoning a subset of
  output before summing tokens. Exposed tokens are not monetary spend; use
  verified class-specific billing only when available.
- Mark unavailable token classes as unavailable; do not derive them from text
  length.
- A treatment with a quality regression loses even if it is faster or cheaper.
- A delegate that receives conflicting owner context or violates its role is
  invalid even when its final answer is correct and cleanup succeeds.
- A treatment that passes one synthetic fixture advances only to a real-task
  pilot. It does not become a default.

## Safety and publication boundary

Fixtures are read-only or use disposable local state. They forbid production
mutation, credentials, sensitive data, external publication, commits, and
deployment. Exact private repository identifiers and raw run transcripts stay
outside the tracked repository. No fixture grants authority beyond its own
declared boundary.
