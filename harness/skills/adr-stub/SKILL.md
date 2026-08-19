---
name: adr-stub
description: Emit a short architecture-decision record. Use when a change affects more than one file's public API, changes deployment shape, or selects between two or more viable stacks or libraries.
---

# ADR stub

> **Sanitized, illustrative sample.** One engineer's convention, extracted from
> a personal global config so the format lives in one place instead of being
> pasted into every layer. Not a framework, policy, or best-practice claim.
> Verify the frontmatter fields against your runtime's current skills
> documentation before installing, and note that repo-relative links below stop
> resolving once this directory is copied out.

The **trigger** for writing an ADR belongs in always-loaded config — a skill
can't fire on a decision the model never noticed it was making. This file owns
only the **format**, so there is one copy to change instead of one per layer.

## Format

```
## ADR: [Title]
Status: Proposed | Accepted | Deprecated | Superseded by <ADR>
Date: YYYY-MM-DD
Context: why needed
Decision: what was chosen
Alternatives: what was considered
Consequences: impact and trade-offs
```

Nothing here is invented, though one line is adapted rather than adopted.
`Title`, `Context`, `Decision`, `Status`, and `Consequences` are Nygard's five
original sections — including the `Status` treatment that carries deprecated
and superseded along with a pointer to the replacement. His template has no
date field: `Date` comes from MADR, whose 4.0.0 `adr-template.md` and
`adr-template-bare.md` carry an optional `date` while the minimal variants
don't. `Alternatives` is the adaptation — a one-line shortening of MADR's
`Considered Options`, not a field either source spells that way.

These fields earn their place because they are what turns a directory of ADRs
into a series you can read backwards: without a status you can't tell a live
decision from a dead one, and without a supersession link the dead one keeps
arguing with you.

MADR also offers `decision-makers` and `Decision Drivers`. Both are omitted
above — `decision-makers` adds little for solo or small-team work, and
`Decision Drivers` overlaps `Context` closely enough to invite writing the same
thing twice. Reinstate either if your situation actually differs.

Sources — Nygard's original article, and MADR's tagged 4.0.0 release:
<https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions>
<https://github.com/adr/madr/releases/tag/4.0.0>

## Notes

- **No narrative sections.** The fields above are one line each on purpose. An
  ADR that grows a *Detailed Design* heading stops getting written, and an ADR
  nobody writes documents nothing. Add a metadata field if you need one; don't
  add a chapter.
- **Alternatives** is the line that earns its keep. A decision with no rejected
  option recorded is indistinguishable from a default nobody examined.
- Write it at decision time, not at the end of the change. Reconstructed
  rationale is guesswork wearing a timestamp.
- Set `Status` when you write it and revisit it when it changes. A permanently
  `Proposed` record is one nobody trusted enough to adopt or delete.
- Where the stub *lands* is the project's call — a `docs/adr/` file, the merge
  request description, or a comment above the code. Decide once per project and
  say so there, not here.

## Example

```
## ADR: Single-writer queue for the export pipeline
Status: Accepted
Date: 2026-08-07
Context: Two schedulers can trigger the same export; duplicate rows reached the
  downstream table twice during staging runs.
Decision: One writer process fed by a queue; schedulers enqueue instead of
  writing directly.
Alternatives: Idempotent upserts — rejected, needs a natural key the source
  doesn't provide. Advisory lock — rejected, silent skips looked like success.
Consequences: A queue to operate and monitor. Export latency rises by about one
  poll interval. The duplicate-write class of bug becomes structurally
  impossible rather than merely unlikely.
```

Note what the `Alternatives` line does there: both rejected options were
plausible, and the reasons they lost are the part nobody remembers six months
later.

---

Sanitized for sharing — last revised 2026-08-07, adding `Status`, `Date`, and
the supersession reference after checking this format against the Nygard and
MADR conventions, and restating the length limit as a prohibition on narrative
sections rather than a line count. Installed and load-tested under both Claude
Code and Codex; not yet exercised on a substantive real ADR.
