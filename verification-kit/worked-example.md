# One failure, start to finish: the unlabeled join

The README's [loop](../README.md#why-it-looks-like-this) says how a failure
is meant to become a rule. This page follows one real case, pattern P13,
through each step, using only what these notes already record about it.
It's one engineer's n=1 case, graded by me; where a step wasn't recorded
publicly, the table says so rather than filling it in.

## The case at a glance

| Step | What happened | Where it's recorded |
| --- | --- | --- |
| Observe | In a product-comparison thread, a cross-brand "tier label" comparison was stated as fact: every input retrieved, the join between them invented. How the failure was first spotted isn't published here. | [Evolution notes](evolution-and-lessons.md), June 10 entry; [taxonomy](failure-pattern-taxonomy.md) Origin column |
| Classify | Minted as P13, unlabeled-join / synthesis-as-fact, with tie-breaks against P1 and P8. | [Taxonomy](failure-pattern-taxonomy.md) table and [distinctions](failure-pattern-taxonomy.md#distinctions-that-keep-grading-honest) |
| Decide | A new rule, in the same entry: a join inherits its weakest input's tier. Whether a watch item was considered first isn't published here. | [Evolution notes](evolution-and-lessons.md), June 10 entry |
| Route | The layer chosen in June isn't published here. Today the rule sits in the account-level profile copy sheet, and coding-tool versions sit in the user-level samples. | [Profile copy sheet](../harness/claude-ai-profile-instructions.example.md#instructions-for-claude); [`CLAUDE.md` sample](../harness/CLAUDE.example.md#evidence--sourcing); [Codex sample](../harness/AGENTS.example.md#evidence-gates) |
| Regression case | The July batch validated the P13 fix, so a private corpus entry covers it; its trigger and check stay private, and when it was minted isn't published here. | [Kit README](README.md#what-the-runs-showed); [corpus method](regression-corpus-method.md#entry-schema) |
| Re-check after drift | The July 26 batch on a newly released flagship model was the first real validation of the P13 fix. Whether a profile-off arm has re-run it isn't published here. | [Evolution notes](evolution-and-lessons.md), July 26 and September 25 entries; [kit README](README.md#what-the-runs-showed) |

## Observe and classify

The evolution notes' June 10 entry describes the failure: a cross-brand
"tier label" comparison stated as fact, with every input individually
retrieved and the join between them invented
([evolution notes](evolution-and-lessons.md)). The taxonomy's Origin column
labels the source "product-comparison thread (per-brand ordinal labels)"
([taxonomy](failure-pattern-taxonomy.md)).

The FAIL test is met when a load-bearing claim formed by joining retrieved
facts is "presented at its inputs' evidential level and never flagged as a
synthesis" ([taxonomy](failure-pattern-taxonomy.md)). Two tie-breaks keep it
apart from its neighbours: in P1 the leaf fact is generated, while in P13
the leaves are real and the operation is the fabrication; and P8 mis-tiers a
source, while P13 leaves the synthesis untiered. Both are in the taxonomy's
[distinctions](failure-pattern-taxonomy.md#distinctions-that-keep-grading-honest).
The audit template's keyed sweep carries a one-line version, and its
correction scan names "two facts joined without labelling the join" as one
way an answer ships wrong, both in the
[template](trace-self-audit-template.md#paste-ready-template-copy-everything-in-the-block).

## Decide and route

The rule, as the June 10 entry states it: a join inherits its weakest
input's evidential tier, so resolve it against a measured anchor, label it
as inference, or drop it if it's load-bearing and unresolvable
([evolution notes](evolution-and-lessons.md)). The entry's lesson: "a
synthesis is a claim of its own."

The entry doesn't say which layer the rule went into. The current sanitized
profile, the account-level layer, carries it: the join "inherits at most the
weakest input's tier", a proxy is itself a join, and either way the join
enters the Checked / Not-checked ledger. See the
[profile copy sheet](../harness/claude-ai-profile-instructions.example.md#instructions-for-claude).
The template notes that P13's test still works without such a ledger, read
as "never flagged as a synthesis"
([template](trace-self-audit-template.md)). The coding-tool samples carry a
version for code: verify a join against the source of truth or label it an
inference
([`CLAUDE.md` sample](../harness/CLAUDE.example.md#evidence--sourcing);
[Codex sample](../harness/AGENTS.example.md#evidence-gates)).

## Regression and drift

On July 26 the corpus re-ran on a newly released flagship model:
eight runs, seven valid passes, no failures, "the first real validation of
the P13 and P14 fixes" ([evolution notes](evolution-and-lessons.md);
[kit README](README.md#what-the-runs-showed)). The kit README's timeline
places that batch in the Opus 5 era. The eighth run was voided for replaying
an origin trace's phrase; which entry it was isn't published here.

Three later findings limit what that pass shows. The June and July runs had no
config-off control arm, so they are a no-regression gate, not proof the rule
caused the pass, and one entry in them was graded from a partial read of the
response; which one isn't published here ([kit
README](README.md#what-the-runs-showed)). And when the first profile-off arm
ran on September 25, on three entries and one model, every pass reproduced
without the profile. Under convention 10 a pass stays *stack-default* until a
profile-off arm reproduces it ([corpus
method](regression-corpus-method.md#conventions)); which entries that arm ran
isn't published here, so on the published record the P13 pass counts as
stack-default. Whether the P13 entry has ever produced a FAIL, which
convention 4 asks before trusting it as a detector, isn't published either
([corpus method](regression-corpus-method.md#conventions)).

## What this doesn't show

- **That the rule works.** One validated pass on one model, with no control
  arm for this entry on record, can't separate the rule from the model.
- **That the loop is complete for this case.** Detection, the routing
  decision, and the entry's mint date aren't published in these notes.
- **A typical case.** P13 was picked because its published record covers
  several steps of the loop, not because it's representative.
- **The entry itself.** Corpus entries come from personal transcripts and
  stay private ([corpus method](regression-corpus-method.md)).
- **Anything about your setup.** n=1, graded by me, tied to the models I
  used and dated; re-check before relying on any of it
  ([caveats](README.md#caveats-upfront)).
