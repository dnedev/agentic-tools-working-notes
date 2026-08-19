# Cursor — durable operating principles

Companion to the installable
[`cursor-user-defaults.example.mdc`](cursor-user-defaults.example.mdc), the
[Claude Code notes](claude-code-notes.md), and the
[verification kit](../verification-kit/README.md). The example owns a sanitized
user-level rule; this file owns placement, maintenance, and enforcement
mechanics. It is **a reference to consult, not always-loaded context**.
The `.mdc` intentionally omits a provenance banner and dated footer because
both would consume context in every session; this companion records that it is
a sanitized snapshot checked on the date below.

**Scope: Cursor Agent (Chat).** Cursor can change its rule, hook, model, and
sandbox surfaces independently of the models it hosts. Treat exact fields and
events below as dated pointers and re-check the linked documentation before
depending on them.

## Instruction layers

Cursor has several instruction sources with different jobs:

- **Team rules** carry organization-wide guidance and can be enforced by an
  administrator.
- **Project rules** under `.cursor/rules/` carry version-controlled,
  repository-specific guidance and can be always-on, file-scoped,
  relevance-selected, or manual.
- **User rules** in Cursor Settings carry account-synced preferences.
  User-rule files under `~/.cursor/rules/` are machine-local instead.
- **`AGENTS.md`** is the portable project baseline. Nested copies combine with
  their parents, with more-specific instructions taking precedence.
- **`CLAUDE.md`** is also read automatically for Claude Code compatibility and
  is always applied. Keep a compatibility adapter lean because Cursor sees it
  even when Claude Code is not the active surface.

Across rule tiers, Cursor documents the order as team rules, then project
rules, then user rules. That ordering is separate from the more-specific-wins
behavior inside a nested `AGENTS.md` chain; do not collapse both into a generic
"closest file always wins" rule.

## Installing the sample

Adapt
[`cursor-user-defaults.example.mdc`](cursor-user-defaults.example.mdc), replace
its placeholders, and save it under `~/.cursor/rules/` with the `.mdc`
extension. It already carries `alwaysApply: true`, which makes it part of every
Agent conversation. Rule names do not create precedence; use a descriptive
filename for people, not to imply an ordering Cursor does not provide.

Files in `~/.cursor/rules/` stay on the machine and do not sync. Cursor Settings
user rules do sync with the account but are not ordinary version-controlled
files. A dotfile manager can make the file-based option reproducible, but that
is a maintenance choice rather than a prompt-quality guarantee.

Verify a new or changed always-on rule in a fresh session. A syntactically valid
file that is not selected can fail by omission rather than by an obvious error.

## Cross-tool prompt architecture

At project scope, keep portable facts and conventions in `AGENTS.md`; use a
thin `CLAUDE.md` import adapter until Claude Code reads `AGENTS.md` natively;
add Cursor project rules only for Cursor-specific scoping or behavior.

There is no equivalent portable user-global file across Claude Code, Codex, and
Cursor. Keep a small transferable behavioral core, then project it into each
surface's native format. A symlink is a poor fit when the targets need different
frontmatter, routing, or enforcement language. A template can reduce text drift,
but only if one source is declared canonical and generated files are not edited
as independent copies.

Write always-loaded guidance as model-neutral outcomes and gates. Cursor's
model picker is not, by itself, a reason to discard personal response
preferences; keep the preferences you want across models and avoid tuning them
to one model's quirks. Move dated platform mechanics here, multi-step procedure
into skills, repository facts into project instructions, and deterministic
controls into hooks or settings.

## Rules, skills, and enforcement are different layers

A prose rule requests behavior; it does not enforce it. Cursor's global ignore
list and project `.cursorignore` can block Agent and editor AI features from
accessing matched files, while `.cursorindexingignore` only removes them from
indexing. Cursor documents an important seam: terminal and MCP tools are not
restrained by `.cursorignore`.

User hooks live in `~/.cursor/hooks.json`. Current hook contracts include:

- `beforeReadFile`: return `permission: "allow" | "deny"`.
- `beforeSubmitPrompt`: return `continue: true | false`.
- `beforeShellExecution` and `beforeMCPExecution`: return
  `permission: "allow" | "deny" | "ask"`.

Hook failures allow the action by default. Set `failClosed: true` only where a
failure should block, and test the real action after installation. Tab has
separate file-read and edit hooks.

Rules apply to Agent (Chat), not Tab completion, Inline Edit, or Bugbot reviews.
Do not assume one rule config shapes every Cursor surface.

Skills are on-demand procedure, not always-loaded policy. Cursor discovers
skills from its own `.cursor/skills/` and `~/.cursor/skills/` roots, the portable
`.agents/skills/` roots, and compatible Claude and Codex skill directories.
Refer to a skill by name in a user rule rather than linking to a repository
relative path that will break after the rule is installed elsewhere.

## Current documentation

- Rules and storage:
  <https://cursor.com/help/customization/rules>
- Rule formats and precedence:
  <https://cursor.com/docs/context/rules>
- Skills and compatibility roots:
  <https://cursor.com/help/customization/skills>
- Ignore-file boundaries:
  <https://cursor.com/docs/context/ignore-files>
- Hook events and outputs:
  <https://cursor.com/docs/agent/hooks>

_Checked 2026-08-18. The sample has not yet been exercised in a fresh Cursor
session; these notes describe the documented mechanism, not a completed
behavioral evaluation._
