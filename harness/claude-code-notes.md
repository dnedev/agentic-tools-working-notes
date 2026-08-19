# Claude Code — durable operating principles

**A reference to consult, not always-loaded context** — don't paste it into
`CLAUDE.md`/`AGENTS.md`. It's deliberately **figure-free**: model IDs, prices,
version floors, per-model effort defaults, and exact caps rot in weeks, so they
live in the docs (linked below), not here. What's below is the part that ages
well. **Scope: standard, public Claude Code** — an internal model gateway can
govern model availability and version floors differently, so verify against your
own platform.

## Principles that don't rot

- **Pin the model; don't ride the alias.** Claude Code's `opus`/`default`
  aliases move over time; a full model ID is a pinned snapshot. For reproducible
  runs, set the full ID — and record which model a result came from.
- **An out-of-date client hides newer models silently — it doesn't error.** A
  model missing from `/model` usually means the client is too old, not that you
  lack access. Check your version against the model's floor and `claude update`.
- **Effort is a behavioral signal, not a token budget.** The default is
  equivalent to omitting it; raise it only for genuinely frontier work (the top
  level over-thinks and over-spends on routine tasks) and lower it for simple,
  high-volume, or latency-sensitive work.
- **Guardrails go in hooks/settings, not prose.** A rule in `CLAUDE.md` is a
  request; a `PreToolUse` hook or a settings deny-rule is enforcement. If it must
  hold every time, make it a hook.
- **Match the verification gate to the autonomy.** Watching → fold the check into
  the prompt. Unattended → a `Stop` hook that blocks the turn until the check
  passes. After a long run → a read-only reviewer subagent in a fresh, isolated
  context, checking the diff against the plan.
- **Context hygiene.** `/clear` between unrelated tasks; `/compact` with a focus
  instruction before a long new task; checkpoints/`/rewind` are local-undo, not
  version control (and don't track bash `rm`/`mv`). Project-root `CLAUDE.md`
  survives compaction; path-scoped rules and nested `CLAUDE.md` don't until re-read.
- **Put a rule in the cheapest layer that holds it.** Always-on fact →
  `CLAUDE.md`/`AGENTS.md` (keep it lean — it reloads every turn); only part of the tree →
  `.claude/rules/`; on-demand procedure → a skill; must fire every time → a hook;
  isolated or noisy side work → a subagent; external system → an MCP server.
- **Autonomous loops close on a pass/fail check.** Give the agent something that
  returns OK/FAIL and it iterates. Scaffold larger work as a durable spec + a
  volatile plan, fan out per item with "return OK or FAIL," gate with a `Stop`
  hook, and use `--bare` for reproducible headless/CI runs.

## Where the current specifics live (look them up — don't trust a cached number)

- Models & IDs, pricing: `platform.claude.com/docs/en/about-claude/models/overview`
- Effort ladder & per-model defaults: `platform.claude.com/docs/en/build-with-claude/effort`
- Claude Code: `code.claude.com/docs/en/` — `model-config`, `hooks`, `sub-agents`,
  `context-window`, `memory`, `features-overview`, `best-practices`, `headless`

_Principles current as of 2026-07-27; the figures are intentionally elsewhere._
