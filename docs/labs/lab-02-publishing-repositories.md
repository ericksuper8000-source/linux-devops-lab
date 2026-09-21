# Lab 02 — Publishing to GitHub & GitLab

> **Phase:** Phase 3 — Version Control & Repositories
> **Estimated duration:** 1 session
> **Status:** ✅ Complete (2026-08-31, Session 07)
> **Prerequisites:** Lab 01 (git installed, first commit made)

---

## Objective

Create the public repositories on **GitHub** and **GitLab**, push the project history to
both, and verify the repository renders correctly as a professional portfolio from its
very first commit.

## Scenario (real world)

Your work is now under version control, but it still only exists on your machine. The
project's core promise is public, real-time evolution. Publishing to both platforms
makes that promise real and sets up the dual-CI strategy used later (ADR-0002).

## Concepts (why first)

- Remote vs local repository; what `git remote` is.
- What a "remote URL" is and the difference between SSH and HTTPS forms.
- Why pushing the **history** (not just files) matters for the portfolio.
- Why two platforms: portfolio breadth + later CI comparison (ADR-0002).
- The Definition of Done: everything is committed AND pushed to both.

## Checklist

- [x] Concept check: student explains remote vs local (mentor validates).
- [x] Create the GitHub repository (public, no auto-generated README):
  - [x] Name: `linux-devops-lab`
  - [x] Do **not** let GitHub create files (avoids a merge conflict on first push)
- [x] Create the GitLab repository (public, same name, no auto-generated files).
- [x] Add the SSH public key to GitHub (`cat ~/.ssh/id_ed25519.pub`).
- [x] Add the SSH public key to GitLab.
- [x] Add remotes to the local repo:
  - [x] `git remote add github git@github.com:ericksuper8000-source/linux-devops-lab.git`
  - [x] `git remote add gitlab git@gitlab.com:ericksuper80/linux-devops-lab.git`
  - [x] Verify: `git remote -v`
- [x] Push to both: `git push -u github main` and `git push -u gitlab main`
- [x] On both platforms verify:
  - [x] README renders
  - [x] Commit history shows the initial commit(s)
  - [x] `.gitignore` working as expected
- [x] Update `execution-plan.md` (Phase 3 checkboxes + Current Status), commit, push to both.
- [x] Update the labs index status in `docs/labs/README.md`.

> ✅ **Completed 2026-08-31 (Session 07).** Project published on both platforms. GitHub user
> `ericksuper8000-source`, GitLab user `ericksuper80`. VM ed25519 public key added to both
> (`Debian VM`). SSH validated on both (`ssh -T git@github.com` / `git@gitlab.com`). Both
> remotes connected and pushed (`Everything up-to-date`); README + commit history verified.
> A note: the **passphrase** (set at `ssh-keygen` time) is prompted by the local keyring and
> is distinct from the Debian login password.

## Mentor Questions

1. What is the difference between `origin`/`github`/`gitlab` and why did we name remotes explicitly?
2. Why did we tell GitHub *not* to create files on the first push?
3. What would happen if you pushed to only one remote?
4. How would an interviewer use the commit history to understand your learning path?

## Report (student fills after the session)

### What I did

Published the project to both platforms: added the VM's ed25519 public key to GitHub (`ericksuper8000-source`) and GitLab (`ericksuper80`) as `Debian VM`, validated SSH to both, created public repo `linux-devops-lab` on each (no auto-generated files), added both remotes, pushed `main` to both, and verified README + history render.

### How it works / why

A local repo is invisible; `git remote` points to a hosted copy and `git push` shares history (not just files). SSH URL form uses key-based auth — the public lock lives on GitHub/GitLab, the private key stays in the VM. Letting the platform auto-create README would diverge history and cause a merge conflict on first push, so both repos were created empty. Two platforms = portfolio breadth + later CI comparison (ADR-0002). `-u` on first push sets upstream tracking.

### Commands I used

| Command | Why I used it |
|---|---|
| `cat ~/.ssh/id_ed25519.pub` | Copy VM public key to both platforms |
| `ssh -T git@github.com` | Validate SSH auth to GitHub |
| `ssh -T git@gitlab.com` | Validate SSH auth to GitLab |
| `git remote add github git@github.com:ericksuper8000-source/linux-devops-lab.git` | Register GitHub remote |
| `git remote add gitlab git@gitlab.com:ericksuper80/linux-devops-lab.git` | Register GitLab remote |
| `git remote -v` | Verify fetch + push URLs for both |
| `git push -u github main` | First push to GitHub, set upstream |
| `git push -u gitlab main` | First push to GitLab, set upstream |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| `ssh -T` prompted to unlock private key | gnome-keyring asking for SSH passphrase (not Debian login password) | Entered passphrase set at `ssh-keygen` time; keyring remembers it for the session |

### Lessons learned / self-explanation

Remote vs local: local history exists only on my machine until pushed. Named remotes (`github`/`gitlab` instead of single `origin`) make dual-push explicit. Pushing to only one remote would break the mirror promise — portfolio and CI comparison depend on both staying in sync. An interviewer reads commit history as a learning timeline, which is why meaningful messages matter from day one.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-02/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended (Session 07, 2026-08-31)
- [x] Execution plan updated
- [x] Committed and pushed to GitHub + GitLab

> 🚀 **Next:** Phase 4 — Linux Fundamentals (Lab 03 — Filesystem & FHS).
