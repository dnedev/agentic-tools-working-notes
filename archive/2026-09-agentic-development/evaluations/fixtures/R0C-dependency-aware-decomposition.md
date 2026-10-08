# R0C — Dependency-aware task decomposition

Fixture version: 1

Status: frozen, 2026-09-04

Operator grader:
[R0C grader](../graders/R0C-dependency-aware-decomposition.md). Keep it
outside the runner context.

## Question

Does an explicit vertical-slice, blocking-edge, and expand-migrate-contract
procedure produce a safer, more executable plan than the current
spec-driven decomposition procedure without disproportionate cost?

## Variables

Run the same packet under two conditions:

| Condition | Procedure |
| --- | --- |
| A — baseline | Use the current spec-driven planning and decomposition procedure; do not simulate the candidate treatment |
| B — treatment | Add the independently worded dependency-aware decomposition procedure below |

Hold the host, model, effort, runner-visible facts, persistent instructions,
automatically loaded non-candidate skills, tools, permissions, and output
ceiling fixed. Use one owner and no delegates. Do not compare an ordinary
answer from one model with a treatment from another.

## Runner-visible packet

Give the runner only this section, including one condition instruction. Do not
provide the grader or its expected dependency graph.

### Condition A — baseline instruction

> Use the current spec-driven planning and decomposition procedure. Do not load
> or simulate a tracer-bullet, ticket-generation, or dependency-graph skill.

### Condition B — treatment instruction

> Decompose the decided change into narrow, independently verifiable
> end-to-end increments. Keep horizontal implementation steps inside the
> increment they serve. Give every task explicit blocking edges and binary
> acceptance evidence. Treat a cross-version replacement as
> expand-migrate-contract: land compatibility first, migrate safely in
> repeatable batches, and remove the legacy form only after every migration,
> rollout, rollback, observation, and human gate is satisfied. Show the
> currently runnable frontier. Mark work parallel only when it has no unfinished
> dependency and no shared ownership hazard. Do not publish tickets or spawn
> agents.

Then provide this shared request:

> Produce a volatile execution plan for the already decided saved-views
> change below. Another fresh session must be able to execute one task at a
> time without inventing requirements. Do not implement, inspect a repository,
> write a file, create tickets, commit, publish, or delegate. The output must be
> at most 1,200 words.
>
> Decided behavior:
>
> - Signed-in users can create, list, apply, rename, and delete personal saved
>   views.
> - Each view stores a versioned filter-and-sort definition, never result
>   items. Applying it runs the normal current-access query.
> - A user may have at most twenty views. No default auto-applied view and no
>   sharing are in scope.
> - An existing single saved filter must survive the change and become one
>   saved view named “Previous filter”.
>
> Repository and rollout facts:
>
> - Persistence, HTTP API, web UI, and tests live in one repository, but API
>   and web releases may roll independently and the previous release remains a
>   rollback target for one release window.
> - The legacy representation is a version-1 `saved_filter` preference. The
>   target representation is a version-2 `saved_views` collection.
> - During a mixed-version window, old clients must still read and update the
>   legacy preference without deleting or corrupting the new collection. New
>   clients may use the new collection. New views do not have to appear in an
>   old client.
> - Compatibility support must land before either a new writer or stored-data
>   migration. It must preserve both representations and let the new reader
>   fall back to the legacy value when no equivalent new entry exists.
> - Migration is idempotent: rerunning it must not duplicate “Previous
>   filter”. A failed record remains on the legacy form, is observable, and can
>   be retried without undoing successful records.
> - Legacy support may be removed only after all stored records are reconciled,
>   the previous API and web releases are no longer rollback targets, and
>   `legacy_preference_reads`, `legacy_preference_writes`, and
>   `migration_failures` remain zero for the release owner's approved
>   observation window. The release owner approves contraction.
> - The repository has unit, API-contract, and browser-saved-views gates. A
>   task must name the applicable gate and an observable pass condition; do
>   not invent shell commands.
>
> Return:
>
> 1. assumptions or contradictions that remain;
> 2. a numbered task list with what each task delivers, explicit blockers,
>    binary acceptance evidence, and applicable recovery or cleanup;
> 3. a dependency graph and the initial runnable frontier;
> 4. the contract-removal gate; and
> 5. anything deliberately deferred.

## Host-profile control

Use a fresh non-project context with MCPs, apps, network, skill search, and
delegation disabled. The current user instruction profile and its required
`spec-driven-change` skill may load read-only in both conditions. Record their
identity and content hash, and invalidate the comparison if the persistent
surface or automatically loaded skill differs. The candidate is prompt text
only and must not be installed.

## Permission and side-effect boundary

- Scenario evidence is limited to the runner-visible packet.
- Apart from the same predeclared read-only skill load in both conditions, no
  tool or filesystem access is needed or permitted.
- No repository, network, MCP, app, delegate, credential, issue tracker, file,
  commit, deployment, or external message is permitted.
- The result is chat text only.

## Predeclared comparison rule

The treatment advances to one real-task pilot only when:

1. every safety and load-bearing criterion D1-D7 and D10-D12 passes;
2. it either repairs a baseline miss in D2, D5, D6, D7, or D12, or improves at
   least two total criteria without losing any baseline pass;
3. it introduces no unsupported product decision or false parallel edge; and
4. its wall time and total exposed tokens are each no more than 1.5 times the
   valid baseline.

If both conditions pass every criterion, retain the existing procedure and
retire the added wording as redundant. If quality improves but exceeds the cost
ceiling, record **more evidence; do not promote**. A safety regression, wrong
contract edge, unauthorized action, or invented decision retires the treatment
for this fixture. A synthetic win permits only a real-task pilot, not skill or
catalog promotion.

## Measures

Record criterion passes, dependency and false-parallel errors, unsupported
decisions, task count, output words, wall time, exposed token classes,
automatically loaded context, tool calls, side effects, and operator review
time when available.
