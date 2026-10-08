# Evidence status — agentic development

This page records what one engineer's agentic-development pilot tested, what
failed, and what was never run, so the guidance can say which of its choices
rest on a run and which are conservative defaults. The
[workflow](agentic-development-workflow.md) and
[working core](working-principles.md) state what to do.

Status: dated evidence record, 2026-09-24; corrected 2026-09-25 (R0A validity,
unrun conditions, the R0C baseline, R1 and R5 fixtures held privately) and
2026-10-01 (a key to the run labels; plainer critique and attribution notes).
No outcome was regraded. It reviews existing records rather than adding an
experiment: primary local run records and a later written critique of the
research program were re-read; raw session traces were not independently
regraded. Private targets, transcripts, model IDs, and internal contribution
sources remain outside this shareable record. It supports the
[documentation revision](../archive/2026-09-agentic-development/revision-spec.md).

## What the evidence permits

Run IDs below are stable experiment labels, not links to a public corpus.
Each reads `<fixture>-<condition>-<sequence>`: the fixture (R0A to R0D are
[archived](../archive/README.md); R1P, R2, and R3 are in
[evaluations](evaluations/README.md); R1 and R5 are held privately), the
condition (A is the baseline or only condition, B the treatment; R0D ran
only a treatment), and the attempt number. C3b and C4 are stages in the
archived [research backlog](../archive/2026-09-agentic-development/research-backlog.md);
S8 is a source row in [source intake](evaluations/source-intake-and-overlap.md),
whose M rows are mechanisms, distinct from the M1 to M9
[measurement candidates](evaluations/measurement-candidates.md); P0-CODEX-FANOUT-01
is a retrospective record outside the fixture series. The public instruments
explain the method; some need operator-owned private inputs and cannot be
replayed from this checkout alone.

| Record | Observed result | Limit and revision decision |
| --- | --- | --- |
| R0A-A-04, B-01, B-02 | A valid ordinary baseline had incomplete decision coverage. B-01 improved coverage but violated dependency order. B-02 was an **invalid** stopped run whose skill surface differed from the comparators; its repeated dependency failure is diagnostic only. Condition C and the B early-stop control were not run. | Retire the tested prompt wording. The baseline's different stop rule limits causal interpretation of coverage differences; do not call this a general test of interviews. Retain fact-first clarification as a working heuristic. |
| R0B-A-01, B-01 | The ordinary baseline already produced direct evidence. The treatment omitted required observations and earned no promotion. | Retain one question, observation, timebox, safe boundary, and cleanup; no new prototype skill. |
| R0C-A-02, B-02 | The baseline was the [spec-driven-change skill](skills/spec-driven-change/SKILL.md) at the file hash pinned as S8 in source intake, before its 2026-09-25 test-first proposal. It passed seven of twelve criteria and produced horizontal domain, API, and UI tasks without the required vertical partial order. The treatment also failed semantic criteria and exceeded its output limit. | Invalid for formal A/B inference; diagnostic observations retire that wording, not decomposition in general. |
| R0D-B-01 | A visible graph improved vertical shape but failed its frozen schema and retained an oversized task. | Retire the exact representation. A deterministic checker is useful only if its input contract is met. The temporary checker source was not retained here; a hash alone is not a replay package. |
| R1-A-03 | Valid efficient-capability, medium-effort single-owner audit with complete held-out substantive coverage on one fixture, in 125.861 seconds and 457,228 tokens. | Cost accounting was partial: phase and human active time were unavailable. This establishes adequacy for that task, not a best model or effort default. |
| R1-B-03 | **Invalid** full-context-fork treatment: conflicting owner context, role violations, forbidden duplicate tests, and an inaccurate owner report of compliance. It tied coverage in 178.096 seconds and 894,324 combined tokens. | Larger wall/token totals are descriptive failure costs. They cannot establish the cost or benefit of compliant delegation. Retire this treatment for the fixture. |
| R1P-A-03 | After two host-interface calibration failures, a fresh-packet child returned the marker, used zero tools, had no descendants, and was awaited, at 43,398 combined exposed tokens. | Interface and observed-compliance preflight only. It did not test useful work or enforced denial of a disobedient action. |
| P0-CODEX-FANOUT-01 | Retrospective broad research fan-out produced evidence but repeated context and missed authorized evidence in one packet. | Tasks, models, effort, and calls differed; no cost ceiling was predeclared and full owner/human cost was missing. Retiring the broad shape was an operator judgment, not a failed predeclared cost gate or model ranking. |
| R2-A-01, B-01 | Local retrieval passed nine of ten criteria; the IDE route passed ten and repaired a critical miss at 2.056 times exposed tokens. | The IDE arm used text search and file reads, not symbol/call analysis. One comparison supports a later gap-driven pilot, not IDE-first routing or semantic-navigation superiority. |
| R3-A-01, B-01 | Both found seeded substantive defects. Separate ledgers improved status reporting but still misplaced a critical concurrency concern under the frozen grader. | Retire the prompt-only treatment. Independent review remains a risk-based choice; more reviewers and mandatory ledgers were not qualified. |
| C4 | Model/effort tuning was not activated for the unqualified explorer topology. | No optimized strong-owner/cheap-worker combination, model ranking, or effort optimum was established. |
| R5 / R7 / R8 | R5 has an unrun synthetic source-only fixture, held privately. R7 lacks an owned authoritative source and independent semantic key. R8 remains pending. | No domain overlay or live-service claim is promoted by this revision. |

These are sparse, subjectively graded observations. Treatment authoring and
grading were not established as blinded and independent throughout the record.
Single trials do not estimate variability. Invalid runs retain safety and
diagnostic value, but must not enter comparative averages as valid treatments.
Historical results remain historical after model or host drift: rerun both
arms under current, matched conditions for a new comparison.

## What changed, and where it belongs

| Disposition | Material | Rationale and owning layer |
| --- | --- | --- |
| Retain as a working choice | One accountable owner; smallest fitting lane; deterministic retrieval first; one writer per coupled unit | Conservative operating choices, not measured universal winners. Concise [core](working-principles.md) and personal samples; detail in the workflow. |
| Retain as baseline, unqualified | The spec-driven-change skill | It remains the on-demand procedure for long or risky work. R0C observed a decomposition gap in the pinned version on one synthetic fixture; it is not a qualified decomposition method, and a successor needs its own frozen comparison. The test-first step added later is not yet evaluated. |
| Revise | Delegation gate and sufficient packet | Include authorization, named consumer, useful owner work, approvals, effective controls, actual-action audit, and stop/cleanup. The [workflow](agentic-development-workflow.md) owns the packet; roles specialize it. |
| Revise | Role contracts | Align context and permission reporting across owner, explorer, reviewer, and classifier. These textual revisions remain unqualified candidates; R1P does not qualify the suite. |
| Revise | End-to-end lifecycle | Name the review artifact, release decision, observation responsibility, recovery, and feedback into intent. No automatic commit, release, monitor, or external write follows from the diagram. |
| Revise | Evaluation method | Add repetitions/order, frozen registration, grader independence, measured approvals, invalidity, and later defects. Thresholds must use available measures; arbitrary trial counts and cost ceilings from critiques are not adopted as optima. |
| Revise | Surface adoption | Codex, Claude Code, and Cowork get concrete guidance and separate mechanics. No assumption that common prose produces equal discovery, permissions, subagents, or persistence. |
| Revise | Repository onboarding | README owns orientation and navigation; contributor instructions own local working rules; focused references own detail. This is a proposal-derived placement choice, not a fresh-start benchmark result. |
| Revise | Research navigation | Archive the roadmap and research notes as dated context; keep dated results here and in source intake, and outstanding work in the archived [research backlog](../archive/2026-09-agentic-development/research-backlog.md), which is not an active queue. Avoid carrying retired tasks as immediate instructions. |
| Remove from shareable copy | Private target names, history identifiers, source-specific grader answers | The R1 packet and key stay private, and no R1 template is published. Private evidence remains unchanged; no invented public replacement is labeled as the historical fixture. |
| Defer | Useful fresh-packet comparison, model/effort tuning, parallel writers, host-native role installation | Require a named task, frozen baseline/key, observable cost and boundaries, then a representative pilot. |
| Reject for this revision | Automatic fan-out, model-ID defaults, a new orchestrator/installer/registry, blanket two-ledger review, whole-bundle skill adoption (the author's personal bundle trial sits outside this; see the [skill-derivation decision](decisions/0001-selective-skill-derivation.md)) | No demonstrated need or qualifying evidence; unnecessary maintenance and wider authority. |

## Critique adjudication

The later written critique of the research program, not published here,
helped locate contradictions; it is not another experimental result. Its role-isolation, measurable-threshold, approval-cost, lifecycle,
sanitization, and attribution concerns led to the revisions above. Its proposed
fixed trial counts and token ceilings remain proposals. Current product claims
were checked afresh instead of copying its older host assumptions.

The original R1 design had a saturated coverage baseline, overlapping owner
and explorer questions, and a cost win dependent on unexposed active time.
The [C3b design gate](../archive/2026-09-agentic-development/research-backlog.md#c3b--useful-fresh-packet-comparison)
therefore requires disjoint questions and an observable decision rule before
any new run. A new prompt or packet gets a new version, not an invisible retry.

## Attribution and publication

Public sources remain credited beside the mechanisms they informed in
[source intake](evaluations/source-intake-and-overlap.md) and the
[workflow influences](agentic-development-workflow.md#influences-not-validation).
Anthropic's playbook supports the artifact chain and incident return edge;
the disposable-prototype lane is a separate local/practitioner influence,
not a stage attributed to that playbook.

Unpublished collaboration and guidance drafts also informed this record; it
neither quotes them nor claims anyone's endorsement. Public sharing needs the
[release checks](sharing-and-release.md).
