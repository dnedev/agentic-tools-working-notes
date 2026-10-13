# harness

Personal config for agentic tools — things like `CLAUDE.md`, custom
instructions, and skills. It's illustrative, not prescriptive: tuned to
my register and defaults, so it's the wrong starting point to copy
wholesale (the same "wrong for you by design" spirit as the
[verification kit](../verification-kit/README.md)).

For today's work you need none of the samples: the
[everyday guide](agentic-development-adoption.md) has a task brief, how to
review and merge the result, and what to do when a session goes sideways.
None of it requires installing agents or running the evaluations below.

## Samples by tool

Lift single rules into what you already have, then start a fresh session and
check what loaded. Some tools' notes say how, as of their dates; check the
tool's current documentation too.

| Tool | Sample, and where it goes | Notes |
| --- | --- | --- |
| Claude Code | A sanitized [`CLAUDE.md` user-global sample](CLAUDE.example.md), for `~/.claude/CLAUDE.md` | [Practical operating notes](claude-code-notes.md) |
| Codex | A sanitized [`AGENTS.md` user-global sample](AGENTS.example.md), for `~/.codex/AGENTS.md` or the Codex home your clients actually load | Shared [OpenAI surface notes](openai-surfaces-notes.md) |
| Cursor | An installable [user-rule sample](cursor-user-defaults.example.mdc), saved under `~/.cursor/rules/` | [Durable operating notes](cursor-notes.md) |
| claude.ai | A [profile-instructions copy sheet](claude-ai-profile-instructions.example.md) for the account profile field, and a [project-instructions copy sheet](claude-ai-project-instructions.example.md) for one project's field, which stacks on the profile | [Surface notes](claude-ai-notes.md) |
| Cowork | A [two-scope instruction copy sheet](cowork-instructions.example.md) for the global field (in the new Claude experience, the same account-level field as the claude.ai profile copy sheet) and a project or folder field | [Surface notes](cowork-notes.md), with explicit limits on parity with coding hosts |
| ChatGPT | A [Personalization copy sheet](chatgpt-personalization.example.md), one block per named Personalization field | The same [OpenAI surface notes](openai-surfaces-notes.md) |
| Snowflake CoCo | A partial [user-defaults sample](coco-user-defaults.example.md), for `~/.snowflake/cortex/AGENTS.md`; partial on purpose, as [explained below](#why-the-samples-are-shaped-this-way) | [Durable operating notes](coco-notes.md) |

**Shared skills** — an [ADR stub](skills/adr-stub/SKILL.md), a
[spec-driven-change loop](skills/spec-driven-change/SKILL.md), and a
[dotfiles-discover](skills/dotfiles-discover/SKILL.md) /
[dotfiles-sync](skills/dotfiles-sync/SKILL.md) pair. Their prose is
runtime-neutral, so the same skill can be installed under each tool's
supported skill root.

## Workflow, evidence, and evaluations

You don't need this section to use a sample.

- **Development workflow** — the [personal workflow](agentic-development-workflow.md)
  connects direct work, discovery, prototypes, and the spec-driven procedure.
  For longer or riskier work, consult only the relevant section. The
  [small working core](working-principles.md) explains the shared choices; the
  [evidence status](evidence-status.md) separates them from failed or untested
  treatments.
- **Evaluation instruments** — [protocol and index](evaluations/README.md),
  source intake, run template, the live fixtures and graders, and candidate
  role contracts (evaluation inputs, not installed agents). The
  [selective-derivation decision](decisions/0001-selective-skill-derivation.md)
  records how candidate procedures can earn promotion.
- **Sharing** — to share an adapted copy for colleague or public review, use
  the [sharing checklist](sharing-and-release.md).

The older research backlog, revision records, and retired fixtures are in the
[archive](../archive/README.md). They remain available without being an active
task queue or required reading for everyday work.

The artifact classes are deliberately separate: examples own installable or
copy-ready instruction content; notes own surface mechanics and dated caveats;
`skills/` owns on-demand procedures; and `evaluations/roles/` owns neutral
responsibility, evidence, permission, budget, and handoff contracts. Fixed
installed filenames such as `CLAUDE.md` and `AGENTS.md` remain visible in their
sample names where that aids recognition.

## Why the samples are shaped this way

Background for adapting a sample; you don't need it to use one.

### Partial projection, where a surface already loads another tool's config

The other global samples here are projections of one transferable core into
each tool's native format. The tested Snowflake CoCo installation changes that
trade-off: fresh sessions discovered user-scope instruction files from more
than one tool's home directory, and loaded the Claude Code global config —
confirmed by both the reported path and a behavioral marker unique to that
file.

That changes what the CoCo layer should contain. Another full projection would
add a second, differently-worded copy of rules already in context, competing
with the better copy for the same always-on budget. So
[`coco-user-defaults.example.md`](coco-user-defaults.example.md) is deliberately
narrow: only the Snowflake-shaped rules that no other layer owns — establishing
effective context, tier isolation, result completeness, validation stage, and the
handoff. That omission assumes both an equivalent general file and an
owner-maintained Snowflake execution contract exist, remain discoverable under
active settings, and fit within the instruction cap. A reader without either
layer needs to add only the missing general gates or execution boundaries
rather than copy this partial projection unchanged.

The discovery and precedence mechanics that make this work — including places
where the CLI observations needed qualification against the Desktop
documentation, and the resulting choice of file name — live in
[the CoCo notes](coco-notes.md), along with the probe method used to establish
them. Those observations came from one CLI release on one machine.

### Development-work completion

Two omissions in recent agent-assisted development work prompted the same
question from different directions: one repository-defined quality gate was
not run, while a separate change omitted an applicable teardown path. The
working hypothesis here is a **change-specific completion
contract** — the relevant behavior and lifecycle obligations, plus the evidence
that can show them complete — rather than permanent "always lint" and "always
add teardown" rules. This wording has not yet been regression-tested.

The pieces live at different layers on purpose:

| Layer | What it owns |
| --- | --- |
| User-global config | The trigger to discover repository-defined completion requirements, map the change's applicable lifecycle and operational consequences, and verify in proportion to risk. |
| Project or subtree instructions | Canonical commands, prerequisites, generated artifacts, supported environments, and non-obvious local risks. |
| Current task plan | The instantiated acceptance criteria: which gates matter for this diff and which lifecycle, recovery, or rollback paths the change can actually encounter. |
| Shared scripts, CI, and hooks | Executable feedback or enforcement for deterministic requirements. Presence or a green result is evidence, not proof that every relevant conditional check ran. |
| `spec-driven-change` skill | The longer procedure for work large or risky enough to justify it; small edits keep the compact global loop. |

The global samples therefore carry the decision procedure, not ecosystem
commands or a production-readiness checklist. Exact commands stay close to the
repository, and must-hold deterministic gates belong in executable surfaces.
That keeps a skipped linter discoverable without pretending a green pipeline
can reason about resource ownership, partial completion, recovery, or cleanup.

The placement is consistent with OpenAI's GPT-5.6 guidance to
[keep prompts lean and state each instruction once](https://developers.openai.com/api/docs/guides/latest-model#favor-leaner-prompts)
(checked 2026-10-01; the page now files it under previous models),
Codex's documented [global-to-project instruction chain](https://learn.chatgpt.com/docs/agent-configuration/agents-md),
and Claude Code's distinction between prose guidance and
[deterministic hooks](https://code.claude.com/docs/en/hooks-guide). Those are
external convergence on the shape, not validation of this wording.

### Maintaining the guidance

The working core's compact SDLC paragraph is projected into Codex, Claude Code,
and Cursor samples. The [archive](../archive/README.md) retains the revision's
intent and acceptance; the [evidence status](evidence-status.md) holds its
evidence decisions.
Review those projections together; retain host-specific scopes and safety rules.
Cowork's copy sheet adapts the same principles for artifact work. CoCo remains
partial because its general layer is owned elsewhere; the 2026-09-24 revision
did not copy the core into it. Chat-only samples do not gain a coding
delegation loop.

No shared include or generated distribution is assumed. The samples are
reviewable text, not live configuration, and none of them establishes
cross-host behavioral parity.
