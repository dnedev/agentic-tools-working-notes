# Claude Code — practical operating notes

Reference, not always-loaded context. Primary documentation was first checked
2026-09-24 and rechecked through 2026-10-10; a line saying "checked <date>" was
rechecked that day against the page it cites. Each behavior line says whether it
was observed, documented, or inferred, with a date. Observations are one
engineer's: a workstation, the author's own cloud sessions, the cloud sessions
of the author's API-harness repository (2026-09-24 and 2026-09-25), and the
author's other setup (2026-10-01 to 2026-10-09, reported back). The probes are
the ones each section names; no other behavior probe was run. They are n=1 and
tied to the versions named. The [user-global sample](CLAUDE.example.md) is
illustrative; the [everyday guide](agentic-development-adoption.md) covers
adoption steps. Managed environments may differ. Resolve current models and
supported settings on the destination host rather than preserving a model alias
as a durable rule.

## Instruction placement

User instructions live at `~/.claude/CLAUDE.md`; project instructions can use
`CLAUDE.md` and imports such as `@AGENTS.md`. Current releases also document
direct `AGENTS.md` loading, conditional on version, settings, and other project
instruction files. This repository retains its thin import. Inspect `/context`
and `/memory` after changes instead of assuming a file loaded. Instructions
and auto memory are context, not enforced configuration.
[Instruction discovery](https://code.claude.com/docs/en/memory)

To check loading from a script or across folders, ask a fresh headless session
with no tools to quote a distinctive line from each file under test, plus a
planted token that should appear nowhere: `claude -p "..." --tools ""
--strict-mcp-config --no-session-persistence`. Without `--tools ""` the session
can read files on demand, and every case passes. Ask for quoted lines rather
than yes/no answers, and repeat a run. On 2026-09-25 on one workstation, such a
check showed that a `CLAUDE.md` in a parent folder stopped a repository's own
`AGENTS.md` from loading; a two-line `CLAUDE.md` containing `@AGENTS.md` fixed
it. The **Project instructions** setting (`instructionFiles`:
`claude-md-and-agents-md`), set at
user level, loads both files together where `AGENTS.md` support is available,
but also loads `AGENTS.md` files you may not mean as instructions, such as
copies kept in a dotfiles repository.

A second method, from the author's API-harness repository (observed
2026-09-24, Claude Code 2.1.281), uses a different negative control: in a
scratch copy rather than the real files, plant a unique token in each file
under test and one in a file that should not load, then ask the same
tool-less session for every token it can see; the command there ends with
`< /dev/null`. The planted token above catches an answer made up; this one
catches a file that loaded when it shouldn't. For a path-scoped rule under
`.claude/rules/`, allow only `Read` (`--tools Read --allowedTools Read`), have
the session read one file that the rule's `paths` match, and ask for tokens
"including system reminders attached to tool results". Content that arrives
this way was reported unevenly: one rule's token was listed in 3 of 4 runs
after reading a matching file, and in 0 of 2 after reading a file outside the
rule's `paths`. A yes/no question ("does your context contain ...") answered
no while the token was there. That harness's rule is to run each case at
least three times. The flags are in the CLI reference (checked 2026-10-10).
[CLI flags](https://code.claude.com/docs/en/cli-reference#cli-flags),
[Path-specific
rules](https://code.claude.com/docs/en/memory#path-specific-rules)

From the author's API-harness repository, canaries run 2026-09-24 on Claude
Code 2.1.281; documented parts checked 2026-10-10.

- **When `AGENTS.md` loads on its own** (documented; partly observed): with
  the default Project instructions setting, from v2.1.277, only when no
  `CLAUDE.md`, `.claude/CLAUDE.md`, or `CLAUDE.local.md` exists in the working
  directory or above it. A subdirectory's `AGENTS.md` loads only in that case,
  once Claude opens a file there with the Read tool, and only if that
  subdirectory has none of those three files of its own. Observed:
  `AGENTS.md` alone loaded, and a `CLAUDE.md` in the same folder without the
  import hid it, as a parent-folder `CLAUDE.md` did in the 2026-09-25 probe
  above. The `.claude/CLAUDE.md`, `CLAUDE.local.md`, and subdirectory cases
  weren't probed.
  [AGENTS.md](https://code.claude.com/docs/en/memory#agents-md)
- **Bare import only** (documented; observed): an `@AGENTS.md` import works
  only outside code spans and fenced code blocks. Observed: a bare import
  loaded both files, the same import in backticks loaded only `CLAUDE.md`,
  and an import inside the imported `AGENTS.md` loaded too. Fences weren't
  probed.
  [Import additional
  files](https://code.claude.com/docs/en/memory#import-additional-files)

**Import order** (documented, checked 2026-10-10): for a `CLAUDE.md` that
starts with `@AGENTS.md` and keeps Claude-specific instructions below it, the
docs say "Claude reads the imported file first, then the rest". The general
import section gives no order, only that imported files load "alongside the
CLAUDE.md that references them". This repository's sentinel names sections,
not a position, so it doesn't depend on either.
[Share one file with other coding
tools](https://code.claude.com/docs/en/memory#share-one-file-with-other-coding-tools)

**Edits during a session** (observed 2026-09-24 in the author's API-harness
repository, version not recorded; documented in part): a running session kept
the `CLAUDE.md` it started with. Several commits after the file had been
replaced, the session was still shown the original text. The docs say the
project-root `CLAUDE.md` is re-read from disk after `/compact` (checked
2026-10-10); that an ordinary edit isn't picked up is inferred from this one
observation. After changing an instruction file mid-session, read the file on
disk before relying on it, or start a fresh session; changed agent
definitions behaved the same way (see Bounded subagents). Nobody checked
whether an imported `AGENTS.md` is re-read after `/compact`, or what subagents
started from the old session load.
[Instruction discovery](https://code.claude.com/docs/en/memory), under
"Instructions seem lost after `/compact`"

Keep personal defaults, local repository commands, and conditional procedures
in separate scopes. Do not import this entire guide or the research backlog.
After an approved change, check for duplicated guidance and preserve the
owning configuration's update and rollback route.

## Bounded subagents

Custom subagents can live in `.claude/agents/` or `~/.claude/agents/` and have
separate context, tool selection, model, and permission fields. Omitted tools
inherit available tools. Parent permission modes can override a child's
`permissionMode`, and plugin agents ignore some fields, including that one.
Read the current precedence rules before claiming a reviewer is constrained.
Interactive sessions enable fork mode by default, and a fork inherits the whole
conversation; use a named custom subagent or a new session when a fresh packet
or independent reviewer matters.
[Subagent configuration](https://code.claude.com/docs/en/sub-agents)

What a subagent starts with (documented, checked 2026-10-10): a subagent that
isn't a fork gets its own prompt, the task message, and the `CLAUDE.md`
hierarchy, including an imported `AGENTS.md`, but not the main conversation
or auto memory. The built-in Explore and Plan agents skip `CLAUDE.md`, and a
custom agent with `omitClaudeMd` skips the user, project, and local files, so
put any rule they need in the task prompt. A fork also gets the main
session's system prompt, tools, and model, and the memory docs name it as the
one subagent that gets the main session's auto memory. The docs put fork mode
off with `-p` and in the Agent SDK. In one cloud session in the author's
API-harness repository on 2026-09-25 (Claude Code 2.1.282), it was off too
(observed): the Agent tool offered no `fork` type and kept its
`run_in_background` parameter, the two signs the docs name. Check which mode a
session is in before relying on either.
[What loads at
startup](https://code.claude.com/docs/en/sub-agents#what-loads-at-startup),
[Fork
mode](https://code.claude.com/docs/en/sub-agents#turn-fork-mode-on-or-off),
[Auto memory](https://code.claude.com/docs/en/memory#auto-memory)

Partial probe on one workstation, 2026-10-01, not an evaluation: a read-only
lookup role that keeps Bash behind an allowlist hook allowed a read and blocked
a file write and a shell redirect; two reviews then found allowlist bypasses,
since closed. A session that had loaded the agent definition before the hook
was added kept dispatching without it, while fresh sessions enforced it, so
start a fresh session before trusting a changed role. Identity and
cancellation were not probed; M1 in the
[measurement candidates](evaluations/measurement-candidates.md) is the planned
check.

A similar read-only hook in the author's own cloud sessions was reviewed on
2026-10-09 and 2026-10-10. The bypass classes found there are general git and
`find` behavior, rerun on 2026-10-10 with git 2.43.0 and GNU findutils 4.9.0
(observed):

- **Negated `git config` actions**: `--no-get` and `--no-list` set the value
  instead of reading it, and a value such as `core.fsmonitor` names a command
  that a later git read, such as `git status`, runs.
- **`find` options before the roots**: `-D` takes a value and `-O<n>` is an
  option, so either can hide a root from a check that parses the roots out.
- **`find -files0-from`**: the roots come from a file or standard input, so
  the command line never shows them.

The author's other setup found one more class in its own hook, reproduced
here on 2026-10-14 with git 2.43.0 (observed):

- **`git config` options after an operand**: git config stops parsing options
  at its first operand, so `git config core.fsmonitor x --list` takes `--list`
  as the value pattern and sets the key. The author's hook had accepted any
  `git config` with a read flag anywhere in it; it now accepts options only
  before the first operand.

Live check in a cloud session, 2026-10-09 (observed): a `PreToolUse` hook set
in a subagent's frontmatter blocked that subagent's `cd` and `touch` and
fired only while the subagent ran; the main session's own Bash wasn't
blocked. As on the workstation, a session that had loaded the agent before
the hook was added ran the same command unblocked. The docs say frontmatter
hooks run only while that subagent is active (checked 2026-10-10).
[Subagent
hooks](https://code.claude.com/docs/en/sub-agents#define-hooks-for-subagents)

Observed 2026-10-09: to see which model a subagent actually ran on, read the
`model` field in its transcript under
`~/.claude/projects/<project>/<session>/subagents/`. In one session that day,
`model: best` resolved to `claude-fable-5-1` and `model: sonnet` to
`claude-sonnet-5-5`; what an alias reaches depends on the account and the date,
so check the transcript rather than the definition.

Model and effort routing, from the author's other setup, each line marked
observed or documented, with the date. Documented parts checked 2026-10-09
against [Subagent configuration](https://code.claude.com/docs/en/sub-agents),
[Environment variables](https://code.claude.com/docs/en/env-vars), and
[Model configuration](https://code.claude.com/docs/en/model-config).

- **Plugin agents without `effort`** (observed 2026-10-09): a plugin reviewer
  that pins a model but sets no `effort` ran at the session's effort, not the
  level intended for it. The docs list `effort` as supported in plugin agents
  and say frontmatter `effort` overrides the session level, but don't say
  what an omitted field does. Where the host's agent call takes an effort,
  pass it on each call.
  [Plugin components](https://code.claude.com/docs/en/plugins/components)
- **`CLAUDE_CODE_EFFORT_LEVEL`** (observed 2026-10-09; documented): it
  overrode an agent's frontmatter `effort`. The docs say frontmatter effort
  overrides the session level but not this variable, which also takes
  precedence over `--effort` and `/effort`.
- **`CLAUDE_CODE_SUBAGENT_MODEL` with `CLAUDE_CODE_SUBAGENT_MODEL_FORCE`**
  (observed 2026-10-09; documented): together they overrode a full model ID
  pinned in an agent's frontmatter. Without the force setting, the documented
  order puts the per-call model and the definition's `model` ahead of the
  variable; the force setting needs v2.1.257 or later (docs, checked
  2026-10-09).
- **`CLAUDE_CODE_WORKFLOW_SUBAGENT_MODEL`** (changelog only, v2.1.296, read
  2026-10-14; not observed): it runs every workflow agent on one model while
  other subagents keep theirs. The environment-variable and workflow pages
  didn't list it that day, and the workflow page counts a model a stage names
  as the per-call model, so how the two rank is undocumented. The other setup
  reported that it overrides per-stage choices (relayed, not re-checked here).
  Keep it unset when routing per stage.
  [Changelog](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md),
  [Workflow cost](https://code.claude.com/docs/en/workflows#cost)
- **Family aliases** (observed 2026-10-09; partly documented): a family alias
  in an agent's frontmatter can resolve to the session's model, while full
  model IDs were served exactly; the session's model family wasn't recorded. The docs say a family alias resolves to the
  session's exact model when the session runs that family, and that aliases
  resolve to earlier versions on some third-party providers. Pin full IDs
  where the exact model matters.

Two settings change what a bounded role can do (documented, checked
2026-10-10). An agent's `memory` field turns on Read, Write, and Edit so it
can manage its memory files, unless auto memory is off. The docs don't say
whether `tools` or `disallowedTools` still limit those, so treat a role with
`memory` as able to write (inferred); one of the author's read-only role
definitions had carried `memory: user` unnoticed until a rewrite on
2026-10-01 (observed). And subagents can spawn their own subagents, three
layers deep by default since v2.1.219; `CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH`
set to `1` in the settings `env` turns nesting off for every subagent in the
session, which can enforce a packet's no-recursive-delegation non-goal
(inferred). In one headless check on 2026-10-01 with it set, a workflow's
stage agents still ran and a nested spawn had no Agent tool (observed), which
matches the documented behavior at the depth limit. To keep one role from
spawning while nesting stays on, leave `Agent` out of its `tools` or add it
to `disallowedTools`. Keep reference files an agent reads on demand outside
`agents/`: the user and project agent directories are scanned recursively for
definitions (a file without a `name` is skipped as documentation).
[Persistent memory](https://code.claude.com/docs/en/sub-agents#enable-persistent-memory),
[Nested subagents](https://code.claude.com/docs/en/sub-agents#let-subagents-spawn-their-own-subagents),
[Environment variables](https://code.claude.com/docs/en/env-vars)

From the author's other setup, relayed on 2026-10-14 and not re-checked here:

- **A fetching agent with a shell and private sources** (2026-10-10): a
  workflow agent fetched public pages while it also held a shell, search over
  private sources, and private notes, so a fetched page had a direct path from
  prompt injection to exfiltration. The fix there: fetch with a fixed-host
  script outside any agent, and read the saved pages with an agent that has
  no network, shell, or search.
- **A retrieval cap by page count** (2026-10-10): a docs fetch capped at a
  number of pages silently dropped the pages the task needed. Size a cap from
  a real run, and report what it skipped.

For when to delegate and what to hand over, use the
[workflow gate and packet](agentic-development-workflow.md#fan-out-gate); a
subagent's `OK` is a claim until its criterion, anchor, and check are shown.

## MCP servers

`claude mcp list` shows a status for each server it lists, such as connected or
needing authentication (WebSocket servers appear only in `claude mcp get` or
`/mcp`). A listed or connected server is still not a working route until one
known-answer read-only query succeeds. Permission allow rules for MCP tools
must name the server (`mcp__<server>__<tool>` or `mcp__<server>__*`); an
unanchored `mcp__*` allow glob is skipped, while a deny rule may use it. Allow
only the read tools a task needs, because a server such as an IDE bridge can
also expose build, terminal, and edit tools. See the workflow's
[discovery ladder and tool use](agentic-development-workflow.md#discovery-ladder-and-tool-use).
[MCP](https://code.claude.com/docs/en/mcp),
[Permission rules](https://code.claude.com/docs/en/permissions)

## Permissions and completion

Use permissions, sandboxing, and applicable hooks for enforceable action
boundaries. Their scope matters: a tool rule must match the actual route, and
a hook is not a universal security boundary. Prose cannot prove denial, and a
clean final tree cannot prove that no forbidden action occurred.
[Permission rules](https://code.claude.com/docs/en/permissions)

File rules (documented, checked 2026-10-10; first read 2026-09-24 in the
author's API-harness repository):

- Only `Edit(path)` and `Read(path)` rules are checked for files. A
  `Write(path)` rule is accepted, never consulted, and draws a warning at
  startup.
- `./path` and bare `path` are relative to the current directory; `/path` is
  anchored at the settings source, which for a rule in `.claude/settings.json`
  is the session's primary working directory; `//path` is absolute.
- Deny rules cover Claude's file tools, the Bash file commands Claude Code
  recognizes (such as `cat`, `sed`, `tee`), and redirections. They don't stop
  a Python or Node process that opens the file itself, or a command that
  reads files without naming them, such as `grep -r pattern .` run from the
  folder that holds the file. On its own a deny list guards against
  accidents rather than drawing a boundary; the docs point to the sandbox
  for that.
  [Read and Edit](https://code.claude.com/docs/en/permissions#read-and-edit)

Observed 2026-09-24 in the author's API-harness repository; version not
recorded: in auto mode, an agent's edit to `.claude/settings.json` was blocked
as self-modification. Propose settings changes as an exact diff for the person
to apply.

From the author's other setup, observed 2026-10-10 (relayed, not re-checked
here): an allow rule that runs scripts in a directory, together with an edit
allow on the same tree, let an agent write a script and run it with no
prompt. Keep runnable paths outside the trees an agent may edit, and check
settings for that overlap.

Observed 2026-10-09 and 2026-10-10 in the author's own cloud sessions, in
auto mode: each refusal named a category. An edit to a repository's hook
script was refused as Self-Modification; a delegated session's request for
push access to a further repository, as Permission Grant; and that session's
edits to instruction files, as Instruction Poisoning (see
[Separate sessions or in-session agents](#cloud-sessions)). A probe agent
whose first command searched the filesystem for the word `password` was
refused as Credential Exploration, and kept being refused for the rest of
that session, so it ran from a fresh one. Results varied between sessions:
another session attached a further repository the same day without refusal. The
refused steps were reported, not retried by another route, and done from a
session a person was directing.

Derive checks from the repository. A hook may automate a deterministic gate,
but do not add one until its trigger, bypasses, failure, and recovery are
understood. A passed test does not establish complete intent, secure behavior,
or operational recovery. Keep independent review and human decisions distinct.

A command hook that times out doesn't block: the tool call continues through
the normal permission flow unless the hook sets `onFailure: "block"` (v2.1.295
or later; documented, checked 2026-10-10). A guard hook that can stall needs
that field, or a deadline of its own that denies. A verify step that fails
when a guard's entry lacks the field turns a dropped line into a visible
failure (suggested by the author's other setup, 2026-10-14).
[Hooks](https://code.claude.com/docs/en/hooks)

A guard hook's decision can be dropped with no visible error (from the
author's other setup, observed 2026-10-01; documented, checked 2026-10-10): a
`PreToolUse` hook that returned `hookSpecificOutput` without `hookEventName`,
and with `reason` in place of `permissionDecisionReason`, had every deny and
ask ignored, with no error seen in that session. The docs require
`hookEventName` inside `hookSpecificOutput` and name `permissionDecision` and
`permissionDecisionReason` for this event. They also say output that fails
schema validation shows a non-blocking hook error, and list a field at the
wrong level among the causes of hook JSON that has no effect and shows no
error; they don't say which of these a missing `hookEventName` gets. Before
trusting a guard, have it deny a harmless probe in a live session.
[PreToolUse decision control](https://code.claude.com/docs/en/hooks#pretooluse-decision-control),
[Hook JSON has no effect](https://code.claude.com/docs/en/hooks-guide#hook-json-has-no-effect)

Once that hook enforced, matching substrings anywhere in a command blocked a
commit message that named a disk-format command and the cleanup of a
temporary folder, and a write guard asked on any path containing "secret",
notes included. The version in use on 2026-10-01 tries to parse each command
the way the shell would: it skips comments, quoted text, and heredoc bodies
that only feed a file, and checks where code runs, such as substitutions,
`sh -c` and `eval` payloads, and text piped or redirected into a shell. A
hand-rolled lexer tried first let through commands it misparsed, and one
review found regressions against the substring version; a second review found
gaps in the shell-like parser that replaced it. Parse failures in that
version answer ask, never allow (observed 2026-10-01).

Effort is not a spend cap. Record effective configuration for comparisons,
include approval and integration cost, and recheck after model/host drift.

`/effort` saves the level as the default for the active model in later
sessions (from the author's other setup, observed 2026-10-09; documented,
checked 2026-10-09); `max`, and a level set in a `-p` run, apply to that
session only. For one session, press `s` in the `/effort` slider or the
`/model` picker (v2.1.257 or later per the docs).
[Adjust effort level](https://code.claude.com/docs/en/model-config#adjust-effort-level)

A missing model or feature needs current diagnosis; do not assume the cause is
client age or recommend an update without checking the active environment.

## Cloud sessions

Notes from the author's own Claude Code cloud sessions. Each line says whether
it was observed there or documented, with the date.

- **Commit identity** (observed and tested 2026-10-09): at start (resume
  wasn't tested), after the environment's Setup script runs, the session
  rewrites `~/.gitconfig` and `/etc/gitconfig` with its own identity
  (`Claude <noreply@anthropic.com>`; also seen 2026-09-24 in the author's
  API-harness repository) and SSH commit signing, so a Setup script can't set
  the commit identity. `GIT_AUTHOR_NAME`, `GIT_AUTHOR_EMAIL`,
  `GIT_COMMITTER_NAME`, and `GIT_COMMITTER_EMAIL` in the environment's
  Environment variables override every git config file, and commits stay
  signed. Commits the agent wrote ended with a
  `Co-Authored-By: Claude <model> <noreply@anthropic.com>` trailer and a
  `Claude-Session:` link (observed 2026-09-24 and 2026-10-09); the `GIT_*`
  variables changed the author and committer, not these trailers.
- **Commit signatures** (tested 2026-10-13): with the author's noreply
  address as committer, the session's signed commits read Unverified on
  GitHub (`unknown_key` in the API). The same tree and message, rebuilt with
  the author as author and the session's own identity as committer, read
  Verified (`valid`), committed by the `claude` account. So set only
  `GIT_AUTHOR_NAME` and `GIT_AUTHOR_EMAIL` and leave the committer to the
  session: the work stays under the author's name, GitHub verifies it, and the
  committer tells a session's commit from one the author made. Without the
  variables, `author.name` and `author.email` in the checkout's git config set
  the author alone (git 2.43.0, tested 2026-10-13). Every signature observed
  from the author's sessions used one key, so it appears to be shared across
  Anthropic-hosted sessions (inferred, not confirmed): don't register it on
  your own account. Commits the author makes on github.com are signed by
  GitHub with GitHub as committer and read Verified (documented; observed on
  the author's merges, 2026-10-13), so the two kinds both read Verified and
  stay apart without a personal key. GitHub's docs say a commit whose signer
  isn't its author reads Partially verified when that author has vigilant mode
  on (GitHub's docs source, read 2026-10-13; not observed).
- **Attribution trailers** (documented, checked 2026-10-13): unless
  `attribution` or `attribution.commit` is set, Claude Code adds
  `Co-Authored-By: <name> <noreply@anthropic.com>`, naming the model in use
  when the commit is made (such as `Claude Sonnet 5`), or `Claude` alone when
  it can't confirm the version. In cloud and Remote Control sessions it also
  adds `Claude-Session:`, which `attribution.sessionUrl: false` turns off. The
  trailer reaches the model as a system reminder, and a `CLAUDE.md` or memory
  rule about it takes precedence unless managed settings set the line; that
  is how the author's trailer stays without a model name (observed
  2026-10-13). The docs also say a cloud session doesn't read your machine's
  `~/.claude/settings.json` or `.claude/settings.local.json`; in a
  one-repository session, commit the key to `.claude/settings.json`. Projects
  ask for different trailers when you contribute: the Linux kernel's current
  text wants `Assisted-by: LLM`, optionally followed by analysis tools, after
  a 2026 change (commit `816d9992d9ed`, in v7.3-rc1) that dropped the model
  because naming it "provides free advertising to proprietary software
  companies while adding little or no useful information"; Kubernetes doesn't
  allow AI co-authors or an `assisted-by` trailer. GitHub's docs describe
  `Co-authored-by`, and neither `Assisted-by` nor `Claude-Session:`.
  [Settings reference](https://code.claude.com/docs/en/settings-reference),
  [Settings in cloud sessions](https://code.claude.com/docs/en/settings#settings-in-cloud-sessions),
  [Context Claude Code adds](https://code.claude.com/docs/en/how-claude-code-works#context-claude-code-adds-on-its-own),
  [Kernel AI coding assistants](https://docs.kernel.org/process/coding-assistants.html),
  [Kubernetes AI guidance](https://github.com/kubernetes/community/blob/master/contributors/guide/pull-requests.md#ai-guidance),
  [Creating a commit with multiple authors](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors)
- **Trailers on applied commits** (observed 2026-09-24 in the author's
  API-harness repository; tested 2026-10-10 in a scratch repository, git
  2.43.0): `git am` and `git cherry-pick` keep the original message, so those
  commits lack the `Co-Authored-By` and `Claude-Session:` trailers the session
  adds to messages it writes. On an unpushed branch of your own,
  `git rebase <base> --exec 'git -c trailer.ifExists=addIfDifferent commit
  --amend --no-edit --trailer "Co-Authored-By: <name> <email>" --trailer
  "Claude-Session: <url>"'` adds them. It amends every commit after `<base>`,
  not only the applied ones. With git's default `trailer.ifExists`
  (`addIfDifferentNeighbor`), commits that already carried a
  `Claude-Session:` trailer got it a second time, and a commit ending with
  both trailers got both again. With `addIfDifferent`, nothing was
  duplicated. Don't rewrite commits already pushed to a shared branch.
  [git commit](https://git-scm.com/docs/git-commit),
  [git interpret-trailers](https://git-scm.com/docs/git-interpret-trailers)
- **When the Setup script runs** (documented, checked 2026-10-09): only when
  the environment's cache builds, on the first session, when the script or
  the allowed hosts change, and when the cache expires after roughly seven
  days. In Anthropic-hosted environments, repository hooks load only in
  single-repository sessions.
  [Environment caching](https://code.claude.com/docs/en/cloud-environments#environment-caching),
  [Settings in cloud sessions](https://code.claude.com/docs/en/settings#settings-in-cloud-sessions)
- **Environment variables and secrets** (documented, checked 2026-10-10): a
  session reads the environment's variables when it's created, and again
  whenever Claude Code starts in its VM after the VM is restored from idle
  or rebuilt. Until then a running session keeps the values it last read,
  so a changed value reaches it only then, or in a new session. Anyone who
  can use the environment can read its variables and Setup script. On Pro
  and Max plans the agent proxy can attach a stored network secret to
  requests without the session seeing it, but never to `api.anthropic.com`
  or the public package registries, so an Anthropic API key has to be a
  plain environment variable.
  [Cloud environments](https://code.claude.com/docs/en/cloud-environments),
  under "Set environment variables" and "Requests that never get the secret"
- **VM lifetime** (documented, checked 2026-10-10; one clause inferred):
  after a few minutes without activity a session's VM pauses with its files
  saved, and a paused VM can later be reclaimed; reopening the session then
  provisions a fresh VM. Work that lived only in the old VM, such as
  unpushed commits or files outside the repository, isn't on the fresh one
  (inferred, not tested), so anything that should outlive the session has
  to be pushed first. Auto memory is one such file (see below).
  [Time limits](https://code.claude.com/docs/en/cloud-environments#time-limits)
- **Installing uv** (documented, checked 2026-10-10; observed 2026-09-24 in the
  author's API-harness repository and 2026-10-10): `astral.sh` isn't on the
  default allowed domains, so uv's install script failed behind the proxy on
  2026-09-24; on 2026-10-10 it downloaded in a container whose network settings
  weren't recorded. PyPI (`pypi.org`, `files.pythonhosted.org`) is on them, and
  `python3 -m pip install --user uv==<version>` worked. The image set
  `UV_NATIVE_TLS`, which uv deprecates in favor of `UV_SYSTEM_CERTS` (from uv
  0.11.9, per its changelog, checked 2026-10-10), so each uv command, still at
  uv 0.13.0, printed a warning until `UV_SYSTEM_CERTS=true` was set. An older uv
  was already first on `PATH`, so compare `uv --version` with what the project
  needs before installing.
  [Cloud environments](https://code.claude.com/docs/en/cloud-environments),
  under "Default allowed domains"; uv's
  [changelog](https://github.com/astral-sh/uv/blob/main/changelogs/0.11.x.md)
- **Keeping user config current** (observed 2026-10-09): symlinks from
  `~/.claude` into an attached repository made content changes apply in the
  next session without re-pasting. A version stamp written by the
  Setup script, plus a `SessionStart` hook that compares it with the
  repository copy, correctly reported a stale pasted copy.
  [SessionStart](https://code.claude.com/docs/en/hooks#sessionstart)
- **Skills** (observed 2026-10-09): `~/.claude/skills` already holds the
  skills synced from claude.ai (under `synced/`) and a built-in skill, so link
  individual skills rather than the directory. The docs say skills turned on
  for the claude.ai account load in Cowork, cloud, and signed-in terminal
  sessions, with the full name `anthropic-skills:<name>`, and claude.ai has
  one account-wide switch per skill (checked 2026-10-11). So a skill written
  for chat and Cowork lands here too: a delegation skill drafted for those
  surfaces was listed among a cloud session's skills, next to the user
  file's own delegation rules (observed 2026-10-11). The next item covers
  keeping one out.
  [Skills synced from
  claude.ai](https://code.claude.com/docs/en/skills#how-synced-skills-behave)
- **Keeping a synced skill out** (documented, checked 2026-10-12; three
  clauses inferred, each marked): the docs' deny table lists several rule
  forms, and three bear on a synced skill. `Skill(anthropic-skills:<name>)`
  names the synced skill, but the docs don't say it also blocks a call by the
  short name. `Skill(<name>)` should catch a call by the short name (inferred
  from its exact-match syntax), and it blocks anything else named `<name>`, a
  nested skill included. When another command takes the short name, the synced
  skill answers only to its full name, so the rule would block that command
  instead (inferred). The parameter form `Skill(skill:<name>)` blocks a skill
  under any of its names, but which value names a synced skill isn't
  documented. `skillOverrides` set to `"off"` hides a skill from Claude's
  listing and the `/` menu and makes a call by its full name return an error.
  It's keyed by skill name, and which key matches a synced skill isn't
  documented; the `/skills` menu writes the setting itself, so it may show the
  key (not checked). Plugin skills are exempt from it, and the deny table says
  Claude Desktop can deliver a synced skill as a plugin. The listing matters
  because every listed skill adds to the context on every turn. A narrower
  description only steers when Claude picks the skill; it doesn't block a call
  (inferred). Setting `syncClaudeAiSkills` to `false` in user settings stops
  syncing and unloads every synced skill on a machine, which the docs describe
  for terminal sessions; it wasn't checked in a cloud session. The author's
  cloud Setup script now writes the full-name and short-name deny rules; that
  they load and block the call was not observed as of 2026-10-12. Whether a
  desktop Cowork session reads the same user settings, and would drop the
  skill too, wasn't checked either.
  [Skills](https://code.claude.com/docs/en/skills), under "Restrict Claude's
  skill access" and "Override skill visibility from settings";
  [Match by input
  parameter](https://code.claude.com/docs/en/permissions#match-by-input-parameter)
- **User-level files** (observed 2026-10-09; partly inferred): a `CLAUDE.md`
  linked into `~/.claude` by the Setup script loaded as user instructions.
  Agents and skills linked the same way were listed; that they came through
  the links is inferred, because the session started in a folder with no
  project `.claude/`. That is a different case from the documented one,
  where your user `~/.claude` isn't carried over from your machine. In a
  session without the linked repository attached, the links dangled,
  nothing errored at startup, and no user instructions loaded. Desktop
  Cowork documents skipping a symlinked `~/.claude/CLAUDE.md`, so this
  approach doesn't carry over there; see the
  [Cowork notes](cowork-notes.md#deliberate-differences-from-a-coding-host).
  [What carries over](https://code.claude.com/docs/en/cloud-environments#what-carries-over-from-your-setup)
- **Auto memory** (documented, checked 2026-10-10; observed 2026-09-24 in the
  author's API-harness repository): auto memory is saved under
  `~/.claude/projects/<project>/memory/` on the machine running Claude Code,
  and the docs say these files are not shared across machines or cloud
  environments. One cloud session's container had no memory directory. A
  memory saved in a cloud session goes when its VM does (inference from the
  docs, not tested across sessions). Keep what a later session needs in the
  repository, committed and pushed.
  [Auto memory](https://code.claude.com/docs/en/memory#storage-location)
- **Plugins** (each sentence marked): a cloud session doesn't install the
  plugins a repository turns on under `enabledPlugins`, including ones from
  marketplaces it lists under `extraKnownMarketplaces` (documented, checked
  2026-10-10). A plugin installed during a session, at project or user scope,
  loaded in a fresh headless session in that container (observed 2026-09-24); an
  install made that way lives in that container's `~/.claude` and goes with it
  (inferred). The official marketplace's plugins weren't among those offered on
  claude.ai that day (observed 2026-09-24), so a Setup script added the
  marketplace and ran `claude plugin install <name>@<marketplace> --scope user`;
  later sessions listed them installed and enabled, and they loaded (observed
  2026-09-25 to 2026-10-10, Claude Code 2.1.282 to 2.1.296). Plugins enabled for
  the account on claude.ai loaded too, as `<name>@synced` (observed 2026-10-09
  and 2026-10-10); the plugin docs name Cowork and terminal sessions as where
  synced plugins load and don't mention cloud sessions (checked 2026-10-10). A
  change to the Setup script's list applies only once the script runs again
  (inferred from the caching above; see When the Setup script runs).
  [Cloud environments](https://code.claude.com/docs/en/cloud-environments),
  under "What carries over from your setup";
  [Plugins synced from
  claude.ai](https://code.claude.com/docs/en/plugins/loading#synced-plugins)
- **Separate sessions or in-session agents** (observed 2026-10-10; a lean,
  not a rule): in-session agents and workflows share the checkout and report
  back when they finish, while a coordinator has to poll a session it started
  to learn how it went. A separate session earned its cost when the work
  needed another environment's secrets or network policy, the session's own
  setup under test, a long unattended run, or a repository hook, since those
  load only in single-repository sessions. In a session started and directed
  by another, auto mode's checks refused both push access to a further
  repository and edits to instruction files that the coordinator's messages
  asked for, so steps like those belong in a session a person is directing.
  In-session agents also share the checkout's current branch. When one
  writer held a branch (observed 2026-10-10; a dispatch practice, not a
  host mechanic), the brief named it, and readers read other branches with
  `git show <branch>:<path>` rather than switching, which would have moved
  the branch under the writer.
- **Fetch refspec** (observed 2026-10-09 and 2026-10-10; cause not
  established): some clones in these sessions lacked a full fetch refspec.
  A clone of an empty repository had none, so `origin/main` was an invalid
  reference. Another clone's `remote.origin.fetch` named only `main`
  (`+refs/heads/main:refs/remotes/origin/main`), so a plain fetch didn't
  track other branches, though no fetch was seen to fail because of it.
  Setting `git config remote.origin.fetch '+refs/heads/*:refs/remotes/origin/*'`
  and fetching again, or fetching one branch as
  `+refs/heads/<branch>:refs/remotes/origin/<branch>`, worked.
- **GitHub through the proxy** (observed 2026-10-09; documented, checked
  2026-10-10): `git push origin --delete` returned HTTP 403, while ordinary
  pushes and local branch deletes worked; `gh issue`, `gh pr`, and `gh label`
  failed with a GraphQL 403, while `gh api` REST calls worked. The docs list
  both: the proxy rejects branch deletions and pushes of anything other than
  a branch, and every GraphQL request. Creating a ruleset was refused as a
  write the proxy doesn't permit, and reading classic branch protection
  returned 403 ("Resource not accessible by integration"), while rulesets
  could be listed. The session's own proxy notes say to report a 403 rather
  than retry it. Merged branches were deleted outside the session, in GitHub's
  web UI; the repository setting that deletes head branches automatically also
  fired for a pull request merged from the command line. A child session goes
  through the same proxy, so it presumably can't delete its branches either
  (inferred, not tested).
  [GitHub proxy](https://code.claude.com/docs/en/cloud-environments#github-proxy)

## Shell and terminal

From the author's other setup, each line marked observed or documented, with
the date.

- **`!` input while the agent is busy** (observed 2026-10-02): input typed
  with a leading `!` while the agent was working was queued as plain chat
  text, not run as a shell command. The current docs say a `!` command typed
  while Claude works is queued, held until the turn ends, and then run as a
  shell command (checked 2026-10-09), which differs from what was seen here;
  the release in use wasn't recorded, so recheck on yours before relying on
  either.
  [Shell mode](https://code.claude.com/docs/en/interactive-mode#shell-mode-with-prefix)
- **zsh `path`** (observed 2026-10-01): in zsh, the variable `path` is tied
  to `PATH`: a loop variable named `path` overwrites `PATH`, so later
  commands in the same shell aren't found. Name loop variables something
  else in scripts an agent may run under zsh.
- **Config managers** (observed 2026-10-02): a dotfile manager's apply step
  needed a terminal to confirm a file that had changed on both sides, so a
  non-interactive agent shell couldn't complete it. Check the drift first;
  merge the destination-side change back into the source, or decide to drop
  it, before applying with the tool's force option.

## Headless runs

From the author's own cloud sessions, scripting `claude -p` for a personal
evaluation on 2026-10-09 and 2026-10-10; each line marked observed or
documented, with the date.

- **Isolating a run** (observed 2026-10-09; documented, checked 2026-10-10):
  `--safe-mode` turns off CLAUDE.md, skills, plugins, hooks, MCP servers,
  custom agents, and auto memory, while authentication, model selection,
  built-in tools, and permissions work normally; managed settings policy
  still applies. In a session with plugins installed, a run with it emitted
  no hook events, and the same run without it fired the plugins'
  `SessionStart`, `UserPromptSubmit`, and `Stop` hooks.
  [CLI flags](https://code.claude.com/docs/en/cli-reference#cli-flags)
- **Replacing the system prompt** (observed 2026-10-09; documented, checked
  2026-10-10): `--system-prompt-file` replaced Claude Code's own prompt, and
  a one-line run's input fell from about 30,000 tokens to about 2,800;
  `--tools` limited the built-in tools to the ones named. Replacing drops the
  default tool guidance and safety instructions too, so the file carries
  whatever the task still needs.
  [System prompt flags](https://code.claude.com/docs/en/cli-reference#system-prompt-flags)
- **Usage readings on a subscription** (observed 2026-10-09): runs signed in
  with a subscription reported `apiKeySource` as `none` and emitted a
  `rate_limit_event` with the 5-hour and 7-day windows' utilization, which a
  script can read to stop scheduling runs before the account reaches overage.
  The reported cost is a client-side estimate, which can differ from the bill
  (documented for `--max-budget-usd`, checked 2026-10-10). On 2026-10-10 the
  event's `rate_limit_info` carried `status`, `overageStatus`,
  `isUsingOverage`, `surpassedThreshold`, and `unifiedWindows`, with each
  window's `utilization` and `resetsAt` (observed). At 0.92 of the 5-hour
  window, `status` read `allowed_warning` with `surpassedThreshold` 0.9; at
  1.0 it read `rejected`, with `overageStatus` `allowed` and `isUsingOverage`
  true, and the call itself still completed, on overage. A minimal call
  reads the windows on demand: `claude -p ok --safe-mode --model <model>
  --effort low --tools "" --output-format stream-json --verbose
  --no-session-persistence`, keeping the `rate_limit_event` line.
  [CLI flags](https://code.claude.com/docs/en/cli-reference#cli-flags)
- **WebFetch results** (observed 2026-10-09): pages that answered 403, 404,
  429, 451, or 503 came back as ordinary tool results with `is_error` false;
  only the event's `tool_use_result.code` and the text "The server returned
  HTTP …" showed the failure, so a script reading transcripts checks that code
  before counting a fetch as retrieved. A successful fetch returns a small
  model's answer about the page, not the page (the tool's own description,
  checked 2026-10-10), so a grader reading the transcript sees that answer.
  To quote a docs page word for word, fetch its Markdown with curl (the
  page's URL plus `.md`) into a scratch file and quote from that, not
  through WebFetch (observed 2026-10-10). The docs host answered 403 to
  Python urllib's default User-Agent and 200 to curl's (observed 2026-10-09,
  rechecked 2026-10-10), so a script sends its own.
- **Scripted runs** (observed 2026-10-09 and 2026-10-10, Claude Code
  2.1.296): with the prompt passed as an argument and stdin not redirected,
  `claude -p` waited 3 seconds for stdin and then printed a warning, so add
  `< /dev/null`. Started from inside a Claude Code session, a run took that
  session's id unless `--session-id` named one, so pass a fresh UUID per
  run. In stream-json output a `system` `task_summary` line followed the
  final `result`, and a parser that opened a turn on every other line made
  an empty last turn. The result's `total_cost_usd` is cumulative across a
  multi-turn run, so don't sum it (the cost docs call it the cumulative
  total, checked 2026-10-10). `modelUsage` also lists the background helper
  model, so take the answering model from the assistant messages' `model`
  field.
- **Multi-turn runs** (observed 2026-10-10): one
  `claude -p --input-format stream-json` process carried a conversation:
  turn 2 answered with turn 1 in context, including turn 1's WebSearch
  calls. The script wrote each user turn only after the previous turn's
  `result` line. `--session-id` and then `--resume` gave the same answer
  but saved the session to disk, so the runner kept stream-json with
  `--no-session-persistence` and a fresh `--session-id`.
- **A grader run** (observed 2026-10-09; documented, checked 2026-10-10):
  `claude -p --safe-mode --model <model> --effort <level>
  --system-prompt-file <grader prompt> --tools "" --json-schema <schema>
  --output-format json` returns the verdict in the result's
  `structured_output` field. The script fell back to parsing `result` as
  JSON, then checked by script that each span the grader quoted appears in
  the transcript.
  [Get structured output](https://code.claude.com/docs/en/headless#get-structured-output)
- **Unattended permissions** (documented, checked 2026-10-10; observed
  2026-10-10): `--permission-prompts none` (v2.1.259 or later) denies
  permission prompts instead of waiting for an answer, and a probe call
  accepted it. `--restricted` (v2.1.248 or later), which the docs describe
  for an evaluation harness driving `claude` on a shared machine, removes
  the tools that run commands or code, and WebFetch, unless `--tools` names
  them individually. It didn't suit fixtures that need Bash, so those runs
  used `--permission-mode dontAsk` with an explicit allowlist instead.
  [Turn off permission prompts in unattended runs](https://code.claude.com/docs/en/headless#turn-off-permission-prompts-in-unattended-runs)

## Continuity and rollback

Keep long-task intent and acceptance in a durable artifact, progress in a
separate plan, and verification with the candidate. On interruption, identify
partial work, pending checks, owned temporary state, and the next authorized
step. Session compaction or rewind is not a substitute for a reviewed diff,
version control, or recovery of external effects.

Cowork uses a separate [surface guide](cowork-notes.md). Do not infer equivalent
instruction discovery, context independence, or permission controls from the
shared product family.
