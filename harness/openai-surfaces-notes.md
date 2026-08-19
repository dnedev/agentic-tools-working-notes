# OpenAI surfaces — durable operating principles

**A reference to consult, not always-loaded context.** It is deliberately
figure-free: model IDs, context sizes, instruction limits, prices, plan gates,
and volatile UI availability belong in the live docs linked below.

These are one engineer's operating notes, not a framework, policy, or
best-practice claim. Take what's useful and verify it against the current
product.

Scope: standard Codex and ChatGPT product surfaces. Managed workspaces and
hosted environments can add policy or provision different files, so verify the
active environment rather than assuming that a local setting travelled.

## Put each rule in the narrowest surface that owns it

| Need | Surface |
| --- | --- |
| Personal defaults for Codex clients using one Codex home | Global `AGENTS.md` |
| Shared repository conventions and verification commands | Repo or nested `AGENTS.md` |
| A current task's goal, context, constraints, and done condition | Current prompt |
| A repeatable, on-demand procedure | Skill |
| Deterministic denial or lifecycle enforcement | Permissions, config, or hooks |
| General behavior in standard ChatGPT | Custom Instructions |
| Stable facts about the user | More about me and Occupation |
| Tone and presentation | Personality and Characteristics |
| Project-only sources and behavior | ChatGPT Project sources and instructions |
| Soft recall from prior work | Memory |

The documented mechanisms checked on 2026-08-05 do not expose a shared portable
include across these targets. The ChatGPT documentation checked describes
Personalization fields and Project sources; it does not describe automatic
loading of arbitrary local repo documents. Codex's documented `AGENTS.md`
discovery covers the global and repository guidance used here. Duplicate the
small transferable core deliberately, then review both projections when it
changes.

## Codex instruction loading

Codex constructs an instruction chain. At global scope it uses
`AGENTS.override.md` when present, otherwise `AGENTS.md`; at project scope it
walks from the project root toward the working directory, with closer guidance
taking precedence. Discovery happens when a run or session starts, so verify
the active sources after changing them.

The Personalization editor in Codex is an editor for personal instructions, not
a separate third instruction target. A local global file should be described as
governing clients that load that Codex home. Do not claim it automatically
reaches an unrelated cloud host unless that environment has been checked.

`AGENTS.md` is guidance, not a hard sandbox. Put deterministic blocks in the
enforcement surfaces the current Codex docs provide.

## Standard ChatGPT personalization

Custom Instructions apply broadly to standard ChatGPT chats. "More about me"
and Occupation should carry stable user facts; behavioral gates belong in
Custom Instructions; personality and Characteristics tune style rather than
capability.

Project instructions are a different scope. Current product documentation says
they apply inside that Project and replace global Custom Instructions there.
Make any must-hold Project instruction self-contained, and re-check the live
docs before relying on that behavior.

Memory can make preferences and context convenient, but it is not the only copy
of a required rule. ChatGPT account memory and local Codex memory are separate
stores. A custom GPT has its own configuration and should not be assumed to
inherit account Custom Instructions or saved memory.

## Using the verification kit in a ChatGPT Project

For a Project-based trace audit, add the tracked taxonomy and trace-audit
template as Project sources, leave Project instructions unset, start a fresh
chat, paste the transcript, then paste the template unchanged. The template is
self-contained and explicitly defines its own rubric; duplicating it into
Project instructions adds a competing copy. Record the active account Custom
Instructions and the Project memory mode as audit-side context because a fresh
chat does not establish a fresh context, and current docs do not establish
whether an empty Project-instructions field suppresses account instructions.

Record the trace-side and audit-side context the template asks for. A fresh
Project chat does not prove independence, and missing render or citation signals
do not prove that the original trace performed no retrieval.

## Live documentation

- [Codex instruction discovery](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- [Prompting and task boundaries](https://learn.chatgpt.com/docs/prompting)
- [ChatGPT personalization](https://learn.chatgpt.com/docs/personalize)
- [Memory separation](https://learn.chatgpt.com/docs/customization/memories)
- [ChatGPT Projects](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
- [Custom Instructions](https://help.openai.com/en/articles/8096356-custom-instructions-for-chatgpt)
- [Personality](https://help.openai.com/en/articles/11899719-customizing-your-chatgpt-personality)
  and [Characteristics](https://help.openai.com/en/articles/20001038-characteristics-in-chatgpt)
- [Custom GPT isolation](https://help.openai.com/en/articles/8554407-gpts-in-chatgpt)

_Principles checked 2026-08-05; product specifics intentionally remain in the
linked live documentation._
