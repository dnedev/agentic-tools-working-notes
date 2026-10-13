# claude.ai — durable operating principles

Companion to the paste-ready
[`claude-ai-profile-instructions.example.md`](claude-ai-profile-instructions.example.md),
[`claude-code-notes.md`](claude-code-notes.md), and the
[verification kit](../verification-kit/README.md). The example owns a
sanitized account-level configuration; this file owns the durable placement
and audit mechanics. It is **a reference to consult, not always-loaded
context**, and deliberately **figure-free** — model IDs, context-window sizes,
and which plan gates which feature rot in weeks, so they live in the docs
(linked below), not here. What's below is the part that ages well: how the
instruction layers fit together, and how to run the trace self-audit on this
surface.

**Scope: consumer / Team claude.ai (web + desktop).** The API and Claude
Code are separate surfaces — the latter is covered in the companion note.
Enterprise deployments can gate features and models differently, so verify
against your own account. Feature names below were checked against the
Claude help center (see the footer); treat any that have since been
renamed as pointers, not gospel.

## The instruction layers (one rule per layer)

claude.ai stacks a few instruction layers. The kit's routing labels map
onto them directly:

- **Profile instructions** — "Instructions for Claude" under Settings.
  Account-wide; applied to every conversation. This is the **[A]
  account-level** floor: cross-domain findings and always-on epistemic
  rules go here.
- **Project instructions** — apply only to chats *within* that project
  (which plans gate projects is a look-it-up — see the footer). This is
  **[B] project-level**: context and requirements
  for one kind of work. A project also carries **Project Knowledge** —
  files the chats in it can read. One example sits in the
  [project-instructions copy sheet](claude-ai-project-instructions.example.md).
- **Skills (and styles, where still shown)** — customize how responses are
  formatted and delivered, and (skills) add task capabilities. The
  personalization article checked 2026-10-01 lists skills and no styles. Keep *behavior* rules out
  of the style layer; a tone preset that quietly carries enforcement is
  the mistake the evolution notes call out
  ([evolution-and-lessons.md](../verification-kit/evolution-and-lessons.md),
  the style-layer audit).
- **Per-session** — the pasted chat-starter, and the audit template
  itself.

The governing principle is the same as everywhere else in the kit: **one
rule per layer.** A rule duplicated across profile and project is a
deletion waiting to happen, not redundancy — see the one-layer-per-rule
lesson in the evolution notes.

## Running the trace self-audit here

The [trace self-audit template](../verification-kit/trace-self-audit-template.md)
is platform-neutral by design. On claude.ai the serious-grading workflow
uses the native primitives:

- **A dedicated audit Project.** Put the failure-pattern taxonomy and the
  audit template into a project's **Project Knowledge**, and keep that
  project's own instructions minimal — the template is self-contained and
  explicitly tells the auditor to ignore any project instructions attached
  to the thread. The taxonomy and template are then the *rubric*, read
  from Knowledge rather than from memory.
- **Grade in a fresh chat with Memory off, not at the tail of the
  thread that failed.**
  Start a new conversation in the audit project and paste in the
  transcript to be graded, then the template. A clean session is the
  closest thing this surface has to an independent reviewer; the model
  that under-investigated is a poor judge of its own under-investigation.
- **Switch model before auditing.** In the model picker, choose a
  different model than produced the trace — ideally a different family.
  Self-preference bias is worst when a model grades its own output, so a
  same-model tail audit is the weakest configuration, not the default.
- **The auditor can't see the trace's original context.** A fresh chat is
  not handed the source session's model, instruction layers, or date, though
  memory, on by default for Free, Pro, and Max plans, can carry other context
  in (checked 2026-10-01); turn it off for the audit chat. That is exactly
  why the template opens with a RECORD block: you supply the trace's model,
  the instruction versions in force *during* the trace, and its date by
  hand, or mark them "unrecorded" rather than inferring.
- **Some chats can't be carried into a fresh session at all.** If a
  transcript won't move or paste — the surface declines it, or reproducing
  the spans would mean re-posting content that tripped a filter — the audit
  runs in place. That is the weakest configuration, so record it as one
  instead of implying a clean session. What leaves such a chat is a
  decontaminated summary: findings, keys, and category-level triggers,
  never the raw spans. A later need for exact wording goes back to the
  origin session and is never reconstructed from memory — the corpus
  method's transport convention covers what that costs an entry.

## Provenance hazards when a trace is graded out of context

The template's PROVENANCE step exists for this surface's normal case — a
transcript audited somewhere other than where it ran. The claude.ai
specifics:

- The **destination project's instructions are visible to the auditor and
  are not the trace's.** Judge adherence only against layers you have
  positive evidence were in force during the trace; don't grade it against
  whatever project you happen to be auditing from.
- **Project Knowledge files are your rubric, not the trace's
  environment.** Reading the taxonomy to grade is correct; faulting the
  trace for not having consulted a file it never had is not.
- A pasted or relocated chat's **timestamp reflects the move, not the
  trace** — infer no date, recency, or ordering from where it now sits.
- Whether the surface lets you literally *move* an existing chat into a
  project, versus paste its transcript into a fresh chat there, is a UI
  detail that changes — **check current docs.** The audit only needs the
  transcript sitting in a clean context; how it gets there doesn't change
  the method.

For turning any confirmed finding into a standing check, the
decontamination and fresh-instantiation rules are surface-independent and
already written up in
[`regression-corpus-method.md`](../verification-kit/regression-corpus-method.md)
— don't re-derive them here.

## Where the current specifics live (look them up)

- Help center (features, plans, settings): `support.claude.com`
- Product & developer docs: `platform.claude.com/docs` (`docs.claude.com`
  redirects there, checked 2026-10-01)
- Things that rot and should be re-checked, never cached here: which plans
  gate Projects and project instructions; the current model lineup and
  per-model context window; whether styles or skills is the live
  tone/format surface; per-model behavioral priors (these age in months —
  the [kit's drift caveat](../verification-kit/README.md) applies).

## Cowork and tasks

On Pro and Max plans in the new Claude experience, any conversation can now do
what Cowork does; Team and Enterprise keep Cowork separate for now (checked
2026-10-01). These chat/profile notes do not establish task execution or
instruction mechanics. Use the [Cowork notes](cowork-notes.md) and its scoped
copy sheet for artifact work. The global instructions field is shared in the
new experience, and projects work in every conversation, so do not paste two
competing global instruction sets or fork a task-only copy of a project's
instructions. The Cowork notes carry the dated primary-source check.

## Checking what actually reaches the model

- **The platform prompt is a layer you don't control.** Anthropic publishes
  the claude.ai system prompt per model in its
  [release notes](https://platform.claude.com/docs/en/release-notes/system-prompts/overview),
  but live sessions read on 2026-09-22 and 2026-09-23 carried lines the
  published copy lacked, and a Cowork task's prompt differed again. Read the
  published copy at each release and confirm in a live session before
  deciding a profile rule is needed or redundant. The per-model pages also
  served Markdown at the same URL plus `.md` (observed 2026-09-24,
  2026-10-09, and 2026-10-10).
- **Make installs checkable.** A short stamp line in each installed
  artifact, such as a version or date the model can quote, lets a fresh
  session confirm what actually reached it; that is how the profile was
  confirmed to reach Cowork tasks (observed 2026-09-23 and 2026-09-28).
- **An instructions edit reaches a running chat late.** An edit to a
  project's instructions field didn't appear in a chat that was already
  running; it appeared after that chat's session restarted. New chats and
  scheduled tasks loaded it at start, each confirmed by quoting its stamp
  line (observed 2026-10-11). Test an edit in a new chat.
- **Large project knowledge isn't in context.** In a project with a large
  knowledge base, a fresh session had only the file list in context, not the
  contents, and read files with the project tool (observed 2026-10-11). The
  help center says retrieval turns on as project knowledge approaches the
  context window, with a project knowledge search tool (checked 2026-10-11);
  that this session was in that mode is an inference. Don't assume a project
  file was read because it is in the project.
  [RAG for projects](https://support.claude.com/en/articles/11473015-retrieval-augmented-generation-rag-for-projects)
- **The project tool's file names.** A session's project tool wrote a bare
  file name under `claude/`, and a leading `/` was kept as part of the name,
  so the session couldn't create a file at the project's root. In one session
  the tool returned a document of about 227 KB inline rather than as a local
  file (both observed 2026-10-11).
- **Chat search has edges.** Past-chat search is a "Search and reference
  chats" toggle in settings, and inside a project it searches only that
  project's conversations (checked 2026-10-02). It was not available inside
  one cloud Cowork task (observed 2026-09-29), and a scheduled-task session
  didn't show up in it a few minutes after it ran (one check, observed
  2026-10-11), so keep version texts in project knowledge rather than relying
  on search to find them.
- **A GitHub repository in a project is a snapshot.** You select files and
  folders from one branch; it refreshes only when you press Sync now, and no
  commit history or pull requests come with it (checked 2026-10-02).

_Principles current as of 2026-08-05; feature names verified against the
Claude help center articles on Projects and personalization (last modified
July 2026), with memory, styles, and the docs host rechecked 2026-10-01, and
the system-prompt pages' Markdown copies fetched 2026-10-10. The last two
sections carry their own dates: "checked" marks a help-center check
on that date, and "observed" marks the author's own sessions. The figures are intentionally elsewhere._
