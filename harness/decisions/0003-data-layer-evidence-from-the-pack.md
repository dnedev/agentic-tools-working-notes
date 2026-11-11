## ADR: The data layer takes its evidence rules from the measured pack

Status: Accepted; a run on the CoCo CLI itself (2026-10-21) found no
detectable difference

Date: 2026-10-21

Context: [Decision 0002](0002-data-work-instruction-layers.md) published a
redesigned data layer as the [CoCo sample](../coco-user-defaults.example.md).
Its Evidence section dropped two lines of the shorter evidence-labelling
pack, which stays as the delegation callee prompt: that memory,
analogy to a similar feature, or an earlier turn is not verification, and
that feature support, syntax, limits and defaults need a documentation search
before an answer. It also dropped the pack's judgement and design-advice
rules. My main worry about a data agent is overconfidence, and those are the
lines aimed at it.

Decision: The data layer's Evidence section now carries the pack's five
evidence bullets, words unchanged and rewrapped, followed by the redesign's
bullets on validation stage, result completeness and per-object summaries. A
new Judgement and design advice section carries the pack's two bullets on
keeping facts and advice apart and on working out what the original SQL or
policy does before changing it. The pack's "this session is read-only" line
stays out: the layer lets a task authorize a named write, and Tiers and writes
already says a write that wasn't run is untested. Every other section of the
redesign stays.

Alternatives:

- **Keep the redesign.** The numbers below don't show it worse overall, but it
  dropped exactly the anti-overconfidence lines, and it did worse on the one
  item they target.
- **Install the pack as the whole layer.** It's the tested text, but it would
  drop the write gate, the data-handling and credential rules, and the handoff,
  none of which the evaluation exercised, and it speaks to every session as a
  delegated run.
- **Rely on the model.** The strongest effect in the data, and still the first
  lever; it doesn't remove the need for evidence rules where the model is fixed
  by the host.

Evidence: the same small evaluation that 0002 describes, not on CoCo, with
its limits: small samples and same-family judges.

- **The item the dropped lines target.** On a core item about masking-policy
  documentation, the pack did better than the redesign, not significantly.
- **Everything else.** No pairwise difference between the redesign and the
  pack reached significance; on unsupported "verified" labels the pack did no
  better.
- **The model.** The only significant effect, as in 0002.

I read this as a regression in evidence behaviour, and the decision rests on
that reading and on caution, not on a measured gain.

A later run on the CoCo CLI itself (2026-10-21), with the stronger model the
CLI served by default: the items the weaker model failed in that evaluation
plus two core items, four runs per item and layer, then eight more per layer on
the one item that first differed. Each layer ran in its own isolated
configuration with only that layer at user scope. SQL ran read-only, and the
runs could fetch documentation pages but not search them. One blind judge per
item graded complete answers; a fresh judge re-graded the item rerun at
twelve, and agreed with the first on every answer both saw.

- **Passes.** 23 of 36 for each layer.
- **Unsupported "verified" labels.** 0 of 36 with this layer, 2 of 36 with the
  redesign (p=0.49, not significant).
- **The one item that differed.** At four runs each, the redesign passed 3 and
  this layer 0; at twelve each, 5 and 6. Most failures on it, in both layers,
  were the same units error (turning concurrent queries into a cluster count),
  which neither layer prevents.

No detectable difference, as with the stronger model in the earlier evaluation,
where it was near ceiling. The decision stays where it was: a reading plus
caution, still without a measured gain.

Consequences:

- The data layer is a new combination; under 0002, any rewording is a new
  variant. The CoCo run above is the check this bullet used to ask for, and it
  found no detectable difference. Items near ceiling for the stronger model
  limit what such a run can show; harder held-out items would show more.
- The layer grew by about a fifth. In the tested setup the loaded instruction
  files measured about 27,000 characters (about 29,600 with the execution
  contract) against CoCo's documented combined cap of about 100,000, which
  skips a file that would exceed it (2026-10-21).
- The execution contract this layer assumes didn't exist in the tested setup
  when the run was made, so the evaluated setup lacked it; it now has a
  [sample](../coco-execution-contract.example.md).
- The callee prompt doesn't change: it already is the pack.
