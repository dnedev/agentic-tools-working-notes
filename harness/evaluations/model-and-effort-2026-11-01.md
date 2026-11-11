# Model and effort benchmark (2026-11-01)

Status: dated record of one run on 2026-11-01, graded by code. One
engineer's check of two of their own rules for picking a model and an
effort level. It isn't a model ranking, and it isn't evidence that the
rules suit anyone else.

## The question

Two rules in my [delegation skill sample](../skills/delegation/SKILL.md):
avoid Haiku, and keep Opus at high effort, with medium only for a very
simple task or one I'm sure of, where "sure" means that something that runs
will check the output. I wanted both checked rather than confirmed.

## What ran

- Claude Code 2.1.316 and `claude plugin eval`, with an isolated config and
  skill and plugin sync off. No skill was under test.
- Haiku 5.5, Sonnet 5.5 and Opus 5.5 as the main session, each at medium
  and at high effort (`CLAUDE_CODE_EFFORT_LEVEL`): 14 tasks, 3 runs each,
  252 runs.
- The tasks, from simple to bigger:
  - a changelog lookup with a revert and a tester preview;
  - a count and total over 120 rows, by hand;
  - a small rate limiter, reviewed against its spec and then fixed;
  - two ledgers to match;
  - a duration parser and a Markdown link checker, built from specs;
  - a token report that counted one message once per line, to fix;
  - a no-count rule checked over 8 notes, then over 24, with decoys;
  - an instruction file audited against checks with licensed exceptions;
  - three edits to a note whose fenced block must not change;
  - a 14-turn research transcript audited against a short list of
    failure types;
  - an open review of a small runner with planted bugs.

  No task allowed Bash, so no model could run its own code.
- Graded by code, against hidden tests, planted answers and decoys. Each
  session's own transcript recorded the effort every request was sent
  with: every run matched its setting, and no run called a subagent.

## Results

| Setup | Runs fully right | Median run | Cost per run, list price |
|---|---|---|---|
| Haiku, medium | 41 of 42 | 16 s | $0.0039 |
| Haiku, high | 42 of 42 | 21.5 s | $0.0055 |
| Sonnet, medium | 41 of 42 | 14 s | $0.049 |
| Sonnet, high | 42 of 42 | 17 s | $0.057 |
| Opus, medium | 42 of 42 | 21 s | $0.115 |
| Opus, high | 42 of 42 | 21 s | $0.129 |

- **Haiku:** its answers matched Sonnet's and Opus's on these tasks. As the
  session it was slower than Sonnet on 11 of the 14, and it thought about
  five times as much, so its edge was price.
- **Effort:** medium missed 2 of 126 runs and high none, too few to show a
  difference. The misses were Haiku on the 120-row count and Sonnet on the
  24-note sweep, both tasks where one skipped item makes the answer wrong.
  High cost 12% more per run on Opus, and took twice as long on the link
  checker.
- I kept both rules. Haiku isn't faster than Sonnet for me, and its saving
  is small next to an Opus main session. High stays my default for sweeps
  and for anything nothing downstream checks.

## What it can't show

- **Task class.** Narrow, single-session tasks, each with a spec or a
  checklist and an answer code can check, a few turns long. Not long
  agentic work, web research, writing quality or open briefs. Anthropic's
  [launch page](https://www.anthropic.com/claude-haiku-5-5) puts Haiku 5.5
  behind Sonnet 5.5 on complex agentic coding (Terminal-Bench 4.0: 39.2%
  against 70.6%, read 2026-11-02).
- **Size.** Three runs per task and setting, near ceiling everywhere, so
  it ranks nothing.
- **Independence.** I wrote the tasks and graders with a Claude model, and
  added harder tasks after trial runs found Haiku at ceiling: a
  model-written benchmark, run on the same family.
- **Surface and cost.** Claude Code main sessions, not claude.ai chats or
  subagents; one afternoon's latency; list prices, where a subscription
  spends quota instead.

The suite and the per-run results aren't published.
