# Claude Code — practical operating notes

Reference, not always-loaded context. Primary documentation checked 2026-09-24
(MCP, permission rules, and instruction loading 2026-09-25; all rechecked
2026-10-01 without changes). One instruction-loading probe was run on
2026-09-25 (see Instruction placement) and one partial subagent probe on
2026-10-01 (see Bounded subagents); no other behavior probe was run. The [user-global sample](CLAUDE.example.md) is
illustrative; the [everyday guide](agentic-development-adoption.md) covers
adoption steps. Managed environments may differ. Resolve current models and
supported settings on the destination host rather than preserving a model alias
as a durable rule.

## Instruction placement

User instructions live at `~/.claude/CLAUDE.md`; project instructions can use
`CLAUDE.md` and imports such as `@AGENTS.md`. Current releases also document
direct `AGENTS.md` loading, conditional on version, settings, and other project
instruction files. This repository retains its thin import. Inspect `/context`
and `/memory` after changes instead of assuming a file loaded. Instructions
and auto memory are context, not enforced configuration.
[Instruction discovery](https://code.claude.com/docs/en/memory)

To check loading from a script or across folders, ask a fresh headless session
with no tools to quote a distinctive line from each file under test, plus a
planted token that should appear nowhere: `claude -p "..." --tools ""
--strict-mcp-config --no-session-persistence`. Without `--tools ""` the session
can read files on demand, and every case passes. Ask for quoted lines rather
than yes/no answers, and repeat a run. On 2026-09-25 on one workstation, such a
check showed that a `CLAUDE.md` in a parent folder stopped a repository's own
`AGENTS.md` from loading; a two-line `CLAUDE.md` containing `@AGENTS.md` fixed
it. The **Project instructions** setting (`instructionFiles`:
`claude-md-and-agents-md`), set at
user level, loads both files together where `AGENTS.md` support is available,
but also loads `AGENTS.md` files you may not mean as instructions, such as
copies kept in a dotfiles repository.

Keep personal defaults, local repository commands, and conditional procedures
in separate scopes. Do not import this entire guide or the research backlog.
After an approved change, check for duplicated guidance and preserve the
owning configuration's update and rollback route.

## Bounded subagents

Custom subagents can live in `.claude/agents/` or `~/.claude/agents/` and have
separate context, tool selection, model, and permission fields. Omitted tools
inherit available tools. Parent permission modes can override a child's
`permissionMode`, and plugin agents ignore some fields, including that one.
Read the current precedence rules before claiming a reviewer is constrained.
Interactive sessions enable fork mode by default, and a fork inherits the whole
conversation; use a named custom subagent or a new session when a fresh packet
or independent reviewer matters.
[Subagent configuration](https://code.claude.com/docs/en/sub-agents)

Partial probe on one workstation, 2026-10-01, not an evaluation: a read-only
lookup role that keeps Bash behind an allowlist hook allowed a read and blocked
a file write and a shell redirect; two reviews then found allowlist bypasses,
since closed. A session that had loaded the agent definition before the hook
was added kept dispatching without it, while fresh sessions enforced it, so
start a fresh session before trusting a changed role. Identity and
cancellation were not probed; M1 in the
[measurement candidates](evaluations/measurement-candidates.md) is the planned
check.

For when to delegate and what to hand over, use the
[workflow gate and packet](agentic-development-workflow.md#fan-out-gate); a
subagent's `OK` is a claim until its criterion, anchor, and check are shown.

## MCP servers

`claude mcp list` shows a status for each server it lists, such as connected or
needing authentication (WebSocket servers appear only in `claude mcp get` or
`/mcp`). A listed or connected server is still not a working route until one
known-answer read-only query succeeds. Permission allow rules for MCP tools
must name the server (`mcp__<server>__<tool>` or `mcp__<server>__*`); an
unanchored `mcp__*` allow glob is skipped, while a deny rule may use it. Allow
only the read tools a task needs, because a server such as an IDE bridge can
also expose build, terminal, and edit tools. See the workflow's
[discovery ladder and tool use](agentic-development-workflow.md#discovery-ladder-and-tool-use).
[MCP](https://code.claude.com/docs/en/mcp),
[Permission rules](https://code.claude.com/docs/en/permissions)

## Permissions and completion

Use permissions, sandboxing, and applicable hooks for enforceable action
boundaries. Their scope matters: a tool rule must match the actual route, and
a hook is not a universal security boundary. Prose cannot prove denial, and a
clean final tree cannot prove that no forbidden action occurred.
[Permission rules](https://code.claude.com/docs/en/permissions)

Derive checks from the repository. A hook may automate a deterministic gate,
but do not add one until its trigger, bypasses, failure, and recovery are
understood. A passed test does not establish complete intent, secure behavior,
or operational recovery. Keep independent review and human decisions distinct.

Effort is not a spend cap. Record effective configuration for comparisons,
include approval and integration cost, and recheck after model/host drift.
A missing model or feature needs current diagnosis; do not assume the cause is
client age or recommend an update without checking the active environment.

## Continuity and rollback

Keep long-task intent and acceptance in a durable artifact, progress in a
separate plan, and verification with the candidate. On interruption, identify
partial work, pending checks, owned temporary state, and the next authorized
step. Session compaction or rewind is not a substitute for a reviewed diff,
version control, or recovery of external effects.

Cowork uses a separate [surface guide](cowork-notes.md). Do not infer equivalent
instruction discovery, context independence, or permission controls from the
shared product family.
