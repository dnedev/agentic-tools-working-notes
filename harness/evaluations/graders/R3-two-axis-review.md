# R3 grader — Blended versus two-ledger review

Grader version: 1

Status: frozen protocol; exact answer key held in the ignored target overlay

## Validity prerequisites

Before execution, freeze the same complete candidate packet, answer key,
prompt contract, host, model, effort, persistent context, and zero-tool
permission boundary for both conditions. The operator, not either runner,
holds the grader.

A changed candidate, hidden author reasoning, model/effort fallback, tool or
delegate call, file/network/external action, output over 900 words, or wall
time over five minutes invalidates the run.

## Binary grader

The private overlay expands L2-L8 into target-specific facts.

| ID | Criterion | Pass rule |
| --- | --- | --- |
| L1 | Frozen packet | Uses only the exact supplied intent, rules, diff, and evidence |
| L2 | Conformance completeness | Finds every critical missing, partial, wrong, and extra behavior in the held-out key |
| L3 | Scope control | Identifies seeded scope creep and does not invent unsupplied requirements |
| L4 | Engineering-risk completeness | Finds every critical reachable correctness, security, atomicity, lifecycle, or operational failure in the key |
| L5 | Repository rules | Correctly distinguishes a documented-rule breach from a heuristic or preference |
| L6 | Axis classification | Places each finding on the right axis; a cross-axis hunk appears twice only for distinct violated invariants |
| L7 | Independent results | Neither axis's clean or noisy result masks the other; per-axis status and the final gate follow the supplied blocking rule |
| L8 | Grounding and actionability | Every finding has the required anchor, violated source/invariant, reachable impact, and smallest correction direction |
| L9 | No unsupported claims | No invented runtime, test result, technology, requirement, caller, or failure path |
| L10 | Review boundary | Does not edit, approve for the human, or broaden into implementation/refactoring work |
| L11 | Output and route | Required finish fields appear within 900 words, with zero tools/delegates/actions and no more than five minutes |
| L12 | Complete cost and cleanup | Wall, output words, exposed token classes, retries, operator time when available, and cleanup are recorded |

## Decision rule

Apply the fixture threshold after grading both independent outputs. Finding
volume is not quality: merge duplicate statements before counting, and reject
generic warnings without a reachable path. If the ordinary reviewer already
passes every criterion, the treatment has no measured gap to fill and is
retired even when its formatting is cleaner.
