# AGENTS.md

Instructions for any coding agent working in this repo. Claude Code reads
`./CLAUDE.md`, which points here — one file, not two copies. Follows the
[agents.md spec](https://agents.md/), so Codex, Cursor, and others read it too.

Working-notes repo: markdown only, nothing to build or run. The docs are
versioned instruments that other copies are graded against, so the risk here is
**drift between them**, not bugs. This file adds only what's specific to this
repo, on top of any user-global and workspace instructions — it doesn't restate
them.

## Preserve the epistemic register — the prime directive

The repo's whole value is honest, grounded, n=1 notes. When editing content:

- Keep the "one engineer's notes, take-what's-useful" framing. Don't upgrade it
  into a framework, a best-practice claim, or policy.
- Don't add confidence terms, counts, or evaluative claims the source doesn't
  earn — this repo literally catalogs that failure (see
  `verification-kit/failure-pattern-taxonomy.md`).
- Preserve the honest caveats (n=1, subjective grading, model drift). Match the
  existing voice; no drive-by rewrites of prose that already works.

## Propagation — the one thing to get right

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

## The instruments are canonical

The taxonomy and the audit template are maintained elsewhere and copied here.
Apply changes verbatim — don't reword, condense, or restructure to taste,
because divergence between copies is the exact problem they exist to prevent. If
something looks wrong, say so and leave the text alone. The one exception is the
no-count convention above: it is canonical for the instruments too, so strip a
bare count or key-range even when you'd otherwise mirror upstream text verbatim —
phrase it collectively instead.

## Sanitization

Keep the tracked repository free of confidential data. Before writing or
committing:

- No secrets, credentials, real cloud account IDs, internal hostnames, or
  connection/warehouse names.
- Trace origins are labeled by *category* ("product-comparison thread"), never
  by the real product, article, phrase, or entity.
- Live configuration text and corpus entries stay out. Published config
  examples and copy sheets under `harness/` are sanitized, genericized
  derivatives, not mirrors of live configuration.
- Flag anything questionable rather than deciding. CI secret detection catches
  secrets, not disclosure judgment — a green pipeline isn't clearance.

## Public release boundary

The public GitHub copy and private source use separate histories. The public
copy is a SHA-1 repository seeded from a sanitized tracked-file snapshot; the
private history is never merged or mirrored into it.

When preparing a release from the private source, export the reviewed tracked
files into the public checkout, omit `_input/` and the GitLab-only
`.gitlab-ci.yml`, inspect the public diff, and rerun the disclosure, secret, and
link gates before committing. When working in the public checkout, accept only
those reviewed snapshot diffs and never add or fetch the private source as a
remote.

## Naming

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

## Applicable guidance

This repository contains personal working notes, not organizational guidance.
It does not represent any employer or replace applicable policy or mandatory
requirements. If repository material conflicts with the rules that apply in
the active environment, follow those rules.

## Not needed here

No build, no tests, no linter. Don't add tooling or CI for its own sake — this
repo is a handful of markdown files and should stay cheap to maintain. The
private source uses **SHA-256 objects**; the public GitHub snapshot uses
**SHA-1** for hosting compatibility. If older Git tooling errors while working
with the private source, the object format is the likely cause, not corruption.
