# ADR-0002 — Mirror Repositories on GitHub and GitLab

**Status:** Accepted
**Date:** 2026-08-03
**Context:** Phase 0 — Planning (repository strategy)

---

## Decision

The project is published as a **mirrored pair**: the same repository is pushed to both
GitHub and GitLab. The canonical working copy lives inside the Debian VM
(`~/linux-devops-labs`); both platforms receive every push.

## Context & Problem

The student wants a clean, visible portfolio that an interviewer can explore. The two
most common platforms in the industry are GitHub and GitLab, and companies use each with
different CI ecosystems (GitHub Actions vs GitLab CI). The project later uses **both**
CI systems (Phase 12), so both hosting accounts are needed anyway.

## Alternatives Considered

- **GitHub only** — simplest, but loses GitLab CI experience and the breadth of having
  both platforms on the CV.
- **GitLab only** — same, reversed.
- **Both, mirrored (chosen)** — one working copy, two remotes, zero extra maintenance
  beyond a second `git push`.

## Why This Option

Mirroring costs almost nothing (one additional remote) and doubles the portfolio surface.
Both CI platforms are used later, so the accounts and familiarity are needed regardless.
The canonical copy stays in the VM — the environment where all real work happens — and
both remotes simply receive the same history.

## Consequences

- `git remote -v` shows two origins (`github`, `gitlab`); every push goes to both.
- Repos on both platforms must stay public and in sync; the Definition of Done includes
  "pushed to both".
- CI workflows are developed and compared on both platforms (Labs 34–35).

## If It Disappeared

The portfolio would be limited to one platform, and the later comparison of GitHub
Actions vs GitLab CI would lose its natural home.
