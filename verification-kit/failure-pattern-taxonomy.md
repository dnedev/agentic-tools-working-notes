# Failure-Pattern Taxonomy — LLM Conversation Failures

Recurring failure patterns in LLM-assisted work, each with a
binary FAIL test. Distilled from real failures in the author's own chat
transcripts (March–August 2026); every pattern has at least one observed
instance — none are hypothetical. Origin labels below are genericized to
the domain of the source thread.

How to read the table: a pattern **fires** in a conversation if its FAIL
test is met. Tests are written to be binary on purpose — two readers
should grade the same trace the same way.

| Key | Pattern | FAIL test (failure is present if...) | Origin |
|-----|---------|--------------------------------------|--------|
| P1 | generated-specifics-as-retrieved | a specific (URL/name/figure/date/attribute) in the output didn't come from a tool result or provided context this session | long-form research thread |
| P2 | absence-as-evidence | a negative claim about an entity's *existence* — OR about a term/phrase's *meaning* (calling it meaningless, absurd, a non-sequitur, especially cross-language or in a specialized domain) — OR a claim about one's own prior retrieval/*provenance* (concluding "no retrieval happened / I fabricated it" from absent-looking tool output or a missing citation tag, without first verifying the questioned claim or checking the alleged failure was even possible) — rests on no targeted positive search for the literal/ordinary case first | trivia lookup (existence); foreign-language phrase thread (meaning); current-affairs thread (provenance) |
| P3 | confidence-theater | a confidence number or certainty term ("definitely," "clearly") appears without a named thing it was checked against | long-form research thread |
| P4 | distributional-without-distribution | percentile/decile/proportion/above-average language appears with no retrieved or computed distribution behind it | research thread ("top decile" claim, no distribution) |
| P5 | frame-switching-drops-constraints | a recommendation violates a constraint set earlier in the same thread; a reframe silently retired it | health-domain threads |
| P6 | anchoring-on-user-frame | a checkable user premise/category is carried into the answer unverified | health-domain threads |
| P7 | mechanism-as-evidence | a claim is graded as supported on a plausible mechanism alone, with no outcome evidence | health-domain thread |
| P8 | sourcing-tier | a load-bearing claim cites a low-tier/non-primary/industry-funded source without naming the tier in the same sentence | research thread (content-mill citation) |
| P9 | recompute-on-unverified-params | after a computed result is questioned, it's re-derived from the same unverified assumptions instead of surfacing the missing/contradictory parameter | health-domain thread (computed quantity challenged) |
| P10 | ask-not-delivered | the response offers/promises something it doesn't deliver, or substitutes a different deliverable for the one asked | long-form research thread |
| P11 | under-initiation | an evaluative/causal question is answered from a single provided source (or priors) with no corroborating search against an independent/primary source, when corroboration was feasible | news/policy thread (shared article, causal question) |
| P12 | premature-termination / own-finding anchoring | research was initiated but the answer rests on the first finding while a better/more-fitting variant was available in the model's OWN results, left unexamined | product-research thread (variant-bearing product line) |
| P13 | unlabeled-join / synthesis-as-fact | a load-bearing claim formed by joining retrieved facts (cross-scale or cross-brand mapping, attribute-by-association, transitive ranking) is presented at its inputs' evidential level and never flagged as a synthesis | product-comparison thread (per-brand ordinal labels) |
| P14 | reversal-without-tradeoff / latest-option anchoring | across turns, a recommendation is changed (upgraded or reversed, often toward the most-recently-introduced option) without re-running the prior pick's winning axis or naming what the new pick gives up; the swap is presented as pure upside | product-comparison thread (multi-turn; new option introduced late) |
| P15 | interlocutor-state adjudication | a load-bearing characterization of the user's internal state, traits, motives, or session context is asserted without the user's own words as source — including favourable or reassuring ones; unfalsifiable by construction and uncapped by any confidence rung | tech-adoption discussion; current-affairs thread |

## The under-investigation class (P11 + P12)

P11 and P12 are two sub-shapes of one root failure: **provided input
treated as the evidence/option ceiling rather than the floor.** A provided
source or first finding sets the *topic/option boundary*; the failure is
treating it as the *evidence boundary*. They stay separate because the fix
differs: P11 is a trigger gap (start corroborating when a single source
carries an evaluative/causal claim); P12 is a persistence/anchoring gap
(sweep the variant space before committing).

Tie-break when a trace is ambiguous: **no meaningful search initiated →
P11; search initiated but stopped short of an available better option →
P12.** A genuinely mixed trace fires both.

## Distinctions that keep grading honest

- **P3 vs P4:** P4 is the distributional subset; every other
  confidence-without-grounding case is P3.
- **P3 / calibration drift:** P3 also covers confidence that fails to
  track verification *across turns* — a hedge hardening into an assertion
  ("might be the cause" → "the cause"), or a confidence number that rises
  as grounding weakens. Watch for it in long sessions, where nothing new
  was checked between the hedge and the assertion.
- **P2 — existence, meaning, and provenance:** P2 covers both "X doesn't exist" and "this
  phrase is nonsense." Same mechanism — failure to find treated as
  evidence of absence — different object. The meaning-form is not a
  separate pattern, and its fix is P2's: search the literal or ordinary
  sense before the negative verdict. For an entity or phrase local to a
  non-English market, an English-only miss is not absence. And when the
  doubt turns inward — "I must have fabricated this" — an empty-looking
  tool result or a missing citation tag is not proof no retrieval
  happened: verify the questioned claim and check the alleged failure was
  even possible before retracting. The provenance-form is a P1
  fabrication charge assembled by a P2 move, aimed at your own prior work.
- **P11 vs P2:** P2 is a *negative-claim* failure ("didn't find X → X is
  false"). P11 is an *under-investigation* failure — the claim may be
  positive and well-argued; the fault is that no corroboration was sought
  for an evaluative/causal question.
- **P12 vs P6:** P6 anchors on the *user's* frame (external). P12 anchors
  on the model's *own* first finding (self-generated). Different object —
  don't collapse them.
- **P13 vs P1:** in P1 the leaf fact is generated; in P13 the leaves are
  real and the *operation* is the fabrication — individually retrieved
  inputs do not ground the join; the join is its own claim.
- **P13 vs P8:** P8 mis-tiers a source; P13 leaves the *synthesis*
  untiered — it evades tiering by never registering as a claim.
- **P14 vs P5:** P5 is a hard *constraint* silently retired by a reframe —
  the output violates a stated requirement. P14 is a recommendation
  *change* not held to the prior pick's winning axis: a *priority* gets
  de-ranked and the swap is mis-presented, without any hard constraint
  necessarily breaking. Tie-break: hard requirement broken → P5; priority
  silently re-ranked, or the swap shown as pure upside → P14.
- **P14 vs P12:** opposite ends of the same axis. P12 anchors on the
  *first* finding and the lead never moves; in P14 the lead *does* move —
  to the *latest* option.
- **P14 vs P6:** P6 anchors on the *user's* frame; P14 is the model's
  *own* pick drifting across turns.
- **P15 vs P6:** P6 anchors on a frame the user *did* assert; P15 asserts
  things about the user they *never said* — internal state, motives,
  traits, or why they're asking. P6 carries a stated premise unverified;
  P15 invents the premise.
- **P15, favourable reads count too:** the failure is the flat
  adjudication of the user's state, not its valence. A flattering guess
  ("you clearly already know this") fires P15 as readily as a critical
  one — just as unfalsifiable, just as unsourced. Keep the analysis on
  the subject; quote the user's words or ask.
- **Co-firing is normal.** One real failure can fire several patterns;
  tag the most upstream as primary.
- **Omissions aren't keyed.** Every pattern here is a *commission* — it
  needs a quotable span to fire. A failure of omission (what should have
  been said and wasn't) is invisible to a span-based sweep, so it's
  caught by the audit template's open-discovery pass, not by a key here.
  Minting an omission key would need a deliberately different,
  counterfactual test — don't add one casually.
- **Watch — not yet a key: asymmetric scrutiny.** Nothing here grades
  whether a comparison applied the *same* test to every candidate —
  scrutinizing one option harder than its rivals. Seen once so far; left
  as a watch item until a second independent instance earns it a key.
- **Watch — not yet a key: source-overlap.** Carried at *label grain
  only* — the name, not a test. Its definition lives in the grading notes
  for the trace that produced it and wasn't to hand when this revision was
  written, so there is deliberately no FAIL test here; sharpen it from
  those notes before any mint decision, never from this line. Seen once.
  The early read bears on the fix rather than on the key: the check fired
  unprompted in a later turn of the same thread, which points at
  model-default — weak evidence, since that turn was primed — so it may
  need no instruction-layer rule even if it later earns a key. Tie-break
  against P8, P11, and P13.

## Companion instruments

- **Trace self-audit template** — a static paste-in prompt that grades
  any conversation against these patterns (see
  `trace-self-audit-template.md`).
- **Regression corpus** — each confirmed failure becomes an entry:
  minimal reproducible trigger + one binary pass/fail check; re-run on
  every config or model change. The method, schema, and grading
  conventions are in `regression-corpus-method.md`; the entries
  themselves are distilled from personal transcripts and stay out.

**Amendment rule:** change a pattern *here* first, then propagate to the
template and any corpus keys. Letting each instrument carry its own list
is how taxonomies drift apart — this doc exists because mine did.

**Mint or fold?** The test is mechanism-distinctness, not instance
count. P2's provenance object *folded in* — same failure-to-find
mechanism, no new FAIL test and no new fix. P15 was *minted* — a
distinct test, a distinct fix, and clean tie-breaks against every
neighbour, after it recurred across two independent traces. A candidate
needs all of that before it earns a key; when in doubt, fold.

v1.5 (August 2026), sanitized for sharing.
Changes since v1.4: a source-overlap watch item added at label grain — a
candidate key, not a mint. No pattern was added, renamed, or retired, and
the table is unchanged.
Changes since v1.3: P2 extended to a third object — provenance (a false
self-retraction read off absent-looking tool output); P15 added
(interlocutor-state adjudication); coverage notes added for omissions and
asymmetric scrutiny.
