# Snowflake execution defaults — example

Scope: personal defaults for Snowflake CoCo sessions on this machine. This file
adds Snowflake-specific guidance without restating execution guidance or general
defaults loaded elsewhere. The partial shape assumes both an owner-maintained
Snowflake execution contract and an equivalent general user-scope instruction
are also loaded; if either is absent, add only the missing execution boundaries,
evidence gates, and safety constraints this environment needs. Workspace
instruction files own real database, schema, role, warehouse, and tier
identifiers. An explicit task can narrow these defaults; it does not relax
authorization or production-safety constraints.

## Effective context

- Before any claim that depends on where a statement ran, state the effective
  context you observed: connection, role, warehouse, database, schema. A
  configured default is a setting, not an observation.
- A statement about the environment is a claim about that context. When the
  context is unestablished, establish it or say so — do not answer as though a
  default applied.
- `USE ROLE` and `USE WAREHOUSE` change the session for everything after them.
  Treat a context switch as a reportable action and state it; do not leave a
  changed session implicit at the end of a turn.

## Tier isolation

- Treat each environment tier — for example `<DEV>`, `<TEST>`, `<PROD>` — as a
  separate source of truth. Schema, data, grants, and object existence diverge
  between them.
- Do not carry a fact observed in one tier into a statement about another.
  Re-verify in the target tier, or label the claim unverified there and name the
  tier where it was actually observed.
- Object names and shapes repeat across tiers. Matching names are not evidence
  of matching definitions.

## Evidence in this environment

- Distinguish, in the answer, catalog or object-search metadata from an executed
  query result, from documentation, from your own computation. Object
  descriptions, comments, and semantic-model text are authored claims, not
  measurements.
- A validation is incomplete until you say which stage passed: local or static
  checks, compilation, execution, or server-side validation. A compiled
  statement is not an executed one.
- Report the completeness of any result you rely on: row limits, truncation,
  offloaded or partial output, sampling, and fetched-content caps. An answer
  drawn from a truncated result says so.
## Returning work

- In a non-trivial handoff, include the Snowflake-specific context that a
  general completion ledger cannot supply: effective context; statements or
  actions run; result completeness; validation stage; and query or request
  identifiers when available.
- Assume the caller cannot see this session. Anything load-bearing that only
  exists in the session transcript is not delivered until it is in the handoff.
