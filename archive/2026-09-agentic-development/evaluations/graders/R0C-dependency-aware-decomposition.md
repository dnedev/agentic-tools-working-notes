# R0C grader — Dependency-aware task decomposition

Grader version: 1

Status: held out from the runner; frozen 2026-09-04

## Expected dependency shape

Equivalent task names and finer safe splits are acceptable. The load-bearing
partial order is:

```text
E — expand compatibility
|
+--> M — reconcile legacy records idempotently
|
+--> V1 — create, list, and apply one saved view end to end
      |
      +--> V2 — rename, delete, and enforce the cap end to end

M + V2 + rollout/rollback/observation/human evidence
|
+--> C — contract legacy support
```

M and V1 are logically unblocked after E. They are not automatically safe for
parallel writers: a plan may sequence them or permit isolated work only after
showing that they do not concurrently own the same persistence or API
contract. V2 may be split into independently useful lifecycle slices, but none
may precede the core create/list/apply path it modifies. C is never part of the
initial implementation frontier.

## Binary grader

| ID | Criterion | Pass rule |
| --- | --- | --- |
| D1 | Uses supplied decisions | Preserves personal scope, versioned filter/sort definitions, current-access evaluation, twenty-view cap, legacy conversion name, and explicit deferrals without inventing product behavior |
| D2 | Expands before change | First load-bearing task makes old and new representations coexist, preserves legacy writes, prevents corruption of the new collection, and supplies new-reader fallback before any new writer or migration |
| D3 | Vertical first value | At least one task delivers create/list/apply behavior through persistence, API, UI, and applicable tests as one independently verifiable user outcome rather than a database-then-API-then-UI sequence |
| D4 | Completes lifecycle | Later task or safe sub-slices cover rename, delete, and the twenty-view cap with current-access behavior and binary unit, API-contract, or browser evidence |
| D5 | Safe migration | Migration is explicitly blocked by expansion, idempotently creates at most one “Previous filter”, retains failed legacy records, exposes failures, and supports retry without undoing successes |
| D6 | Safe contraction | Legacy removal is blocked by reconciliation, completed feature/lifecycle work, end of the rollback window, zero named signals for an approved window, and release-owner approval |
| D7 | Correct graph | Every task names blockers; graph is acyclic and preserves E before M/V1, V1 before V2, and M plus V2 plus operational evidence before C |
| D8 | Executable tasks | Every task names one observable deliverable, applicable gate, binary pass evidence, and relevant failure, recovery, or cleanup behavior; oversized tasks are split |
| D9 | Honest frontier | Initial frontier contains only E; later potential concurrency is distinguished from safe concurrent writing, and no work sharing an ownership unit is marked parallel without isolation or sequencing |
| D10 | Scope and authority | Does not add sharing, default views, result snapshots, new infrastructure, invented commands, issue publication, commits, implementation, or agent dispatch |
| D11 | Artifact completeness | Separates assumptions/contradictions, numbered tasks, explicit graph/frontier, contraction gate, and deferrals within the word ceiling |
| D12 | No horizontal or premature plan | Does not make non-verifiable layer-only phases the primary delivery units and does not migrate/write v2 before expansion or contract legacy support before every named gate |

## Cost and validity

Record task count and output words directly. Use host telemetry for wall time,
input, cached input, output, reasoning, and total tokens; mark unavailable
classes unavailable. A run is invalid if its model, effort, persistent
instructions, automatic skill load, evidence packet, permissions, or output
ceiling differ from the comparator, or if it uses a forbidden tool or effect.

## Decision rule

Apply the fixture's predeclared rule exactly. Do not award a pass for saying
“expand-contract” without the required edges and acceptance evidence. Do not
penalize a baseline merely for using different task names or for placing
horizontal implementation notes inside an independently verifiable vertical
task.
