# Preparing these notes to share

Status: my own review checklist, 2026-09-24; release flow revised 2026-10-01.
Adapt it to your setup. Preparation is not publication approval. No commit,
push, PR/MR, public synchronization, or external message is implied.

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
branch, so review sees exactly what will be published. In a checkout with
remotes `staging` and `public`, and `user.email` set to the GitHub noreply
address:

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

Before pushing anywhere, run the gates under
[Review before export](#review-before-export) on the new tree, and check that
`git log --format='%h %ae %ce' staging/public..publish` shows only the noreply
address. Then push it for review, and put the staging `main` commit it was built
from in the pull request description rather than in the public commit:

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

## Syncing with the private source

The private source uses SHA-256 Git objects and staging uses SHA-1, so the two
never share commits; changes cross as reviewed file changes. Never add or fetch
the private repository as a remote of staging or public.

- **Staging to private source.** After a merge to staging `main`, hand over the
  diff since the last synced staging commit, a short note per change (what,
  why, and what may need adapting there), and the staging SHA. The receiving
  agent reviews and adapts rather than applying blindly, and records
  `Sync-from: staging <sha>` so the next handoff knows its base.
- **Private source to staging.** Extract only reviewed, sanitized changes into
  a staging branch, run the checks under [Review before export](#review-before-export)
  before the push, and merge through a pull request. Adaptations made for the
  private context stay there. Omit `_input/`, `_output/`, and CI configuration.

## Review handoff

The release owner records: intended audience; selected source revision/files;
destination state; disclosure questions and disposition; exact check commands
and outcomes; excluded files; fixture replay limits; pending approvals; and
the next authorized action. Keep private attribution out of a public PR body.
The documentation author does not self-certify employer disclosure approval.
