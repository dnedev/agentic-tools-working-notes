# Guided-development source intake and overlap — first pass

Status: frozen intake baseline, 2026-09-03

Amended 2026-09-24: the S2 files-reviewed cell and M7 mechanism and evaluation
text were narrowed to what the source supports (see the evidence status's
attribution section), and the S8/S10 rows were sanitized. Amended 2026-09-25:
the M1 outcome and the M8 need note now separate the valid R0A dependency
failure from the invalid rerun, M9 records which IDE operations were actually
used, and S15 notes that R5's baseline must be re-frozen before any run; links
were updated for files moved into the archive, and the S8 skill has since
gained a 2026-09-25 proposal, so its hash no longer matches the tracked file;
the R5 links were removed when the fixture was held privately, and the S0 row
was generalized for sharing. Amended 2026-10-01: the S7 file link never
resolved at its pin, because upstream split that page on 2026-08-30; it now
points to the planning-path successor at the same pin, where the routing
mechanism appears, and which text the original review read is not recorded.
The S15 research-plan reference is plain text because that file is left out of
public releases. S0 and the B1 to B3 baselines are private, so the baseline
comparison and overlap matrix cannot be replayed from this repository. Frozen
pre-run text is otherwise unchanged.

This is the first mechanism-level intake under the accepted
[selective-derivation decision](../decisions/0001-selective-skill-derivation.md).
It covers guided discovery and question-driven prototyping because those are
the first evaluation candidates. It does not approve a skill, install a bundle,
or claim that any source improves this engineer's work.

The public record names public sources and sanitized local baselines. Exact
private catalog paths and machine observations stay in the ignored evidence
register. Later tranches below cover decomposition, existing IDE retrieval,
review structure, and a source-only Terraform overlay. Agent dispatch and the
remaining data, semantic-model, incident, security, and cross-host mechanisms
still need their own intake before entering the adoption queue.

## Source pins

Retrieved 2026-09-03. Repository pins are full commits from the default branch
at retrieval time; a later upstream change does not silently alter this review.

| ID | Source and revision | Files reviewed | Rights and use boundary |
| --- | --- | --- | --- |
| S0 | An existing shared skill catalog at a privately recorded revision | Collaborative brainstorming, adversarial challenge, broad web-prototype, spec, planning, and agent-dispatch procedures | Approved private source; compare behavior without reproducing its text here |
| S1 | Current personal [workflow](../agentic-development-workflow.md) and [spec procedure](../skills/spec-driven-change/SKILL.md) | Uncertainty router, guided lane, disposable-prototype lane, spec trigger | Repository license applies; this is the cheaper local baseline |
| S2 | Anthropic, [AI-native SDLC playbook](https://claude.com/blog/the-ai-native-sdlc-playbook) | Intent, specification, plan, implementation/tests, review, and incident artifacts | Pattern evidence and attribution only; do not copy article text or treat vendor guidance as validation |
| S3 | Matt Pocock skills [`6654f6b60cd9d5be8b54c6fafe44346dabeb3b76`](https://github.com/mattpocock/skills/tree/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76) | [`grilling`](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/skills/productivity/grilling/SKILL.md), [`grill-me`](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/skills/productivity/grill-me/SKILL.md), and [`prototype`](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/skills/engineering/prototype/SKILL.md) | MIT; any copied or derivative portion retains the copyright and license notice plus a visible local delta |
| S4 | GitHub Spec Kit [`db64869985644df296827a5bbbaa0181a58a058e`](https://github.com/github/spec-kit/tree/db64869985644df296827a5bbbaa0181a58a058e) | [`clarify`](https://github.com/github/spec-kit/blob/db64869985644df296827a5bbbaa0181a58a058e/templates/commands/clarify.md) | MIT; use as a bounded comparison, not a reason to install its CLI or artifact system |
| S5 | Superpowers [`b36e0829c6d0140e93cfef2ca599b1b07d4a7797`](https://github.com/obra/superpowers/tree/b36e0829c6d0140e93cfef2ca599b1b07d4a7797) | [`brainstorming`](https://github.com/obra/superpowers/blob/b36e0829c6d0140e93cfef2ca599b1b07d4a7797/skills/brainstorming/SKILL.md) | MIT; the shared catalog already contains an attributed derivative, so another copy would be duplication |
| S6 | gstack [`0d1bd5616c0ef096bb7ccee336f63c60ee408618`](https://github.com/garrytan/gstack/tree/0d1bd5616c0ef096bb7ccee336f63c60ee408618) | [`office-hours`](https://github.com/garrytan/gstack/blob/0d1bd5616c0ef096bb7ccee336f63c60ee408618/office-hours/SKILL.md) and its product/engineering plan split | MIT; inspect the premise-testing mechanism only, without bundle routing, telemetry, or commit behavior |
| S7 | BMAD Method [`891c0abbc1128f318e098a566f925155022aef12`](https://github.com/bmad-code-org/BMAD-METHOD/tree/891c0abbc1128f318e098a566f925155022aef12) | [`choose-a-planning-path`](https://github.com/bmad-code-org/BMAD-METHOD/blob/891c0abbc1128f318e098a566f925155022aef12/docs/plan/choose-a-planning-path.md) (successor to `workflow-map`) | MIT with a separate trademark notice; use generic routing ideas without names, marks, or framework packaging |

The license check establishes permission to evaluate and, where applicable,
derive. It is not approval to publish a derivative into the shared catalog.
That requires an owner, destination review, retained notice, frozen evaluation,
and the catalog's own contribution process.

## Local baselines

The overlap audit found four materially different baseline shapes:

| Baseline | Useful existing mechanism | Mismatch with the desired lane |
| --- | --- | --- |
| B1 — collaborative brainstorming | Reads project context, asks one question at a time, proposes alternatives, recommends an approach, and obtains approval | Trigger is broad; full path mandates a design/spec workflow and may assume a commit and a particular planning skill |
| B2 — adversarial challenge | Explicit “grill me” trigger, bounded question count, code-aware challenge, architecture/requirements modes, and a verdict | It is intentionally skeptical and withholds solutions; it does not build a shared decision tree or produce a collaborative intent record |
| B3 — broad prototype builder | Clear validation goal, mock-data and safety controls, runnable UI, demo decision, and archive/convert lifecycle | Optimizes for polished web demonstrations over one technical question; assumes a particular stack and can create a sizeable artifact |
| B4 — personal uncertainty workflow | Separates requirements ambiguity from solution uncertainty, requires one prototype question and cleanup, and composes with a durable spec | Procedure is guidance rather than a tested, user-invoked skill; no frozen guided/prototype comparison has run |

The immediate gap is therefore not “a brainstorming skill” or “a prototype
skill.” It is a narrower interaction contract whose trigger, output, and
side-effect ceiling differ from the existing choices.

## M1 — Decision-frontier guided discovery

- **Identity:** S3 `grilling` and its user-invoked `grill-me` wrapper.
- **Need:** An ambiguous request can hide dependent human decisions that a flat
  checklist either asks too early or misses entirely.
- **Mechanism:** Model decisions as a dependency tree, ask only the current
  frontier, retrieve objective facts rather than asking the user, include a
  recommendation, and recompute after each answer.
- **Overlap:** B1 already supplies collaborative questions, alternatives, and
  recommendations. B2 already owns adversarial “grill me.” Neither combines a
  decision frontier with a correctable intent and a no-write default.
- **Proposed contract:** User-invoked while unproven; repository facts first;
  one question or one independent frontier per round; recommended answer and
  trade-off; user owns decisions and can stop; output is decisions,
  assumptions, scope, open branches, acceptance sketch, and prototype
  candidates. No implementation, commit, issue publication, or external write.
- **Assumptions to remove:** A subagent is always available for fact finding;
  exhaustive questioning is always worth its interaction cost; “relentless” is
  an appropriate default tone; completing the interview authorizes action.
- **Evaluation:** R0A compares free-form clarification, bounded guided
  discovery, and an explicitly requested deep mode. The early-stop control is
  mandatory.
- **Lifecycle:** If retained, one neutral contract belongs in the shared
  catalog and host projections remain generated. Recheck S3 at an explicit
  update; never auto-merge it.
- **Verdict:** **Prototype the independently worded treatment in R0A.** The v1
  fixture implements the reviewed mechanism without copying the upstream
  procedure. A later skill needs a fresh text-level provenance review and must
  be reclassified if it incorporates upstream expression. Do not mirror the
  wrapper or install the upstream collection.

## M2 — One-question disposable prototype

- **Identity:** S3 `prototype`.
- **Need:** A load-bearing technical assumption can block a responsible plan
  even after product intent is clear.
- **Mechanism:** Name one question, select a logic/state or UI observation,
  build the smallest trivial-to-run artifact, expose relevant state, and carry
  the answer—not prototype code—back into the real work.
- **Overlap:** B4 already names one question, representative input, observation,
  and cleanup. B3 adds safety and lifecycle practice but targets polished web
  demos rather than cheap technical evidence.
- **Proposed contract:** Trigger on solution uncertainty, never on size alone;
  timebox before building; no persistence, network, new dependencies, or
  production data by default; one owner per isolated question; record the
  command, observation, verdict, decision change, and cleanup result.
- **Assumptions to remove:** A frontend route is available; a particular task
  runner exists; tests and error handling should always be skipped; the
  prototype should be committed to a throwaway branch; prototype code can be
  promoted directly.
- **Evaluation:** R0B compares discussion-only planning with an executable
  evidence spike against the same seeded concurrency question.
- **Lifecycle:** If retained, keep the generic procedure separate from any
  domain or UI overlay. Re-evaluate promotion after a real-task pilot and
  retire it if prototypes become unowned artifacts.
- **Verdict:** **Prototype the independently worded treatment in R0B.** The v1
  fixture implements the reviewed mechanism without copying the upstream
  procedure. Revisit provenance if later skill text incorporates upstream
  expression. Do not replace the broader demo builder, whose purpose is
  different.

## M3 — Bounded specification clarification

- **Identity:** S4 `clarify`.
- **Need:** Prevent endless interviewing when only a few consequential
  ambiguities block a spec.
- **Mechanism:** Scan for meaningful ambiguity, ask a bounded number of targeted
  questions, stop early when directed, and write answers into the spec.
- **Overlap:** B4 now has a bounded review point and an intent artifact. The
  spec procedure already makes durable requirements correctable.
- **Assumptions to remove:** A Spec Kit directory and command lifecycle exist;
  the spec is always the current artifact; a fixed question cap fits every
  risk class.
- **Evaluation:** Use as the bounded control in R0A, not as a separate
  installation candidate.
- **Lifecycle:** Revisit only if R0A shows that the local bound or update
  behavior is weak.
- **Verdict:** **Keep as comparison evidence; do not derive now.**

## M4 — Mandatory design brainstorming

- **Identity:** S5 `brainstorming`; an attributed derivative is already present
  in the shared catalog.
- **Need:** Surface intent and approaches before implementation.
- **Mechanism:** Explore context, ask one question at a time, present several
  approaches, recommend one, present a design, and obtain approval.
- **Overlap:** B1 is the existing implementation and therefore the baseline.
- **Assumptions to test rather than inherit:** Every creative change requires
  the full gate; a design document, commit, and downstream planning skill are
  always appropriate; heavier classification is the safe default.
- **Evaluation:** R0A baseline plus later trigger-positive and trigger-negative
  cases.
- **Lifecycle:** Any future change should narrow or consolidate the existing
  derivative through its owner; never add a second copy.
- **Verdict:** **Keep the existing baseline for evaluation; reject another
  import.**

## M5 — Premise pressure test

- **Identity:** S6 `office-hours`.
- **Need:** A well-written plan can still optimize the wrong premise or confuse
  product desirability with engineering feasibility.
- **Mechanism:** Challenge the premise, force alternatives, and review product
  and engineering reasoning as different questions.
- **Overlap:** B2 already provides adversarial challenge; later two-axis review
  covers the plan split.
- **Assumptions to remove:** The surrounding framework, routing, telemetry,
  document layout, and commit lifecycle are present.
- **Evaluation:** Add its strongest premise question to R0A's grader; evaluate
  the product/engineering split later with the review fixture.
- **Lifecycle:** Citation-only unless a later measured gap survives B2.
- **Verdict:** **Pattern evidence only.**

## M6 — Complexity-routed analysis

- **Identity:** S7 workflow map.
- **Need:** A single amount of discovery is wasteful for small work and too
  shallow for consequential work.
- **Mechanism:** Make brainstorming and idea pressure-testing optional analysis
  stages and choose a later workflow track by complexity.
- **Overlap:** B4 separates size/risk from uncertainty and composes lanes; the
  spec trigger already scales ceremony by scope and consequence.
- **Assumptions to remove:** The framework's roles, artifacts, commands, and
  trademarked workflow are installed.
- **Evaluation:** R0A and R0B test the local router directly.
- **Lifecycle:** Revisit only if those fixtures reveal a missing route.
- **Verdict:** **Pattern evidence only; reject bundle adoption.**

## M7 — Intent-to-release artifact chain

- **Identity:** S2 AI-native SDLC playbook.
- **Need:** Preserve corrected human intent as work passes between agents,
  sessions, implementation, and review.
- **Mechanism:** Connect intent, specification, plan, diff, tests, and review
  findings, with incident feedback returning to intent.
- **Overlap:** The roadmap and B4 already implement this as a hypothesis.
- **Assumptions to remove:** One vendor's harness, organization, or case-study
  outcome transfers to this environment.
- **Evaluation:** R0A and R0B cover local discovery/prototype choices, not the
  full source-derived chain. The planned end-to-end fixture would test handoff
  loss; it has not run.
- **Lifecycle:** Keep as attributed influence and periodically verify the page;
  do not copy it into runtime instructions.
- **Verdict:** **Retain as architecture evidence; no skill import.**

## Mechanism overlap matrix

Legend: **yes** means the mechanism is explicit; **partial** means it exists but
with a different trigger, artifact, or permission boundary; **no** means this
review found no equivalent in the bounded source. An empty search outside this
bounded review would not establish absence.

| Mechanism | B1 brainstorm | B2 challenge | B3 demo prototype | B4 personal workflow | Candidate action |
| --- | --- | --- | --- | --- | --- |
| Retrieve available facts before asking | Yes | Partial | Partial | Yes | Keep; make it a binary R0A criterion |
| Ask only decisions whose prerequisites are settled | No | No | No | Partial | Prototype M1's decision frontier |
| Give a recommendation and material trade-off | Yes | No by design | Partial | Yes | Keep in M1; do not change B2's adversarial purpose |
| Bounded default plus explicit deeper mode | Partial | Yes | No | Yes | Test M1 against B2 rather than merge them |
| Human can stop without losing a useful artifact | Partial | Partial | Partial | Yes | Require an early-stop intent record |
| No implementation or commit implied by discovery | No | Yes | No | Yes | M1 must default to no writes |
| Correctable intent feeds the next artifact | Spec, with fixed path | Verdict only | Demo outcome | Yes | Use the smaller intent record in M1 |
| Task size is separate from uncertainty | Partial | Partial | No | Yes | Keep B4 routing; use M6 only as comparison |
| Prototype answers one named technical question | No | No | Partial | Yes | Prototype M2; do not replace B3 |
| Prototype is trivial to run and exposes state | No | No | Partial | Partial | Add to M2 treatment |
| Persistence, network, and dependencies absent by default | No | No | No | Partial | Make explicit in M2 |
| Cleanup is executed and recorded | No | No | Archive/convert | Yes | Preserve B4 cleanup; test it in R0B |
| Independent fact finding can fan out without delegating decisions | No | No | No | Partial | Keep optional and read-only; not part of first variable |

## First-pass decisions

1. Do not install any reviewed collection.
2. Do not add another general brainstorming skill.
3. Preserve adversarial challenge as a separate job from collaborative guided
   discovery.
4. Evaluate the independently worded guided-discovery treatment frozen in R0A.
5. Evaluate the independently worded question-driven-prototype treatment
   frozen in R0B without replacing the broader demo-prototype procedure.
6. Do not vary model, effort, topology, or host during either first comparison.
7. Promotion remains blocked until a second, real-task pilot shows value beyond
   the frozen fixture and the destination owner accepts the maintenance cost.

## Intake queue recorded after R0A and R0B

This is the queue as recorded when the first tranche froze. The decomposition,
review, code-intelligence, and first Terraform items are addressed by later
tranches below; agent dispatch and the remaining domain/cross-host items remain
open.

- dependency-aware vertical decomposition and tracker publication;
- specification conformance versus engineering-risk review;
- owner, explorer, reviewer, and classifier contracts;
- code intelligence and organization retrieval;
- Terraform, data, semantic-model, incident, and security overlays; and
- cross-host discovery, permissions, fallback, and cleanup behavior.

## Post-intake evaluation outcome — 2026-09-04

The intake above remains the frozen pre-run decision record. The subsequent
comparisons changed the adoption decision:

- **M1 treatment not promoted.** The bounded treatment improved coverage from
  one of five decisions to four of five and covered all critical nodes, but it
  asked a dependent decision before its prerequisite. A stricter prompt-only
  rewrite repeated the ordering failure on its first question (an invalid run;
  diagnostic only). Retain the need
  for a visible decision frontier; retire these hidden-map prompt variants.
- **M2 treatment not promoted.** Ordinary planning already produced a minimal
  deterministic unsafe-state trace. The treatment added no required direct
  observation, omitted the guarded-success trace, and used more tokens. Retain
  the one-question, observation, timebox, and cleanup rule in the workflow;
  wait for a new recurring gap before testing a skill.

These are single synthetic-fixture results. They reject the tested wording and
promotion claim, not every possible guided conversation or disposable
prototype.

## Second-tranche intake — dependency-aware decomposition

Status: frozen before R0C execution, 2026-09-04

This tranche addresses the first pending mechanism without reopening the R0A
or R0B decisions.

| ID | Source and revision | Files reviewed | Rights and use boundary |
| --- | --- | --- | --- |
| S8 | Current local [spec-driven-change](../skills/spec-driven-change/SKILL.md) with private revision retained by the operator, file SHA-256 `21faf28d4408663f42edee919a4983aed701dfd96bc693c597fde1e4760ee9ab` | Trigger, separate plan/decompose pass, session-sized tasks, binary acceptance, lifecycle and review gates | Existing local baseline; unchanged at the recorded revision |
| S9 | Matt Pocock skills [`6654f6b60cd9d5be8b54c6fafe44346dabeb3b76`](https://github.com/mattpocock/skills/tree/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76) | [`to-tickets`](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/skills/engineering/to-tickets/SKILL.md): tracer-bullet slices, blocking edges, wide-refactor expand-contract, approval, and tracker publication | MIT; evaluate the generic decomposition mechanism with attribution, but do not copy the expression, setup assumptions, tracker writes, labels, or bundle flow |

### M8 — Vertical, dependency-aware decomposition

- **Need:** The local procedure says to plan and then decompose, but does not
  require an explicit graph, independently useful vertical slices, an
  expand-migrate-contract shape for cross-version replacement, or a runnable
  frontier. The earlier R0A treatment violated prerequisite order in a valid
  run and again, diagnostically, in an invalid rerun, which
  makes dependency visibility an observed local gap even though R0A itself was
  an interview fixture.
- **Overlap:** S8 already owns the durable-spec versus volatile-plan split,
  session-sized tasks, binary criteria, risk-scaled lifecycle evidence, and
  fresh review. A third ticket artifact would duplicate the volatile plan.
- **Candidate mechanism:** Keep tasks inside the volatile plan; make each
  delivery slice independently observable across the layers it needs; name
  blockers and the runnable frontier; use expand-migrate-contract when a
  cross-version replacement cannot stay green as a direct switch; mark
  concurrency only after dependency and ownership checks.
- **Assumptions removed:** An issue tracker is configured; publication is
  authorized; a specific label vocabulary exists; one file per ticket is
  desirable; exact paths should always be frozen into a long-lived ticket; and
  agent-ready work should be published automatically.
- **Evaluation:** R0C compares S8 alone with an independently worded treatment
  on a fully decided, mixed-version saved-view migration. One owner produces
  chat text only; the held-out grader checks the partial order, vertical value,
  safe migration/contraction, binary evidence, false parallelism, and cost.
- **Lifecycle:** If the treatment wins a synthetic and later real-task pilot,
  revise the existing decomposition section rather than install a second
  planning skill. Preserve S9 attribution and the local delta beside that
  revision. Retire it if S8 already produces the same graph or if review
  overhead erases the gain.
- **Verdict:** **Prototype in R0C; do not install or publish.** The candidate is
  prompt-only, locally worded, and narrower than the upstream skill.

### M8 post-intake outcome — 2026-09-04

- **Baseline retained.** Valid R0C-A-02 passed seven of twelve criteria. It
  handled compatibility, partial migration, recovery, and contraction, but
  decomposed the feature into horizontal domain, API, and UI tasks and did not
  expose the required vertical partial order.
- **Treatment wording retired.** R0C-B-02 still produced horizontal API and UI
  tasks, contradicted its own migration edge, introduced unsupported cap and
  feature-flag assumptions, and returned 1,286 words against a 1,200-word
  ceiling. Its diagnostic score was five of twelve; the ceiling violation
  makes the treatment invalid for formal A/B inference.
- **No promotion.** Do not edit the installed spec skill or create a
  decomposition skill from this result. A later candidate must externalize the
  task table and use a deterministic acyclic-graph/frontier check rather than
  another hidden prompt-only rewrite.

### M8 follow-on — externalized graph candidate

- **Observed gap:** R0C failed on vertical task shape, semantic edges, runnable
  frontier, and prose/graph consistency. More invisible wording would not make
  those claims inspectable.
- **Candidate mechanism:** R0D makes one JSON task graph authoritative. A
  standard-library, no-network checker validates schema, references,
  acyclicity, computed frontier, conservative concurrency claims, and coarse
  phase ancestry before the held-out semantic grader runs.
- **Boundary:** Mechanical validity does not establish correct blockers,
  genuinely vertical outcomes, or sufficient acceptance evidence. Those
  remain held-out semantic judgments. The runner does not receive the checker
  result or grader.
- **Verdict:** **Exact R0D representation retired.** The frozen treatment
  produced a safe-looking vertical order at similar measured cost, but renamed
  the required fields, duplicated the graph, and kept the lifecycle in one
  oversized task. The standard-library checker rejected the result after the
  root schema mismatch. Retain the deterministic-validation boundary; do not
  install the prompt or temporary checker.

## Third-tranche intake — existing code-intelligence route

Status: frozen before R2 execution, 2026-09-04

This tranche evaluates retrieval order, not an IDE product or a new indexing
system. It uses a clean Python repository and an index that is already running
on the operator's machine.

| ID | Source and revision | Surface reviewed | Use boundary |
| --- | --- | --- | --- |
| S10 | Private Python tooling fixture at an operator-retained immutable revision | Repository instructions plus deterministic `git`, `rg`, and bounded file slices | Cheaper local-search baseline; read-only and repository-scoped |
| S11 | Configured IDEA MCP observed 2026-09-04 | Module inventory, symbol search, call analysis, symbol information, file reads, and text/regex search; a module-inventory probe returned the three expected project modules | Existing local index only; no installation, re-indexing, IDE terminal, mutation, or claim that inventory proves answer quality |

### M9 — Local search with indexed escalation

- **Need:** Symbol and call-path work can consume repeated text searches, but
  an index adds startup, tool-output, staleness, and false-edge risks. Tool
  availability alone does not say which route costs less for a complete
  answer.
- **Overlap:** The working retrieval ladder already starts with local search
  and permits an IDE or organization index when discovery is weak. It has no
  measured threshold for moving the IDE earlier.
- **Candidate mechanism:** Keep local search as the first rung unless the
  already configured IDE route repairs a critical miss, removes at least two
  retrieval calls at equal quality, or cuts both wall time and exposed tokens
  by at least twenty percent at equal quality.
- **Assumptions removed:** Semantic search is automatically more accurate;
  call-hierarchy output is complete for dynamic code; another index should be
  installed; a successful module listing proves the route is useful; and raw
  tool output is equivalent to a grounded answer.
- **Evaluation:** R2 freezes one program-shape control/data/output path. One
  fresh owner uses only bounded local reads; another uses only the existing
  IDEA route. A private operator key grades thresholds, consumers, an
  unaffected output, direct tests, gaps, and exact anchors.
- **Lifecycle:** Prefer no new maintained artifact. If the IDE wins, document
  it as an on-demand retrieval rung and recheck after tool or IDE changes. If
  it ties or loses, retain local search first and use the IDE only when a
  concrete localization gap remains.
- **Verdict:** **Run R2; do not install or configure another index.**

### M9 post-intake outcome — 2026-09-04

- **Local-first retained.** The local condition passed nine of ten grader
  criteria in six calls and 161,368 exposed tokens. It answered the principal
  control and output path but omitted part of the frozen statistics inventory,
  so it missed the critical-behavior gate.
- **IDE qualified only as escalation.** The IDEA-only condition passed all ten
  criteria and repaired that critical miss. It used the same six calls and was
  5.5% faster by wall time, but consumed 331,779 exposed tokens—2.056 times the
  baseline. Four of five file reads included middle truncation.
- **No broad promotion.** Keep deterministic local search first. Permit one
  real-task pilot of the existing IDE for unresolved symbol, call-path, or
  cross-cutting completeness questions, favoring semantic searches over broad
  file reads. Do not install another index or automate IDE-first routing from
  this synthetic result.
- **Amendment, 2026-09-25.** The IDE arm used one text search and five file
  reads, with no symbol or call operations, so this result says nothing about
  semantic navigation. The recorded decision follows R2's frozen
  "preferred second rung" rule rather than the candidate wording above, whose
  "first rung unless … repairs a critical miss" clause the IDE met; "qualified
  only as escalation" means eligible for one gap-driven pilot.

## Fourth-tranche intake — review-axis separation

Status: frozen before R3 execution, 2026-09-04

| ID | Source and revision | Mechanism reviewed | Rights and use boundary |
| --- | --- | --- | --- |
| S12 | Current local [reviewer role](roles/reviewer.md) and [spec-driven procedure](../skills/spec-driven-change/SKILL.md) at the current working revision | Fresh context, complete candidate/intent/evidence packet, conformance plus risk review, actionable findings, and owner-held progression verdict | Existing local baseline; it names both concerns but does not require separate ledgers |
| S13 | Matt Pocock skills [`6654f6b60cd9d5be8b54c6fafe44346dabeb3b76`](https://github.com/mattpocock/skills/tree/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76) | [`code-review`](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/skills/engineering/code-review/SKILL.md): fixed-point validation, separate standards/spec axes, missing-spec stop, isolated parallel reviewers, and side-by-side reporting | MIT; evaluate axis separation with attribution, but do not copy the smell catalog, tracker/setup assumptions, mandatory parallelism, or host syntax |
| S14 | Sanitized local infrastructure-review observation, exact task evidence retained privately | Fresh read-only reviewer plus owner review found material issues, but the reviewer alone used 4,163,677 exposed tokens and the combined turn used about 12.7 million without a predeclared comparison | Cost/failure-mode evidence only; not a controlled result and not proof that review fan-out is ineffective |

### M10 — Specification-conformance and engineering-risk ledgers

- **Need:** A blended review can let extensive engineering commentary obscure
  a missed requirement, or let literal requirement coverage obscure a
  reachable failure. The local infrastructure observation also shows that an
  unconstrained “review everything” delegate can consume far more context than
  the final decision warrants.
- **Overlap:** S12 already requires both intent reconciliation and risk tracing,
  fresh context, complete evidence, and an owner-held gate. S13 contributes the
  narrower idea that the axes stay visibly separate so one cannot compensate
  for the other.
- **Candidate mechanism:** First test one owner with two ledgers:
  **conformance** for missing, partial, wrong, or extra behavior against the
  supplied intent; **engineering risk** for violated repository rules and
  reachable correctness, security, lifecycle, or operational failure. A hunk
  may appear in both for different reasons. Each axis receives its own result;
  the owner derives the gate mechanically from blocking findings rather than
  ranking the axes against each other.
- **Assumptions removed:** Parallel reviewers are automatically cheaper or
  more independent; a generic smell catalog overrides repository evidence; an
  issue tracker exists; absence of a spec authorizes invented requirements;
  review implies edits or a final human approval; and more findings are better.
- **Evaluation:** R3 compares ordinary blended review with the two-ledger
  treatment on one self-contained diff/spec/standards packet. It holds model,
  effort, context, evidence, and permissions fixed and uses no tools. A later
  topology comparison is eligible only if axis separation wins and a truly
  independent unresolved axis remains.
- **Lifecycle:** If retained, revise the existing reviewer contract instead of
  installing a second review skill. Preserve S13 attribution beside the local
  delta. Retire it if the baseline already keeps the axes complete and
  independent or if the added structure only duplicates findings.
- **Verdict:** **Prototype axis separation in R3 with one owner; do not fan out
  or install.**

### M10 post-intake outcome — R3 completed

R3-A-01's ordinary blended reviewer found every seeded substantive defect and
passed ten of twelve criteria. It failed only the review-structure criteria:
findings mixed the two axes and did not report an independent status for each.
R3-B-01 added the frozen two-ledger wording, passed eleven of twelve criteria,
used 111 fewer final words and nearly the same exposed tokens, and repaired the
independent-status gap. It still placed the check-then-insert concurrency race
only in the conformance ledger, failing the critical classification criterion.

**Decision:** retire the prompt-only treatment. Keep the existing concise
reviewer contract and one-owner topology. Do not make separate ledgers or
parallel reviewers a default from this evidence. If a real review later shows
one axis masking the other, test a visible requirement/risk coverage matrix
against the retained baseline.

## Fifth-tranche intake — source-only Terraform assessment

Status: frozen before R5 execution, 2026-09-04

This tranche tests whether a small domain overlay improves classification and
readiness evidence. It does not derive or install a Terraform skill, run
Terraform, or turn an infrastructure observation into a controlled baseline.

| ID | Source and revision | Mechanism reviewed | Rights and use boundary |
| --- | --- | --- | --- |
| S15 | Current [workflow](../agentic-development-workflow.md), research plan (archived), [owner](roles/owner.md), and [reviewer](roles/reviewer.md) contracts at the frozen R5 working revision. These contracts were revised on 2026-09-24 (workflow, owner v3, reviewer v2, archived research plan); re-freeze and pin the baseline revision before any R5 run | Generic evidence reconciliation, repository-defined checks, lifecycle and recovery criteria, and scoped gate recommendation | Existing local baseline; no infrastructure-specific treatment wording |
| S16 | HashiCorp's official Terraform [style](https://developer.hashicorp.com/terraform/language/style), [`validate`](https://developer.hashicorp.com/terraform/cli/commands/validate), [`test`](https://developer.hashicorp.com/terraform/cli/commands/test), [`depends_on`](https://developer.hashicorp.com/terraform/language/meta-arguments/depends_on), and [automation](https://developer.hashicorp.com/terraform/tutorials/automation/automate-terraform) guidance, from the dated 2026-09-03 local evidence snapshot | Separate format, initialization/validation, refresh, test, plan, and apply concerns; dependency-lock and automation boundaries; conservative explicit dependencies | Official-source mechanism evidence; not refreshed during the offline R5 pass and not evidence for a real provider or environment |
| S17 | Sanitized local source-only infrastructure review, exact repositories and revisions retained privately | Phase gates, lockout ordering, suspicious network inputs, state/output access, imperative-provider behavior, partial-apply recovery, exact-tree binding, and whole-review cost | Failure-mode and fixture-shaping evidence only; no private source text is reproduced and the uncontrolled review is not a baseline |

The first-party HashiCorp agent-skill collection remains a later source-review
candidate. It is not needed to test this independently worded overlay, and no
unpinned skill text enters R5.

### M11 — Terraform source/effect boundary overlay

- **Need:** Generic review can find code defects while still collapsing static
  checks, provider installation, refresh, tests, plan, and apply into one vague
  notion of “Terraform validation.” It can also miss that the remotely planned
  tree, dependency lock, phase transition, and recovery authority are separate
  readiness gates.
- **Overlap:** S15 already requires repository evidence, applicable lifecycle
  and recovery, exact checks, skipped-check risk, and human ownership. The gap
  to test is a compact IaC-specific classification and ordering prompt, not a
  second end-to-end workflow.
- **Candidate mechanism:** Map phases and external prerequisites; reconcile the
  reviewed tree with the executed tree and lock; classify each Terraform action
  by evidence and side effects; trace state, remote-output, lockout, partial
  failure, recovery, and human authorization; keep plan and apply verdicts
  separate; refuse to guess current provider behavior or suspicious network
  intent.
- **Assumptions removed:** `fmt` proves configuration correctness; `validate`,
  `test`, or `plan` is necessarily local or inert; a plan authorizes apply; a
  precondition proves runtime reachability; Terraform rolls back a partial
  apply; a provider lock can be repaired by hand; and a plausible CIDR should
  be silently normalized or corrected.
- **Evaluation:** R5 (held privately) compares S15 with the independently
  worded M11 overlay on the same synthetic source packet. The held-out grader
  checks exact-tree and lock binding, phase and lockout gates, state/provider
  effects, source-only claim calibration, recovery, authorization, and
  whole-task cost.
- **Lifecycle:** A synthetic win permits one representative source-only real
  task. It does not authorize a state-aware plan, install a skill, or create a
  shared default. Promotion would still require source/licensing review for any
  expression adopted from an external skill, an owner, a real-task win, and a
  host projection with refusal and cleanup tests.
- **Verdict:** **Freeze R5; do not run or install during the offline drafting
  pass.** Retire the overlay if the generic baseline already passes every
  critical criterion or if the treatment's extra cost exceeds its fixed gate.
