# Data-work session defaults — example

Scope: personal defaults for Snowflake CoCo sessions on this machine, which are
data work by default. This file adds only data-work rules, without restating
execution guidance or general defaults loaded elsewhere. It assumes an execution
contract and a general user-scope instruction are also loaded; it does not stand
alone. Workspace instruction files own real database, schema, role, warehouse,
and tier identifiers; repository files own commands and gates. An explicit task
can authorize a write by naming the action and its tier (see Tiers and writes);
it cannot relax authorization or production-safety constraints that workspace or
repository files own. Repository or module text may narrow or instantiate the
write and data-handling defaults below, never relax them; a repository-declared
sandbox target counts as the named tier only where that repository says so.

## Effective context

- Before any claim that depends on where a statement ran, state the effective
  context you observed: connection, role and any additional active roles,
  warehouse, database, schema. A configured default is a setting, not an
  observation. When the context is unestablished, establish it or say so; do not
  answer as though a default applied.
- A role or warehouse switch (for example `USE ROLE`, `USE WAREHOUSE`) or
  enabling additional roles changes the session for everything after it. Switch
  to a role, or enable additional roles, only when the task names that role;
  after a privilege error, report it and stop rather than switching. Report each
  switch you ran, and do not leave a changed session implicit at the end of a
  turn. Where each tool call is its own session, put the context statements in
  the same call as the statement that needs them.

## Tiers and writes

- Treat each environment tier — for example `<DEV>`, `<TEST>`, `<PROD>` — as its
  own source of truth; schema, data, grants, and object existence diverge
  between them. Don't carry a fact observed in one tier into a claim about
  another: re-check in the target tier, or label the claim unverified there and
  name the tier where you observed it. Matching names are not matching
  definitions.
- Default to read-only. Run a write, grant, drop, full rebuild, or compute
  change only when the task names that action and its tier, and list it as an
  action taken. A write you did not run is untested; don't predict its outcome.
- Before a run that calls AI functions or repeats agent or evaluation calls,
  state the expected spend and its basis.

## Evidence

- Label each load-bearing claim with its source: an executed statement (give it,
  with the query ID when available), catalog or object metadata, documentation
  (quote the exact sentence and give the URL), or your own reasoning. Object
  comments and descriptions are authored claims, not measurements.
- Use "verified" only when a tool call in this turn produced the evidence, and
  name that call. Documentation counts as verified only when you retrieved it in
  this turn and quote the sentence. Memory, analogy to a similar feature, or an
  earlier turn is not verification: say "inferred" or "unverified" instead.
- For feature support, syntax, limits and defaults, search the documentation
  before answering. If you can't retrieve it, say so rather than answering from
  memory.
- An empty result or "does not exist or not authorized" shows only that this
  session can't see the object with its current roles. Report exactly that.
  Don't name a cause you haven't checked.
- When an object named in the request isn't visible, stop and say which one.
  Don't substitute a similar object.
- Name the validation stage reached: static checks, compilation, execution,
  tests, or server-side validation. A compiled statement is not an executed one.
- Report the completeness of any result you rely on: row limits, truncation,
  sampling, partial or offloaded output, and fetched-content caps. Don't derive
  a total from a limited result.
- When a summary combines per-object facts from separate statements, keep each
  statement next to its result and check each summary value against the result
  it came from. One catalog query covering all objects is fine.

## Judgement and design advice

- Keep facts and advice apart. For a design or correctness claim, give the
  reasoning and say what would test it. Don't call advice verified unless you
  ran that test.
- Before recommending a change to SQL, a policy or a query plan, work out what
  the original does in every case it handles and confirm that your version
  still answers the question that was asked.

## Data handling

- Select the columns you need and prefer counts or aggregates. Treat a column as
  personal or restricted if it carries a tag or masking policy or its name says
  so. Don't copy row values of such columns into answers, files, or handoffs
  unless the task names those columns; then copy only the rows the task names.
- Don't read or print transformation-runner profiles, connection files,
  environment variables, or other locations that hold credentials; take settings
  from the session or ask.

## Task-type modules

- Each recurring data task type has its own module, installed as a skill.
  Load the module for the task type at hand before starting that work.

## Returning work

- In a non-trivial handoff, include what a general completion report cannot:
  effective context; statements or actions run, with query or request IDs when
  available; result completeness; validation stage; and, for a multi-part
  request, each part's answer with its own evidence or a note that it wasn't
  checked.
- Assume the caller cannot see this session. Anything load-bearing that exists
  only in the transcript is not delivered until it is in the handoff.
