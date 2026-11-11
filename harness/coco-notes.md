# Snowflake CoCo — durable operating principles

Companion to the installable
[`coco-user-defaults.example.md`](coco-user-defaults.example.md) and
[`coco-execution-contract.example.md`](coco-execution-contract.example.md), and
a sibling of the [Claude Code](claude-code-notes.md), [Cursor](cursor-notes.md),
and [OpenAI surfaces](openai-surfaces-notes.md) notes. The first sample owns a
sanitized user-level instruction file, the always-on layer for data work; the
second owns the execution contract that layer assumes; the task-type rules it
points to live in on-demand skills, which these notes don't publish. This file
owns placement,
discovery, precedence, and enforcement mechanics. It is **a reference to
consult, not always-loaded context** — the samples deliberately carry no
provenance banner or dated footer, because both would consume context in every
session, and this companion records that they are sanitized snapshots checked
on the date below.

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
that the user `AGENTS.md`, an execution-contract `CORTEX.md`, and the Claude
global file loaded. A collision probe inside a repository loaded both workspace
and user `AGENTS.md` paths. The documentation itself is internally tense here:
it says files are deduplicated by path, then says a workspace file causes a
same-named user file to be skipped. The observation matches the path rule, not
the same-name sentence. The Desktop collision remains unexercised.

`AGENTS.md` is therefore the best-evidenced shared user-scope target: documented
for Desktop and observed on the tested CLI. Patterns beyond `AGENTS.md`,
`CORTEX.md`, and the Claude global were not characterized well enough to
support general positive or negative claims about CLI discovery.

On CLI 1.2.18 (2026-10-21) the debug log (`COCO_LOG_DIR` with `COCO_DEBUG=1`)
named what it looks for at user scope: `AGENTS.md`, `CLAUDE.md`, `CORTEX.md`,
`RULES.md` and `.cursorrules`, in the home directory, `~/.claude/`, and the
Snowflake home and its `cortex/` folder. It read the Claude global and the
user `AGENTS.md`. An execution-contract file was missing in that probe; the
[execution-contract sample](coco-execution-contract.example.md) fills that
slot, and a marker probe confirmed an installed copy loads.

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
The Desktop instruction-files page also lists `~/.cursor/rules/` for user-level
`.mdc` files (checked 2026-10-01), so an installed Cursor user rule may load
there as well. That is an untested reading of the documentation; check what
actually loads before installing both. On CLI 1.2.18 a user-level Cursor rule
didn't load (debug log, 2026-10-21); the Desktop is unchecked. By the same
reading, a repository that keeps the same rules in both a `CLAUDE.md` and an
`AGENTS.md` loads them twice in the Desktop, which lists both names; whether it
expands a `CLAUDE.md` that imports `AGENTS.md` isn't documented (checked
2026-10-16, untested).
The personal layer earns its place only where a rule is data-work-shaped and
unowned by any other layer: effective context, tiers and writes, evidence
specific to warehouse results, data handling (credential locations included),
a one-line pointer to the task-type modules, and the handoff. Rules for one
task type live in on-demand skills, not in this file. Repository or module text
may narrow the layer's write and data-handling defaults, or fill them in with
real targets, but not relax them.

A data section doesn't also go into the Claude global: CoCo loads that file
too (observed on the tested CLI), so the section would load twice in CoCo and
cost every non-data Claude Code session. The price of that choice is that
Claude Code has no always-on data layer, and no read-only data default until a
hook provides one.

The same reasoning kills a routing or delegation section. A file loaded by the
executing agent must not instruct it to hand Snowflake work to itself; host-side
routing belongs in the host's own configuration. Any host file CoCo also
discovers needs a callee audience guard or must omit that routing section.

## Layer map

| Need | Surface |
| --- | --- |
| Vendor or organization execution contract, connection discipline | Execution-contract instruction file: `~/.snowflake/cortex/CORTEX.md`, as in the [sample](coco-execution-contract.example.md) |
| General epistemic and coding defaults | Existing user-scope file, when present and discovered |
| Data-work rules no other layer owns | `~/.snowflake/cortex/AGENTS.md` |
| Real identifiers, tier topology, canonical models, repo gates | Workspace instruction files |
| Repeatable multi-step procedure | Skill |
| Rules for one recurring data task type | Task-type skills in a user skill directory that both CoCo and Claude Code read |
| One delegated run where no instruction file loads | Per-call system prompt for the delegated run |
| Deterministic denial or lifecycle enforcement | Settings, permissions, hooks |
| Target context, read-only boundary, tool allowlist for one run | Per-call envelope |

Precedence, as documented: workspace files, then user-level files, then profile
files, with workspace content included first.

**Skills.** The CLI extensibility page lists `~/.claude/skills/` as a user
skill location and ranks project skills above user skills and bundled skills
last. Its two location tables disagree only on `~/.snowflake/cortex/skills/`,
user and global in one, global in the other (checked 2026-10-16). The modules
sit in `~/.claude/skills/`, so the CLI and Claude Code read one copy; the
Desktop skills page documents registered folders instead and doesn't mention
that directory, so Desktop loading is unchecked.
Whether CoCo lists user-skill descriptions to the model before a skill is
invoked isn't documented, so the sample names the modules in one line. Bundled
skills cover some of the same tasks; no names collide, and which skill fires on
an overlapping task is untested. Local skills don't reach CoCo in Snowsight.

## Context caps

Combined instruction content has a documented cap, and files that would exceed
it are skipped — failure by omission rather than by error. Measure the real
loaded set instead of assuming headroom; consult the current instruction-files
documentation for the value.

Measured on CLI 1.2.18 (2026-10-21): the Claude global, the data layer and the
execution contract came to about 29,600 characters against a documented cap of
about 100,000. In the same sessions the first turn already carried roughly
75,000 to 98,000 tokens of context before any work, most of it skill
descriptions, so the instruction files are a small part of the fixed cost.

The Desktop also reads rule files from `.claude/rules/` and `.cursor/rules/`
and concatenates everything it finds, so a repository that keeps the same rules
in two formats loads them twice there. `.github/instructions/` files with an
`applyTo` glob attach only when matching files are in context (checked
2026-10-16).

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
presence. These flags were verified against the installed binary. As of
2026-10-01 the reference page lists `--max-turns`, `--cloud`,
`--allowed-tools`, and `--disallowed-tools`; `--blocked` remains undocumented.

On CLI 1.2.18 (2026-10-21), checked run by run:

- **Headless allowlist.** A headless run refused every tool that `--allowed`
  didn't match, a read-only `SELECT` included, and didn't offer unmatched tools
  to the model. Pattern names differ from the internal tool names: `sql`
  matched the SQL tool and `WebFetch` the fetch tool; no name tried matched the
  web-search tool. With `sql` allowed, a write ran without a prompt, so the
  allowlist alone is not a read-only boundary.
- **Refusals look like results.** A refused call came back as an ordinary tool
  result beginning "Tool denied", not as an error, so a harness that counts
  tool calls has to count refusals separately.
- **Restricted session scopes.** `--with-restricted-session-scope` binds a
  scope object: an unqualified name resolves in the user's personal database,
  and the predefined `SNOWFLAKE$` scopes are for session policies rather than
  this flag. A user-managed scope built from the documented YAML of the
  predefined read-only scope refused a table create in a writable schema; the
  same create succeeded without it.
- **Hooks from Claude Code.** The CLI loaded the hooks in the Claude Code user
  settings (the counts matched event by event), so those hooks may fire in
  CoCo sessions too; loading was observed, firing wasn't probed.

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
- **Isolated homes for an A/B.** `SNOWFLAKE_HOME` relocates the whole
  configuration, connections included, so each arm can run in its own home
  holding only the layer under test, with no edit to the live one. Confirm with
  the marker probe that each arm loaded only its own layer, and pin the CLI
  version for the run: it updates itself on first run unless told not to.
- **Collision probe.** Run the same probe from inside a repository that has its
  own `AGENTS.md`, and from a directory that has none. Comparing the two is what
  distinguishes "not loaded" from "loaded but overridden".
- **Skill probe.** For each module, a task prompt in a fresh session; it
  passes if the trace shows the matching skill invoked before the first
  warehouse call, in three of three runs for modules that carry safety rules.
  Add a "which skill fired" case with the bundled skills present, and an
  ablation with the module pointer removed from the sample.
- **Behavioral probes.** Fabrication against a plausible non-existent object;
  a fact established in one tier then queried in another; a question answerable
  from catalog metadata alone; a truncated result followed by a question about
  the total; an environment-sensitive question with no context supplied; a
  mutating request with no authorization; a multi-part request, each part
  answered with its own evidence; a refused command; and a request to route
  Snowflake work to CoCo, which should be done or declined rather than
  delegated to itself. The host-side delegation module carries an audience
  guard for that reason: CoCo can see `~/.claude/skills/` too.

Remove probe files afterwards and confirm their removal. A sentinel left behind
in user scope is a silent instruction in every later session.

## Instructions and model choice

One small, read-only evaluation of a data agent, not on CoCo, bears on what the
sample can promise. Almost all of the agent's recurring judgement errors —
design advice called documented or verified without evidence — went away with a
stronger model, not with higher effort or an evidence-labelling instruction
pack. With the pack, unsupported "verified" labels fell, not significantly. A
re-test sent the redesign's text alone (this sample before decision 0003) as
the agent's instructions; it made no detectable difference on either model, the
stronger one being near ceiling already. So the sample doesn't claim
correctness gains. Its rules target what a transcript shows — context, writes,
labels, data handling, the handoff — but those read-only items didn't exercise
the write or data-handling rules. Model choice stays with the host's model
policy. A later run on the CoCo CLI itself (2026-10-21) compared the data layer
with the redesign before it, with the stronger model the CLI served by default,
and found no detectable difference. The layer design and its evidence are in
[decision 0002](decisions/0002-data-work-instruction-layers.md); the evidence
section went back to the pack's wording in
[decision 0003](decisions/0003-data-layer-evidence-from-the-pack.md).

## Current documentation

- [Instruction files](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code-desktop/instruction-files)
- [Personalization](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code-desktop/personalization)
- [Security best practices](https://docs.snowflake.com/en/user-guide/cortex-code/security)
- [Agent tools](https://docs.snowflake.com/en/user-guide/cortex-code/tools)
- [CLI reference](https://docs.snowflake.com/en/user-guide/cortex-code/cli-reference)
- [Extensibility](https://docs.snowflake.com/en/user-guide/cortex-code/extensibility)
- [Bundled skills](https://docs.snowflake.com/en/user-guide/cortex-code/bundled-skills)

_Checked 2026-08-19 against the linked documentation and CoCo CLI 1.1.66;
documentation rechecked 2026-10-01, and on 2026-10-16 for instruction files,
skills, and bundled skills. CLI 1.2.18 probed on 2026-10-21 for user-level
discovery, the loaded set, headless tool patterns and restricted session
scopes, and the data layer and execution contract through the marker probe;
the task-type skills haven't been through the skill probe yet. Each set of CLI
observations came from one release on one machine, with positive and negative
controls; they are not a claim about behavior after an update. The Desktop
same-name collision remains unexercised._
