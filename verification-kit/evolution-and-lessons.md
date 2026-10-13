# How It Evolved — Milestones and Lessons (Mar–Oct 2026)

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
constraint. *(Correction, 2026-10-02: that paper measures keyword-inclusion
instructions and reports three model-dependent degradation patterns and a
bias toward earlier instructions; a general ceiling at that size is not
what it shows. Where a rule sits, and how long a conversation runs, look
like the nearer risks at this scale.)* Auditing a sibling project the same week found ~40% of its
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

**September 3 — the sequence became the unit of inspection.** A multi-thread
product-comparison scan exposed a longer form of P14. Individual recommendation
changes could each look locally plausible while the lead alternated across the
thread, because the criteria weights were silently rebuilt from the user's
latest emphasis. That folded into P14 rather than minting a key: the mechanism
and fix were already there — a priority was silently re-ranked, so pin and echo
the ranking before the next recommendation and name what moved when the answer
changes. A separate old-thread specimen exposed the same issue for time: a turn
order establishes position, not wall-clock timing, so phrases such as "just
now" or "this afternoon" are generated specifics when no date or timing was
established. That folded into P1, with positional references as the repair.
The same pass found confidence footers staying flat or moving without explaining
what changed in the evidence. The account-level example now asks later footers
on the same question to state both the move and its cause, and makes explicit
that an unsupported hedge-to-assertion change in the answer body fails the same
test. The private corpus has provisional checks for these behaviors; they had
not been run when this note was written. *Lesson: a turn can look reasonable
while the sequence is unstable. Inspect what stayed pinned between turns —
priority, evidence, or time — before treating each answer as an isolated call.*

**September 3 — provenance applied to the rules themselves.** The same source
reconciliation found that a private taxonomy/history chain described the
August interlocutor clause as recast into a replacement grammar. The recorded
decision and installed text instead showed deletion on preference grounds. The
tracked evolution note had already preserved the deletion accurately; the
taxonomy now states the distinction explicitly and the private regression case
is a no-clause watch, not a test of a rule that does not exist. *Lesson: a rule's
lineage is a factual claim too. Verify it against the installed text or the
decision record before propagating a neat explanation across artifacts.*

**September 22–28 — the layer under the profile.** Reading the claude.ai
system context directly, in live sessions, turned up two lines that mattered
to the account-level profile and appeared only there, not in the published
copy of the system prompt: one telling the model to treat earlier answers as
done, and one applying user preferences by default only when they are phrased
as always-on. A Cowork task carried a different prompt again. The profile
answered both — earlier answers stay open to correction, and the defaults now
say they apply in all chats and tasks — but the larger change was to method:
whether a profile rule is needed is a per-model, per-surface question, so the
platform layer gets re-read at each release instead of being assumed from the
published text. *Lesson: you don't control the layer under your instructions,
and its published copy isn't necessarily the one that runs. Re-read it before
calling a rule necessary or redundant.*

**September 25 — a control arm took the credit.** The first profile-off
control arm ran three regression entries through an API harness on one model:
single turn, five repeats per arm, graded by log checks and a blinded model
grader with my own review still pending. 15 of 15 runs passed with the
profile and 15 of 15 without it. That doesn't show the rules are useless; it shows these
three checks, on this model, can't tell — and none of them has yet produced the
FAIL that would validate it as a detector. The corpus now calls such passes
*stack-default* until a control arm reproduces them. *Lesson: a PASS under
your full stack is not evidence that the stack caused it.*

**September — keep the text, not just the story.** The profile's version
history had been replacing its installed copy at each install, so the
outgoing version's verbatim text was overwritten each time; several versions
had to be reconstructed by reversing recorded edits. The history now keeps
every installed version's verbatim text beside its rationale. *Lesson: a
version history without the versions' text is a story about them. Keep the
text.*

**October 12 — the judges agreed with each other more than with me.** The
September checks had never failed on the model they ran on, so I built a private
suite of cases that can: drafted, mostly by a model, from the kinds of questions
I ask, plus new ones written to probe particular rules. I kept the 23 that drew
a FAIL in a screen without my profile, 19 from both judges and 4 from the larger
judge alone, and ran each five times per setup, on one or two models: 545 runs
across four setups, graded blind by two model judges, though the profile's
confidence footer gives the setup away. Where both judges agreed, 39 of 105 runs
failed with the platform prompt alone and 18 of 114 with my profile added;
stratified by case and model, the odds of a FAIL were 3.4 to 4.4 times higher
without it, however the split verdicts are counted, and the gap held with
either judge's verdicts alone and with any one case left out. Across all 545,
110 runs they split on or couldn't grade are still mine to review. The price:
answers about 75% longer and runs about 70% slower (medians).

Removing the first rule each case lists left the runs between the two, closer
to the profile, and older profile versions showed no detectable difference
from the current one, so the gain may sit in other rules or in the profile as
a whole. The checks grade whether a rule was followed, some in the profile's
own wording, on cases mostly drawn from what the profile was written from; the
two that weren't showed nothing either way.

Then I labelled 20 runs the judges had agreed on: five
passes and five fails, each with and without the profile. Weighted back to all
the agreed runs in those two setups, I agreed with them on about half of those I
could decide (roughly a third to two thirds): a fifth without the profile, four
fifths with it. Two models, one of them a judge model, re-read the checks with
the judges' reasons in view and found the check as written behind the judges'
call on 19 of the 20. Going by my own reasons, I was grading something else:
whether the answer was right, deep enough, searched when it should have, or
ended with the footer my profile asks for. By my labels the profile looked
better still, but that footer told me which setup I was reading every time, and
I wrote the profile. *Lesson: a check tests one rule; I judge the whole answer.
Measure both, and say which one a number is.*

## The lessons, distilled

1. **One layer per rule.** Duplication across layers is deletion.
2. **Every rule must beat the default.** If the model already does it,
   the rule is dilution.
3. **Failures → binary regression checks** beat clever rewrites. Grade
   in a fresh session, not at the tail of the thread that failed.
4. **Provided input is the floor, not the ceiling** — for sources,
   options, and first findings alike.
5. **Version, date, and eval-gate everything.** The version log is
   where the lessons turned out to live — and it needs each installed
   version's text, not just a description of it.

## More, learned since

6. **Sharpen before you add.** A new failure that shares an existing
   pattern's mechanism is a broadening, not a new key.
7. **A check that has never failed may be testing nothing.** Validate
   your detectors, or retire them. And a pass under your whole stack may
   be the model's until a control arm says otherwise.
8. **A rule that's known and not followed needs a different shape, not a
   louder voice.** Compile the check into an output you already have to
   produce, at the point the decision gets made. An appended "check
   yourself" step arrives after the verdict and gets answered with
   narration.
9. **Inspect the sequence, not just each turn.** A recommendation can look
   defensible one change at a time while the full thread oscillates. Keep the
   decision criteria visible so later movement has a stable reference.
10. **The layer under yours moves.** Re-read the platform's own prompt at each
    release before deciding a rule is needed or redundant.

October 2026, sanitized for sharing.
