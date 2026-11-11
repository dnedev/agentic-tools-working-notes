---
name: writing-for-others
description: >-
  Voice and a check before handing over, for text someone other than the
  user will read: documents, reports, handovers, wiki pages, emails, chat
  posts, pull request descriptions, requests to other teams. Use when drafting
  or revising such text. Do NOT use for replies to the user themself; their
  reply style covers those.
---

# Writing for others

> **Sanitized, illustrative sample.** One engineer's voice for writing other
> people read, split out of a personal reply style so it fires per task
> instead of shaping every reply. Not a framework, policy, or best-practice
> claim, and the preferences are mine: swap them for yours. Verify the
> frontmatter fields against your runtime's current skills documentation
> before installing, and note that repo-relative links below stop resolving
> once this directory is copied out.

My voice for shared writing: my style as I write for other people, not the way
I type prompts. Clear, informative, easy to read, and convincing where it needs
to be. Several drafts are normal; stop when the document does its job.

## Voice

- Write complete, plain sentences. Keep my terms and phrasing where they work;
  drop prompt shorthand, typos, and chat informality.
- Use concrete verbs and evidence rather than adjectives. Leave out stock AI
  phrasing, canned transitions, slogans, and promotional, ceremonial, or
  self-congratulatory language.
- Convincing means a clearer claim, better support, and the reader's likely
  objection answered, not louder adjectives or a bigger implied impact. Keep a
  strong claim when it is defensible; don't inflate the author, and credit
  colleagues for their part.
- Be sharp without being petty: professional, and neutral in tone when the
  document may travel beyond its first reader.
- No em dashes. Use a comma, a colon, brackets, or a new sentence instead.

## Structure

- Put the key message first: what the reader needs to understand or decide,
  then layered detail for those who want it. For senior or mixed audiences,
  lead with the point, the decision, and the trade-offs; for engineers, add
  constraints, interfaces, alternatives, and evidence.
- Use headings and subheadings that follow the reader's questions.
- Use bullets for genuinely parallel items (reasons, actions, rules), nested
  only where items have levels. Write explanations, narratives, and caveats as
  paragraphs, with a bold lead-in where it helps scanning. Structure helps;
  overboard doesn't.
- Use a table for comparisons, and a diagram where it shows a flow or an
  architecture better than text.
- Use emphasis sparingly: **bold** for the few load-bearing phrases, *italics*
  for contrast or a defined term, `monospace` for identifiers, table names,
  paths, and commands.
- Add short clarifications in brackets (a term or acronym on first use, say)
  where they help the reader, not in every sentence. Common acronyms in the
  reader's organization need none.
- Write dates as `2026-Sept-24`, or `Sept-24` when the year is clear.
- Keep evidence, interpretation, proposals, and unknowns distinguishable.
  Never cut a qualification that changes the claim.
- Agents may read it too: plain structure and explicit terms serve both kinds
  of reader.

## Messages and revisions

- A covering message says why it is being sent, the main point, and the ask.
  Don't invent a deadline or a decision request.
- When asked for something short, give the short version first; add a longer,
  detailed tier only when asked or clearly useful.
- In revisions, keep accepted passages and earlier corrections, make the
  smallest useful change, and don't bring back rejected wording.

## Check before handing over

A rule that keeps slipping needs a mechanical check, not louder wording. Before
handing a draft over, search it for the em-dash character, spaced en dashes,
and numeric dates such as `2026-09-24`, and fix every hit outside code; then
reread the draft as its reader, since a clean search is not a review. My own
setup runs a small read-only checker that also flags stock phrases,
exclamation marks, and paragraphs heavy on brackets, list lines, or bold; a
plain search covers the core of it.

## Fuller agreement

If you keep a fuller private working agreement for documents (a notes-vault
page, say), point to it here, read it before a substantial document, and don't
copy its content into shared artifacts.

---

Sanitized for sharing, 2026-10-21. The voice rules restate what I had asked
for across several weeks of document requests, mostly about em dashes, stock
phrasing, and how much structure is too much. Installed under Claude Code
only; not yet exercised on a real document beyond its first day.
