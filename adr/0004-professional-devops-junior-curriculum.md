# ADR-0004 — Professional DevOps Junior Curriculum

**Status:** Accepted
**Date:** 2026-08-10
**Context:** Phase 0/1 — Curriculum revision after student request for a professional DevOps deployment track

---

## Decision

Adopt a **professional DevOps Junior curriculum** structured in two tracks:

1. **Core (mandatory):** Linux administration fundamentals, in strict incremental order
   (filesystem → users → permissions → shell → processes → packages → scripting →
   storage/compression → networking/SSH → security → services → Docker → Compose).
2. **Professional (mandatory):** Python for DevOps (as prerequisite for quality gates),
   VPS + **observability**, **code quality gates** (`pytest`, `mypy`, `ruff`, `black`,
   `bandit`, `pip-audit`), **multi-registry publishing** (Docker Hub, GHCR, GitLab
   Registry), **GitHub Actions**, **GitLab CI + self-hosted GitLab Runner** on the VPS,
   and a full production pipeline: commit → quality → build → push → deploy →
   health-check → rollback.

**Explicitly out of scope:** Kubernetes (single small VPS does not need it). **Deferred /
optional:** Terraform/IaC (added as an awareness module + optional stretch at the end)
and app-layer tools (Celery, Watchtower).

## Context & Problem

The student's goal is a **professional deployment**: a VPS that hosts a small future
project following a real production pipeline, exactly as a trusted DevOps Junior would
build it. The original roadmap ended at "Docker + CI/CD basics". The student explicitly
requested a deeper, market-grade DevOps layer (quality gates, unit tests, linters,
security scanners, multiple registries, both CI platforms, a self-hosted runner).

## Alternatives Considered

- **Keep original roadmap without the professional layer** — rejected: leaves the
  portfolio without evidence of real production practice (quality, security, multi-CI).
- **Add Terraform/Kubernetes to the core** — rejected: violates incremental learning and
  the zero-cost principle; a single free VPS does not require cluster orchestration. K8s
  is explicitly recorded as out of scope.
- **Professional track with Python prerequisite (chosen)** — the quality tools
  (`pytest`, `mypy`, `bandit`, `pip-audit`, `ruff`, `black`) are Python ecosystem tools;
  the student must understand Python at a working level before applying them, so a
  "Python for DevOps" module precedes the quality-gate module.

## Why This Option

A DevOps Junior with this profile is credible in the 2026 market: solid Linux
administration + Docker + a real VPS + a production pipeline that enforces **quality and
security gates** and consistently ships to **multiple registries** across **both** CI
platforms, exercised with a real rollback. Observability is included so the server is
not "deployed and forgotten": health checks, resource monitoring, and logs are part of
production.

Terraform stays optional for a deliberate reason: learning to justify *why not* a tool
is as valuable in an interview as learning the tool itself. If the student later grows
the fleet, Terraform becomes the natural next step.

## Consequences

- New modules added to the roadmap: Python for DevOps, Observability, Quality Gates,
  Multi-Registry, GitLab Runner.
- Redis enters as a real administered service (cache scenario). Celery/Watchtower are
  deferred to the optional app-migration track.
- Timeline extended slightly; cadence remains gated by understanding, not calendar.
- Kubernetes remains documented as explicitly out of scope.

## If It Disappeared

The project would become a "Linux labs" repository without professional deployment
evidence — a common portfolio that does not differentiate in a junior DevOps interview.

---
> Supersedes the implicit "Docker/CI basics only" scope of the original roadmap in
> `docs/project-specification.md` (section 3) and `docs/execution-plan.md` (Phases 10–12).