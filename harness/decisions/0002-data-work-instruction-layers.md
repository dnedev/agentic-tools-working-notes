## ADR: Data-work instructions as layers, one owner per kind of rule

Status: Accepted for the files. The data layer's evidence wording is
superseded by [decision 0003](0003-data-layer-evidence-from-the-pack.md).
Updated 2026-10-22: on 2026-10-21, marker probes on the tested CLI confirmed
that the data layer and the execution contract load, and the loaded set was
measured ([CoCo notes](../coco-notes.md)); the skill probe for the task-type
modules hasn't run. Updated 2026-10-22: the task-type modules and the callee
prompt aren't published here; these notes describe them.

Date: 2026-10-16

Context: The CoCo sample covered five data-specific rule areas. Data work
spans task types with different hazards: warehouse administration (grants,
policies, compute), infrastructure as code (plans, applies, state),
transformation code in SQL models and dataframe jobs (a run is a write;
backfills and full refreshes), data and semantic modelling (grain, fan-out,
metrics), building and evaluating data agents, validation and analysis, and
delegating work to another agent. Repository instructions I've seen leave gaps
an agent hits: no read-only default, nothing on reading infrastructure plans
or grant changes, and nothing keeping an agent away from credential files. All
of it in the always-on file would cost every session, and CoCo caps combined
instruction content, skipping a file that would exceed the cap. On the tested
CLI, CoCo also loaded the Claude global, so a data section there would load
twice. Separately, a small evaluation of a data agent, not on CoCo (Evidence,
below), found that almost all of its recurring errors went away with a
stronger model, not with higher effort or instructions.

Decision: Seven layers, each owning one kind of rule.

| Layer | Owns | Loaded |
| --- | --- | --- |
| L0 Enforcement | Anything that must hold every time | Always, deterministic: permissions, hooks, CI, server-side scope |
| L1 General core | Evidence, candor, calibration | Always: the user-level file, which CoCo also loaded on the tested CLI |
| L2 Execution contract | Connection discipline, vendor execution rules | Always, owner-maintained: [the sample](../coco-execution-contract.example.md) |
| L3 Data layer | Rules for every data turn: effective context, tiers and writes, evidence for warehouse results, data handling, the module pointer, the handoff | Always in CoCo: [the sample](../coco-user-defaults.example.md) |
| L4 Repository files | Real identifiers, commands, tiers, gates, local traps | Inside that repository |
| L5 Task-type modules | Rules for one task type, in any repository | On demand: task-type skills |
| L6 Per-call prompt | One delegated run where no instruction file loads | A callee prompt |

A new rule goes to the first layer that fits:
- **L0** if it must hold every time. A prose copy elsewhere is a backup, not
  the control.
- **L1** if it's true for any agent turn.
- **L4** if it names a real identifier, command, tier or gate.
- **L6** if it's true for one run.
- **L5** if it's true for one task type.
- **L3** if it's true for every data turn. It also has to name a data-specific
  failure, be observable in a transcript, and not be owned by a lower layer.

Reasons, dates, and results stay out of instruction text.

For data-work content, precedence runs repository, then module, then data
layer. Repository or module text may narrow the write and data-handling
defaults, or fill them in with real targets, but never relax them. A
repository's sandbox target counts as a named tier only where that repository
says so. The sample and two modules state rules that must always hold: the
read-only default, no infrastructure apply, no unrequested full refresh. Each
needs an L0 control; until one exists, the rule is requested, not enforced.

Alternatives:

- **One always-on file with everything.** Simple, but every session pays for
  every task type's rules, the loaded set nears the combined cap, and a
  modelling session carries infrastructure rules it never uses.
- **A data section in the Claude global.** One file for both tools, but CoCo
  would load it twice, and every non-data Claude Code session pays for it.
- **Repository files only.** Closest to the code, but the repository files
  I've seen aren't mine to change and say nothing about these hazards for
  agents.
  A personal layer can't rely on them.
- **More instructions as the fix for judgement errors.** The evidence below
  argues against it, within its limits.

Evidence: one small, read-only evaluation of a data agent, not on CoCo.
Scripts graded what they could, and blind judges from the same model family as
the arms graded the rest. Its conclusions, within those limits:

- **The model.** A stronger model removed almost all of the recurring
  judgement errors: design advice called documented or verified without
  evidence. It was the only significant effect.
- **Effort.** Higher effort on the weaker model didn't remove them.
- **An instruction pack.** A short evidence-labelling pack didn't either. With
  it, unsupported "verified" labels fell on two core items, not significantly;
  higher effort showed the same fall.
- **This sample's text as of 2026-10-16,** sent alone as the agent's
  instructions without the general file and execution contract it assumes,
  made no detectable difference on either model. The stronger model was
  already near ceiling on these items, so they couldn't show a gain there.
  Some of its runs finished only because the turn limit was raised.

Review: before install, the layer and the modules went through three reviews:
two by an Opus reviewer in a fresh context, and one by a different Claude
model. They changed:
- **Role switches.** A switch, or enabling additional roles, after a privilege
  error was only "reportable". It now needs the task to name the role;
  otherwise the agent reports the error and stops.
- **Module write gates.** Three modules relaxed the data layer's write gate, by
  qualifier or by instruction. Each now needs the task to ask for the action,
  against the tier the task names or a sandbox target the repository declares.
- **Delegation.** A delegation brief could authorize a write that the callee
  prompt forbids. A write can't be delegated through that prompt now.
- **Data handling.** The rule gained a test: a tag, a masking policy, or a
  column name marks a column personal or restricted.
- **Infrastructure.** The module contradicted itself on live API calls during
  a plan.
- **Smaller fixes:** a catalog query over many objects allowed again, the
  delegation module made reachable, and environment variables added to the
  credential locations.

Consequences:

- The sample doesn't claim correctness gains. Its rules target what a
  transcript shows directly, but the evaluation's read-only items didn't
  exercise the write, scope, or data-handling rules, and the evaluated agent
  couldn't load the modules. Where the model is fixed by the host, model
  choice stays with the host.
- Claude Code has no always-on data layer, and no read-only data default until
  a hook provides one. The modules load there without the defaults they add to.
- The modules are candidates until the skill probe in the
  [CoCo notes](../coco-notes.md) passes: the matching skill invoked before the
  first warehouse call, three of three runs for modules that carry safety
  rules. Bundled skills cover some of the same tasks, so a "which skill fired"
  case runs with them present. The probe checks loading, not benefit: under
  [decision 0001](0001-selective-skill-derivation.md), making any of them a
  default still needs a frozen evaluation against a baseline, a behavioral
  fixture, an owner, and a retirement condition.
- The callee prompt is the measured pack, rewrapped with its words unchanged.
  Any rewording is a new variant to measure. One reviewer's variant, which adds
  a rule against returning personal columns, is recorded here and not applied.
- The whole loaded set has to stay under the documented cap with room to
  spare. Measured on 2026-10-21: about 29,600 characters against a cap of
  about 100,000 ([decision 0003](0003-data-layer-evidence-from-the-pack.md)).
