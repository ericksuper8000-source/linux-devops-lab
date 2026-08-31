# ADR-0001 — Version Control from Day One

**Status:** Accepted
**Date:** 2026-08-03
**Context:** Phase 0 — Planning (documentation architecture restructure)

---

## Decision

Git is installed and the repository is created **immediately after Lab 00** (Phase 3),
so the public evolution of the project is versioned from the very beginning instead of
waiting several months.

## Context & Problem

The original plan placed Git in a "Git & Documentation" phase several months into the
project. However, a core requirement of the project is that an interviewer can watch the
progress **in real time** in the public repositories. If Git arrives late, the earliest
weeks of learning (Meeting Debian, first observations) are invisible in version history.

## Alternatives Considered

- **Git at month 3 (original plan)** — respects "no tool before need" strictly, but
  hides the most impressive part of the story: the clean server and its first
  observations.
- **Git after Lab 00 (chosen)** — versioning is introduced as soon as there is
  documentation to protect, which is a genuine, non-artificial need.
- **Git immediately, before any Linux** — rejected: version control without any content
  to version teaches nothing and violates incremental learning.

## Why This Option

There is a real need the moment documentation exists: protecting and sharing it. Lab 00
produces the first documents and evidence, so committing them right after is natural —
not premature. It also gives the student the most valuable portfolio asset early:
a visible, growing commit history starting from a clean install.

## Consequences

- Lab 00 is the first commit; the commit history becomes the narrative.
- Git is introduced before package management, storage, and networking — acceptable
  because its need (protecting work) is already present, and Lab 01/02 are scoped to
  Git basics only.
- The execution plan moves Git to Phase 3, immediately after Lab 00.

## If It Disappeared

Without early versioning, the public repositories would start weeks or months late and
the earliest (and most honest) part of the story would be lost.
