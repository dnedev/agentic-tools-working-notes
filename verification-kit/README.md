# A personal verification kit for LLM-assisted work

**Working notes, not a framework.** I'm not a prompt engineer — I'm an
engineer who uses LLMs for research, analysis, and decisions, and who got
tired of plausible-but-ungrounded answers. Starting in March 2026 I
iterated on my personal assistant configuration and, along the way, built
a small set of instruments that turned out to be the durable part. This
package shares those. It's one person's method, graded by one person's
judgment. Take what's useful, discard the rest.

## What's here

- **[Failure-pattern taxonomy](failure-pattern-taxonomy.md).** Recurring ways
  LLM answers go wrong, each with a binary FAIL test. Every pattern came from a
  failure in my own chat transcripts rather than from an attempt to enumerate
  the space.
- **[Trace self-audit template](trace-self-audit-template.md).** A static,
  domain-neutral prompt that grades a supplied conversation against the
  taxonomy, requires a quote for each finding, forbids manufacturing them, and
  routes each finding to an account-level rule, a project-level prompt, or a
  watch item.
- **[Regression corpus method](regression-corpus-method.md).** How a confirmed
  failure becomes a private regression entry, including the run protocol and
  grading conventions. The entries stay private; this repository contains the
  method.
- **[Evolution and lessons](evolution-and-lessons.md).** A dated account of
  what changed, what failed, and which apparent improvements were later
  withdrawn or narrowed.

## How I use the regression loop

Grading is manual: start a fresh chat, provide the trigger, and judge the result
against the binary check. There is no automation or CI. A pass over the corpus
is a handful of fresh chats and a Markdown table; the
[corpus method](regression-corpus-method.md) owns the details.

The corpus has a handful of private entries. Its purpose is a no-regression
gate for this workflow, not a benchmark or a claim that the instructions caused
an outcome.

## What the runs showed

- The first baseline ran 2026-06-10: two entries across two current models,
  fresh chats, and 4/4 passes after the config fix the original failures
  motivated. The same run showed that a planned config rewrite was unnecessary,
  so I dropped it unshipped.
- A second batch ran 2026-07-26 against a newly released flagship model: eight
  entry-model runs, **seven valid passes, no failures**, including the first
  real validation of the P13 and P14 fixes and confirmation of three
  provisional entries.
- The remaining run was discarded because it reused the origin trace's phrasing
  and tested recall rather than the fix. That entry remains open.

The limits matter: there was no config-off control arm, so the green results are
a no-regression gate and not proof that the instructions caused the passes; one
entry was graded from a partial read of the response; and several patterns
still have no regression entry. The useful result is not the score. The loop
changed a decision and caught itself grading a result that did not count.

## Try it in ten minutes

1. Take a recent substantive LLM conversation — research, a comparison,
   a recommendation you acted on.
2. Paste the self-audit template at the end (or, better, into a fresh
   chat with the transcript attached — a model grades its own thread
   more gently than a clean session does).
3. Read the findings. If one stings, write the one-line rule that would
   have prevented it, and put it where the routing says it belongs.

## Caveats, upfront

- **n = 1.** Patterns and fixes come from my usage profile; yours will
  surface different failures.
- **Subjective grading.** Binary checks reduce but don't remove judgment;
  I am the only grader so far.
- **Drift.** Model-version-specific observations age in months. The
  taxonomy and the loop age well; any per-model claims should be
  re-verified before you rely on them.
- **Not included, by choice:** my actual configuration text (tuned to my
  register and defaults — wrong for you by design); the corpus *entries*
  themselves (distilled from personal transcripts; the method is in
  `regression-corpus-method.md`); and the one-time, venue-specific
  internal-socialization prompt for deciding where to post this (it names
  internal tooling, so it stays out).

Adapt freely. If you build your own corpus, I'd genuinely like to see
which patterns your usage surfaces that mine didn't.
