# Changelog

Dated record of what changed here and why. Written retroactively on
2026-08-10 from the commit history and the working notes behind it, so
entries before that date are reconstructions — coarser than the commits
they summarize, and silent about whatever the commits did not record.
Updated when a convention changes or the repo changes shape, not on every
edit.

Two omissions are deliberate. There is no version number: this is not
released software, and the only versioned things in it are the
verification-kit instruments, which carry their own version lines. And
there is no pattern count anywhere below — the taxonomy table is the only
place one lives, for the reason recorded under 2026-08-05.

The taxonomy and the audit template are maintained elsewhere and copied
here. Entries below describe what landed in this copy.

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
