# A personal verification kit for LLM-assisted work

**Working notes, not a framework.** I'm not a prompt engineer — I'm an
engineer who uses LLMs for research, analysis, and decisions, and who got
tired of plausible-but-ungrounded answers. Starting in March 2026 I
iterated on my personal assistant configuration and, along the way, built
a small set of instruments that turned out to be the durable part. This
package shares those. It's one person's method, graded by one person's
judgment. Take what's useful, discard the rest.

## What's in the package

**1. A failure-pattern taxonomy** (`failure-pattern-taxonomy.md`).
Recurring ways LLM answers go wrong, each with a binary FAIL
test. Not theoretical — every pattern was distilled from a real failure
in my own chat transcripts. Examples: presenting a generated URL or
figure as if it were retrieved; treating "I didn't find X" as "X doesn't
exist"; quietly joining two retrieved facts into a new claim that nothing
actually supports.

**2. A trace self-audit template** (`trace-self-audit-template.md`).
A static, domain-neutral prompt you paste at the end of any conversation
(any major LLM platform). It makes the conversation grade itself against
those patterns, with a quote-or-it-didn't-happen rule and explicit
guardrails against the auditor inventing findings. Output routes each
finding to where a fix belongs: your global custom instructions, a
project-level prompt, or a watch list.

**3. The regression corpus method** (`regression-corpus-method.md`).
The third instrument, and the one that isn't a document: how a confirmed
failure becomes a regression entry, the run protocol, and the
grading conventions — including the two that exist because I threw away
a result. No entries, just the shape.

**4. The backstory** (`evolution-and-lessons.md`). A one-page
timeline of how this evolved — what failed, what each failure taught,
and the lessons that transfer even if you adopt nothing else here.

## The loop (and what I actually ran)

The third piece is a discipline rather than a document — now written up
in `regression-corpus-method.md`. Grading is manual: fresh chat, paste trigger, judge
against the check. No automation, no CI. A run is four chats and a
markdown table.

Honest status: the corpus has a handful of entries. The first baseline
ran 2026-06-10 — two entries across two current models, fresh chats,
4/4 pass after the config fix the original failures motivated — and the
same run showed that a config rewrite I had planned was unnecessary, so
I dropped it unshipped. A second batch ran 2026-07-26 against a newly
released flagship model: eight runs, **seven valid passes, no
failures**, including the first real validation of the P13 and P14
fixes, and three provisional entries confirmed as standing.
The eighth run was thrown out — it had reused the origin trace's own
phrasing, so it tested recall rather than the fix, and that entry is
still open. Three caveats I'd rather state than bury: there was no
config-off control arm, so a green board is a no-regression gate and not
proof that my instructions caused the passes; one entry was graded on a
partial read of the response; and several patterns still have no entry
at all. That's the whole pitch in one anecdote: even a manual,
binary-graded loop changed a decision — and caught itself grading a
result that didn't count.

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
