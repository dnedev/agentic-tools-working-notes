# Agentic-development evaluation run record

Status: template v3, 2026-09-24; revised 2026-09-25 to add the cost ceiling,
a versioned role-contract pin, and the workflow's capability classes.

Copy this file for one run. Complete **Pre-registration** before starting the
agent. Do not edit the fixture or grader after seeing the result; a correction
creates a new fixture version and invalidates comparisons against the old one.

This Markdown contract replaces the originally planned JSON schema because the
working-notes repository is Markdown-only. Required fields use **Required** in
the field tables. Use `unavailable` when the host does not expose a measure and
`not applicable` only when the field genuinely cannot apply. Never estimate
missing token or timing data.

## Field contract

### Identity and pre-registration

| Field | Requirement | Value |
| --- | --- | --- |
| Run ID | **Required.** `<fixture>-<condition>-<sequence>` | |
| Fixture and version | **Required.** Exact fixture ID and frozen version | |
| Condition | **Required.** Baseline or named treatment | |
| Trial and order | **Required.** Index, repetitions, arm order, common stop rule, and cost ceiling declared before execution | |
| Frozen registration | **Required.** Immutable registration/grader identity or digest and timestamp; retain the actual artifacts privately when needed | |
| Grader independence | **Required.** Grader identity, treatment-author relationship, blinding or explicit limitation | |
| Hypothesis | **Required.** One sentence and one changed variable | |
| Predeclared threshold | **Required.** Binary keep/change/retire rule | |
| Date and operator | **Required.** UTC date plus human decision owner | |
| Repository and revision | **Required when code-backed.** Public-safe name or private pointer plus immutable revision | |
| Prompt packet | **Required.** Exact text, hash, or durable path shown to the runner | |
| Grader and version | **Required.** Durable path; must remain hidden from the runner | |
| Evidence boundary | **Required.** Sources the runner may treat as authoritative | |
| Permission ceiling | **Required.** Read/write/network/external-action boundary | |
| Cleanup contract | **Required when anything may be written.** Targets and proof of cleanup | |

### Effective execution configuration

| Field | Requirement | Value |
| --- | --- | --- |
| Host and version | **Required.** Record what actually ran | |
| Fresh context | **Required.** `yes` or `no`, with reason if no | |
| Delivery lane | **Required.** Direct, guided, prototype, or spec; domain/incident overlay separately | |
| Topology | **Required.** Owner and every delegate | |
| Context mode | **Required for every delegate.** Fresh packet, selected context, or full fork; record what was observed, not requested | |
| Role contract | **Required.** Durable path plus version or revision, or `inline baseline` | |
| Capability class | **Required.** The workflow's class: strong general, efficient general, fastest adequate, or smallest capable | |
| Requested model | **Required.** Exact run-time request or `host default` | |
| Effective model | **Required.** Observed identifier or `unavailable` | |
| Requested effort | **Required.** Exact request or `host default` | |
| Effective effort | **Required.** Observed level or `unavailable` | |
| Fallback | **Required.** Observed fallback or `none observed` | |
| Instructions and skills | **Required.** Only material loaded surfaces | |
| Tools and retrieval routes | **Required.** Available, used, and denied | |
| Isolation | **Required.** Checkout/worktree/sandbox/temp boundary, including the effective working directory for every resumed turn | |

### Time, interaction, and resource measures

| Field | Requirement | Value |
| --- | --- | --- |
| Envelope preflight | **Required.** Effective directory, startup tools/network, instruction/skill loading, permissions, and measurement readiness | |
| Approval interruptions | **Required.** Count, measured delay, blocked actions, or unavailable | |
| Owner integration | **Required when delegated.** Validation/synthesis time and evidence or unavailable | |
| Started / ended | **Required.** UTC timestamps | |
| Wall time | **Required.** Measured duration | |
| Active agent time | Record when exposed, else `unavailable` | |
| Human framing time | **Required.** Measured, explicitly zero, or unavailable with reason | |
| Human answering/steering time | **Required.** Measured, explicitly zero, or unavailable with reason | |
| Human review time | **Required.** Measured, `pending` until reviewed, or `unavailable` with reason | |
| Turns | **Required.** User/agent exchange count under the fixture | |
| Questions asked | Required for guided discovery; otherwise `not applicable` | |
| Tool calls | **Required.** Count by material route when possible | |
| Retries and failures | **Required.** Count and concise cause | |
| Compactions and model switches | Record when exposed, else `unavailable` | |
| Input/output/reasoning/cache/tool-output tokens | Record each exposed class separately; otherwise `unavailable` | |
| Other cost | Record when exposed, else `unavailable` | |

### Outcome and decision

| Field | Requirement | Value |
| --- | --- | --- |
| Result artifact | **Required.** Durable path or complete answer | |
| Binary grader result | **Required.** Pass/fail for every criterion | |
| Unsupported claims | **Required.** Count plus anchors, or `none found` | |
| Missed material decisions/findings | **Required.** Count plus IDs, or `none` | |
| Rework | **Required.** Loops, reason, and affected criterion | |
| Side effects | **Required.** Observed writes/actions, including accidental ones | |
| Cleanup evidence | Required when cleanup applies | |
| Checks | **Required.** Exact commands and outcomes | |
| Checks not run | **Required.** Reason, substitute, and residual risk, or `none` | |
| Operator decision | **Required.** Keep, change, retire, or more evidence | |
| Decision rationale | **Required.** Tie directly to the predeclared threshold | |
| Release/handoff | **Required.** Candidate location, next authorized gate, owner, and pending operational evidence | |
| Later defects | **Required.** Observation owner/window, escaped defects or pending/not observed; link any correction to a criterion | |
| Follow-up | **Required.** One bounded next step or `none` | |

## Pre-registration

### Run identity

- **Run ID:**
- **Fixture and version:**
- **Condition:**
- **Trial index / repetitions / arm order / common stop / cost ceiling:**
- **Frozen registration identity / timestamp:**
- **Grader identity / independence / blinding:**
- **Date and operator:**
- **Repository and revision:**

### Controlled comparison

- **Hypothesis:**
- **Single independent variable:**
- **Factors held fixed:**
- **Predeclared threshold:**
- **Invalidation conditions:**

### Input and boundaries

- **Prompt packet:**
- **Grader and version:**
- **Evidence boundary:**
- **Permission ceiling:**
- **Forbidden routes or actions:**
- **Cleanup contract:**

## Effective execution configuration

- **Host and version:**
- **Fresh context:**
- **Delivery lane:**
- **Topology and roles:**
- **Role contract (path plus version or revision):**
- **Capability class:**
- **Requested model / effective model:**
- **Requested effort / effective effort:**
- **Fallback:**
- **Instructions and skills:**
- **Available / used / denied tools:**
- **Isolation:**

If a delegate participates, add one row per delegate:

| Delegate | Identity / context mode | Self-contained question | Model / effort | Requested and actual tools / effects | Start / stop | Result path | Tokens |
| --- | --- | --- | --- | --- | --- | --- | --- |
| | | | | | | | |

For a permission-sensitive delegate, record the preflight or enforcement that
observed its role and context. Distinguish a marker response from an actual
permission-enforcement test; record missing telemetry explicitly. After completion, inspect the execution record
for recursive delegation, duplicate work, writes, tests, network, and other
forbidden routes. A clean final tree does not prove that the role stayed within
its boundary.

## Observations

- **Envelope preflight / startup effects:**
- **Approval interruptions / delay / blocked actions:**
- **Owner validation / integration time:**
- **Started / ended / wall time:**
- **Active agent time:**
- **Human framing / answering / review time:**
- **Turns / questions:**
- **Tool calls:**
- **Retries / failures:**
- **Compactions / model switches:**
- **Token classes / other cost:**
- **Unexpected behavior:**

Keep token subclasses separate until their inclusion relationships are known;
do not count cached input or reasoning output twice. Do not convert total
tokens to monetary cost at an assumed flat rate. Whole-task accounting includes
preflight, failed attempts, approvals, synthesis, review, and rework.

## Grading

Copy the fixture's criterion IDs; do not replace them with a summary.

| Criterion | Pass / fail | Evidence anchor | Notes |
| --- | --- | --- | --- |
| | | | |

- **Validity and exclusion from comparison (if invalid):**
- **Unsupported claims:**
- **Missed material decisions/findings:**
- **Rework loops:**
- **Observed side effects:**
- **Cleanup evidence:**
- **Exact checks and outcomes:**
- **Checks not run, substitute, residual risk:**

## Decision

- **Operator decision:** keep / change / retire / more evidence
- **Threshold comparison:**
- **Quality gained or lost:**
- **Human and resource cost gained or lost:**
- **Maintenance or portability consequence:**
- **Next bounded step:**

## Handoff and later observation

- **Artifact / revision and review disposition:**
- **Release state and next authorized gate:**
- **Observation owner / window / success or failure signal:**
- **Escaped defects:** pending / not observed within the stated window / observed
- **Defect evidence and affected intent or criterion:**
- **Recovery / cleanup / corrective action owner:**

Use `not applicable` for genuinely non-operational work, not as a substitute
for missing follow-up. No observation means no claim of defect-free operation.

## Record handling

The compact, sanitized run record may be tracked. Raw transcripts, private
repository names, internal sources, exact machine paths, and current account or
model availability stay in the approved private evidence location. A transcript
is evidence for the run, not a reusable instruction or trusted knowledge source.
