# Project instructions

<!-- Claude Code's current documentation says it reads CLAUDE.md rather than
     AGENTS.md natively and prescribes this import adapter:
     https://code.claude.com/docs/en/memory#agentsmd. Keep the import until the
     official documentation says otherwise. -->

@AGENTS.md

> **Import sentinel.** If you don't see project-specific rules (the Propagation
> rule, the "instruments are canonical" rule, the epistemic-register directive)
> below this point, the `@AGENTS.md` import may have failed silently — read
> `AGENTS.md` directly before proceeding.

Project instructions live in `AGENTS.md` (read by Codex, Cursor, Copilot, and other
agents per the [agents.md spec](https://agents.md)). Don't add instructions here —
keep this file as a Claude Code adapter that imports the canonical file.
