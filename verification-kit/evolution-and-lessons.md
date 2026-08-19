# How It Evolved — Milestones and Lessons (Mar–Aug 2026)

Companion to `README.md`. This is the curated story of how the
taxonomy and the audit template came to exist — compiled from the
project's version logs and chat history on 2026-06-12. Token counts are
approximate; minor version steps between named milestones are elided,
not lost. The configs themselves aren't included (see the README's
caveats); the lessons are the part that transfers.

**March — starting point.** Frustrated with default assistant register
and ungrounded answers; wrote a first set of global preferences and a
dedicated project for working on the instructions themselves.
*Lesson: your configuration is an artifact. Version it, date it, treat
it like code.*

**March–April — first artifacts, first pipeline.** A project-instructions
doc (~620 tokens) and a reusable chat-starter prompt (~340 tokens), plus
a default execution path: Identify → Plan → Audit → Draft → Critique →
Finalize. *Lesson: for anything you'll do twice, a boring repeatable
pipeline beats clever ad-hoc prompting.*

**April — the kitchen-sink phase.** Both artifacts balloon (starter
~990 tokens, instructions ~1,400) as every framework that sounded good
got inlined. *Lesson (learned the hard way next): adding rules feels
like progress; past a point it's dilution.*

**April 12 — research, then rebuild.** A deep-research pass produced 45
findings (binary pass/fail beats Likert scales; per-dimension checks
beat one "God evaluator"; write the evals before the artifact). Rebuild:
the starter cut ~990 → ~380 tokens by making each rule live in exactly
one layer; an instruction-budget ceiling (~150–200 distinct rules before
adherence degrades, arXiv:2507.11538) became a standing design
constraint. Auditing a sibling project the same week found ~40% of its
instructions duplicated the global layer. *Lessons: duplication across
layers is a deletion, not an addition — and token budget is attention
budget.*

**May — the four-failure rewrite (v5.0).** Seventeen documented failures
across two long threads (a long-form research thread and a trivia
lookup) clustered into four root causes: generation passed off as
retrieval, absence treated as evidence, confidence as performance, and
scope drift. Each got a different *type* of rule: a hard retrieval gate
(specifics must trace to a retrieval or named computation), an absence
cap (≤0.6 confidence on negative claims from secondary sources),
calibration grounding (name the source before the number), and
source-disagreement surfacing in the answer body. *Lesson: name the
failure before writing the rule. Different root causes need different
instruction types, not stronger wording.*

**Late May — cross-domain recalibration.** Self-audits on four unrelated
everyday-research threads found the *same* failures recurring across
domains: invented confidence numbers, fabricated composition/spec
details presented as retrieved, "~30% of people" with no distribution
behind it, an industry-funded source cited without its tier, arithmetic
run for four turns on one unasked parameter. The fix sharpened existing
blocks in place rather than appending new ones. *Lesson: cross-domain
recurrence is the test for what belongs at the account level — this is
where the audit template's A/B/C routing comes from. And sharpen in
place; appending is how configs bloat.*

**May — the style-layer audit.** The tone preset got the same treatment:
negation rules ("no X tone") out, positive format triggers in, and a
guard keeping tone and behavior in separate layers. *Lesson: never let
the tone layer carry behavior rules — you'll lose track of where
enforcement lives.*

**Early June — the under-investigation campaign.** Two traces exposed
one root failure in two shapes: a provided source treated as the
evidence boundary, and the model's own first finding treated as the
whole option set. This became patterns P11/P12 plus two rules: corroborate
evaluative/causal claims beyond the provided source, and sweep the
variant space before committing. Notably, the failure persisted even
at maximum reasoning effort. *Lesson: provided input is the floor, not
the ceiling — and that's a framing rule, not an effort knob.*

**June 10 — first regression baseline.** Two corpus entries × two
models, fresh chats: 4/4 pass — and the same baseline showed a planned
model-specific rewrite was unnecessary, so it was dropped unshipped.
*Lesson: eval-gate your config changes. The cheapest fix is the one the
baseline tells you not to ship.*

**June 10 — the join rule.** A cross-brand "tier label" comparison was
stated as fact: every input individually retrieved, the join between
them invented. New rule: a join inherits its weakest input's evidential
tier — resolve it against a measured anchor, label it as inference, or
drop it if it's load-bearing and unresolvable. This is pattern P13.
*Lesson: a synthesis is a claim of its own. Retrieved leaves don't
ground an invented branch.*

**Late June — the fourteenth pattern, and a broadened second.** An
audit scan across two unrelated everyday threads produced one new
pattern and one correction. The new one: across turns, a recommendation
migrated to the most-recently-introduced option, with the swap presented
as pure upside and the previous pick's winning axis never re-run. That's
P14 — the mirror image of P12, where the lead never moves at all. The
correction: P2 had been written for existence claims ("X doesn't
exist"), but the same mechanism was firing on *meaning* — a foreign-
language phrase declared nonsense without anyone searching its literal
sense. Same failure, different object, so it broadened P2 rather than
becoming P15. *Lesson: before minting a new pattern, check whether an
existing one has the same mechanism and a narrower object. Taxonomies
grow by sharpening at least as often as by adding.*

**July 26 — second baseline, on a new model.** A newly released
flagship model arrived, so the corpus re-ran: eight runs, seven valid
passes, no failures — the first real validation of the P13 and P14
fixes, and three provisional entries confirmed. The eighth was thrown
out on inspection: the run had reused the origin trace's own phrase, so
it tested whether the model remembered a solved case rather than whether
the fix held. It was the most convincing result in the batch and it was
worth nothing. Two conventions came out of it — check for replay before
grading, and label any entry whose trigger has never produced a FAIL as
unvalidated *as a detector*. *Lesson: the corpus needs a corpus. A check
that cannot fail is a comfort blanket.*

**July — reading a model release honestly.** The same release reported,
in the vendor's own system card, that the model had improved on exactly
the under-investigation failures P11/P12 were written for — while
ticking *up* slightly on factual hallucination, which is P1/P3
territory. So the honest response to the upgrade was neither "keep
everything" nor "the model handles this now": the anti-fabrication rules
earned their keep, and the investigation-forcing ones became
belt-and-suspenders, kept but marked. *Lesson: model upgrades don't
retire your rules uniformly. Re-triage per pattern, not per release —
and note that without a config-off control arm, a green board still
can't tell you which layer earned the pass.*

**July — independent corroboration, from an unrelated direction.** A
published field report on spec-driven development — different company,
different problem, no contact with this work — independently arrived at
three of the practices here. It recommends reviewing agent output in a
fresh session because a clean context catches what the context that
produced the work cannot; it extracts shared organization-wide
requirements into one referenced file so individual specs stay short;
and it writes explicit acceptance criteria per task because binary,
checkable goals give both humans and agents an unambiguous feedback
loop. Those are, respectively, the fresh-session grading rule, the
one-layer-per-rule principle, and the binary-check-per-entry
convention. *Lesson: for a method with n = 1 and a single grader,
independent overlap is an external signal, not a validation. Look for
it deliberately — when someone else solving a different problem lands
on a similar rule, that is consistent with the rule being about the
tools more than about you, but it does not prove it.*

**August 1 — the interlocutor-state cluster.** A scan across two unrelated
everyday threads — a tech-adoption discussion and a current-affairs thread
— surfaced two failures that shared a shape: asserting things about *me* I
had never said. One minted the fifteenth pattern, P15: a load-bearing
characterization of the user's state, motives, or context, stated without
their own words behind it — a flattering guess fires it as readily as a
critical one, and being unfalsifiable it dodges every confidence rung. The
other broadened P2 a second time, to a third object — *provenance*: the
model declared its own earlier, correctly-retrieved answer a fabrication
after reading an empty-looking tool result. A false self-retraction —
absence-as-evidence turned inward. Three global-preferences rules came out
of the cluster: retraction discipline (verify the questioned claim before
recanting; provenance signals aren't evidence), a ledger-placement
amendment (disclosing a gap doesn't license leaning on it), and an
interlocutor clause (don't adjudicate the user's internal state; quote or
ask). *Lesson: the failures that survive longest are the ones aimed inward
— at your own prior output, and at the person you're talking to. Neither
shows up in a span-based sweep of the subject matter, which is why the
audit template keeps an open-discovery pass and a provenance guard that the
keyed sweep can't replace.*

**August 8 — the same rules, recompiled.** No new pattern came out of this
one; what changed was the *shape* two existing rules were written in. The
residue of the August 1 cluster turned out not to be a missing rule but a
gap between knowing and doing: the Checked/Not-checked ledger was getting
written, and the retrieval it was supposed to force wasn't happening. The
rejected fix was a generic "now check yourself" step — models are trained
against scaffolding directives and answer them with narration, and a review
step arrives after the verdict has already formed anyway. What shipped
instead rewrote the ledger line's own definition so it carries the gate: an
item one query away doesn't belong under Not-checked, so run the query or
the claim it supports goes provisional. The audit instrument got the
mirror-image change — a triage step that sorts the gaps a trace disclosed
about itself and counts only one bucket as a finding, the retrievable item
nobody tried to retrieve. *Lesson: when a rule is known and not followed,
the promising direction is a required output whose shape enforces it, not
another rule. Watch what that displaces, though — a gate on the ledger line
can also be satisfied by writing a shorter ledger.*

**August 8 — and one rule taken back out.** The same revision deleted the
interlocutor clause installed a week earlier — don't adjudicate the user's
state, quote or ask — on the plainest grounds there are: I didn't want it. No
evidence was retracted, so the pattern stays keyed in the taxonomy, and its
standing check flipped to watching for the failure *without* the clause
installed. The rules around it were already carrying most of the load —
accuracy over agreement, no validation openers, displeasure isn't an argument —
and what left was the narrower guard against flattery-by-characterization.
*Lesson: a rule can be well-evidenced and still not worth keeping. "I don't
want this" is a sufficient reason to remove one, as long as you record that the
evidence didn't change — otherwise the removal reads later as a retraction, and
someone re-derives the rule from the same traces.*

## The lessons, distilled

1. **One layer per rule.** Duplication across layers is deletion.
2. **Every rule must beat the default.** If the model already does it,
   the rule is dilution.
3. **Failures → binary regression checks** beat clever rewrites. Grade
   in a fresh session, not at the tail of the thread that failed.
4. **Provided input is the floor, not the ceiling** — for sources,
   options, and first findings alike.
5. **Version, date, and eval-gate everything.** The version log is
   where the lessons turned out to live.

## More, learned since

6. **Sharpen before you add.** A new failure that shares an existing
   pattern's mechanism is a broadening, not a new key.
7. **A check that has never failed may be testing nothing.** Validate
   your detectors, or retire them.
8. **A rule that's known and not followed needs a different shape, not a
   louder voice.** Compile the check into an output you already have to
   produce, at the point the decision gets made. An appended "check
   yourself" step arrives after the verdict and gets answered with
   narration.

August 2026, sanitized for sharing.
