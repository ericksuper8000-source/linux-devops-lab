# ADR-0003 — Zero-Cost Cloud Strategy

**Status:** Accepted
**Date:** 2026-08-03
**Context:** Phase 0 — Planning (requirements update: budget constraint)

---

## Decision

The project **must stay at $0 cost** for as long as possible (ideally forever). Every
cloud service, tool, and domain must be free-tier or free. Any expense requires explicit
justification, mentor discussion, and student approval **before** it happens.

For the VPS migration (Phase 11), the current first choice is a **free-tier provider** —
at the time of writing, **Oracle Cloud Free Tier** (Always Free) is the strongest
candidate because it offers permanent free VMs with usable resources, but the decision is
revisited at Phase 11 based on what is still available for free at that moment.

## Context & Problem

The student currently has no income. A realistic project must not silently accumulate
costs (a VPS, a domain, a monitoring service). This constraint shapes decisions across
the whole roadmap: cloud provider, CI minutes, registries, DNS, and certificates.

## Alternatives Considered

- **Paid VPS (e.g., a few USD/month)** — rejected: violates the $0 constraint.
- **Oracle Cloud Free Tier (chosen candidate)** — Always Free ARM/x86 VMs; best resource
  profile among free tiers. Downside: account verification friction and historical
  free-tier availability changes — must be re-verified at Phase 11.
- **Other free options (Google Cloud free tier, AWS Free Tier, free plans of Fly.io /
  Render / Railway)** — valid backups; each has limits (time-bounded or resource-thin) and
  is re-evaluated when we reach Phase 11.
- **Keep everything local (no VPS at all)** — always available as a fallback; the labs
  remain fully valid in the VM.

## Why This Option

The zero-cost principle is not a preference — it is a hard requirement given the student
has no income. Free tiers (especially Oracle Cloud Free Tier) give enough resources for
the exact scope of this project: a small Dockerized stack (Nginx + PostgreSQL + app) plus
CI/CD. If free tiers disappear, the project falls back to the local VM rather than paying.

## Consequences

- Cloud, domain, DNS, CI, and registry choices are all constrained to free tiers.
- Oracle Cloud Free Tier is the default candidate, **not a locked decision** — it is
  re-verified in Phase 11 and recorded in the lab report.
- Any future expense needs an explicit "cost request" discussion with the mentor.
- The tentative app-migration step (Labs 44–45) is also $0: the same free VPS and
  free CI minutes cover it.

## If It Disappeared

Without this constraint, small costs would accumulate quietly. With it, the project
remains viable with no income — and the portfolio gains a realistic engineering
discipline: designing within hard constraints.
