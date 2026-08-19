---
name: dotfiles-sync
description: Reconcile and push chezmoi-managed dotfile changes. Use when asked to update, sync, save, commit, or push dotfiles / chezmoi config, or when `chezmoi status` shows drift (MM / DA rows). Resolves the live-vs-source direction per file, secret-checks staged changes before committing, and pushes only on confirmation. Do NOT use to discover new files to track (that is dotfiles-discover) or for unrelated git repos.
---

# dotfiles-sync

> **Sanitized, illustrative sample.** One engineer's convention for moving
> dotfile changes in the right direction, written after nearly losing a day of
> live edits to a stale source copy. Not a framework, policy, or best-practice
> claim. The chezmoi subcommands, status codes, and flags below were checked
> against chezmoi v2.71.1 — verify them against the version you actually run
> before installing, and note that the repo-relative links stop resolving once
> this directory is copied out.

Move dotfile changes between the live files and the chezmoi source repo, then
commit and push — without clobbering uncommitted edits or leaking secrets.

## Responsibility

One job: bring the chezmoi source repo and the live dotfiles into a chosen,
clean, committed, pushed state. Discovery of *new* files to track is out of
scope — that is [`dotfiles-discover`](../dotfiles-discover/SKILL.md).

## The core footgun (why this skill exists)

chezmoi has two sides: the **source** (`chezmoi source-path`, a git repo) and
the **live** files in `$HOME`. `chezmoi apply` writes source → live and will
**overwrite** live edits. Editing a live file directly creates *drift*. Pushing
the wrong direction loses work. Source filenames also carry attributes
(`dot_`, `private_`, `encrypted_`, `executable_`) — never hand-edit those names.

The asymmetry is what makes this dangerous. Getting the direction wrong toward
the source produces a bad commit you can inspect and revert; getting it wrong
toward live silently overwrites files that had no other copy.

## Workflow

### 1. Orient

```bash
chezmoi source-path
chezmoi status            # two-column codes, see table
git -C "$(chezmoi source-path)" status -s
```

Status code reading (col1 = add-direction, col2 = apply-direction):

| Code | Meaning |
|------|---------|
| `MM` | live and source diverged both ways — **decide which wins** |
| ` M` / `M ` | one-sided modification |
| `DA` | source has it, live is missing — `apply` would (re)create it |
| `A ` / ` A` | present one side only |

### 2. Preview each drifted file

```bash
chezmoi diff "$HOME/<path>"   # '-' = live, '+' = source
```

Never skip this on an `MM` row. The status code tells you *that* both sides
moved, not which side holds the version you want.

### 3. Decide direction per file (ask once if unclear)

- **Keep the live edits** (you edited on purpose): pull live → source.
  ```bash
  chezmoi re-add "$HOME/<path>"   # or: chezmoi re-add   (all modified)
  ```
- **Source wins** (discard live drift): push source → live.
  ```bash
  chezmoi apply "$HOME/<path>"          # prompts if live has drifted
  chezmoi apply --force "$HOME/<path>"  # only with explicit confirmation
  ```
  Non-interactive runs abort on the "changed since chezmoi last wrote it" prompt
  (`could not open a new TTY`) — that is the safety net, not a bug. Surface it
  and get a decision rather than forcing past it.

For files you edit live and test live — skills, editor config, anything you
iterate on in place — `re-add` is nearly always the right answer, because the
copy you have been testing is the live one.

### 4. Secret-check before committing

The gate is chezmoi's built-in gitleaks scan on `add`/`re-add`, enforced by
`add.secrets = error`. See
[`dotfiles-discover`](../dotfiles-discover/SKILL.md) step 4 for the canonical
rule and the `# gitleaks:allow` allowlist procedure — one source of truth, do
not re-implement it here.

If any `chezmoi add` / `chezmoi re-add` in this workflow prints a secret
detection or exits non-zero, **HARD STOP**: do not stage, do not commit. Never
pass `--secrets=ignore` to push a file through. Report the file and the rule
that fired (redact the value). A `warning` is not a `stop` — rely on `error`
mode, and if it is somehow set to `warning`, treat a detection as a stop anyway.

### 5. Commit and push (confirm before push — outward-facing)

**Never `chezmoi git -- add -A`.** The source repo is a long-lived git repo and
may already carry unrelated modifications from an earlier session; `-A` sweeps
them into your commit unreviewed. Read status first, then stage explicit paths.

```bash
chezmoi git -- status                     # READ IT — expect unrelated dirt
chezmoi source-path "$HOME/<path>"        # target path → source path to stage
chezmoi git -- add <source-path> [...]    # explicit paths only, never -A
chezmoi git -- diff --cached              # confirm nothing extra got staged
chezmoi git -- commit -m "<concise message>"
# PUSH publishes — confirm first:
chezmoi git -- push
```

## Guardrails

- **Never clobber silently.** If live drift exists and no direction has been
  chosen, stop and ask — state preserved, nothing applied or committed.
- **Secrets are terminal.** A secret-scan hit blocks the commit outright.
- **Confirm before push.** Push is outward-facing and hard to reverse.
- **Escape hatch:** at any ambiguous step, abort leaving the tree exactly as
  found and report `chezmoi status` plus `git status`.
- Does NOT discover new files to track — that is
  [`dotfiles-discover`](../dotfiles-discover/SKILL.md).

## Teaching

Each run, name which direction moved for each file and why, so the operator
internalizes source-vs-live instead of re-learning the footgun.

---

Sanitized for sharing — last revised 2026-08-07, replacing a `git add -A` step
with explicit-path staging after the source repo turned out to be carrying
unrelated pre-existing modifications that `-A` would have swept into an
unrelated commit. Publishes as a pair with
[`dotfiles-discover`](../dotfiles-discover/SKILL.md), which owns the secret gate
step 4 defers to; this file is not safe to install alone. Exercised on one real
reconciliation run, where `chezmoi apply` would have reverted a day of live
edits and the direction rule above is what caught it. Installed and load-tested
under both Claude Code and Codex.
