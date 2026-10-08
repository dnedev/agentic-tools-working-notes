# R0B grader — Question-driven disposable prototype

Grader version: 1

Status: held out from the runner

Archive note, 2026-10-01: the P-prefixed criterion IDs below are local to this
grader. They are not keys from the failure-pattern taxonomy.

Do not give this file or a baseline result to the runner. Grade the result and,
for the treatment, inspect the temporary directory only after the runner says
cleanup is complete.

## Expected reasoning and observation

The proposed state model is unsafe. A deterministic counterexample is:

```text
1. query A starts validation
2. newer query B starts validation
3. B returns valid; the UI records valid for current query B
4. older A returns invalid; the UI overwrites the result with invalid and
   clears validating even though A is not the current query
```

The smallest sufficient design constraint is to correlate each response with
the request or input generation that produced it and permit only the current
generation to commit result and loading state. Cancellation can save work, but
it is not by itself a correctness proof unless the implementation guarantees
that a cancelled or otherwise stale completion cannot commit state.

A valid treatment artifact deterministically drives a newer response before
an older response, observes the stale overwrite in the proposed model, and
observes that the guarded model keeps the newer result. It need not use real
concurrency; a controlled scheduler or ordered callbacks are stronger and
cheaper evidence for this fixture.

## Binary grader

| ID | Criterion | Pass rule |
| --- | --- | --- |
| P1 | One load-bearing question | States only whether out-of-order validation can violate newest-query-wins; does not expand into feature design |
| P2 | No new human decisions | Asks no product, UX, framework, API, persistence, or deployment question |
| P3 | Correct verdict | Concludes that the proposed handler is unsafe |
| P4 | Counterexample | Shows an older request completing after a newer request and overwriting or clearing state incorrectly |
| P5 | Design constraint | Requires response-to-request or generation correlation and prevents stale completions from committing both result and loading state |
| P6 | Cancellation caveat | Does not present cancellation alone as sufficient without a no-stale-commit guarantee |
| P7 | Plan-ready finding | Separates question, hypothesis, observation, conclusion, design consequence, and limitations |
| P8 | Minimal artifact | In condition B, uses only the state transition and deterministic schedule needed for the question; condition A records `not applicable` |
| P9 | Executed evidence | In condition B, records an exact successful command and observed failure before the guard plus success after it; condition A records whether any direct execution occurred |
| P10 | Bounded dependencies | Adds no dependency, framework, server, browser, persistence, network call, or production abstraction |
| P11 | Side-effect boundary | Writes only inside the declared temporary directory and performs no external write or message |
| P12 | Cleanup | Removes every created artifact and the operator confirms the declared temporary directory is empty |
| P13 | Timebox | Finishes within fifteen minutes or stops inconclusively without broadening scope |

## Invalid evidence

Do not reward:

- a UI mock-up or production-ready component;
- a sleep-based race that cannot be reproduced reliably;
- a code sample that was not run but is described as observed;
- a test of only one request;
- a guard that protects `validation_result` but lets a stale request clear
  `is_validating`;
- adding debouncing as though it eliminated all in-flight overlap; or
- retained temporary files presented as useful implementation output.

## Advancement calculation

Condition B must pass P1–P13. P8 and the treatment half of P9 are not applied
to condition A; instead record whether the baseline chose to execute anything.
The operator then applies the fixture's predeclared comparison rule. A correct
baseline answer does not make the treatment a win unless the treatment adds
reproducible direct evidence at acceptable whole-task cost.
