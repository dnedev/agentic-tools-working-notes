# The Regression Corpus — Method

The third instrument in the kit, and the one that isn't a document.
The taxonomy names failures; the self-audit template finds them; the
corpus is what stops a fixed failure from quietly coming back.

**What's here:** the method — entry schema, run protocol, grading
conventions, and the failure modes of the method itself. **What's not:**
my actual entries. They're distilled from personal transcripts and would
be useless to you anyway; the shape is the transferable part.

Everything below is manual. No automation, no CI. A run is a handful of
fresh chats and a markdown table, and it has still changed decisions.

## Why bother

A conversation-level fix — a new rule in your global preferences, a
sharpened project instruction — has no test. You change the config,
things feel better, and six weeks later the same failure reappears in a
different domain and you don't notice because you're not looking.

The corpus is the standing external check. Two properties make it worth
the effort:

- **Real traces beat invented ones.** Every entry comes from a failure
  that actually happened, so the corpus tests the thing your config was
  written against, not a hypothetical.
- **A fresh session beats self-critique.** The model that made the error
  is a poor judge of it (Huang et al., ICLR 2024, arXiv:2310.01798;
  Kamoi et al., TACL 2024, arXiv:2406.01297). Grading in a clean session
  is the whole point — running the check at the tail of the thread that
  failed grades a defendant, not a case.

## Entry schema

- **ID** — a stable identifier you can cite in a version log.
- **Pattern** — the taxonomy key (primary; note secondaries if co-firing).
- **Source** — the originating trace, labeled by *category* rather than
  raw specifics ("product-comparison thread," not the actual product).
- **Trigger** — the minimal reproducible input. Category-level, not
  verbatim (see convention 1). Mark *derived* if minted after the fact.
- **Observed failure** — what the model did, with the quoted signal, plus
  **detected-by** (self / user / eval).
- **Principle** — the config clause the fix lives in.
- **Expected** — what correct behavior looks like.
- **Binary check** — one check. PASS = correct behavior; FAIL = the
  failure reproduces.
- **Routing** — [A] account-level / [B] project-specific / [C] watch.
- **Provenance** — observed under config vX / model + effort; fixed in vY,
  or "open."

One check per entry, binary, no Likert scale. If you can't write the
check as a single pass/fail sentence, the entry isn't ready.

## How to run

1. Open a **fresh chat** under the config version *and* the model + config
   under test. Record the model even when you can't control it
   ("default," plus whatever the UI shows).
2. **Mint a fresh instantiation** of the entry's trigger — never paste the
   origin trace's own specifics.
3. Compare the response against the binary check.
4. Record PASS/FAIL + version + model in the run log.
5. A previously-PASS entry going FAIL is a **regression**: fix it before
   shipping the version bump that caused it.

Re-run the corpus on **two** triggers: any config change, and any **model
change**. The second one matters more than it sounds — see convention 4
and the note on model upgrades at the end.

## Conventions

These accumulated one incident at a time. Each exists because skipping it
produced a result I later had to throw away.

1. **Fresh instantiation.** The reproducible unit is the trigger
   *category*, not its wording. A verbatim replay of the original tests
   whether the model remembers a resolved case, not whether the fix holds.
2. **Record at audit time.** Model, config, and detected-by go into the
   entry when you observe it, not when you get around to it. Reconstructed
   provenance is guesswork wearing a timestamp.
3. **Explicit destinations.** Any prompt that dispatches corpus work names
   the destination artifact and project. Deictic references ("the doc,"
   "that project") rebind unpredictably across chats.
4. **Detector validation.** An entry whose trigger has *never* produced a
   FAIL is unvalidated **as a detector** — it may be testing nothing at
   all. Label it, and at the next pass either re-mint the trigger harder
   (adversarial instantiation) or retire the entry. A corpus of checks
   that cannot fail is a comfort blanket, not a test suite.
5. **Replay check.** Before grading, confirm the run's instantiation
   actually differs from the origin trace's specifics. Same entity,
   phrase, product, or article means the run is VOID regardless of
   outcome. Check this *first* — it's cheap, and it invalidates
   everything downstream.
6. **Trigger provenance.** Entries minted check-only (no trigger field)
   get one written at confirmation, marked *derived* — reconstructed from
   the source trace's shape, not carried from it. Derived triggers are
   prime candidates for convention 4 review.
7. **Provenance signals aren't evidence.** When an entry grades a
   *self-retraction* — the model calling its own earlier output unsourced,
   fabricated, or hallucinated — grade it against the questioned claim
   itself, never against the signal that prompted the doubt. From inside a
   session an empty tool result, a cleared one, and a genuine no-op read
   identically, as do a citation that was never emitted and one dropped in
   rendering. An entry that lets those signals stand in for a check
   commits the very failure it is testing (taxonomy P2, provenance object),
   and its verdict is VOID like a replay. This is the audit template's
   render-ambiguity carve-out, applied to grading.
8. **Transport-tier provenance.** An entry minted from a *summary* of a
   trace — because the original couldn't be moved, pasted, or re-read —
   says so, and carries no raw spans. Quote what the summary quoted and
   nothing further: a span reconstructed from memory of a trace you can no
   longer open is generated, not retrieved (taxonomy P1). If you need the
   exact wording later, go back to the origin session and ask for it. Such
   an entry is still valid — it just sits a tier lower on provenance, and
   the run log should be able to say which entries those are.

Conventions 4 and 5 both came from the same run. An entry passed cleanly,
and the response did everything the check asked for — searched first,
refused the wrong framing, got the right answer. Then it turned out the
tester had reused the origin trace's own phrase, which the original thread
had already searched and resolved. The run tested recall of a solved case.
**PASS reversed to VOID, entry back to open.** It was the most convincing
result in the batch and it was worth nothing.

## Positive regressions

Not every entry stores a failure. A **positive** entry stores a behavior
you want to *keep*: PASS means the good behavior is still present. These
are the ones that catch a config edit quietly trading away something that
was working — the failure mode where every individual change looks like an
improvement.

Worth keeping a couple. They're also the entries most likely to fall foul
of convention 4, since a preserve-this check rarely fails.

## Run log

One row per run, so a future reader can tell what a green board rests on:

| Bump | Date | Model + config | Entries run | Pass | Fail | Regressions | Notes |
|------|------|----------------|-------------|------|------|-------------|-------|

Log **what you couldn't control** as well as what you could. "Default
settings, UI showed X" is a real entry; a blank is not. And if a model
column was inferred from execution order rather than observed, say so in
the row — an inferred provenance that reads as observed is exactly the
failure the taxonomy's P1 is about, committed against your own notes.

## Known limits of the method

- **n = 1 grader.** Binary checks reduce judgment; they don't remove it.
- **Coverage is uneven.** Patterns that produced a memorable failure get
  entries; the others don't. Mine still has patterns with no entry at all.
- **Some failures may not be prompt-fixable.** Long-context decay is the
  clearest candidate: the check is easy to write and the fix may not exist
  at the instruction layer.
- **A green board is a no-regression gate, not proof of lift.** Without a
  config-off control arm, a passing run can't separate your instruction
  layer from the model's own improvement. Running that arm on two entries
  is cheap and I keep not doing it — stated here so the omission is
  visible rather than implied.
- **Model upgrades don't retire your rules uniformly.** A new model can
  fix one failure class while regressing another, which means the honest
  response to a release is a per-pattern re-triage, not a wholesale "the
  model handles this now." Vendor release notes and system cards are
  useful evidence here, and they are the *vendor's* evidence — your corpus
  is how you check it against your own usage.

August 2026, sanitized for sharing.
