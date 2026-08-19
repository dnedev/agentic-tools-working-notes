# agentic-tools-working-notes

This repository contains one engineer's date-stamped, sanitized working notes on
coding-agent instruction design and verification. It collects a
failure-pattern taxonomy, a trace self-audit template, a regression-corpus
method, evolution notes, and sanitized configuration and skill samples.

The material is n=1, subjectively graded, and model/version sensitive. Treat it
as a set of artifacts to inspect and adapt, not as a framework, benchmark,
policy, comprehensive methodology, best-practice or production-readiness claim,
or scientifically validated evidence. Take what's useful, verify it in your own
environment, and discard the rest.

## Why this exists

I kept finding that a plausible instruction change had no durable
test in my own workflow. So I started using this loop: observe the
failure, classify the trace, decide whether anything should change,
route any warranted fix to the right instruction layer, add a
regression case where a stable check exists, and revisit it after
model or harness drift.

The example configurations are supporting artifacts, not the main
claim. The focus is the inspectable method — including cases where
it invalidates its own apparent successes.

## What's here

- **[`verification-kit/`](verification-kit/README.md)** — a personal
  method for keeping LLM-assisted work grounded: a
  [failure-pattern taxonomy](verification-kit/failure-pattern-taxonomy.md)
  (the recurring ways LLM answers go wrong, each with a binary
  test), a paste-in
  [trace self-audit template](verification-kit/trace-self-audit-template.md)
  that makes any conversation grade itself against those patterns, a
  [regression corpus method](verification-kit/regression-corpus-method.md)
  for turning confirmed failures into binary regression checks, and
  the [evolution story](verification-kit/evolution-and-lessons.md)
  behind them.
- **[`harness/`](harness/README.md)** — personal config and operating
  notes for agentic tools. Includes sanitized examples of my user-global
  config — [`CLAUDE.example.md`](harness/CLAUDE.example.md) for Claude Code,
  [`AGENTS.example.md`](harness/AGENTS.example.md) for Codex,
  [`cursor-user-defaults.example.mdc`](harness/cursor-user-defaults.example.mdc)
  for Cursor, and
  [`coco-user-defaults.example.md`](harness/coco-user-defaults.example.md) for
  Snowflake CoCo —
  copy sheets for [claude.ai profile
  instructions](harness/claude-ai-profile-instructions.example.md) and
  [ChatGPT personalization](harness/chatgpt-personalization.example.md), plus
  durable, figure-free operating principles for
  [Claude Code](harness/claude-code-notes.md),
  [Cursor](harness/cursor-notes.md),
  [Snowflake CoCo](harness/coco-notes.md),
  [claude.ai](harness/claude-ai-notes.md), and
  [OpenAI surfaces](harness/openai-surfaces-notes.md). Also sample
  [`skills/`](harness/skills/): an ADR stub format, a spec-driven-change
  loop, and a chezmoi dotfiles pair.

Dated changes, and the reasoning behind the conventions, are in
[CHANGELOG.md](CHANGELOG.md).

## Scope

This is a sanitized personal project. It contains verification
instruments, operating notes, and example configurations — not raw
transcripts, live configuration, or private regression-corpus entries.

These are personal working notes, not organizational guidance. They do
not represent any employer and do not replace applicable policy or
mandatory requirements. If anything here conflicts with the rules in
your environment, follow those rules.

## License

Licensed [CC BY 4.0](LICENSE) — use, adapt, and share, including
commercially, as long as you credit this repository and link back to it.
Crediting the repo is the attribution asked for here; no personal name is
needed. Provided as-is, with no warranty. The `LICENSE` file is the
unmodified Creative Commons legal code; attribution belongs here, not in
it. Linked third-party works remain under their own terms; this license
covers this repository's notes and samples, not the works they cite.
