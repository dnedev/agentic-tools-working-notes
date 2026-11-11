# CoCo execution contract — example

Scope: how Snowflake CoCo sessions on this machine execute work. It pairs with
the data-work defaults in `AGENTS.md` beside this file and the general
user-scope instruction file, and doesn't restate either.

## General rules loaded from Claude Code

- The Claude Code global file (`~/.claude/CLAUDE.md`) loads here too. Its rules
  on reasoning, evidence, calibration, interaction and safety apply. Rules
  there that name Claude Code features (models and effort, subagents and
  workflows, plugins, review tools, commit credit) are about Claude Code and
  don't direct CoCo.

## Connections

- Work in the connection the session started with. Don't switch to another
  connection or account unless the task names it.
- Run SQL through the SQL tool, not through a CLI in the shell, unless the task
  asks for the CLI: a CLI can use a different connection, role or session from
  the one you report.

## Refusals and restricted scopes

- A rejected permission prompt, a denied tool, or a statement refused by a
  restricted session scope is a boundary, not a fault. Report the exact message
  and stop that line of work. Don't retry it through another tool, the shell, a
  subagent, or another role.
- When a statement is refused, or what you can see differs from what was
  expected, add any active restricted session scope to the effective context:
  `SELECT SYS_CONTEXT('SNOWFLAKE$SESSION', 'ACTIVE_RESTRICTED_SESSION_SCOPES')`.

## Documentation

- For Snowflake documentation, use `cortex search docs <query>` or fetch the
  page (docs.snowflake.com pages also serve a `.md` version), and quote the
  sentence you rely on with its URL.

## Session side effects

- Don't create scheduled work or background agents unless the task asks for
  them. Write files only in the working directory or a path the task names.
