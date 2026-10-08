# Using the notes in everyday work

Personal working habits, revised 2026-09-25. Adapt what helps; nothing here is
behaviorally qualified, and none of it requires installing agents or adopting
the research material.

## Start a task

Use this brief with your existing instructions. Fill only what matters:

```text
Outcome: [observable result and intended user]
Scope: [repository/folder, allowed sources, included and excluded work]
Authority: [local changes allowed; delegation allowed or not; external or consequential actions excluded]
Acceptance: [what would make this result useful and how to check it]
Open decisions: [what only I or another named owner can decide]

Inspect the relevant existing guidance and evidence. Choose the lightest
useful approach: direct work, discovery, a probe, or a spec. State a short plan
for non-trivial work and proceed within this authority. Keep one owner unless the authority above allows delegation.
Return the result, evidence, exact checks, gaps, and any next decision.
```

For a small edit, that can be the whole setup. For longer or riskier work, use
the [workflow](agentic-development-workflow.md) and the
[spec-driven procedure](skills/spec-driven-change/SKILL.md).

## Review the result, then get it merged

- Read the diff before the agent's summary. A summary that says done or `OK`
  is a claim until it names the criterion, the anchor, and the check that ran.
- Use the returned completion record as the PR or MR description: what
  changed, exact checks and outcomes, checks not run and why, and residual
  risk.
- CI is one of those checks, not the acceptance criteria. A green pipeline
  does not show that the intended behavior, recovery path, or cleanup exists.
- The team's human reviewer is the acceptance gate. An agent review, even from
  a fresh session, is pre-review, not approval.
- Keep one branch or worktree per task and commits sized for review. The agent
  commits, pushes, or opens a PR only when asked.
- Know what a merge triggers in that repository. Where merging deploys, it is
  a release decision with a named owner and an observation window; see the
  workflow's [handoff section](agentic-development-workflow.md#handoff-and-operational-feedback).

## When a session goes sideways

- Start a fresh session with a short packet — intent, acceptance, what is done,
  what failed, the current diff — rather than compacting or correcting through
  accumulated confusion. Compaction or rewind is not a substitute for version
  control.
- Keep context lean: check what actually loaded (`/context` in Claude Code),
  load a skill or guide when its trigger fires, and do not paste whole
  document sets.
- Take the task back when the next step is quicker to type than to specify,
  when the agent repeats an approach that already failed, or when the change
  needs a judgment you cannot hand over.
- For a session whose reasoning went wrong — an invented specific, a
  retraction built on an empty-looking result, a recommendation that drifted —
  audit it with the [trace self-audit template](../verification-kit/trace-self-audit-template.md),
  on a surface that transcript is allowed to reach. It is for the occasional
  bad session, not every session.

## Changing your setup (optional)

| Surface | Proposed destination | Smallest adoption step | Verify after an approved change |
| --- | --- | --- | --- |
| Codex | Personal `AGENTS.md` in the Codex home the host actually loads; repository rules remain local | Compare [the Codex sample](AGENTS.example.md) with existing personal/managed guidance and retain only missing principles | Start a new task in the intended checkout; inspect loaded guidance and effective permissions; try a bounded read-only task |
| Claude Code | User `~/.claude/CLAUDE.md`; repository guidance via the active instruction mechanism | Compare [the Claude Code sample](CLAUDE.example.md); keep the repository's existing thin `CLAUDE.md` import where used | Inspect `/context` and `/memory`, check for duplicate or excluded instructions, then try the same bounded task |
| Cowork | Global instruction field for general preferences; project/folder instructions for source and output boundaries | Adapt [the Cowork copy sheet](cowork-instructions.example.md) in the visible UI, starting with a disposable working folder; first check whether a local session already loads your Claude Code user file | Record session type, selected folder/project, available actions, and output location; inspect the resulting files and actions |

Before changing live settings, diff the sample against what you already have
and keep only the missing rules. Leave out exact model IDs, worker counts,
auto-routing, repository commands, and copied organization instructions; keep
credentials, evidence not approved for that surface, and full coding-host
configuration out of Cowork fields, and personal setup or experiment history
out of repository instructions. Check imports, collisions, and any
generated-file owner before accepting the change; this repository does not
manage those settings. Keep mandatory managed settings as they are and change
them only through their owner. After a change, start a fresh session and check
what loaded; if loading or boundaries are unclear, restore the previous content
and use the task brief meanwhile.

The [Cursor sample](cursor-user-defaults.example.mdc) carries the same
task-scale paragraph as the Codex and Claude Code samples; install and verify
it through the [Cursor notes](cursor-notes.md). Organization-specific evidence
routes — company search, cross-repository code search, documentation, the
source host, a tool catalog — belong in your own workspace or user
instructions, where they can name real systems; the samples here stay generic.
The mechanics and primary-source dates live in the
[OpenAI surface notes](openai-surfaces-notes.md),
[Claude Code notes](claude-code-notes.md), and [Cowork notes](cowork-notes.md).
The table is a proposed destination, not confirmation of the reader's
installed client, account entitlements, or corporate policy.

For repository guidance, the README owns orientation and navigation, and the
repository's `AGENTS.md` owns local commands and working rules, with enough
vocabulary for a fresh agent to begin. The root `AGENTS.md` in **this**
repository opens with a short orientation for an agent you point at these
notes; its "Editing this repository" section is contributor guidance for
editing them. Neither part is a
personal core to install.

## Keep what helps

Keep instructions only where they reduced repeated coaching or prevented a
specific error. A single successful use establishes usability on that task,
not superiority. Formal comparisons follow the
[evaluation protocol](evaluations/README.md); colleague feedback and public
sharing follow the [sharing checklist](sharing-and-release.md).
