# R0D — Externalized decomposition graph

Fixture version: 1

Status: frozen fixture; exact treatment retired after R0D-B-01, 2026-09-04

Operator grader:
[R0D grader](../graders/R0D-externalized-decomposition.md). Keep it and the
expected graph outside the runner context.

## Question

Does making the task graph authoritative, visible, and mechanically checkable
repair R0C's horizontal task shape and contradictory dependency/frontier claims
without installing another planning skill?

This is a follow-on to R0C, not a second attempt at hidden prompt wording. The
mechanism under test is one externalized plan representation plus a
deterministic structural check. The checker can establish internal graph
consistency; the held-out grader still owns whether the declared edges and
task outcomes are semantically correct.

## Conditions

Use the exact **Shared request** from the runner-visible packet in
[R0C fixture version 1](R0C-dependency-aware-decomposition.md). Hold the host,
model, effort, persistent instructions, automatically loaded skill, evidence,
permissions, and output ceiling fixed.

| Condition | Procedure |
| --- | --- |
| A — baseline | Current spec-driven planning and decomposition procedure, with R0C's baseline instruction and ordinary text output |
| B — externalized graph | Same procedure and request, plus the representation contract below; no R0C prompt-only treatment |

R0C-A-02 may serve as A only if the operator verifies byte-identical shared
request and baseline instruction plus the same effective host, model, effort,
persistent instruction hashes, skill hash, permissions, and output ceiling.
Otherwise run a fresh A. Record reuse as a predeclared choice before B.

## Condition B representation contract

Give the runner this additional instruction before the unchanged shared
request:

> Make one fenced `json` object the authoritative execution plan. Do not state
> dependency or frontier claims elsewhere. Each task must deliver one
> independently observable user or operator outcome across every layer it
> needs; layer-only work stays inside that task. Use only supplied facts. List
> hard blockers in `depends_on`, shared edit or operational surfaces in
> `ownership_units`, and only proven safe concurrency in `parallel_with`.
> Record binary acceptance evidence and relevant recovery. Use phase
> `expand`, `migrate`, `feature`, or `contract`. Keep brief assumptions and
> deferrals outside the object, and remain within the shared word ceiling.

The JSON object has this shape. Values below describe types, not literal
runner output:

```json
{
  "schema_version": 1,
  "completed": [],
  "claimed_initial_frontier": ["T1"],
  "tasks": [
    {
      "id": "T1",
      "outcome": "one observable increment",
      "phase": "expand",
      "boundaries": ["persistence", "api", "web", "tests", "operations"],
      "depends_on": [],
      "ownership_units": ["named shared surface"],
      "parallel_with": [],
      "acceptance": ["binary evidence"],
      "recovery": "relevant stop, retry, rollback, or not applicable with reason"
    }
  ]
}
```

Task ids must match `T[1-9][0-9]*`. Arrays contain unique strings. Every task
field is required; `outcome`, `boundaries`, `ownership_units`, `acceptance`,
and `recovery` cannot be empty. `completed` is empty for this planning fixture.
Do not add a separate graph: `depends_on` is the graph.

## Deterministic structural check

Before semantic grading, the operator extracts the single fenced JSON object
and runs a no-network checker whose exact source and SHA-256 are frozen in the
private run record. Use only a standard-library JSON parser. The checker must
return a non-zero status and name the failed invariant when any condition
below is false:

1. the object parses and has the required top-level and task fields with the
   declared types, enums, id form, non-empty fields, and unique array values;
2. task ids are unique, and every dependency or concurrency reference names a
   different declared task;
3. a complete topological sort exists;
4. the computed initial frontier — unfinished tasks whose dependencies are all
   in `completed` — exactly equals `claimed_initial_frontier` as a set;
5. every `parallel_with` claim is reciprocal, has no dependency path in either
   direction, and has disjoint `ownership_units`;
6. every `migrate` task has an `expand` ancestor; and
7. every `contract` task has every `migrate` and `feature` task as an ancestor.

The report records pass/fail for each invariant, the computed topological
order, computed initial frontier, and concurrency claims. It does not infer
that an outcome is genuinely vertical, that a blocker is factually required,
or that acceptance evidence is sufficient.

## Host, permissions, and cleanup

Use the same fresh non-project, one-owner, no-delegate, read-only envelope as
R0C. The runner may read only the same predeclared spec-driven skill, then
return chat text. It may not use repositories, other files, network, MCPs,
apps, credentials, trackers, writes, commits, deployment, or external actions.

The operator checker runs only after runner completion against an isolated
copy of the JSON. It receives no credentials, uses no network, does not edit a
repository, and is removed with its output after the run. Retain only its hash,
result, and private run record.

## Predeclared comparison rule

B advances only when:

1. the run is valid, the deterministic checker passes every invariant, and
   every critical grader criterion passes;
2. B repairs D3, D7, D8, D9, and D12 from the valid R0C baseline without
   losing any prior pass;
3. B adds no unsupported product decision or false concurrency claim; and
4. runner wall time and total exposed tokens, excluding the deterministic
   checker, are each no more than 1.5 times A. Checker wall time is reported
   separately and must be under five seconds on this fixture.

A synthetic win permits one real-task pilot and a proposal for a reusable
checker in the canonical tooling repository. It does not edit the installed
spec skill, install a new skill, or make the representation a global default.
A structural pass with a semantic failure retires this representation for the
fixture. If A now passes every criterion, keep A and retire B as unnecessary.

## Measures

Record criterion results, checker invariants and duration, task count,
dependency/frontier/concurrency errors, unsupported decisions, output words,
runner wall time, exposed token classes, effective context and model/effort,
tools, side effects, cleanup, and operator review time when available.

## Execution result

R0D-B-01 used the valid R0C-A-02 comparator under matching CLI, model, effort,
instructions, skill, prompt facts, permissions, and output ceiling. The
treatment stayed within the time, token, and word ceilings and produced a
semantically conservative vertical order. It did not implement this frozen
schema: it renamed required fields, omitted the declared frontier fields,
added a second graph representation, and made the full lifecycle one oversized
task. The frozen checker rejected all seven invariants after the root schema
mismatch.

Retire this exact prompt-only representation. Keep deterministic validation as
a general boundary, but do not edit the installed planning skill or promote
the one-off checker. A future external graph mechanism would need controlled
schema production and a new frozen comparison.
