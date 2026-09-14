# Laboratories

## Index & Evidence Rules

**Project:** Linux DevOps Labs

---

## Index

| Lab | Title | Phase | Status |
|---|---|---|---|
| 00 | [Meeting Your Debian Server](lab-00-meeting-debian.md) | 2 | ✅ Complete |
| 01 | [Installing & Configuring Git](lab-01-installing-git.md) | 3 | ✅ Complete |
| 02 | [Publishing to GitHub & GitLab](lab-02-publishing-repositories.md) | 3 | ✅ Complete |
| 03 | [Filesystem & FHS](lab-03-filesystem-fhs.md) | 4 | ✅ Complete |
| 04 | [Files, Inodes & Links](lab-04-files-inodes-links.md) | 4 | ✅ Complete |
| 05 | [Users & Groups](lab-05-users-groups.md) | 4 | ✅ Complete |

> More labs are created progressively — each one is written in detail only when we reach
> its phase (see `docs/execution-plan.md` for the full roadmap).

### Optional / tentative (final step — may never happen)

| Lab | Title | Phase | Status |
|---|---|---|---|
| 44 | Migrating a Real Python App | 13 | ⭐ Optional |
| 45 | Real App CI/CD Pipeline | 13 | ⭐ Optional |

> These labs are **tentative by design**: they only happen if the student decides to,
> after the core project is finished. Files are created when (if) the decision is made.
> They are recorded so the plan can absorb them without pressure.

---

## Evidence Rules

Every lab produces **evidence** — proof that the work happened and can be reproduced.

### Screenshots

- One folder per lab: `screenshots/lab-00/`, `screenshots/lab-01/`, …
- Name files descriptively: `01-version-info.png`, `02-users-list.png`, …
- Capture what matters (commands + output), not the whole screen.
- On the VM, you can take host screenshots (Windows) or use a tool like `scrot`/`import`
  (introduced later). The mentor will show you the cleanest option for your setup.

### Command logs

- Save meaningful command output as text files under `screenshots/lab-NN/` when a
  screenshot is not practical.

### Reproducibility

- Another person must be able to follow the lab document and get the same result.
- Include every command with a one-line "why".

---

## Definition of Done (applies to every lab)

A lab is complete when **all** are true:

- [ ] All checklist items in the lab document are ticked.
- [ ] The **Report** section at the bottom of the lab is filled by the student.
- [ ] Evidence exists in `screenshots/lab-NN/`.
- [ ] ADR written if a meaningful decision was made.
- [ ] `session-log.md` has a new entry.
- [ ] `execution-plan.md` checkboxes + Current Status updated.
- [ ] Committed and pushed to **both** GitHub and GitLab.
- [ ] The student can explain the lab back to the mentor (mentor validation passed).

---

## Lab Template

Every lab file follows `_template.md`. The template guarantees consistency, which makes
the repository easy to read for an interviewer and easy to resume for an AI.
