# R0B — Question-driven disposable prototype

Fixture version: 1

Status: frozen, 2026-09-03

Operator grader: [R0B grader](../graders/R0B-question-driven-prototype.md).
Keep it outside the runner context.

## Question

Does a one-question disposable prototype produce decision-relevant evidence
that normal planning does not, without turning the spike into production code
or a polished proto-product?

## Variables

Run the same packet under two conditions:

| Condition | Procedure |
| --- | --- |
| A — baseline | Resolve the uncertainty using the host's normal planning behavior; do not load a prototype procedure |
| B — treatment | Use the candidate question-driven-prototype contract: one question, one minimal executable observation, one finding, then cleanup |

Hold the host, model, effort, prompt packet, tools, permissions, standard
runtime, and operator fixed. Both conditions may use the same empty temporary
directory and runtime. The procedure is the only intended independent
variable; invalidate the comparison if either run receives additional facts or
a different execution environment.

## Runner-visible packet

Give the runner only this section, including the requested condition. Do not
provide the grader or its expected trace.

Prepend exactly one condition instruction to the shared request.

### Condition A — baseline instruction

> Use your normal planning behavior. Do not load or simulate a prototype
> procedure. You may use the available tools if your normal approach would do
> so.

### Condition B — treatment instruction

> Use a one-question disposable-prototype procedure. Before building, state
> the uncertainty, hypothesis, observable result, timebox, and cleanup target.
> Create only the smallest deterministic executable artifact that can
> distinguish the unsafe and safe outcomes. Run it, capture the observation,
> carry the finding into the plan-ready answer, and execute cleanup. Do not
> promote prototype code into implementation.

Then provide this shared request:

> We have already decided to validate an editable filter query asynchronously.
> The interface must show a validation result only for the newest query, and it
> must remain in the validating state until that newest request settles.
>
> The proposed state and event handling are:
>
> ```text
> state: current_query, is_validating, validation_result
>
> on_input(query):
>     current_query = query
>     is_validating = true
>     validate(query).then(result):
>         validation_result = result
>         is_validating = false
> ```
>
> Requests may finish in a different order from the order in which they start.
> Determine whether this state model preserves the requirement. Produce a
> plan-ready finding that states the question, hypothesis, observation,
> conclusion, and smallest justified design constraint. Do not design the rest
> of the feature or ask me to make new product decisions.
>
> An empty temporary directory and one preselected, already-installed
> standard-library runtime are available. You may create and run a disposable
> artifact there, but must not use the network, install dependencies, touch a
> production repository, use persistent services, or access real user data.
> Record the exact run command and remove anything you created before ending.

## Execution protocol

Before each run, the operator selects one locally available standard-library
runtime, records its version and the empty temporary path in the run record,
and holds both fixed across conditions. The runner may decline to build an
artifact under the baseline; record that choice rather than adding one after
seeing the treatment result.

For condition B, the executable artifact must be the smallest deterministic
state transition needed to answer the question. A simulated response schedule
is sufficient. UI rendering, a server, persistence, packages, generated
scaffolding, and production abstractions are outside the fixture.

The runner's final answer must include:

- the single uncertainty and hypothesis;
- the artifact path and exact command, or `none` for the baseline;
- the observed event and state sequence;
- the finding and plan/spec consequence;
- limitations that could change the conclusion; and
- cleanup action and evidence.

## Permission and side-effect boundary

- Read only the runner-visible packet.
- Writes are limited to the operator-provided empty temporary directory.
- Run only the preselected local standard-library runtime against the
  disposable artifact.
- No repository edits, production data, network, dependency installation,
  browser, persistent service, issue, commit, deployment, or external message.
- Remove all created artifacts. The operator verifies that the temporary
  directory is empty.

## Timebox

The treatment has a fifteen-minute wall-time ceiling. Stop with an explicit
inconclusive result when the question cannot be answered within the boundary;
do not broaden the prototype.

## Predeclared comparison rule

The candidate advances to one real-task pilot only when condition B:

1. passes every binary criterion in the grader;
2. produces deterministic executable evidence for the correct safety verdict;
3. adds no user-answering turn, dependency, network call, persistent service,
   or production-repository write;
4. completes within the timebox and proves cleanup; and
5. supplies direct evidence that condition A did not produce.

If the baseline produces equivalent direct evidence, or both runs merely state
the same reasoning in different forms, record **more evidence** rather than
keep. Any wrong verdict, non-deterministic demonstration, added product scope,
forbidden side effect, missing cleanup, or timebox overrun is **retire this
wording**.

Neither result is eligible for shared-catalog promotion from R0B alone.

## Measures

Record:

- correct verdict and required design constraint;
- executable artifact, command, repeat count, and observed state trace;
- wall time, active agent time, human time, and turns;
- exposed token classes, tool calls, and retries;
- dependencies, scaffolding, or scope added;
- production and external side effects; and
- cleanup result.
