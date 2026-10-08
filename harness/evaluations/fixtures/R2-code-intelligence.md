# R2 — Local search versus an existing IDE index

Fixture version: 1

Status: frozen protocol, 2026-09-04

Operator grader: [R2 grader](../graders/R2-code-intelligence.md). The exact
approved repository, revision, question, and held-out answer key belong in the
ignored private target overlay, not this public-safe protocol.

## Question

For a representative symbol-and-call-path question, does the already
configured read-only IDE index improve correctness or whole-task cost over
deterministic local search?

This fixture evaluates a retrieval route. It does not evaluate a new index,
authorize repository changes, or treat tool inventory as functional evidence.

## Target selection

Before either run, freeze one clean repository revision and one question that:

- requires a symbol definition, at least two call or data-flow steps, and
  related test coverage;
- has a complete operator answer key established from repository evidence;
- contains at least one plausible false inference that anchors can refute;
- is answerable read-only without dependency installation, tests, network,
  credentials, generated state, or external services; and
- is representative of the engineer's current work rather than selected to
  favor one tool.

Record exact private identifiers only in the ignored overlay and run records.
The tracked record may describe the language and question class generically.

## Conditions

| Condition | Retrieval route |
| --- | --- |
| A — local | Repository instructions plus read-only `git`, `rg`, and bounded file slices |
| B — IDE | The same repository instructions plus only the existing IDE's read-only module, symbol, call-hierarchy, file-read, and text-search tools |

Use one fresh owner per condition with the same model, effort, instructions,
question, output contract, repository revision, read-only sandbox, and
wall/output ceiling. Keep all configured retrieval surfaces available in both
conditions, but the runner may call only its condition's allowlist. No
delegates or automatically loaded procedure skill.

## Runner output contract

Return at most 900 words:

1. direct answer;
2. execution or call path in order;
3. exact controls, branches, thresholds, or precedence relevant to the
   question;
4. user-visible or machine-visible outputs affected and unaffected;
5. direct tests and at least three material coverage gaps;
6. exact repository-relative file and line anchors;
7. explicit inferences; and
8. checked and not checked.

## Budgets and safety

- At most six retrieval calls and eight wall-clock minutes per condition.
- Read-only repository and IDE queries only. Do not run tests or code.
- No writes, refactors, builds, terminals through the IDE, network, other MCP,
  apps, credentials, delegates, commits, or external actions.
- Do not read denied credential or environment paths.
- Stop when the output contract is supported; unused call budget is not a
  target.

## Predeclared comparison rule

The IDE route becomes the preferred second rung for this question class only
when:

1. every critical held-out fact and safety criterion passes;
2. it has no unsupported claim or stale/ambiguous anchor;
3. it either repairs a critical local-search miss, uses at least two fewer
   retrieval calls at equal quality, or reduces both wall time and total
   exposed tokens by at least twenty percent at equal quality; and
4. the returned answer, not merely the raw tool output, remains within the
   ceiling and is independently gradable.

If quality ties without that cost win, local search remains first and the IDE
remains an on-demand escalation. If either route cannot establish a complete
answer, record the limitation rather than mixing tools after the run. One
synthetic win permits a real-task pilot; it does not justify a new index.

## Measures

Record correctness, unsupported claims, anchors, tool names and calls, raw
result truncation, follow-up calls, output words, wall time, exposed token
classes, operator review time when available, effective model/effort/context,
side effects, and cleanup.
