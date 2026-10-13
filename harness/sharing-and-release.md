# Preparing these notes to share

Status: my own review checklist, 2026-09-24; release flow revised 2026-10-01
and 2026-10-10. Adapt it to your setup. Preparation is not publication
approval. No commit, push, PR/MR, public synchronization, or external message
is implied.

## Two audiences, one sanitized general body

| Audience | Material to review | Keep outside that package |
| --- | --- | --- |
| Colleagues with authorized internal access | The same working core, adoption guide, workflow, evidence limits, and relevant examples; a separately reviewed private cover note can name internal contributions and questions | Raw traces, credentials, live personal configuration, unrelated private evidence |
| Public readers | Reviewed tracked-file snapshot, public-source attribution, generic examples, and explicit replay/validation gaps | Internal program/team names, private links, target repositories and defects, private history, private corpus, machine/account identifiers |

Suggested reading order: [adoption](agentic-development-adoption.md),
[working core](working-principles.md), [workflow](agentic-development-workflow.md),
then the [evidence status](evidence-status.md).
Invite feedback on one real task: what was missing, what was redundant, what
failed, and whether total framing/review/rework improved. Request replication
or contradiction, not endorsement of an n=1 package.

Internal attribution belongs in a private companion through the approved
internal route. A private source repository does not make every tracked file
suitable for public history export. Questionable disclosures stay flagged
until the owner resolves them; a clean secret scan cannot clear provenance or
confidentiality judgment.

## Review before export

1. Review the exact source diff and intended file list. Include new approved
   files deliberately; do not sweep untracked or ignored material into a copy.
2. Inspect the **whole proposed snapshot**, not just the newest diff, for
   internal names, URLs, domains, account/connection identifiers, machine paths,
   source-specific trace details, and private-history references. Check prose,
   links, filenames, fixtures, graders, and examples.
3. Run the configured secret-detection gate through an authorized route.
   Record unavailable scans and their substitute. Pattern checks are useful
   triage, not equivalent to the CI analyzer or disclosure clearance.
4. Check local links including heading targets, fences, tables, whitespace,
   fixture/grader pairs, sample consistency, and any changed taxonomy/template
   coupling. Preserve licenses and attribution.
5. Inspect whether a public fixture can actually be replayed. If it needs a
   private subject/key or a missing checker, say so. Do not distribute the
   private input merely to remove that caveat.

## Publishing a release

Staging `main` is the editing home and keeps full history. Public `main`
receives one squashed snapshot per release through the staging `public`
branch, so review sees exactly what will be published. The author runs this
checklist on their own machine with commit signing on (`commit.gpgsign`), so
the snapshot commit is signed when it's made and the commit reviewed is the
one published: no amend, no force-push. The signing key is registered on the
author's GitHub account as a signing key, which is what lets GitHub show the
release commit as Verified (GitHub docs, checked 2026-10-10). A cloud session
signs its commits with a key that isn't the author's (see
[Commit identity](claude-code-notes.md#cloud-sessions)), and the author's
signing key stays on their machine and isn't put in a cloud environment
(decided 2026-10-10), so the release isn't made there. In a checkout with
remotes `staging` and `public`, `user.email` set to the GitHub noreply
address, and signing on:

```sh
git fetch staging main public
git fetch public main
git switch -C publish staging/public
git read-tree -u --reset staging/main
git show staging/main:.publish-exclude | grep -v -e '^#' -e '^[[:space:]]*$' |
  git rm -r -q -f --ignore-unmatch --pathspec-from-file=-
git diff --cached --name-status staging/main  # expect only the excluded paths, as D
git commit -m "Release YYYY-MM-DD: <summary>"
```

The first time, create the staging `public` branch from public `main` with
`git push staging public/main:refs/heads/public`. If `.publish-exclude` ever
lists nothing, skip the `git rm` step. Untracked files in the worktree are not
committed.

The noreply check below reads author and committer, not trailers. What
GitHub does with a commit trailer (documented, checked 2026-10-10): a
`Co-authored-by` trailer is a line in the commit message, and the docs tie it
to a person through its email: "For the commit to count as a contribution, use
an email address associated with their account on GitHub.com." The
contributions reference, which doesn't name co-authors, puts a commit on
someone's contribution graph only if its email is associated with their
account, it was made on the default branch (or `gh-pages`) of a repository
that isn't a fork, and they are a collaborator or organization member, have
forked the repository, or have opened a pull request or issue in it.
Private-repository activity is hidden by default; if the person turns it on,
people without access "will see the number of contributions you made each
day. They will not see specific details." The pages read don't say how GitHub
displays a trailer whose email belongs to no account, or to someone else's.
[Creating a commit with multiple authors](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors),
[Profile contributions reference](https://docs.github.com/en/account-and-profile/reference/profile-contributions-reference),
[Contributions on your profile](https://docs.github.com/en/account-and-profile/concepts/contributions-on-your-profile)

Public issues report the second case for Claude Code's trailer addresses
(checked 2026-10-10): [`noreply@anthropic.com`, opened
2025-06-05](https://github.com/anthropics/claude-code/issues/1653), closed that
day as a duplicate of
[an issue](https://github.com/anthropics/claude-code/issues/1655) whose closing
reply calls the `claude` account "our account"; and
[`claude-code@anthropic.com`, opened
2026-05-12](https://github.com/anthropics/claude-code/issues/58479), closed by
a bot as not planned. On 2026-10-10 a small sample from GitHub's public commit
search showed the `noreply@anthropic.com` trailer linked to the `claude`
account; the other address wasn't checked. So what a trailer address shows on
GitHub has been reported to change, and is worth checking before a history
that carries trailers, staging `main`'s included, becomes public.

Before pushing anywhere, run the gates under
[Review before export](#review-before-export) on the new tree, and check
identity and signature:

```sh
git log --format='%h %an <%ae> %cn <%ce> %G?' staging/public..publish
```

Every line should show only the noreply address, as author and committer,
and end in `G`, a good signature. For an SSH signing key, git reports `G`
only when the key is listed in `gpg.ssh.allowedSignersFile` (git
documentation, checked 2026-10-10). Without that file, an SSH-signed commit
read `N` after an error about the missing file (observed 2026-10-10, git
2.43.0, without `ssh-keygen` installed). That check reads author, committer,
and signature only. A commit written in a Claude Code cloud session also
carries a `Co-Authored-By` trailer and a `Claude-Session:` link in its message
([observed](claude-code-notes.md#cloud-sessions)); if a release shouldn't
carry them, read `git log --format=%B staging/public..publish` before pushing.
The snapshot is one squashed commit whose message is written at release time,
so session trailers in staging history don't reach public; only that message
does. The author's release messages carry neither trailer, a choice made
2026-10-08. In private repositories the author's convention, decided 2026-10-10,
is that the author stays author and committer and Claude is credited with
`Co-Authored-By: Claude <noreply@anthropic.com>`, without a model name, next
to the `Claude-Session:` link. Then push it for review, and put
the staging `main` commit it was built from in the pull request description
rather than in the public commit:

```sh
git push staging publish:publish/YYYY-MM-DD
```

Open a pull request from `publish/YYYY-MM-DD` into `public`. After review,
fast-forward from the command line rather than the merge button, which would
create a different commit:

```sh
git push staging publish:public
git push public publish:main
```

Anything that cites the notes should pin the resulting public commit. A new
snapshot does not remove anything from already published history; discovery of
an older leak needs a separate owner-led response.

After the first signed release, the public repository gets a ruleset on its
default branch with **Restrict deletions**, **Block force pushes**, and
**Require signed commits**. GitHub's docs (checked 2026-10-10): with required
signing, "contributors and bots can only push commits that have been signed
and verified to the branch", and "GitHub will automatically use GPG to sign
commits you make using the web interface". So the rule alone wouldn't stop a
commit GitHub signs for someone with write access (inferred; not tested). From
then on cloud sessions don't get write access to the public repository:
agents prepare a release on staging, and only the author pushes public. This
is the author's setup, decided 2026-10-10. The author also turns on GitHub's
vigilant mode. The docs (checked 2026-10-10) mark an unsigned commit
Unverified when its committer or an author has vigilant mode on; they don't
say how unsigned commits pushed before it was turned on will read, the older
public ones included (not checked). Cloud-session commits already read
Unverified.
[Displaying verification statuses](https://docs.github.com/en/authentication/managing-commit-signature-verification/displaying-verification-statuses-for-all-of-your-commits),
[About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification),
[Available rules for rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets)

## Syncing with another copy

If you keep an adapted copy elsewhere, move changes as reviewed file changes,
not shared history, and never add the other repository as a remote. (Mine can't
share commits anyway: it uses a different object format.)

- **Out to the other copy.** After a merge to `main`, hand over the diff since
  the last synced commit, a short note per change (what, why, and what may need
  adapting there), and the base SHA. The receiving agent reviews and adapts
  rather than applying blindly, and records `Sync-from: staging <sha>` so the
  next handoff knows its base.
- **Back from it.** Extract only reviewed, sanitized changes into a branch here,
  run the checks under [Review before export](#review-before-export) before the
  push, and merge through a pull request. Adaptations made for the other context
  stay there. Omit `_input/`, `_output/`, and CI configuration.

## Review handoff

The release owner records: intended audience; selected source revision/files;
destination state; disclosure questions and disposition; exact check commands
and outcomes; excluded files; fixture replay limits; pending approvals; and
the next authorized action. Keep private attribution out of a public PR body.
The documentation author does not self-certify employer disclosure approval.
