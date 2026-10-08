# R0D grader — Externalized decomposition graph

Grader version: 1

Status: held out from the runner; frozen 2026-09-04

Use the expected dependency shape and supplied-fact interpretation from the
[R0C grader](R0C-dependency-aware-decomposition.md). The deterministic report
is evidence only for representation and graph consistency; it cannot award a
semantic pass.

## Validity prerequisites

Before B, record whether A is a fresh run or the predeclared, verified reuse of
R0C-A-02. Freeze the exact shared request, B prefix, host, model, effort,
persistent instructions, spec-driven skill, permission envelope, output
ceiling, checker source, and checker SHA-256. Keep this grader and the R0C
expected graph outside the runner context.

A changed evidence packet, model/effort fallback, undeclared context, forbidden
runner tool or action, more than one plan object, invalid JSON, output over
1,200 words, or runner wall over ten minutes invalidates B. A checker that
uses a model, network, credentials, or repository writes also invalidates B.

## Binary grader

| ID | Criterion | Pass rule |
| --- | --- | --- |
| D1 | Uses supplied decisions | Preserves every decided behavior and deferral from R0C without inventing product behavior |
| D2 | Expands before change | Compatibility expansion precedes every new writer and migration and preserves both representations plus fallback |
| D3 | Vertical first value | A task delivers create/list/apply across persistence, API, UI, and applicable tests as an independently verifiable outcome |
| D4 | Completes lifecycle | Later tasks or safe sub-slices cover rename, delete, the cap, current-access behavior, and applicable named gates |
| D5 | Safe migration | Migration has the supplied expansion blocker, idempotence, partial-failure preservation, observability, and retry behavior |
| D6 | Safe contraction | Contraction has reconciliation, completed lifecycle, rollback expiry, named zero signals, observation window, and owner approval |
| D7 | Correct semantic graph | The authoritative dependencies preserve the R0C held-out partial order and do not contradict the task outcomes |
| D8 | Executable task records | Every task has one observable outcome, only the layers needed for it, binary evidence, and relevant recovery; oversized tasks are split |
| D9 | Honest frontier and concurrency | Computed initial frontier contains only expansion; concurrency claims are both mechanically valid and operationally safe |
| D10 | Scope and authority | Adds no unsupported behavior, mechanism, command, publication, implementation, dispatch, or external action |
| D11 | Artifact completeness | Exactly one authoritative JSON plan plus brief assumptions and deferrals fits the ceiling and has no competing graph claim |
| D12 | No horizontal or premature plan | Layer-only phases are not primary delivery units, and no migrate, new writer, or contraction can run before its supplied gates |
| D13 | Structural validation | All seven deterministic invariants pass; report includes topological order, computed frontier, concurrency claims, duration, and checker hash |
| D14 | Complete cost and cleanup | Runner/checker time, output words, exposed token classes, retries, tools, effects, operator time when available, and cleanup are recorded |

## Decision rule

Apply R0D's predeclared comparison rule exactly. D3, D7, D8, D9, D12, and D13
are critical. Do not award verticality because `boundaries` lists several
layers, or semantic graph correctness because a topological sort succeeds.
Reject a parallel claim that passes disjoint-string checks but still shares a
real repository or operational ownership surface under the supplied facts.

The treatment's purpose is to make contradictions rejectable, not to make an
incorrect plan look precise. If the mechanical structure passes while any
critical semantic criterion fails, retire it rather than weakening the key.
