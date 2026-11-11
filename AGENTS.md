# AGENTS.md

One engineer's working notes on instructing coding agents and chat
assistants, and on checking the answers they give: markdown only, nothing to
build or run. Claude Code reads `./CLAUDE.md`, which points here — one file,
not two copies. Follows the [agents.md spec](https://agents.md/), so Codex,
Cursor, and others read it too.

Three kinds of agent read this file:

- **Someone pointed you at these notes so they can use them:** read
  **Using these notes** and **Applicable guidance**, and stop there.
- **You're helping someone adapt their own copy:** read those, then
  **Adapting your own copy**.
- **You're editing the author's own copy:** pass **Maintaining this copy**
  first.

## Using these notes

- Start at [README.md](README.md). Its **Start here** section routes by what
  the person wants, in four groups (see the setup, use it with an agent, how
  the author tests and grades, why it's this way); each row is a separate
  entry point, not a step.
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
  and `harness/decisions/`. They and `CHANGELOG.md` explain why
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

## Maintaining this copy

**Stop before your first edit, branch, commit, or push.** The rules for
maintaining the author's copy (the repositories behind it, how changes come
in and go out, how releases run) live in `MAINTAINING.md`. That file is kept
only in the author's private source repository and isn't published.

- **`MAINTAINING.md` is in your checkout:** read all of it now, then the rules
  under **Adapting your own copy**, which apply to this copy too. Where the
  two differ, `MAINTAINING.md` wins. If your context doesn't contain its
  sections "How the copies relate" and "Repositories and release flow", you
  haven't read it: read it before going on.
- **It isn't:** you're in a published copy or an adaptation. Don't
  reconstruct the author's release or sync flow from these notes; follow
  **Adapting your own copy** and use your own flow.

## Adapting your own copy

These are the rules the author's copy keeps when it changes. They're written
for that copy, so names like "the taxonomy" and "the template" point at the
files here; in your copy, keep them for the files you adapt. The docs are
versioned instruments, so the risk is **drift between them**, not bugs.

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
  same rules, since merge commits keep branch names.
- Flag anything questionable rather than deciding. CI secret detection catches
  secrets, not disclosure judgment — a green pipeline isn't clearance.

Use ignored `_input/` for private source material and `_output/` for generated
drafts, reviews, handoffs, and exports. An archive kept in a public copy holds
only sanitized historical notes. Archiving pending research does not mark it
complete or authorize its execution; preserve evidence links and status when
moving it.

### Commits and citations

Every published commit's author uses a GitHub noreply address, never a
personal mailbox. Anything that cites these notes pins a public release
commit, never a commit from a private copy.

### Not needed here

No build, no tests, no CI. Don't add tooling for its own sake — this repo is
markdown notes and should stay cheap to maintain. A maintainer's local checks
run the greps this file already asks for (links and anchors resolve, no
taxonomy count back in prose); a passing run doesn't clear disclosure
judgment or replace saying what you verified.
