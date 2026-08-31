# Lab 01 — Installing & Configuring Git

> **Phase:** Phase 3 — Version Control & Repositories
> **Estimated duration:** 1 session
> **Status:** ⬜ Pending
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

- [ ] Concept check: the student explains why version control is needed (mentor validates).
- [ ] Install Git: `sudo apt update && sudo apt install -y git`
- [ ] Configure identity:
  - [ ] `git config --global user.name "<Your Name>"`
  - [ ] `git config --global user.email "<your email>"`
  - [ ] `git config --global init.defaultBranch main`
- [ ] Configure a text editor (nano is fine for now; justify the choice).
- [ ] Generate an SSH key pair: `ssh-keygen -t ed25519 -C "<your email>"`
  - [ ] Explain why ed25519 and why a passphrase.
- [ ] Initialize the repository: `git init` inside `~/linux-devops-labs`
- [ ] Verify `.gitignore` excludes `_archive/` and junk:
  - [ ] `git status` shows only intended files
- [ ] Stage and review: `git add .` then `git diff --cached` (learn to inspect before committing)
- [ ] **First commit:** `git commit -m "docs: initialize linux devops labs repository"`
- [ ] Show history: `git log --oneline`
- [ ] Verify nothing sensitive is tracked (no `.env`, keys, personal data)

## Mentor Questions

1. What is the difference between `git add` and `git commit`?
2. Why do we use SSH keys instead of passwords to authenticate?
3. Why does `git config --global` matter vs per-repo config?
4. What is the difference between a working tree, the index, and the repository?

## Report (student fills after the session)

Follow the template: what you did, commands table, problems, self-explanation, evidence.

> 🚀 **Next:** Lab 02 — Publishing to GitHub & GitLab, where this history becomes public.
