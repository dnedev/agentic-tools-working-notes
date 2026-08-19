---
name: spec-driven-change
description: "Use when a coding change is large enough that intent can drift from implementation: work spanning multiple sessions or context windows, a feature touching many files or services, requirements that are ambiguous or contested, or anything where being wrong is expensive (payments, auth, migrations, data deletion, anything customer-facing). Produces a durable spec and a volatile execution plan, then implements task by task against binary acceptance criteria. Do NOT use for single-file edits, one-line fixes, adding a field, renaming, or any change fully describable in a sentence — the overhead makes simple work worse."
---

# Spec-driven change

> **Sanitized, illustrative sample** of an installed skill — one engineer's
> lightweight take on spec-driven development. Not a framework, policy, or
> best-practice claim. It is **synthesized from public writing** on the
> subject rather than distilled from personal usage traces: a digest of
> others' practice, not a personally-validated finding, and not yet
> exercised end-to-end on a real multi-session change. The closing section
> says which parts are externally informed. Repo-relative links below stop
> resolving once this directory is copied out.

A lightweight version of spec-driven development. The goal is one thing:
**stop intent from drifting away from implementation** on work too big to
hold in a single session.

## Check the trigger first

This skill is overhead. On a small change it is strictly worse than a
precise one-shot prompt — more steps, more files, same result. Before
running it, confirm at least one is true:

- the work spans more than one session or context window
- it touches multiple files, modules, or services
- the requirements are ambiguous, contested, or came from someone else
- being wrong is expensive: money, auth, migrations, deletion, customer-facing

None true → skip this skill, make the change, verify it, done. Say that
you're skipping and why, so the choice is visible rather than silent.

## Level: spec-anchored

Three levels exist — spec-first (write it, use it, discard it),
spec-anchored (it lives alongside the code and both evolve), and
spec-as-source (only the spec is edited by hand). **Target spec-anchored.**
Code stays the source of truth, tests stay the enforcer, and the spec
stays current enough to onboard a fresh session faster than reading the
code.

## Separate what from how

The most important structural rule. Two artifacts, different lifetimes:

- **The spec** — what we're building and why. Durable, lives in the repo,
  reviewed, updated whenever reality diverges from it.
- **The plan** — which piece to build next, and how. Volatile, a delta,
  discardable once the task is done, doesn't need to be committed.

Merging them blurs the line between spec and code, and once that happens
the spec stops being worth reading.

For anything but the smallest features, prefer **one spec per feature**
over a monolithic document — lighter on context, and far likelier to
survive.

Published toolchains split three ways rather than two, breaking the task
list out from the plan. Two is a deliberate choice here: the plan below is
already discardable, so a third artifact adds a file to keep in sync
without adding a lifetime the other two don't cover.

## The loop

**1 — Specify.** Best written in dialogue, not dictated: describe the
intent, let the model structure it, surface missing requirements and
vague language. Gather technical requirements by *reading the existing
code*, not by guessing at it. Cover what the change does, who it's for,
the functional requirements, and the edge cases and non-happy paths.
Leave out implementation detail that doesn't matter — over-specifying
blurs spec into code; under-specifying leaves too much to interpretation.

When work changes the ownership or lifetime of state, resources,
registrations, or scheduled or long-running activity — or changes persistent
data through a migration — specify the applicable terminal, failure, recovery,
compensation, reversal, and cleanup behavior. This is a trigger, not a stock
section: include only paths the change can actually encounter.

Calibrate detail to **risk**: a local script gets a paragraph; anything
touching money, auth, or customer data gets the edge cases written out.

If the repo has shared, org-wide non-functional requirements, **link
them, don't restate them.** Same non-duplication rule that governs the
instruction layers.

**2 — Plan, then decompose.** Settle the approach first; break it into
tasks as a **separate pass**, not in the same breath. Folding
decomposition into planning is how a plan becomes a wish — it's the
ordering constraints that expose step four needing something step two was
supposed to produce. Tasks should be small enough that one fits in one
session and can be implemented *and tested* within it.

Each task gets **binary acceptance criteria** — checkable by a human or a
test, not "works correctly." The requirements-engineering notation EARS
gives that a shape worth borrowing, in its event-driven pattern:

```
WHEN <trigger>
THE SYSTEM SHALL <observable behavior>
```

The value isn't the ceremony — it's that an untestable criterion fails to
fit the template and you notice while writing rather than while reviewing.
"The endpoint should be fast" won't go in the form; "WHEN a list request
exceeds 200 rows THE SYSTEM SHALL return a cursor instead of a full
result set" does. EARS defines other patterns too — `WHILE` for
state-dependent behavior, `IF`/`THEN` for unwanted conditions — so reach
past the one form when it starts distorting what you mean.

Where Specify identified lifecycle or operational obligations, make the
applicable terminal, failure, recovery, compensation, reversal, or cleanup
behavior and its evidence part of the acceptance criteria. A criterion that
covers only initiation or the happy path is incomplete. For runtime or
deployment behavior, include the signal that distinguishes acceptable
operation from failure or degradation.

The notation is from Mavin, Wilkinson, Harwood & Novak, RE'09
(<https://doi.org/10.1109/RE.2009.9>).

If the plan can't be written without a decision that affects more than one
file's public API, that decision gets an
[ADR stub](../adr-stub/SKILL.md) before the plan does.

Review the plan before any code is written; this is the cheapest possible
moment to catch a wrong frame.

**3 — Implement.** One task at a time. Don't hand over the whole spec and
hope. When implementation forces a decision the spec didn't anticipate —
and it will — **update the spec**. Every unspecified decision is a spec
gap, and an out-of-date spec is worse than none because it's trusted.

Amend it as a **diff to the spec file**, with the reason, not as a
decision remembered in conversation. And **never amend a criterion to
match what got built** — that turns a failed check into a passing one by
editing the exam. It's the same move as weakening a test, and the spec is
a check.

**4 — Validate.** Tests, then review. For anything non-trivial, run the
review in a **fresh session** — a clean context catches what the context
that wrote the code cannot. Agent review is support, not a replacement:
for critical changes, a human signs off. You are accountable for what
ships regardless of who typed it.

Run what the project actually configures, not what you assume it has. Derive
the relevant gates from the closest instructions, manifests and task runners,
CI workflows, and tracked hook configuration, then trace the scripts they
invoke and when they run. Treat those surfaces as evidence: a present or green
workflow does not show that a conditional check ran, and a local hook may be
absent or bypassed.

Prefer the repository's canonical local commands and targeted tests over the
full suite unless the change is broad. Do not blindly reproduce cloud-only,
secret-dependent, deployment, publishing, or unrelated jobs. A failure from a
check the project never adopted is noise, and reporting it as a finding is
worse than noise.

## Signals you've got it about right

- The spec answers "what are we building" without answering "how does the
  code do it."
- A fresh session can pick up the plan and make progress without you
  re-explaining anything.
- Review comments have moved from "this is wrong" to nitpicking. When the
  reviewer starts arguing about trivia, the important issues are handled.
- The spec still matches the code after the third task. If it doesn't,
  the loop broke at step 3.

## Failure modes

- **Ceremony on small work.** The trigger check exists for this. Skipping
  it is the most common way this discipline turns into overhead.
- **Spec rot.** Updated during Specify, never again. A stale spec is worse
  than no spec — it gets trusted.
- **Spec that's just code in prose.** If it's pinning down implementation,
  it's the plan, not the spec.
- **One giant task.** If a task can't be implemented and tested in one
  session, it isn't decomposed yet.
- **Happy-path-only lifecycle.** The spec covers initiation or normal operation
  but omits applicable terminal, failure, recovery, compensation, reversal, or
  cleanup behavior.
- **Rubber-stamp validation.** A review by the same context that wrote the
  code grades its own homework.
- **Amending the spec to match the diff.** Silent divergence is bad; a
  criterion quietly relaxed until the implementation passes it is worse,
  because the spec now certifies the thing it was supposed to catch.

## Where this came from

Several rules above match entries in
[`evolution-and-lessons.md`](../../../verification-kit/evolution-and-lessons.md)
— binary acceptance criteria, one-layer-per-rule (here: link shared
requirements rather than restate them), and fresh-session review are all
there, and are also where an unrelated published field report landed
independently (that file's July entry). Read the match as **convergence,
not lineage**: this file was synthesized from public writing, while those
entries came out of runs. The overlap is an external signal about the
tools, not validation of the method.

The separate decomposition pass was informed by the three-artifact workflows in
[GitHub Spec Kit](https://github.com/github/spec-kit) and
[Kiro specs](https://kiro.dev/docs/specs/). Kiro's
[requirements-first workflow](https://kiro.dev/docs/specs/feature-specs/requirements-first/)
also uses the EARS criterion shape. The amendment guardrail and original
project-configured-checks rule were synthesized from surrounding
spec-driven-development writing rather than drawn from my own runs. No source
text is copied here. These pieces remain because the gaps they close were real
ones: an earlier version of this file said nothing whatsoever about a spec
turning out wrong, and folded decomposition into planning where the ordering
constraints go unexamined.

The repository-contract and lifecycle additions were prompted by two omissions
in my own agent-assisted development work, informed by external structure, and
are not yet regression-tested as a package. The split between repository-native
commands, CI, and hooks is consistent with GitHub's
[`scripts-to-rule-them-all`](https://github.com/github/scripts-to-rule-them-all)
pattern and Git's documentation that client-side
[`pre-commit` hooks](https://git-scm.com/docs/githooks#_pre_commit) can be
bypassed. The risk-scaled lifecycle lens is consistent with Google SRE's
service-specific [production-readiness review](https://sre.google/sre-book/evolving-sre-engagement-model/),
the Twelve-Factor App's [disposability](https://12factor.net/disposability),
and AWS's guidance on [small, reversible changes](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_dev_integ_freq_sm_rev_chg.html).
That convergence motivated a trigger, not a universal checklist. Externally
informed structure remains locally unverified; weigh it accordingly.

---

Sanitized for sharing — last revised 2026-08-12, adding repository-contract
discovery and risk-scaled lifecycle acceptance criteria. The prior revision
added the separate decomposition pass, the EARS criterion shape, the amendment
guardrail, the project-configured-checks rule, and the ADR-stub cross-reference.
The frontmatter is the installed version's, unshortened: this 620-character
`description` loads under both Claude Code and Codex, from the same file —
which says nothing about a parser ceiling, and the documented figures aren't
ceilings either. The portable spec allows 1–1,024 characters. Claude Code
truncates the combined `description` and `when_to_use` *listing* text at
1,536. Codex caps the initial skill list in aggregate — 2% of context, or
8,000 characters when that's unknown — and shortens descriptions to fit. The
spec also recommends the body stay under 5,000 tokens and the file under 500
lines.
