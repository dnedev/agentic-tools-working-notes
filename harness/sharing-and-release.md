# Preparing these notes to share

Status: my own review checklist, 2026-09-24; revised 2026-10-01,
2026-10-10, and 2026-11-11. Adapt it to your setup. Preparation is not
publication approval. No commit, push, PR/MR, public synchronization, or
external message is implied.

## What a public copy holds

| Material to review | Keep outside the public copy |
| --- | --- |
| Reviewed tracked-file snapshot, public-source attribution, generic examples, and explicit replay/validation gaps | Internal program/team names, private links, target repositories and defects, private history, private corpus, machine/account identifiers, raw traces, credentials, live personal configuration |

Suggested reading order: [adoption](agentic-development-adoption.md),
[working core](working-principles.md), [workflow](agentic-development-workflow.md),
then the [evidence status](evidence-status.md).
Invite feedback on one real task: what was missing, what was redundant, what
failed, and whether total framing/review/rework improved. Request replication
or contradiction, not endorsement of an n=1 package.

A private source repository does not make every tracked file suitable for
public history export. Questionable disclosures stay flagged until the owner
resolves them; a clean secret scan cannot clear provenance or confidentiality
judgment.

## Review before export

1. Review the exact source diff and intended file list. Include new approved
   files deliberately; do not sweep untracked or ignored material into a copy.
2. Inspect the **whole proposed snapshot**, not just the newest diff, for
   internal names, URLs, domains, account/connection identifiers, machine paths,
   source-specific trace details, and private-history references. Check prose,
   links, filenames, fixtures, graders, and examples.
3. Run the configured secret-detection gate. Record unavailable scans and
   their substitute. Pattern checks are useful triage, not equivalent to the
   CI analyzer or disclosure clearance.
4. Check local links including heading targets, fences, tables, whitespace,
   fixture/grader pairs, sample consistency, and any changed taxonomy/template
   coupling. Preserve licenses and attribution.
5. Inspect whether a public fixture can actually be replayed. If it needs a
   private subject/key or a missing checker, say so. Do not distribute the
   private input merely to remove that caveat.

## Publishing a snapshot

One way to publish from a private editing repository: release a squashed
snapshot of its tree, minus the repository's own tooling, and review that
exact commit before it goes public, as a pull request in a private
repository that holds the same commits as the public one. A fork can't be
that private copy, because a fork's visibility follows its upstream's
([GitHub's
docs](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-permissions-and-visibility-of-forks),
checked 2026-11-11). Push the reviewed commit itself, as a fast-forward that
keeps its SHA, rather than with a merge button, which would create a
different commit.

Before pushing anywhere, run the checks under
[Review before export](#review-before-export) on the new tree, and check each
commit's identity and signature:

```sh
git log --format='%h %an <%ae> %cn <%ce> %G?' <public-main>..<release-branch>
```

Every line should show only a noreply address as author and the expected
committer, and end in `G`, a good signature. For an SSH signing key, git
reports `G` only when the key is listed in `gpg.ssh.allowedSignersFile` (git
documentation, checked 2026-10-10); without it, read GitHub's verdict after
pushing for review with
`gh api repos/<owner>/<repo>/commits/<sha> --jq .commit.verification`.

That check doesn't read trailers. GitHub ties a `Co-authored-by` trailer to an
account through its email; its docs don't say how it shows an address that
belongs to no account or to someone else's, and public issues report Claude
Code's trailer addresses linking to an account (checked 2026-10-10:
[multiple authors](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors),
[contributions reference](https://docs.github.com/en/account-and-profile/reference/profile-contributions-reference),
[issue 1653](https://github.com/anthropics/claude-code/issues/1653)). A
commit written in a Claude Code cloud session carries such a trailer and a
`Claude-Session:` link ([observed](claude-code-notes.md#cloud-sessions)), so
read `git log --format=%B` over the range if a release shouldn't carry them.
A squashed snapshot whose message is written at release time keeps the
private history's trailers out of public.

Anything that cites the notes should pin the resulting public commit. A new
snapshot does not remove anything from already published history; discovery of
an older leak needs a separate owner-led response.

Once a release reads Verified, give the public repository a ruleset on its
default branch with **Restrict deletions**, **Block force pushes**, and
**Require signed commits** (GitHub's
[available rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets),
checked 2026-10-10). GitHub signs web-interface commits itself, so the rule
alone wouldn't stop one from someone with write access (inferred; not tested).
I keep vigilant mode off: with it on, a signed commit whose committer isn't
the author reads Partially verified, which would cover every session commit
(GitHub's
[verification statuses](https://docs.github.com/en/authentication/managing-commit-signature-verification/displaying-verification-statuses-for-all-of-your-commits),
read 2026-10-13; not observed).

## Keeping an adapted copy in sync

If you keep an adapted copy elsewhere, move changes as reviewed file changes,
not shared history, and never add the other repository as a remote.

- **Out to the other copy.** After a merge, hand over the diff since the last
  synced commit, a short note per change (what, why, and what may need
  adapting there), and the base SHA. The receiving agent reviews and adapts
  rather than applying blindly, and records the base in a commit trailer so
  the next handoff knows it. Put that line in the message's last paragraph,
  with the other trailers: a line above the blank line before the trailers
  isn't a trailer, so `%(trailers)` log formats miss it (observed with git
  2.43.0 on 2026-10-14).
- **Back from it.** Extract only reviewed, sanitized changes into a branch,
  run the checks under [Review before export](#review-before-export) before
  the push, and keep adaptations made for the other context there.

## Review handoff

The release owner records: intended audience; selected source revision/files;
destination state; disclosure questions and disposition; exact check commands
and outcomes; excluded files; fixture replay limits; pending approvals; and
the next authorized action. Keep private attribution out of a public PR body.
