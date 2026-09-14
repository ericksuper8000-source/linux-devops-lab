# Linux DevOps Labs

> Turning a clean Debian installation into a modern, self-hosted infrastructure — laboratory by laboratory, publicly documented from day one.

**Type:** Practical learning project + professional portfolio
**Duration:** ~12 months (2 sessions/week)
**Language:** English (public documentation)

---

## The Story

If you are interviewing me a year from now, this is what you will find: a repository that does not start with a finished product. It starts with a clean, freshly installed Debian server in a virtual machine — no Git, no Docker, no VPS, no automation. Only a vanilla operating system.

Then, laboratory by laboratory, the story unfolds:

1. First, I **meet** the server and learn to observe a clean Linux system.
2. I install **Git** and start versioning everything publicly on **GitHub** and **GitLab** from the very beginning.
3. I learn **Linux fundamentals** — filesystem, inodes, users, groups, permissions — not as commands, but as concepts.
4. I learn to **administer** the system: processes, systemd, logs, packages, scripts, automation.
5. I learn **storage**, **networking**, and **security**.
6. I install real **services** (Nginx, PostgreSQL).
7. When services become painful to manage, I introduce **Docker** and **Docker Compose** — not because they are trendy, but because I understand the problem they solve.
8. I migrate the whole environment to a **free VPS**.
9. I automate deployment with a professional **CI/CD pipeline**: quality gates (pytest, mypy, ruff, black, bandit, pip-audit), multi-registry publishing (Docker Hub, GHCR, GitLab Registry), and a self-hosted GitLab Runner.
10. The server ends as a small, modern, documented infrastructure running a FastAPI application with PostgreSQL, Nginx, and HTTPS — and, as a **tentative optional** final step, my own real Python product is migrated here with its own CI/CD pipeline.

Every step is documented with evidence, screenshots, and the reasoning behind each decision. This is not a tutorial; it is a complete engineering journey.

Every session begins with a **recap mini-session**: I explain back what I learned, one question at a time, so understanding is real — not memorized.

---

## Why This Project Exists

This project is not about memorizing commands. It is about building **technical judgment** — the ability to explain why each piece exists, how the components communicate, and how to diagnose a problem when something breaks.

The goal is that after a year, when asked *"Why did you configure those permissions?"*, *"What does systemd actually do?"*, or *"Why Docker Compose instead of installing PostgreSQL directly?"*, the answer comes from real understanding, not from a copied tutorial.

---

## Cost Policy

The project is built to cost **$0**. All tools, cloud services, and domains are free-tier or free. The student has no income during the project, so any expense must be justified, discussed with the mentor, and explicitly approved before it happens. Cloud provider strategy is documented in [`docs/adr/0003-zero-cost-cloud-strategy.md`](docs/adr/0003-zero-cost-cloud-strategy.md).

---

## Repository Layout

```
.
├── AGENTS.md                     # Operating manual for any AI mentor working on this repo
├── docs/
│   ├── project-specification.md  # Vision, scope, success criteria
│   ├── mentor-constitution.md    # Pedagogical & technical principles of the mentor
│   ├── learning-roadmap.md       # Competency map — "you are done when you can..."
│   ├── execution-plan.md         # ⭐ THE status file — phases, checklists, current state
│   ├── session-log.md            # Daily diary (reverse-chronological)
│   ├── setup.md                  # VM environment setup (VirtualBox + Debian)
│   ├── adr/                      # Architecture Decision Records
│   └── labs/                     # One document per laboratory
├── screenshots/                  # Evidence, one folder per lab
├── scripts/                      # Scripts created during labs
└── .gitignore
```

---

## Phase Map

| Phase | Topic | Status |
|---|---|---|
| 0 | Planning & Documentation Architecture | ✅ Complete |
| 1 | VM Environment Setup | ✅ Complete |
| 2 | Meeting Debian | ✅ Complete |
| 3 | Version Control & Repositories | ✅ Complete |
| 4 | Linux Fundamentals | 🔄 In Progress (Labs 03–05 ✅) |
| 5 | System Administration | ⬜ Pending |
| 6 | Storage | ⬜ Pending |
| 7 | Networking | ⬜ Pending |
| 8 | Security | ⬜ Pending |
| 9 | Services | ⬜ Pending |
| 10 | Docker | ⬜ Pending |
| 11 | VPS + Observability | ⬜ Pending |
| 12 | CI/CD — Professional Pipeline (quality gates, multi-registry, GitLab Runner) | ⬜ Pending |
| 13 | Final Project & Portfolio | ⬜ Pending |

> **Live status:** see [`docs/execution-plan.md`](docs/execution-plan.md) — the single source of truth for what is done and what is next.

---

## How This Repository Is Maintained

- **Single source of truth:** [`docs/execution-plan.md`](docs/execution-plan.md) stores the current phase, the current lab, and every checkbox. It is updated at the end of every session.
- **Daily recap ritual:** every day starts with a recap mini-session — the AI summarizes the journey simply and validates understanding with one question at a time before any progress (see [`AGENTS.md`](AGENTS.md)).
- **AI-friendly:** Any AI agent that joins the project follows the bootstrap protocol in [`AGENTS.md`](AGENTS.md), which guarantees instant recall of what exists, what is done, and what is next.
- **Definition of Done:** a lab is finished only when it is documented, evidenced, committed, and pushed to **both** GitHub and GitLab.
- **Mirrored repositories:** the project lives in the Debian VM and is pushed to GitHub and GitLab in parallel.
- **Zero cost:** the whole project runs on free-tier services (see Cost Policy).

---

## First Steps

1. ✅ Read [`docs/setup.md`](docs/setup.md) and prepare the VirtualBox environment.
2. ✅ Complete **Lab 00 — Meeting Your Debian Server** ([`docs/labs/lab-00-meeting-debian.md`](docs/labs/lab-00-meeting-debian.md)).
3. ✅ Set up Git and publish the repository (Labs 01–02) — project is public on GitHub + GitLab.
4. 🔄 **Next:** Phase 4 — Lab 03 — Filesystem & FHS.

---
