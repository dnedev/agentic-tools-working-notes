# harness

Personal config for agentic tools — things like `CLAUDE.md`, custom
instructions, and skills. It's illustrative, not prescriptive: tuned to
my register and defaults, so it's the wrong starting point to copy
wholesale (the same "wrong for you by design" spirit as the
[verification kit](../verification-kit/README.md)).

## Surfaces and artifacts

- **Claude Code** — a sanitized
  [`CLAUDE.md` user-global sample](CLAUDE.example.md) and
  [durable operating notes](claude-code-notes.md).
- **claude.ai** — a
  [profile-instructions copy sheet](claude-ai-profile-instructions.example.md)
  and [surface notes](claude-ai-notes.md).
- **Codex** — a sanitized
  [`AGENTS.md` user-global sample](AGENTS.example.md), with shared
  [OpenAI surface notes](openai-surfaces-notes.md).
- **ChatGPT** — a
  [Personalization copy sheet](chatgpt-personalization.example.md), with the
  same [OpenAI surface notes](openai-surfaces-notes.md).
- **Cursor** — an installable
  [user-rule sample](cursor-user-defaults.example.mdc) and
  [durable operating notes](cursor-notes.md).
- **Snowflake CoCo** — a partial
  [user-defaults sample](coco-user-defaults.example.md) and
  [durable operating notes](coco-notes.md).
- **Shared skills** — an [ADR stub](skills/adr-stub/SKILL.md), a
  [spec-driven-change loop](skills/spec-driven-change/SKILL.md), and a
  [dotfiles-discover](skills/dotfiles-discover/SKILL.md) /
  [dotfiles-sync](skills/dotfiles-sync/SKILL.md) pair. Their prose is
  runtime-neutral, so the same skill can be installed under each tool's
  supported skill root.

The roles are deliberately separate: examples own installable or copy-ready
instruction content; notes own surface mechanics and dated caveats; `skills/`
owns on-demand procedures. Fixed installed filenames such as `CLAUDE.md` and
`AGENTS.md` remain visible in their sample names where that aids recognition.

## Partial projection, where a surface already loads another tool's config

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

## Development-work completion

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

The placement is consistent with current OpenAI guidance to
[keep prompts lean and state each instruction once](https://developers.openai.com/api/docs/guides/latest-model),
Codex's documented [global-to-project instruction chain](https://learn.chatgpt.com/docs/agent-configuration/agents-md),
and Claude Code's distinction between prose guidance and
[deterministic hooks](https://code.claude.com/docs/en/hooks-guide). Those are
external convergence on the shape, not validation of this wording.
