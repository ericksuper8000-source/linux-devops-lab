# Lab 02 — Publishing to GitHub & GitLab

> **Phase:** Phase 3 — Version Control & Repositories
> **Estimated duration:** 1 session
> **Status:** ⬜ Pending
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

- [ ] Concept check: student explains remote vs local (mentor validates).
- [ ] Create the GitHub repository (public, no auto-generated README):
  - [ ] Name: `linux-devops-labs`
  - [ ] Do **not** let GitHub create files (avoids a merge conflict on first push)
- [ ] Create the GitLab repository (public, same name, no auto-generated files).
- [ ] Add the SSH public key to GitHub (`cat ~/.ssh/id_ed25519.pub`).
- [ ] Add the SSH public key to GitLab.
- [ ] Add remotes to the local repo:
  - [ ] `git remote add github git@github.com:<user>/linux-devops-labs.git`
  - [ ] `git remote add gitlab git@gitlab.com:<user>/linux-devops-labs.git`
  - [ ] Verify: `git remote -v`
- [ ] Push to both: `git push -u github main` and `git push -u gitlab main`
- [ ] On both platforms verify:
  - [ ] README renders
  - [ ] Commit history shows the initial commit(s)
  - [ ] `.gitignore` working as expected
- [ ] Update `execution-plan.md` (Phase 3 checkboxes + Current Status), commit, push to both.
- [ ] Update the labs index status in `docs/labs/README.md`.

## Mentor Questions

1. What is the difference between `origin`/`github`/`gitlab` and why did we name remotes explicitly?
2. Why did we tell GitHub *not* to create files on the first push?
3. What would happen if you pushed to only one remote?
4. How would an interviewer use the commit history to understand your learning path?

## Report (student fills after the session)

Follow the template: what you did, commands table, problems, self-explanation, evidence.

> 🚀 **Next:** Phase 4 — Linux Fundamentals (Lab 03 — Filesystem & FHS).
