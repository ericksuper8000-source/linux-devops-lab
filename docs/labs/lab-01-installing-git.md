# Lab 01 — Installing & Configuring Git

> **Phase:** Phase 3 — Version Control & Repositories
> **Estimated duration:** 1 session
> **Status:** ✅ Complete (2026-08-31, Session 07)
> **Prerequisites:** Lab 00 complete; baseline snapshot exists

---

## Objective

Understand why version control exists, install Git in the Debian VM, configure it
correctly, and make the **first commit** of the whole project.

## Scenario (real world)

Everything you have built (Lab 00 report, screenshots, all documentation) lives in files
with no history. You want to fix a file and find it two weeks later; you want an
interviewer to see your evolution; you want a safety net. That is exactly the problem
Git solves — and now there is a real, material need for it.

## Concepts (why first)

- What problem version control solves (history, rollback, collaboration, evidence).
- Working directory → staging area → repository (the three states).
- What a commit is and what makes a commit *meaningful*.
- Why authentication to GitHub/GitLab uses **SSH keys** instead of passwords.
- Git is **local first** — `git commit` works offline; `git push` shares.

## Checklist

- [x] Concept check: the student explains why version control is needed (mentor validates).
- [x] Install Git: `sudo apt update && sudo apt install -y git`
- [x] Configure identity:
  - [x] `git config --global user.name "Erick_Dev"`
  - [x] `git config --global user.email "ericksuper80@gmail.com"`
  - [x] `git config --global init.defaultBranch main`
- [x] Configure a text editor (nano is fine for now; justify the choice).
- [x] Generate an SSH key pair: `ssh-keygen -t ed25519 -C "ericksuper80@gmail.com"`
  - [x] Explain why ed25519 and why a passphrase.
- [x] Initialize the repository: `git init` inside `~/linux-devops-labs`
- [x] Verify `.gitignore` excludes `_archive/` and junk:
  - [x] `git status` shows only intended files
- [x] Stage and review: `git add .` then `git diff --cached` (learn to inspect before committing)
- [x] **First commit:** `git commit -m "docs: initialize linux devops labs repository"`
- [x] Show history: `git log --oneline`
- [x] Verify nothing sensitive is tracked (no `.env`, keys, personal data)

> ✅ **Completed 2026-08-31 (Session 07).** Identity configured to match the Windows host
> (`Erick_Dev` / `ericksuper80@gmail.com`) so authorship is consistent across machines.
> ed25519 SSH key generated in the VM (not copied from Windows). Public key saved at
> `C:\Users\XPC\Desktop\Archivo.txt` for adding to GitHub/GitLab in Lab 02. The repository
> `.git` lives inside the VM at `~/linux-devops-labs` (host folder has no `.git`).

## Mentor Questions

1. What is the difference between `git add` and `git commit`?
2. Why do we use SSH keys instead of passwords to authenticate?
3. Why does `git config --global` matter vs per-repo config?
4. What is the difference between a working tree, the index, and the repository?

## Report (student fills after the session)

### What I did

Installed Git in the Debian VM, configured identity to match the Windows host (`Erick_Dev` / `ericksuper80@gmail.com`), generated a dedicated ed25519 SSH key pair inside the VM, initialized the repo at `~/linux-devops-labs`, and made the first commit of the whole project documentation.

### How it works / why

Git is local-first: `git commit` freezes a snapshot offline, `git push` shares it later. The three states are working directory → staging area (index) → repository. `git add` moves files to staging, `git commit` freezes staging into history. Identity (`user.name`/`user.email`) is per-machine config — same values on Windows and VM keep authorship consistent. SSH keys are per-OS: the VM generated its own pair, no private key was copied from Windows. The public key is the lock shared with servers, the private key never leaves the machine.

### Commands I used

| Command | Why I used it |
|---|---|
| `sudo apt update && sudo apt install -y git` | Install Git on Debian |
| `git config --global user.name "Erick_Dev"` | Set authorship identity (match Windows host) |
| `git config --global user.email "ericksuper80@gmail.com"` | Set authorship email |
| `git config --global init.defaultBranch main` | Use `main` as default branch |
| `ssh-keygen -t ed25519 -C "ericksuper80@gmail.com"` | Generate VM-only SSH key pair |
| `cat ~/.ssh/id_ed25519.pub` | Show public key to add to GitHub/GitLab in Lab 02 |
| `git init` | Initialize repo in `~/linux-devops-labs` |
| `git status` | Verify only intended files tracked |
| `git add .` | Stage everything |
| `git diff --cached` | Inspect staged changes before committing |
| `git commit -m "docs: initialize linux devops labs repository"` | First commit |
| `git log --oneline` | Confirm history |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| None reported | — | — |

### Lessons learned / self-explanation

Version control solves history, rollback, and evidence: without it, fixing a file two weeks later is guesswork. `git add` stages, `git commit` freezes. Global config applies to all repos on that machine; per-repo config would override it. The working tree is what I edit, the index is what I staged, the repository is frozen history. SSH beats passwords because the private key never travels — the server holds the public lock.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-01/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended (Session 07, 2026-08-31)
- [x] Execution plan updated
- [x] Committed and pushed to GitHub + GitLab (push completed in Lab 02)

> 🚀 **Next:** Lab 02 — Publishing to GitHub & GitLab, where this history becomes public.
