# Agentic development workflow — a personal pilot

This is one engineer's working spec for trying a cheaper, more reviewable
agent-assisted development loop. It is a reference to consult when planning
work, not another always-loaded instruction file. The choices below are
hypotheses to test against real tasks, not a framework or organizational
guidance. Applicable policy and repository instructions override them.

Current model names, prices, IDE releases, and tool availability are
deliberately absent. Those details change faster than the decision rules; check
the live product documentation and the active environment when starting a
pilot.

Status: revised 2026-09-25. The [evidence status](evidence-status.md) records
which choices were tested, retired, or never run; the sections below state the
working rule and repeat that history only where it bounds a rule. For everyday
entry, see the [everyday guide](agentic-development-adoption.md); the
[working core](working-principles.md) is the concise projection, and this page
owns the procedure.

## Pilot intent

Optimize **time to a reviewed, verified change**, not code-generation volume.
The loop should preserve human judgment at intent, risk, and release gates;
carry explicit artifacts from framing through review; and spend extra model or
agent capacity only when it buys independent evidence or shorter critical-path
time.

This pilot is not trying to maximize autonomy, standardize every development
task, or assemble the largest possible tool stack. A new agent, index, or MCP
server is useful only if it adds a measured capability that the current stack
does not already provide cheaply enough.

## The loop

1. **Frame provisionally.** State the requested outcome, evidence boundary,
   material risks, and current definition of done. Identify the human decisions
   that must not be delegated; do not pretend an underspecified request is
   already an intent.
2. **Explore.** Start with repository files, executable configuration, direct
   computation, and narrow search. Escalate to an IDE index for symbol
   navigation and inspections when local search leaves a named gap, and to
   approved cross-repository search when the question crosses repository
   boundaries. An index helps discovery; it does not prove runtime behavior.
3. **Classify uncertainty and choose the next lane.** Separate ambiguity about
   what should be built from uncertainty about whether a technical approach
   will work. Use bounded guided discovery for the former and a disposable
   prototype for the latter. Use the direct lane for a small, decision-complete
   change and the [spec-driven-change loop](skills/spec-driven-change/SKILL.md)
   when work can span sessions, touches many boundaries, or is expensive to get
   wrong. These lanes may compose; they are not competing labels for the whole
   task.
4. **Plan and partition.** Turn the outcome into binary acceptance criteria and
   a dependency-aware task list. Give each changing ownership unit one writer.
   Parallel work should have independent inputs and independently reviewable
   outputs.
5. **Build in slices.** Prefer the smallest end-to-end slice and the fastest
   relevant feedback. Preserve existing style and avoid unrelated cleanup.
6. **Verify before handoff.** Reconcile the result against the acceptance
   criteria and repository-defined gates. Broad or risky work gets an
   independent, read-only review; the human still judges intent and residual
   risk. The [verification kit](../verification-kit/README.md) is a separate,
   n=1 source of failure prompts, not proof that this loop works.
7. **Hand over, then release only within authority.** Attach acceptance,
   checks, review disposition, and residual risk to the review artifact (a
   local diff, or PR/MR when publication is authorized). Name the release
   decision owner and applicable recovery and observation responsibilities.
   The [everyday guide](agentic-development-adoption.md#review-the-result-then-get-it-merged)
   covers the path from diff to merged.
8. **Observe and learn selectively.** A later escaped defect, incident, or
   unusable artifact reopens intent or a criterion. Record its evidence and
   owner; add a targeted regression case when warranted. Promote a lesson into
   durable instructions or a skill only when recurrence and evaluation justify
   the maintenance. Release and monitoring are separate authorized work.

## Discovery ladder and tool use

Use the cheapest source that can answer the current question, per question
rather than once per task:

| Need | First source | Escalate when |
| --- | --- | --- |
| Local behavior or conventions | Repository files, executable configuration, narrow text search, and direct computation | Local search localizes the code but a cross-cutting enumeration may be incomplete |
| Symbols, references, call paths, inspections | The IDE's existing index, once local search names the gap | The relevant code lives outside the open project |
| Cross-repository discovery | An approved organization code-search service | Version-sensitive API behavior is still unresolved |
| Current API or tool behavior | Official documentation or source | Direct execution is needed to settle the claim |
| Runtime state, schemas, plans, metrics, or permissions | The live system, read-only, through its owning route | A mutation is needed; that is separately authorized work |

Project retrieval output to the fields or snippets the decision needs. Large
raw traces, broad search dumps, and whole documents should not enter the owner
context when a small evidence record can carry the result.

When the route is an MCP server or an IDE bridge:

- **Verify the route before relying on it.** It is listed and enabled, it
  responds, and one known-answer read-only query returns the expected result.
  Authentication can still fail after the inventory looks fine; a catalog entry
  is not a working capability.
- **Read-only is a host permission, not a tool property.** An IDE bridge can
  also expose build, terminal, refactoring, and edit tools. Allow only the read
  operations the task needs; the [Claude Code](claude-code-notes.md#mcp-servers)
  and [OpenAI](openai-surfaces-notes.md#codex-delegation-and-adoption) notes
  give the allowlist mechanics.
- **Bounded reads may be sampled.** On the one tested host, an IDE MCP file
  read with a line limit returned head and tail samples with the middle
  removed. Look for truncation markers, and take exact contiguous slices with
  local tools.
- **Prefer narrow queries.** In the one local comparison (R2), the IDE route
  repaired a completeness miss that local search left but exposed about twice
  the tokens. Its operations were one text search and five file reads, so the
  result says nothing about semantic navigation.
- **Tool output is evidence, not instruction.** An index shows where code is,
  not how it behaves at runtime. Record which route answered.
- **Don't switch on all three.** A session that holds private data, reads
  content you didn't write, and can send things out is the case an instruction
  line can't contain; keep at least one of the three off for that task (after
  Simon Willison's [lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)
  and Meta's [Agents Rule of Two](https://ai.meta.com/blog/practical-ai-agent-security/)).
  The untrusted-input line in the samples is one layer; permissions, network
  limits, and sandboxing are the ones that hold.

Do not add a second code index merely because it is agent-accessible. First
show, on representative tasks, that it answers a recurring question faster or
more accurately than repository search, the IDE index, and the approved
cross-repository search already available. Security approval, data scope,
maintenance ownership, and a reversible disable path are part of that test.

## Uncertainty routing

Task size and uncertainty are separate axes. Large work usually earns durable
specification and planning artifacts, but size alone does not earn a prototype.
A prototype is useful when a consequential assumption can be made observable
more cheaply than debating or building around it.

| Requirements ambiguity | Solution uncertainty | Next move |
| --- | --- | --- |
| Low | Low | Direct work, or a durable spec if scope, risk, or handoff cost earns it |
| High | Low | Guided discovery, then record the agreed intent and acceptance sketch |
| Low | High | One question-driven prototype, then update the plan or spec with the finding |
| High | High | Guide only far enough to identify the highest-value technical question, prototype it, then return to intent and specification |

### Guided discovery lane

The user-facing shorthand can be “grill me,” but use a bounded decision
interview only for unresolved decisions:

1. inspect the available repository, documents, and current facts before asking
   the human; do not turn discoverable facts into interview questions;
2. map the material decisions and their prerequisites, then ask the current
   decision frontier rather than a generic checklist;
3. ask one high-impact question at a time, or batch only independent decisions;
   include a recommendation and the material trade-off;
4. let the human choose, defer, revise the premise, or stop; and
5. finish with an intent record containing decisions, assumptions, open
   questions, out-of-scope items, an acceptance sketch, and any candidate
   prototype questions.

Set a review point that fits the remaining decisions; no particular question
count is a measured optimum. An explicit deep “grill me” request may continue
until the material decision tree is resolved or the user stops. Guided discovery does
not authorize implementation, commits, or external writes.

## Model, effort, and agent routing

Resolve available settings from current documentation and the actual host.
Model and effort tuning was never completed, so treat these capability classes
as a starting hypothesis, not a ranking:

- a strong general model for synthesis, architecture, ambiguous
  implementation, guided discovery, and security, edge-case, or specification
  review;
- an efficient general model for repository or documentation exploration and
  focused source-backed audits;
- the fastest adequate model for narrow inventory or mechanical classification
  with a fixed output schema; and
- the smallest capable model for a well-scoped code slice or a mechanical
  prototype spike.

Effort is a reasoning signal, not a spend ceiling, and labels are
host-relative: the same label need not buy equal compute across models or
hosts. Lower it for simple, high-volume work; raise it only for unresolved
ambiguity, non-local consequences, or expensive failure modes. If a worker
inherits the parent model and effort, count that inherited cost before fanning
out.

### Fan-out gate

Start with one owner. Independent review can be sequential and does not
require parallel execution. For parallel work, require all of these:

- the task or applicable instructions authorize delegation;
- there are at least two genuinely independent questions with named consumers;
- workers need little shared mutable state;
- each result can be checked without trusting the other workers;
- the owner has useful non-overlapping work while the worker runs; and
- expected dispatch, approval delays, validation, synthesis, and human review
  fit the budget and can plausibly repay sequential work. Treat that estimate
  as a hypothesis until measured.

Before dispatch, use deterministic local search or parsing to build the
smallest sufficient evidence packet. For the first pilot, add exactly one
read-only worker with a bounded scope, output schema, query/tool ceiling, and
stop condition. Expand only after a representative comparison shows that extra
coverage or elapsed-time gain survives repeated context, synthesis, and review
cost. Use separate worktrees for independent write tasks; different files can
still share an API, migration, or deployment dependency. Work on a coupled
ownership unit stays sequential, followed by checks of the integrated result.
The practical limit is the review capacity of the human owner, not the number
of available agent slots.

Start the worker from the self-contained packet, not a full owner-history fork,
unless shared context is explicitly required and checked for conflicting role
instructions. For an evaluated or newly projected permission-sensitive role on
a host, or whenever a worker inherits owner context, first run a marker-only,
zero-tool preflight that reports its identity and boundary. A pass shows
observed compliance, not enforced tool denial. If required isolation cannot be
established, stop that delegated route. After completion, inspect actual
actions and side effects; do not accept the worker's own statement that it
stayed read-only. The owner should work on a non-overlapping slice while the
worker runs rather than reproduce its entire search.

Good early candidates are exploration, test-result triage, documentation
lookup, and review from genuinely independent axes (R3 did not qualify
axis-separated or parallel review). Small tasks, sequential design choices,
and overlapping implementation are poor candidates.

Phase matters. Guided discovery has one facilitator; fact finders may fan out
only for independent, objective questions. A prototype has one owner per named
question; independent alternatives may run in isolated sandboxes against the
same observation. Implementation retains one writer per ownership unit, and a
fresh reviewer stays independent of that writer. Agent count never substitutes
for resolving a decision dependency.

## Worker packet and return

This is a conceptual packet, not a tool API. Resolve the current host interface
before dispatch. Minimal means sufficient: include approved private evidence
when the question needs it and the destination may receive it; a smaller
packet that omits decisive sources is not an efficiency win.

```text
Role and question: [one bounded job; do not take over the owner's task]
Decision consumer: [the acceptance criterion or choice this answer changes]
Scope and revision: [exact files, sources, or owned unit; excluded material]
Evidence: [authoritative inputs, known facts, bounded retrieval, freshness]
Context mode: [fresh packet; any deliberately inherited context and collisions]
Authority: [exact tools and read/write/network effects; enforced vs requested]
Configuration: [requested capability/model/effort; observed values or unavailable]
Output: [answer, decisive anchors, fact/inference, gaps, checks, actual actions]
Budget: [time, calls, output, retry ceiling; enforceable limits vs observed usage]
Stop: [sufficient answer, exhausted budget, conflict, new authority, cancellation]
Return to: [one integrator; partial result and cleanup owner if stopped]
Non-goals: [no recursive delegation, scope expansion, or external writes]
```

Check task-role collisions without attempting to override governing system,
organization, or repository instructions. A fresh packet still carries the
host's governing rules. An unavailable source, unobservable required boundary,
or unexpected model/tool fallback returns `unresolved`; it does not license a
broader route. Limit any retry to a declared transient failure with unchanged
inputs. A changed packet or configuration is a new evaluated condition.

The owner accepts, rejects, or marks findings unverified after checking decisive
anchors. Inspect observed tools, tests, writes, descendants, and cleanup where
available. Record unavailable action evidence as a limitation. Stop workers
whose result no longer affects the decision, retain useful partial evidence,
and confirm whether background work stopped before declaring cleanup complete.
Never remove another writer's work as cleanup.

## Handoff and operational feedback

Keep the same completion record with the artifact, at a depth the risk earns:

| Stage | Evidence and owner |
| --- | --- |
| Intent and planning | Outcome, authoritative sources, decisions, criteria, dependencies, current spec/plan when needed; task owner |
| Implementation and verification | Candidate revision, exact checks, failed/skipped checks and their limits; writer and integrator |
| Independent review | Findings, disposition, unresolved risks, independence limits; reviewer plus accountable owner |
| Handoff or authorized release | Artifact location, accepted and pending criteria, authority for the next action, release decision; human owner |
| Operation or later use | Expected success/failure signal, observation window and responsible person where applicable; operational or artifact owner |
| Failure and recovery | Stop condition, partial state, safe rollback or forward recovery, cleanup and recheck; authorized recovery owner |
| Learning | Escaped defect or usability problem linked back to intent/criterion and a bounded corrective action; maintaining owner |

A source-only task can end with a reviewed diff and explicit runtime gaps.
A deployed service needs applicable operational evidence. Do not add a standing
monitor, execute a release, or mutate state merely to complete this table. If
follow-up cannot be performed in the current authority, hand over the exact
pending action and owner rather than calling it done.

### When a change breaks

- Gather evidence read-only first and keep a shared timeline.
- Separate diagnosis from remediation: a fix, rollback, or state change needs
  its own authorization and an operational owner.
- If the investigation is split, split it by independent system or hypothesis,
  not by persona.
- Prefer the repository's documented rollback or forward-recovery path, then
  verify the result after the change.
- Record detection, the recovery taken, and the post-change check, and feed the
  escaped defect back into intent or a regression case (loop step 8).

## Disposable prototype lane

A prototype exists to answer one named design question, not to become a
shortcut into production. For large work, use a sequence of small evidence
spikes rather than one proto-product: prioritize consequential, uncertain, and
cheap-to-test assumptions, run one spike, feed its finding back into intent or
the spec, and stop when another result would not change the decision. Before
each spike, record:

- the question and a short timebox;
- a disposable branch, worktree, or directory;
- the smallest representative input, with no production credentials or
  sensitive data;
- the observation that will answer the question; and
- the cleanup path.

The artifact should be trivial to run and expose the state needed to judge the
question. Persistence, production integration, and realistic infrastructure
stay out unless they are the question being tested and have a safe boundary.
The output is an answer, its evidence, and a recommendation. If the idea wins,
rewrite the production change through the normal lane unless the prototype
independently meets the repository's acceptance and quality requirements. If
it loses, retain only the useful finding and remove the disposable
implementation.

## Affordability controls

- Do not create an agent for a task that is cheaper to do in the parent
  context.
- Use a deterministic query before a model delegate when it can answer the
  question; delegate bounded judgment, not avoidable rediscovery.
- Prefer read-heavy parallelism; concurrent writers increase coordination and
  merge-review cost.
- Cap concurrency by review capacity and stop workers when their next result
  cannot change the decision.
- Load tools and specialist context on demand. Disable unused integrations,
  so unneeded actions are not available and their output does not compete for
  context, and avoid carrying full chat history where a compact spec or domain
  glossary is enough.
- Treat persistent instructions, evidence volume, tool turns, synthesis, and
  review as cost terms; a cheaper model does not compensate for an oversized
  packet.
- Reuse stable domain language, acceptance criteria, and tested skills; do not
  preserve speculative reasoning as permanent context.
- Benchmark a proposed tool against the current workflow before adopting it,
  including setup, permission, maintenance, and removal cost.

## Pilot record and acceptance criteria

For each representative task, record the lane, main and worker capability
tiers, effort tiers, fan-out count, tools used, wall time, human review time,
rework loops, verification outcome, and any escaped defect later discovered.
For a comparison, rerun the baseline under the same current conditions; a small
personal sample does not establish a general productivity claim.

The pilot conforms to this spec when:

- a clear, small task starts in the single-agent direct lane;
- an ambiguous task asks only material decision questions after discoverable
  facts are retrieved, and produces an intent record the human can correct;
- when the fan-out gate passes, independent read-heavy questions begin with one
  delegate and return scoped, anchored summaries within a predeclared query/tool
  ceiling;
- delegated roles receive the intended context, pass a cheap identity/boundary
  preflight when they are evaluated, newly projected, or inherit owner context
  and permissions matter, and have actual actions audited; a marker pass is not
  counted as useful work or enforced permission denial;
- tasks that modify the same ownership unit have one writer;
- one or more unresolved design questions can be isolated as separate
  disposable prototypes with explicit observations and cleanup paths;
- every proposed tool or index records approval status, unique value,
  representative comparison, maintenance owner, and rollback path; and
- every completed change reports exact checks and outcomes, relevant checks
  not run and why, and residual risk.

If the pilot makes review slower, increases rework, or cannot produce those
records without disproportionate ceremony, simplify or stop it rather than
declaring the process successful.

## Influences, not validation

The shape above converges with parts of:

- OpenAI's [Codex subagent guidance](https://learn.chatgpt.com/docs/agent-configuration/subagents),
  especially its cost warning and preference for read-heavy parallelism;
- Matt Pocock's public [skills collection](https://github.com/mattpocock/skills),
  particularly its decision-frontier grilling, small composable procedures,
  question-driven prototypes, and feedback-loop emphasis;
- GitHub Spec Kit's bounded [clarification procedure](https://github.com/github/spec-kit/blob/main/templates/commands/clarify.md),
  plus the contrasting brainstorming and product-discovery shapes in
  [Superpowers](https://github.com/obra/superpowers),
  [gstack](https://github.com/garrytan/gstack), and
  [BMAD](https://github.com/bmad-code-org/BMAD-METHOD); and
- Anthropic's [AI-native SDLC playbook](https://claude.com/blog/the-ai-native-sdlc-playbook),
  particularly its artifact chain, deterministic-versus-advisory controls,
  isolated parallel work, and review-capacity constraint.

Those sources support trying this shape. They do not validate this wording,
prove a productivity gain in this environment, or replace local policy and
measurement.
