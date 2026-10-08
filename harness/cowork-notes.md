# Cowork — practical operating notes

Reference, not always-loaded instructions. Primary documentation checked
2026-09-24 and rechecked 2026-10-01; no Cowork session, account, or permission
probe was run for these notes. The [copy sheet](cowork-instructions.example.md) is an adoption preview.

## Use the surface that is actually present

Pro and Max accounts are moving to what Anthropic calls the new Claude
experience: Cowork is no longer a separate mode, and what it does is available
from any conversation. Team and Enterprise organizations keep chat and Cowork
as they are for now. Where a Cowork selector remains, global instructions may
appear under Cowork settings; in the new experience they are part of
Instructions for Claude in General settings (checked 2026-10-01). Folder
instructions apply to a selected desktop folder, and Claude can update them
itself during a session. The documentation also describes coordinated
subagents and approval modes. These facts do not establish which UI or
controls a particular account has. [Getting started](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork),
[New experience](https://support.claude.com/en/articles/16761823),
[Architecture](https://support.claude.com/en/articles/14479288)

Projects have instructions, sources, and project-scoped memory. Account-backed
projects and projects created from a local folder have different persistence:
the latter stay on that computer. The project documentation does not extend
Cowork projects to Claude Code. A fresh task in a remembered project should
not be described as independent context merely because it is new. Cloud
sessions also start from what Claude remembers from chats, and task context
carries back to chat; record that before claiming independence or choosing
which evidence to supply ([Getting started](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)).
[Projects](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-claude-cowork)

The documentation says sessions run in the cloud on every surface, and it also
refers to local sessions. From October 6, 2026, new tasks on Pro and Max plans
run in the cloud and the option to run only on your computer is removed; tasks
already started on a computer stay there, and existing desktop deployments
keep local execution (checked 2026-10-01). Local files, local connectors, browser use, and
computer use go through the desktop app; a cloud session reaches connected
local folders only while the desktop app is open and when the session was
started on desktop. Record the session type and approved sources before
relying on access or persistence.
[Web, desktop, and mobile](https://support.claude.com/en/articles/15520349-use-claude-cowork-on-web-desktop-and-mobile)

## Deliberate differences from a coding host

Use Cowork for an inspectable work product: a document, evidence synthesis,
spreadsheet, or bounded file task. Carry the same intent, evidence, ownership,
review, and handoff principles, but instantiate checks for that artifact.
For example, a report needs source and calculation checks and, when layout
matters, inspection of the rendered output. A repository test command is not
a useful stand-in.

The Claude Code documentation says desktop Cowork sessions load user-scope
files such as `~/.claude/CLAUDE.md`, skipping imports that resolve outside the
session's working directory and a `~/.claude/CLAUDE.md` that is a symlink or
hard link. Check whether that file is already active before adding the Cowork
global preview, so two differently worded global instruction sets do not
compete. That statement covers desktop sessions; the documentation checked on
2026-10-01 does not say whether cloud tasks load the file. The desktop
changelog adds that, in a folder with no `CLAUDE.md`, Claude reads `AGENTS.md`
for project instructions. Inspect active sources rather than assume parity.
[Instruction loading](https://code.claude.com/docs/en/memory),
[Changelog](https://claude.com/docs/cowork/changelog)

Subagent coordination is documented; configurable child model/effort, fresh
packet selection, per-child tool denial, action telemetry, and cancellation
parity with Codex or Claude Code were **not established by this review**.
Use the [packet](agentic-development-workflow.md#worker-packet-and-return) as
a task contract when supported, and label unenforced limits as requests. If a
task requires a boundary the surface cannot demonstrate, keep it in a host
where that boundary can be checked or return the unresolved decision.

## First-use recipe

1. Select a disposable folder or project with only approved inputs. Choose an
   output location separate from protected source documents.
2. Inspect visible instructions, memory/context, execution mode, connectors,
   and approval choices. Adapt the copy sheet only after reviewing existing
   guidance; do not lower controls for convenience.
3. Give one small deliverable with explicit acceptance and authorized effects.
   Retain a single integrator. No custom plugin, schedule, or agent definition
   is needed for this first use.
4. Inspect the actual output and available action history. Verify decisive
   sources/calculations and applicable formatting. Record unavailable evidence
   rather than accepting a self-report of read-only behavior.
5. If interrupted, retain completed artifacts, current decisions, remaining
   checks, and cleanup responsibility in the authorized output area. Recheck
   state on resume. Restore unintended instruction changes through their
   normal owner; remove only task-owned temporary artifacts.

These are proposed operating steps. A successful task can justify another
bounded use, not a claim that all three surfaces enforce the same contract.
