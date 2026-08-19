# Snowflake CoCo — durable operating principles

Companion to the installable
[`coco-user-defaults.example.md`](coco-user-defaults.example.md), and a sibling
of the [Claude Code](claude-code-notes.md), [Cursor](cursor-notes.md), and
[OpenAI surfaces](openai-surfaces-notes.md) notes. The sample owns a sanitized
user-level instruction file; this file owns placement, discovery, precedence,
and enforcement mechanics. It is **a reference to consult, not always-loaded
context** — the sample deliberately carries no provenance banner or dated
footer, because both would consume context in every session, and this companion
records that it is a sanitized snapshot checked on the date below.

These are one engineer's operating notes, not a framework, policy, or
best-practice claim. Managed environments can deploy settings that constrain or
override user configuration, so verify the active environment rather than
assuming a local file governs.

**Scope: standard CoCo CLI and CoCo Desktop.** Exact discovery can differ by
surface, version, and active instruction patterns. Treat every mechanism below
as a dated pointer and re-check it before depending on it.

## Instruction discovery is surface- and version-sensitive

Snowflake's detailed instruction-files documentation sits under the
**Desktop** section. It documents `~/.snowflake/cortex/AGENTS.md` at user scope,
and the Desktop Personalization editor reads and writes that same file.

On the tested CLI installation, fresh-session behavioral markers established
that the user `AGENTS.md`, the owner-maintained `CORTEX.md`, and the Claude
global file loaded. A collision probe inside a repository loaded both workspace
and user `AGENTS.md` paths. The documentation itself is internally tense here:
it says files are deduplicated by path, then says a workspace file causes a
same-named user file to be skipped. The observation matches the path rule, not
the same-name sentence. The Desktop collision remains unexercised.

`AGENTS.md` is therefore the best-evidenced shared user-scope target: documented
for Desktop and observed on the tested CLI. Patterns beyond `AGENTS.md`,
`CORTEX.md`, and the Claude global were not characterized well enough to
support general positive or negative claims about CLI discovery.

## Why the personal layer stays narrow

On the tested installation, the general epistemic core — retrieval over memory,
absence-is-not-proof, retraction discipline, the calibration footer — was
already present in fresh CoCo sessions because `~/.claude/CLAUDE.md` loaded. The
CLI reported both that path and a marker unique to it. This is a local
precondition, not a portable guarantee: the file must exist, remain discoverable
under active settings, and fit within the combined instruction cap. The sample
makes that dependency explicit so a reader without it can add only the missing
general gates.

Under that precondition, a personal CoCo file has no reason to restate the core.
Doing so would put a second, competing copy of the same rules into always-on
context, worded slightly differently, which can compete with the existing copy.
The personal layer earns its place only where a rule is Snowflake-shaped and
unowned by any other layer: effective context, tier isolation, result
completeness, validation stage, and the handoff.

The same reasoning kills a routing or delegation section. A file loaded by the
executing agent must not instruct it to hand Snowflake work to itself; host-side
routing belongs in the host's own configuration. Any host file CoCo also
discovers needs a callee audience guard or must omit that routing section.

## Layer map

| Need | Surface |
| --- | --- |
| Vendor or organization execution contract, connection discipline | Owner-maintained instruction file |
| General epistemic and coding defaults | Existing user-scope file, when present and discovered |
| Snowflake-specific personal gaps | `~/.snowflake/cortex/AGENTS.md` |
| Real identifiers, tier topology, canonical models, repo gates | Workspace instruction files |
| Repeatable multi-step procedure | Skill |
| Deterministic denial or lifecycle enforcement | Settings, permissions, hooks |
| Target context, read-only boundary, tool allowlist for one run | Per-call envelope |

Precedence, as documented: workspace files, then user-level files, then profile
files, with workspace content included first.

## Context caps

Combined instruction content has a documented cap, and files that would exceed
it are skipped — failure by omission rather than by error. Measure the real
loaded set instead of assuming headroom; consult the current instruction-files
documentation for the value.

The Desktop Custom instructions editor has a separate documented cap. It reads
and writes `~/.snowflake/cortex/AGENTS.md`, so in-app edits and direct file edits
target the same file. Consult the Personalization documentation for the current
limit.

## Rules request behavior; other layers enforce it

An instruction file is guidance. The enforcement surfaces are separate:

- Operational modes gate tool calls: a default confirm mode, a plan mode, and a
  bypass mode that disables normal confirmation prompts.
- SQL is classified by operation type. Both writes and session-context
  statements such as `USE ROLE` and `USE WAREHOUSE` can prompt, but the
  permission gate controls the call; it does not require the agent to report the
  resulting session-state change. That is why the prose reporting rule remains
  useful.
- Persistent permission grants live in
  `~/.snowflake/cortex/permissions.json` and are scoped as appropriate by
  project directory, tool type, or command pattern. Deleting the file resets
  everything; deleting the corresponding project entry resets permissions for
  that project. A cached grant from an earlier session is not evidence that the
  current operation was reviewed.
- Hooks can return an explicit permission decision before a tool runs. Anything
  that must hold every time belongs here rather than in prose.
- Environment variables tune the permission cache lifetime and can force
  prompting for SQL writes even in bypass mode.

For headless runs, the non-interactive mode disables plan mode and auto-rejects
interactive prompts. The installed CLI's `cortex exec --help` also exposes
`--allowed`, `--blocked`, and `--max-turns`; `--cloud` enables a server-side
sandbox. A blocked-tool list strengthens a behavioral probe: with file and
shell tools blocked, the model cannot retrieve markers from disk, so loaded
context is the only legitimate source and the controls can expose fabricated
presence. These flags were verified against the installed binary rather than
inferred from flags not listed on the rendered reference page.

## Verifying a change to the personal layer

Always-on instruction files fail quietly, so verify in a fresh session rather
than by reading the file back.

- **Marker probe.** Put a unique behavioral marker in the candidate file and a
  different marker in a known-loaded positive-control file. Start a fresh
  session with file and shell tools blocked and ask for the behavior each marker
  specifies. Include a token and a plausible path that exist nowhere as
  negative controls. A positive control establishes that discovery is working;
  negative controls catch fabricated presence; the behavioral marker is
  stronger than asking the model merely to recall a path.
- **Collision probe.** Run the same probe from inside a repository that has its
  own `AGENTS.md`, and from a directory that has none. Comparing the two is what
  distinguishes "not loaded" from "loaded but overridden".
- **Behavioral probes.** Fabrication against a plausible non-existent object;
  a fact established in one tier then queried in another; a question answerable
  from catalog metadata alone; a truncated result followed by a question about
  the total; an environment-sensitive question with no context supplied; a
  mutating request with no authorization; a refused command; and a request to
  route Snowflake work to CoCo, which should be done or declined rather than
  delegated to itself.

Remove probe files afterwards and confirm their removal. A sentinel left behind
in user scope is a silent instruction in every later session.

## Current documentation

- [Instruction files](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code-desktop/instruction-files)
- [Personalization](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code-desktop/personalization)
- [Security best practices](https://docs.snowflake.com/en/user-guide/cortex-code/security)
- [Agent tools](https://docs.snowflake.com/en/user-guide/cortex-code/tools)
- [CLI reference](https://docs.snowflake.com/en/user-guide/cortex-code/cli-reference)
- [Extensibility](https://docs.snowflake.com/en/user-guide/cortex-code/extensibility)
- [Bundled skills](https://docs.snowflake.com/en/user-guide/cortex-code/bundled-skills)

_Checked 2026-08-19 against the linked documentation and CoCo CLI 1.1.66. The
CLI observations above came from that release on one machine, with positive and
negative controls; they are not a claim about behavior after an update. The
Desktop same-name collision and other CLI instruction patterns remain
unexercised or insufficiently characterized._
