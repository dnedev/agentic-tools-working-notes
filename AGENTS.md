# AGENTS.md

One engineer's working notes on instructing coding agents and chat
assistants, and on checking the answers they give: markdown only, nothing to
build or run. Claude Code reads `./CLAUDE.md`, which points here — one file,
not two copies. Follows the [agents.md spec](https://agents.md/), so Codex,
Cursor, and others read it too.

Two kinds of agent read this file. If someone pointed you at these notes so
they can use them, read **Using these notes** and **Applicable guidance**,
and skip **Editing this repository**: its rules don't apply to you. If you're
changing files in this repository for its author, or reviewing changes to
them, all of it applies; if both apply, the editing rules win. In your own
adapted copy, keep the register and sanitization rules and replace the
release flow with your own.

## Using these notes

- Start at [README.md](README.md). Its **Start here** table routes by what the
  person wants; each row is a separate entry point, not a step.
- One entry point needs no setup: the
  [task brief](harness/agentic-development-adoption.md#start-a-task), pasted
  into a session when the person starts a task. It's a message, not a config
  file; don't add it to their always-on instructions.
- The `*.example.*` files under `harness/` are sanitized, genericized
  derivatives of the author's own instructions: user-level files for coding
  tools, and copy sheets for account, project, and folder fields. They're
  tuned to the author's register and defaults. The
  [harness index](harness/README.md#samples-by-tool) lists each one with where
  it goes and its notes.
- To adapt a sample, read its header first (for Cursor, its notes): it says
  what to adapt, replace, or delete. Diff it against the person's existing
  instructions, asking for them if you can't see them, and propose only the
  missing rules, each with why it's there. The
  [working core](harness/working-principles.md) and the
  [evidence status](harness/evidence-status.md) explain the shared rules and
  what they rest on, and the harness index's
  [background](harness/README.md#why-the-samples-are-shaped-this-way) explains
  why the samples are shaped as they are, including which layer the completion
  rules belong in and why the CoCo sample stays partial. Read what bears on a
  rule before proposing it. Don't install a sample wholesale, even where a
  copy sheet says to paste its full block.
- Change the person's own instructions or settings, not this repository's
  files, and only after they approve the specific change. Keep the previous
  content so it can be restored, and leave managed or organization settings
  to their owner. Then have the person check what loaded in a fresh session:
  in Claude Code they type `/context` and `/memory`. For other tools, look in
  that tool's notes; not all of them say how, so check its current
  documentation too.
- For a conversation that went wrong, use the audit template's
  [paste block](verification-kit/trace-self-audit-template.md#paste-ready-template-copy-everything-in-the-block)
  as written: in a fresh chat, the person pastes or attaches the transcript
  first and the block after it, on a surface that transcript is allowed to
  reach. It's static by design; don't generate a per-thread variant.
- Not for installing: this file, `CLAUDE.md`, `harness/evaluations/`,
  `harness/decisions/`, and `archive/`. They and `CHANGELOG.md` explain why
  things are the way they are; open them when the person asks why. The tool
  notes, the workflow, and the working core are references to read, not
  instruction files.
- Keep the notes' limits when you summarize them: n=1, graded by the author,
  tied to the model versions the author used, and dated. Re-check a tool
  mechanic against current documentation before relying on it, and don't
  present the notes as a framework, a best practice, or evidence that
  something will work for the person.

## Applicable guidance

This repository contains personal working notes, not organizational guidance.
It does not represent any employer or replace applicable policy or mandatory
requirements. If repository material conflicts with the rules that apply in
the active environment, follow those rules.

## Editing this repository

Everything from here down applies when you change files in this repository.
The docs are versioned instruments that other copies are graded against, so
the risk here is **drift between them**, not bugs. These rules add only what's
specific to this repo, on top of any user-global and workspace instructions —
they don't restate them.

They stay in this auto-loaded file on purpose, for the reason Propagation ends
with: a rule kept where nobody looks while editing doesn't hold. The cost is
that an agent only using the notes loads them too; the opening lines tell it
to skip them.

### Preserve the epistemic register — the prime directive

The repo's whole value is honest, grounded, n=1 notes. When editing content:

- Keep the "one engineer's notes, take-what's-useful" framing. Don't upgrade it
  into a framework, a best-practice claim, or policy.
- Don't add confidence terms, counts, or evaluative claims the source doesn't
  earn — this repo literally catalogs that failure (see
  `verification-kit/failure-pattern-taxonomy.md`).
- Preserve the honest caveats (n=1, subjective grading, model drift). Match the
  existing voice; no drive-by rewrites of prose that already works.

### Propagation — the one thing to get right

`verification-kit/failure-pattern-taxonomy.md` is the source of truth for the
failure patterns. **The table rows are the list — they are the only place a
count lives.** Everywhere else, refer to the patterns collectively ("the
recurring patterns", "every key in the taxonomy", "these patterns"), never with
a bare number or a key-range like "P1–P15". That phrasing is deliberate: it is
what keeps adding a pattern from turning into a dozen one-line count edits.

One structural coupling survives this, on purpose: the template's **Part B keyed
sweep lists one line per taxonomy key**, so the template still works when the
taxonomy isn't reachable. That list must match the taxonomy's keys one-for-one.

So when a key is added, removed, or renamed — within this tracked repo:

1. Edit the taxonomy table and its dated amendment/changelog note.
2. Update the template's Part B key list to match — same keys, one-for-one.

That's the whole tracked-repository chore. There is no count to chase through
the READMEs or the evolution doc, because none of them state one — and if you're
tempted to add one, don't. The private regression corpus keys off the same
patterns, but its entries live outside this repo
(`verification-kit/regression-corpus-method.md` describes the method; the
entries stay out) and are reconciled in that private environment by whoever owns
it — not from here, and not something an agent working in this repo should reach
for.

Before finishing an edit anywhere in `verification-kit/`, grep the repo for a
count reintroduced into prose — spelled ("fifteen"), numeric ("15 patterns"),
key-range ("P1–P15"), category-range ("(1–15)") — and rephrase it collectively.
Two things look like counts but aren't, and stay: **dated history** ("the
fifteenth pattern, P15, minted July 2026") and **empirical run-data** ("eight
runs, seven valid"). Those are facts about events, not a live tally of the
taxonomy. Then confirm internal links still resolve, and report what you
verified — "checked" on its own isn't a result.

This lives here, and not only in the taxonomy's own amendment note, because
that note sits at the bottom of the file you're least likely to have open while
editing a README. Count drift is how these copies came apart before the counts
were removed — the rule was right and nobody was looking at it.

### The instruments are ported derivatives

The taxonomy, the audit template, and the corpus conventions are maintained in
the author's private instrument repository, with a published copy in their
claude.ai project, and ported here sanitized: the same keys, FAIL
tests, tie-breaks, and design notes, in this copy's structure and voice, with
origins labeled by category. Port a change as that semantic delta. Don't reword
what's already here to taste, and don't re-sanitize settled text, because
divergence between copies is the exact problem they exist to prevent. If this
copy and the source disagree on substance, say so and leave the text alone; the
fix goes back to the source. The no-count convention above applies to every
port: strip a bare count or key-range even when the source carries one, and
phrase it collectively instead.

### Sanitization

Keep the tracked repository free of confidential data. Before writing or
committing:

- No secrets, credentials, real cloud account IDs, internal hostnames, or
  connection/warehouse names.
- Trace origins are labeled by *category* ("product-comparison thread"), never
  by the real product, article, phrase, or entity.
- Live configuration text, version histories, and corpus entries stay out.
  Published config examples and copy sheets under `harness/` are sanitized,
  genericized derivatives, not mirrors of live configuration: a copy sheet is
  a parameterized snapshot of one installed version with a dated footer, not
  a lineage.
- Branch names, pull request titles and bodies, and merge messages follow the
  same rules, since merge commits keep branch names. If a branch name would
  reveal another setup, merge from the command line with a neutral message or
  rename the branch first. Keep notes about the other side in its handoff
  package, not the pull request title or body; a handoff posted as a pull
  request comment is that package, held to these same rules, under a neutral
  heading.
- Flag anything questionable rather than deciding. CI secret detection catches
  secrets, not disclosure judgment — a green pipeline isn't clearance.

Use ignored `_input/` for private source material and `_output/` for generated
drafts, reviews, handoffs, and exports. The tracked `archive/` holds only
sanitized historical notes. Archiving pending research does not mark it complete
or authorize its execution; preserve evidence links and status when moving it.

### Repositories and release flow

Staging, this private copy, is the editing home: its `main` holds every
shareable file and keeps full history (branches, pull requests, merge commits);
nothing on it is rewritten. The public repository receives only reviewed release
snapshots, by fast-forward. Two private sources feed staging and never receive
releases: a separate repository, whose history never enters staging or public,
and the author's private instrument repository, which holds the canonical
instruments; the author's claude.ai project holds a published copy of them.
Local `_input/` and `_output/` are ignored everywhere.

Staging holds only publishable material, because a private repository is one
visibility setting away from public. Leaving a file out of a release is a choice
about what to publish, not a hiding place.

- **Shareable work** happens on a staging branch and merges into `main`; an
  agent opens the pull request only when the author asks. Hand the work to the
  separate repository as a reviewed package: the diff since the last synced
  staging commit, a note per change, and that commit's SHA. The agent there
  adapts it with judgment and records `Sync-from: staging <sha>`; don't ask
  for a blind apply.
- **Work from either private source** arrives only as a sanitized extraction
  (packages from the instrument repository are unpacked in `_input/`): a
  staging pull request, gated (disclosure, secret, link) before the push.
  Adaptations made there never flow back. After a port from the instrument
  repository merges, send the author a return note to relay to it: the public
  release commit, refinements made while porting, divergences found, and
  decisions it tracks.

**Publishing.** The staging `public` branch mirrors public `main` and gets one
squashed snapshot commit per release: staging `main`'s tree minus the paths in
`.publish-exclude`. Review it as a pull request into `public`, then
fast-forward staging `public` and public `main` to it from the command line.
The merge button would create a different commit under the web identity. The
author makes the snapshot and pushes it from their own machine with commit
signing on. An agent here prepares a release on staging (gates, tree, pull
request description) and doesn't push the staging `public` branch, public
`main`, or a `publish/` release branch: on a release pull request it reports,
and any fix lands on staging `main` before a new snapshot. The
[sharing checklist](harness/sharing-and-release.md#publishing-a-release) holds
the commands. Run the gates on the snapshot before it is pushed anywhere, and
check commit metadata: every published commit's author and committer use the
GitHub noreply address, never an employer or personal mailbox. Set `user.email`
to it in every GitHub checkout. Never add or fetch the separate repository as a
remote here; its object format can't share commits with this one anyway.

Anything that cites these notes pins a public release commit, never a staging
commit: staging commits are private, and the two `main` branches have different
histories.

**Deploying to the author's own setups.** The author runs parts of these notes
from their own cloud sessions and machines; an agent here can't change those
setups. When a merged change touches something the author runs, such as a sample
section, a skill, or a setup script, end with a **To deploy** line saying what
to update where, or that nothing needs deploying.

### Naming

`harness/CLAUDE.example.md` keeps its name deliberately — it's a published
sample of a *user-level* global config (`~/.claude/CLAUDE.md`), a different scope
from this project-level file. Don't rename it for consistency with AGENTS.md;
they aren't the same thing.

The same split holds for `AGENTS.md`: this root file is *project* guidance for
agents working in this repo, while `harness/AGENTS.example.md` is a sanitized
sample of a *user-level* global Codex config (`~/.codex/AGENTS.md`) — the Codex
counterpart to `CLAUDE.example.md`, published alongside it. Same reasoning:
don't merge or rename across scopes.

`harness/cursor-user-defaults.example.mdc` is a sanitized sample of a
*user-level* Cursor rule installed under `~/.cursor/rules/`, not a project rule
under this repository's `.cursor/rules/`. Keep the `.mdc` extension and keep it
separate from `harness/cursor-notes.md`: the sample owns installable rule
content, while the notes own placement, maintenance, and enforcement mechanics.

`harness/claude-ai-profile-instructions.example.md` is different again: a
copy sheet for the account-level claude.ai profile field, not an installed
`CLAUDE.md` filename. Keep it separate from both the Claude Code sample and the
claude.ai operating notes; the copy sheet owns paste-ready instructions, while
the notes own surface mechanics and audit guidance.

`harness/claude-ai-project-instructions.example.md` is its project-level
counterpart: a copy sheet for one claude.ai project's instructions field,
which stacks on top of the profile. Keep the two copy sheets separate, because
they target different fields and scopes.

`harness/coco-user-defaults.example.md` is a sanitized sample of a *user-level*
Snowflake CoCo instruction file, installed at `~/.snowflake/cortex/AGENTS.md`.
It is named for its surface and role rather than its installed filename, because
`harness/AGENTS.example.md` is already the Codex user-level sample and this
repository's root `AGENTS.md` is project guidance — three different things that
would otherwise collide on one name. Keep it separate from
`harness/coco-notes.md`: the sample owns installable instruction content,
while the notes own discovery, precedence, caps, and enforcement mechanics. The
sample is deliberately narrower than the other global samples; the reason is
recorded in the harness README and the notes, so don't "complete" it by copying
the shared core or execution contract into it without first verifying which
assumed layer is absent.

`harness/cowork-instructions.example.md` is a copy sheet for two Cowork fields
— the global instructions field and a project or folder field — not an
installed filename. Keep it separate from `harness/cowork-notes.md`: the copy
sheet owns paste-ready text, while the notes own surface mechanics, loading
behavior, and first-use checks. In the new Claude experience its global
field is the same account-level field the claude.ai copy sheet targets, so
paste into that field's existing content rather than adding a second set; the
two copy sheets stay separate files.

### Not needed here

No build, no tests, no CI. Don't add tooling for its own sake — this repo is
markdown notes and should stay cheap to maintain. The one exception is small:
staging `main` carries local git hooks, run by
[prek](https://github.com/j178/prek) from `.pre-commit-config.yaml`, offline,
with stdlib Python scripts in `scripts/`, both left out of public releases by
`.publish-exclude`. They run the greps this file already asks for — relative
links and anchors resolve, no taxonomy count back in prose (Propagation) — and
a few cheap guards: added lines wrap at 80 columns, no machine paths or private
repository URLs, no private keys, no stray whitespace. Install with
`prek install`; run them all with `prek run --all-files`. A passing run doesn't
clear disclosure judgment or replace saying what you verified. Add a hook when
it would have caught a real slip, not for coverage.
