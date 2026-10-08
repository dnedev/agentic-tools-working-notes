# Changelog

Dated record of what changed here and why. Written retroactively on
2026-08-10 from the commit history and the working notes behind it, so
entries before that date are reconstructions — coarser than the commits
they summarize, and silent about whatever the commits did not record.
Updated when a convention changes or the repo changes shape, not on every
edit.

Two omissions are deliberate. There is no version number: this is not
released software, while individual instruments and candidate contracts carry
their own version lines. And there is no pattern count anywhere below — the
taxonomy table is the only place one lives, for the reason recorded under
2026-08-05.

The taxonomy and the audit template are maintained in the claude.ai project
and ported here. Entries below describe what landed in this copy.

## 2026-10-08

- Reordered the entry points by what a reader came for, after a friend called
  the notes "too much framework" and said a few readers didn't run most of it.
  Simulated cold reads by three reader personas, and a structure map, found
  the usable parts behind about forty lines of caveats, method, and a
  directory listing, every
  sample two clicks from the README, and an agent file written only for
  maintainers. The README now opens with a short intro that carries the
  caveats, then a **Start here** table of separate entry points: the task
  brief, a hand-off prompt for the reader's own agent, review, recovery, the
  audit prompt's paste block, the coding-agent samples, the other tools'
  samples, the workflow, and passing the notes on.
  Where the notes came from, the method, and its evidence follow, and the full
  disclaimer moved into Scope rather than being cut. The samples and the
  method are now described as two halves of the same work rather than the
  samples as supporting artifacts. The [harness index](harness/README.md)
  leads with a table of samples by tool; its background essays follow the
  catalog, grouped under one heading and otherwise unchanged. The kit's quick
  start is now "Try it on one conversation", because a simulated cold reader
  found "ten minutes" oversold for the
  length of the paste block. No file moved, and no instrument changed.
- [AGENTS.md](AGENTS.md) now opens with a short section for an agent that
  someone points at these notes to use them. Every maintainer rule stays in
  the same auto-loaded file under "Editing this repository", unchanged apart
  from its heading level and the section's opening lines ("Applicable
  guidance" moved up beside the new section, since it applies to both),
  because that is where an editing agent sees the propagation rule; the
  taxonomy's amendment note alone didn't stop count drift. The cost is that
  an agent only using the notes loads those rules too, and the file, already
  past the under-200-lines target in Claude Code's
  [memory documentation](https://code.claude.com/docs/en/memory) (checked
  2026-10-08), grows further. The CLAUDE.md sentinel names the new sections.
- Added a [hand-off prompt](README.md#hand-it-to-an-agent) for a reader who'd
  rather point their own agent at the notes and ask what's useful. Its limits
  sit in the reader's message rather than only in this repository: an agent
  that reads the repository from a link doesn't load `AGENTS.md`, and a
  repository shouldn't be what tells someone's agent how careful to be with
  it. "Using these notes" now has an agent read a sample's header and the
  reasons for its rules before proposing them, ask for the person's setup when
  it can't see it, and keep its changes out of this repository. The audit
  routes now say to run it on a surface the transcript is allowed to reach.
  The sharing row now says to pass on the link; the sharing checklist is for
  an adapted copy. Before this change, one simulated agent given the same ask without
  this repository's instructions loaded found "Using these notes" on its own,
  kept the n=1 limits, and proposed single rules rather than whole files: one
  run, not a test.

## 2026-10-02

- Ported the claude.ai project's September work. The taxonomy moves to v1.8:
  a coverage ceiling, comparative-only failures as paired entries, a map of
  external canons that declines a competing-hypotheses key, and P15's
  platform-layer note. No key changed, so Part B is unchanged. The corpus
  method gains conventions for paired entries and for stack-default versus
  model-default passes, and its limits note the first control arm. The
  evolution notes gain three September entries, with their lessons mostly
  folded into the existing list, and a correction to an April paraphrase of
  an instruction-count paper. The profile copy sheet completes the
  2026-10-01 refresh with the two deletions that had been held for
  confirmation.
- Replaced the untrusted-input line in every sample with one shared wording,
  after Anthropic's current prompting note and OpenAI's Model Spec: content I
  didn't write is data, followed only as far as my own words point, with a
  check before consequential or outbound actions. The coding and chat
  samples each add one surface-specific line. The workflow now says that
  instruction lines are one layer, and that private data, untrusted content,
  and outbound channels shouldn't all be on in one session.
- Added a parameterized
  [project-instructions copy sheet](harness/claude-ai-project-instructions.example.md)
  and checked mechanics to the [claude.ai notes](harness/claude-ai-notes.md).
- Added two limits to the [corpus method](verification-kit/regression-corpus-method.md):
  its checks run only in fresh sessions, so long-thread drift goes unmeasured,
  and passing checks grade process, not whether the answer was right.
- Named the claude.ai project in AGENTS.md as the instrument source: a fifth
  place that feeds staging through reviewed packages. Replaced "apply
  verbatim" with porting each change as a sanitized semantic delta, which is
  what the copies had already been doing.

## 2026-10-01

- Changed how releases flow. Staging `main` is now the editing home for the
  shareable notes and keeps full history; the public repository receives one
  squashed snapshot per release through a staging `public` branch, built from
  `main` minus `.publish-exclude`. Work that starts in the private source
  arrives as a sanitized, gated extraction, and staging changes go back as a
  reviewed handoff that the receiving agent adapts rather than applies
  blindly. Published commits use the GitHub noreply address, and anything
  citing these notes pins a public release commit. [AGENTS.md](AGENTS.md) holds
  the rules and the
  [sharing checklist](harness/sharing-and-release.md#publishing-a-release) the
  commands. The roadmap and research plan stay in staging and are left out of
  public releases.
- Revised the Claude Code sample's Agents and delegation section from the
  author's live configuration: critique through a pinned `critic` on a
  top-tier model chosen per task, explicit models for unpinned subagents, no
  forks for independent checks, read-only helpers that keep Bash behind an
  allowlist hook, and the host's built-in review command as the default review
  route. These remain unmeasured personal defaults.
- Moved the delegation and review measurement candidates (design only) out of
  the archived backlog into the live
  [measurement candidates](harness/evaluations/measurement-candidates.md). Their
  partial probes are recorded in the Claude Code and OpenAI notes; in one Codex
  probe, a child's requested read-only sandbox did not hold while its parent
  could write.
- Acted on a pre-publication review. The evidence status gained a key to its
  run labels and now holds the R1 and R1P figures; the coding samples'
  task-scale paragraph and the task brief use plainer words; the spec-driven
  skill's test-first step became a regular instruction; and the September
  entries below were compressed to changes in shape, leaving run figures to
  the evidence status and source intake.
- Rechecked the surface notes against current documentation: Cowork's move
  into the new Claude experience and the October 6 cloud-only change for new
  Pro and Max tasks, default-on claude.ai memory, custom GPTs moving to
  plugins, Cursor's renamed rule settings and hook failure behavior, newly
  documented CoCo CLI flags, and redirected or dead links. Refreshed the
  claude.ai profile copy sheet from the current live profile.

## 2026-09-25

- Consolidated the notes for daily use after a read-only once-over review (a
  review, not an experiment). The
  [everyday guide](harness/agentic-development-adoption.md) became the daily
  page — the task brief, reviewing and merging the result, recovering a
  session that goes sideways, and optional setup — and the README separates
  "Today" from "When you are changing how you work".
- Moved the evidence record out of the archive to
  [harness/evidence-status.md](harness/evidence-status.md), because the
  guidance links to it, and corrected it in place where a pre-commit review
  found errors (R0A-B-02 invalid, unrun R0A conditions, the R0C baseline), with
  dated amendment notes in frozen files. Moved the role contracts under
  `harness/evaluations/roles/` and archived the retired R0A to R0D
  fixture/grader pairs; R1 and R5 are held privately.
- Reworked the workflow's discovery section into a discovery ladder with tool
  use: route verification, host-enforced read-only access, sampled IDE reads,
  and narrow queries, drawn from R2. Replaced the model/effort table with
  capability classes and added a short incident lane. The Claude Code and
  OpenAI notes gained MCP status and allowlist mechanics, and the Cowork notes
  were corrected, against current documentation.
- Shortened the task-scale paragraph to three sentences, identical across the
  three coding samples, and added an unexercised test-first proposal to the
  spec-driven skill. adr-stub gained an optional Decided by field; the Claude
  Code notes describe a tool-less loading check and the parent `CLAUDE.md` gap
  it found; and this repository's import sentinel no longer depends on the
  import's position.
- Prepared the tracked tree for a reviewed public snapshot: generalized
  catalog, distribution, and baseline wording, and held the R1 operator
  templates and the unrun R5 fixture privately.

## 2026-09-24

- Archived the roadmap and research plan, lightly revised, and replaced the
  next execution plan with a shorter
  [research backlog](archive/2026-09-agentic-development/research-backlog.md).
  Added the revision spec and evidence reconciliation, and ignored `_output/`
  for private drafts and handoffs. Archived pending work remains pending.
- Added a small [working core](harness/working-principles.md) and an everyday
  adoption path with previews for Codex, Claude Code, and Cowork, keeping
  personal samples, contributor guidance, on-demand procedures, and
  experiments in separate scopes. Projected a compact task-scale and
  delegation paragraph into the Codex, Claude Code, and Cursor samples, and
  rewrote the Claude Code notes against current documentation, withdrawing the
  earlier per-item fan-out and client-age update advice.
- Extended the workflow through handoff, authorized release, operational
  observation, failure and recovery, and feedback into intent, with one
  sufficient worker packet that counts approvals and whole-task review cost.
  These remain working choices, not a validated productivity package.
- Reconciled the evidence: R1's delegated treatment stays invalid, R1P stays
  marker-only, the P0 fan-out record cannot rank models, R2's IDE result used
  text and file operations only, and model/effort tuning (C4) was not
  completed. Retired prompt treatments were not promoted. Aligned the candidate
  role contracts and added run-record fields for repetitions, frozen
  registration, grader independence, approvals, and later defects.
- Removed private subject names, private-history references, and
  source-specific grader answers from shareable evaluation material; no
  historical result was regraded. Added a two-audience
  [sharing checklist](harness/sharing-and-release.md). The verification-kit
  instruments and installed skills were unchanged.

## 2026-09-04

- Ran the first frozen comparisons; outcomes and figures are in the
  [evidence status](harness/evidence-status.md) and
  [source intake](harness/evaluations/source-intake-and-overlap.md). In short:
  R0A's guided treatment improved decision coverage but violated prerequisite
  order, and its stricter rewrite was an invalid run; R0B's prototype treatment
  added no direct evidence; R0C's decomposition treatment failed, and R0D's
  graph representation failed its schema; R3's two-ledger review made per-axis
  status visible but misplaced a critical risk; R2's IDE route repaired a
  completeness miss at about twice the exposed tokens; R1's forked explorer was
  invalid; and the R1P marker preflight passed. No prompt-only procedure was
  promoted to an installed skill, and no index or role was installed.
- Froze R5, a source-only Terraform assessment comparing the generic review
  contract with one independently worded overlay. It has not run.
- Held automatic fan-out: one delegate first, after a fresh-packet, zero-tool
  role preflight, instead of the earlier "two or three delegates" heuristic. A
  retrospective broad research fan-out produced useful evidence but was
  retired by operator judgment; it had no predeclared cost ceiling and cannot
  rank models.
- Materialized vendor-neutral v1 role contracts for the
  [owner](harness/evaluations/roles/owner.md),
  [explorer](harness/evaluations/roles/explorer.md),
  [reviewer](harness/evaluations/roles/reviewer.md), and
  [classifier](harness/evaluations/roles/classifier.md) as evaluation
  candidates, and revised the owner and explorer contracts to capture context
  mode, role identity, and actual tool and effect compliance. A role label or a
  clean final tree is no longer treated as proof that a worker stayed
  read-only.
- Versioned the R0A fixture after invalid baselines exposed an objective-stop
  gap and profile contamination, and split the model-capability and
  reasoning-effort experiments so each run changes one variable. Persistent
  context, evidence volume, tool turns, synthesis, and review are explicit
  whole-task cost terms; model tier alone is not the main cost control.

## 2026-09-03

- Accepted the
  [selective-derivation decision](harness/decisions/0001-selective-skill-derivation.md):
  keep neutral contracts, derive only mechanisms that beat an existing
  baseline on a frozen local comparison, preserve license and provenance, and
  behavior-test host-native projections. Acceptance authorizes the structure,
  not any individual skill.
- Added the first
  [source-intake and overlap record](harness/evaluations/source-intake-and-overlap.md),
  a [run-record contract](harness/evaluations/run-record-template.md), and
  frozen R0A, R0B, and R1 fixture/grader pairs. They pin the reviewed public
  revisions and licenses and predeclare safety, quality, cost, cleanup, and
  keep/change/retire rules before any run. The run record stays a Markdown
  contract; a machine schema is deferred unless the manual instrument earns
  it. No skill or collection was installed.
- Promoted guided discovery and question-driven prototyping to explicit
  workflow lanes, separating requirements ambiguity from solution
  uncertainty. Spec Kit, Superpowers, gstack, and BMAD are comparison sources;
  their broader bundles and side-effect assumptions are not adopted.
- Added a research and execution plan (archived; not in public releases) that
  extends the program across application code, infrastructure, data, semantic
  models, incidents, and research, and separates portable role contracts from
  host-native projections. Machine state, internal sources, exact model IDs,
  and the detailed claim register stay in ignored private files.
- Synced the [failure-pattern taxonomy](verification-kit/failure-pattern-taxonomy.md)
  to its September v1.6 semantics. P1 now makes explicit that unsupported
  wall-clock language about a conversation's own history is a generated
  specific; P14 covers the repeated oscillation caused by silently reweighted
  criteria; and the P15 note records that its related account-level clause was
  removed by preference rather than recast. The key set did not change, so the
  audit template's Part B sweep remains unchanged.
- Refreshed the
  [claude.ai profile copy sheet](harness/claude-ai-profile-instructions.example.md)
  from the September source snapshot: positional references when prior-turn
  timing is not established, verification-tracking in the answer body as well
  as the footer, and later footers that state a confidence move and its cause.
  Raw registry, profile lineage, and private regression-corpus inputs stayed
  ignored; none of their identifiers entered the tracked files.

## 2026-09-01

- Added a master roadmap (archived; not in public releases) above the task
  workflow, and a cross-surface
  [agentic-development workflow pilot](harness/agentic-development-workflow.md)
  for choosing a direct, disposable-prototype, or spec-driven lane, routing
  model capability and effort, and deciding when read-heavy fan-out is worth
  its review cost.
- Kept the note figure-free and policy-neutral, and added an adoption gate for
  another code index or MCP integration: approval, a distinct capability
  demonstrated against the existing discovery ladder, maintenance ownership,
  and a reversible disable path.
- Recorded the external sources as influences rather than validation: Codex
  subagent guidance, Matt Pocock's public skills collection, and Anthropic's
  AI-native SDLC playbook.

## 2026-08-19

- Added a sanitized, installable
  [Snowflake CoCo user-defaults sample](harness/coco-user-defaults.example.md)
  and separate [CoCo operating notes](harness/coco-notes.md). The sample
  covers establishing effective context, tier isolation, result completeness,
  validation stage, and the handoff; the notes own discovery, precedence, caps,
  enforcement, and the probe method.
- Made this sample a **partial** projection rather than another full one. On the
  tested installation, fresh CoCo sessions loaded the Claude Code global config,
  confirmed by its path and a unique behavioral marker; restating the shared
  evidence, calibration, continuity, and coding gates would add a competing
  copy. The sample and notes make both dependencies explicit: the general file
  and owner-maintained execution contract must exist, remain discoverable under
  active settings, and fit within the instruction cap, or their missing gates
  and boundaries need adding.
- Recorded positive observations from CoCo CLI 1.1.66: the user `AGENTS.md`,
  owner-maintained `CORTEX.md`, and Claude global file loaded. A collision probe
  loaded both workspace and user `AGENTS.md` paths; the Desktop documentation
  itself conflicts between path-based deduplication and skipping same-named
  files. Other instruction patterns were not characterized well enough to
  support general positive or negative CLI claims.
- Added a generic callee audience guard to the Claude Code sample's specialist
  routing section. A specialist that auto-loads its host's global file must not
  follow an instruction to delegate its own work back to itself.
- Noted in the notes, not in the sample, that always-on instruction files fail
  by omission — over the size cap, or by a name one surface ignores — which is
  why the verification advice is a fresh-session marker probe with a negative
  control rather than reading the file back.
- Tightened the repository opening for public sharing: dated and sanitized,
  n=1 and subjectively graded, useful as artifacts rather than a framework,
  benchmark, comprehensive methodology, production-readiness claim, or
  scientifically validated evidence. The project instructions now require
  public distribution to use a fresh sanitized snapshot rather than the
  private repository's history, and Finder metadata is ignored.
- Tightened third-party provenance before that export. The spec-driven-change
  sample now describes Spec Kit and Kiro as documented influences rather than
  borrowed text, removes an unverified paper page range, and links the Kiro
  behavior it names; the ADR sample uses MADR's actual template name. The
  license section now makes clear that linked works remain under their own
  terms.
- Reworked the harness inventory around agent surfaces while keeping its small
  file set flat. Samples remain next to their operating notes, and shared
  procedures remain under `harness/skills/`; vendor nesting and an underscore
  prefix would add path churn without clarifying ownership at this size.
- Shortened the root inventory to directory-level summaries and added
  task-oriented starting points, leaving detailed surface discovery to the
  harness index. Reworked the verification-kit index into unnumbered,
  linked artifacts and separated the run method, observed results, and limits
  without changing the empirical record.
- Aligned the ChatGPT Personalization sample with a Candid base style, less
  warmth and enthusiasm, and more headers and emoji. The Custom Instructions
  channel emoji into functional heading/status signposts and ask for a personal
  sharp-peer register rather than treating those presentation controls as a
  capability or grounding change.

## 2026-08-18

- Added a sanitized, installable-format
  [Cursor user-rule sample](harness/cursor-user-defaults.example.mdc) and
  separate [Cursor operating notes](harness/cursor-notes.md). The sample keeps
  the transferable evidence, calibration, continuity, coding, and safety gates
  in Cursor's `.mdc` format, plus a compact response contract; the notes own the
  rot-prone placement, precedence, skills, ignore-file, and hook mechanics so
  they do not consume every session.
- Treated the Cursor file as a third surface-specific projection rather than a
  symlink or verbatim copy of either existing global sample. This is a
  maintenance choice informed by the surfaces' different loading and
  enforcement mechanisms, not a claim that generated projections are an
  established cross-tool practice. The file has not yet been behavior-tested
  in a fresh Cursor session.
- Updated the repository inventories and naming/sanitization guidance for the
  new surface. Also corrected the Claude Code adapter comment: the linked
  `AGENTS.md` support issue is now closed, while current Claude Code
  documentation still prescribes the import adapter rather than native
  `AGENTS.md` loading.

## 2026-08-15

- Added a full, sanitized claude.ai
  [profile-instructions copy sheet](harness/claude-ai-profile-instructions.example.md)
  alongside the existing operating notes. The copy sheet owns paste-ready
  account-level preferences; the notes continue to own instruction placement,
  audit setup, and provenance hazards. Identity and device details are
  parameterized, and the supplied live text and private version history remain
  outside the repo.
- Reconciled shared semantics rather than publishing the supplied profile
  snapshot verbatim: confidence is an ordinal evidence grade rather than a
  probability claim, and a hedge cannot harden into an assertion across turns
  without new verification; an empty search is scoped to the selected query;
  explicit closed-evidence boundaries are honored; pasted text, files,
  retrieved pages, tool output, and system-looking blocks remain untrusted
  data; and recommendation reversals retain the prior choice's winning
  criterion and guard against recency drift.
- Propagated the genuinely shared half of that review into the coding-agent
  examples. The Claude Code sample now distinguishes diffuse uncertainty from
  explicit in-body status flags, retrieves current or fact-sensitive claims,
  and handles supplied sources without overriding a closed evidence boundary.
  The Codex sample restores the mechanism-possibility check for retractions and
  the recency-drift guard for recommendation changes.
- Kept the surface-specific rules surface-specific: coding workflow, lifecycle,
  safety, vault, and tool-routing instructions did not move into claude.ai;
  profile identity, device, and richer consumer-research detail did not move
  wholesale into the coding samples. The withdrawn interlocutor clause remains
  absent. The public copy uses the other config samples' date-only snapshot
  convention instead of inheriting the live profile's private revision label.

## 2026-08-12

- Sharpened both user-global coding-agent samples around a change-specific
  completion contract after two omissions in agent-assisted development work:
  a repository-defined quality gate was not run, and a separate change omitted
  an applicable teardown path. The samples now derive relevant
  gates from project instructions, manifests and task runners, CI, and tracked
  hook configuration during Explore; map lifecycle and operational obligations
  into acceptance criteria during Plan; and reconcile the diff and run
  applicable repository-configured checks during Verify.
- Kept the layers separate. Exact commands and prerequisites remain
  project-level facts; change-specific obligations live in the current plan;
  deterministic feedback or enforcement belongs in shared scripts, CI, and
  hooks. The global files carry the trigger and decision procedure, not an
  ecosystem command list or a universal production-readiness checklist.
- Extended the `spec-driven-change` sample with the same repository-contract
  discovery and a risk-scaled lifecycle lens for state, resources, and
  long-running activity. Its provenance section records the public sources that
  informed the addition. The harness README now records the layer architecture
  so the longer rationale does not have to be repeated in both global samples.
- This is a working prompt change, not a new failure-pattern key. Both source
  incidents are omissions, which the audit template already routes through open
  discovery rather than its span-based keyed sweep. The exact wording has not
  yet been regression-tested.

## 2026-08-10

- Synced both instruments from canonical. The taxonomy gains a
  source-overlap watch item, carried at label grain: the name and the
  tie-break neighbours travel, the FAIL test doesn't exist yet. The audit
  template gains a ledger-triage step between the cold read and the keyed
  sweep, which sorts the gaps a trace disclosed about itself and treats
  only one bucket — never attempted, though retrievable — as a finding. No
  pattern was added, so the keyed sweep is unchanged.
- Dropped the interlocutor guard from all three config samples — the
  [Claude](harness/CLAUDE.example.md) and [Codex](harness/AGENTS.example.md)
  ones and the [ChatGPT sheet](harness/chatgpt-personalization.example.md). It
  came out again on preference grounds a week after landing, and the ground was
  a preference about being characterized, which isn't specific to one surface.
  The evidence behind it didn't change, so the taxonomy still keys the pattern:
  what a trace gets graded for and what a config should instruct are separate
  questions, and only the second one is a preference.
- Folded the ledger-placement rule into the **Not checked** line's own
  definition in the Claude and Codex samples, replacing the two paragraphs that
  used to trail the ledger. An item one query away isn't a disclosure, it's a
  query nobody ran. This is the config-side half of the template's new triage
  step — same rule, compiled into a line that already has to be written rather
  than restated as another rule after it.
- Added the August milestones and a distilled lesson to the
  [evolution notes](verification-kit/evolution-and-lessons.md): a rule that
  is known and not followed gets recompiled into the shape of an output you
  already have to produce, rather than restated as one more rule — and, the
  same week, a rule removed outright on preference grounds with its evidence
  left standing.
- Fixed two references that pointed at nothing. The template's yield note
  cited a worked example "in these notes"; it lives in the private history
  behind them, not in this repo. And the template's footer listed
  flagged-chat handling among the machinery relocated to the
  [claude.ai notes](harness/claude-ai-notes.md), which never carried it —
  those notes now cover the case, and the
  [corpus method](verification-kit/regression-corpus-method.md) gains the
  provenance convention that goes with it.
- License attribution no longer names a person. CC BY 4.0 itself is
  unchanged — crediting this repository and linking back is an
  attribution manner the license lets the licensor designate.
- Trimmed self-referential phrasing in the harness README and the Claude
  config sample. The n=1 framing stays, because it is the point; what
  went was the "my own" intensifier in front of it.
- Added this changelog.

## 2026-08-07

`harness/skills/` starts here, and changed shape twice in one day.

- Added [`adr-stub`](harness/skills/adr-stub/SKILL.md) and
  [`spec-driven-change`](harness/skills/spec-driven-change/SKILL.md), then
  extracted the ADR format out of
  [`CLAUDE.example.md`](harness/CLAUDE.example.md) and into the skill, so
  the format lives in one place instead of being pasted into every layer.
- Corrected that skill's provenance against primary sources: which fields
  come from Nygard's original article, that `Date` comes from MADR, and
  that `Alternatives` is an adaptation rather than a quotation. A
  repository URL that no search could confirm was left uncited instead of
  reproduced.
- Published [`dotfiles-discover`](harness/skills/dotfiles-discover/SKILL.md)
  and [`dotfiles-sync`](harness/skills/dotfiles-sync/SKILL.md) as a pair.
  These are the first samples published standalone rather than because a
  config sample links to them — a change to what `harness/skills/` is
  for, not just another file. The pair is cross-linked and not safe to
  install split: `dotfiles-sync` defers its secret gate to
  `dotfiles-discover`.
- In that pair, a `git add -A` staging step became explicit-path staging,
  after the real dotfiles source repo turned out to be carrying unrelated
  modifications that `-A` would have swept into the commit.
- The root README began listing `harness/skills/` at all. It had covered
  the config samples and the per-surface notes and skipped the directory.

## 2026-08-06

- Repositioned the notes as dual-use — readable outside the environment
  they were written in. Named internal policy documents came out in favor
  of a generic deferral ("if anything here conflicts with the rules in
  your environment, follow those rules"), which resolved the outstanding
  link placeholders by removing the need for them.
- Tightened the confidence ladder, and pulled back lessons that had
  claimed more than the runs supported.
- Reflowed the ChatGPT
  [personalization sheet](harness/chatgpt-personalization.example.md) so
  the fields paste cleanly into the real form.

## 2026-08-05

- **Adopted the no-count convention.** The taxonomy table rows are the
  list; every other mention refers to the patterns collectively. Counts
  had already drifted between copies — a stale number outlived the
  taxonomy change that invalidated it, in more than one file. Removing the
  numbers removed the chore of chasing them.
- Synced the taxonomy and the audit template from canonical.
- Added the [license](LICENSE) and the
  [claude.ai notes](harness/claude-ai-notes.md).
- Added the OpenAI-side samples in one pass: a Codex user-global config
  ([`AGENTS.example.md`](harness/AGENTS.example.md), the counterpart to
  the Claude one), a ChatGPT
  [personalization sheet](harness/chatgpt-personalization.example.md),
  and [surface notes](harness/openai-surfaces-notes.md). Aligned the
  confidence ladder across surfaces, and rewrote passages that leaned on
  product figures into figure-free prose.

## 2026-07-27

- Added [`CLAUDE.md`](CLAUDE.md) and [`AGENTS.md`](AGENTS.md), with
  `CLAUDE.md` as a thin adapter that imports `AGENTS.md` — one
  instruction file rather than two copies to keep in step.
- Added the sanitized global Claude config example.
- Synced the verification kit from canonical and added the
  [regression corpus method](verification-kit/regression-corpus-method.md).
- Slimmed [claude-code-notes.md](harness/claude-code-notes.md) to durable
  principles plus pointers to the official docs. Product figures go stale
  faster than notes get revised, so the notes stopped carrying them.

## 2026-06-13

- Initial import: the [verification kit](verification-kit/README.md) and a
  `harness/` scaffold.
- Enabled SAST and Secret Detection in CI, from the hosting UI. Worth
  stating plainly, since the repo's own guidance does: secret detection
  catches secrets, not disclosure judgment, so a green pipeline is not
  sanitization clearance.
