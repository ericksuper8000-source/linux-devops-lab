# PROJECT SPECIFICATION

> **Project:** Linux DevOps Labs
> **Version:** 3.1 (2026 revision)
> **Status:** Active
> **Type:** Documented practical learning + professional portfolio

---

## 1. Vision

Linux DevOps Labs is a practical learning project that builds the technical competencies
required to work as a **Linux System Administrator (Junior)** and later as a **DevOps
Junior**.

The project does not teach isolated commands or tutorial completion. Its purpose is to
develop the ability to understand, administer, and evolve a Linux server from its
fundamentals to a modern, fully documented infrastructure.

Everything is built publicly as professional evidence of learning.

---

## 2. Main Objective

Build, step by step, a real Linux infrastructure that starts as a clean Debian virtual
machine and evolves into a small production server deployed on a free VPS, administered
with good engineering practices and deployed through CI/CD.

The student must understand each component **before** automating it.

---

## 3. Scope

Included:

- Linux administration and Debian server management
- Users, groups, permissions, filesystems
- Processes, services, logs, package management
- Networking, storage, security
- Automation (Bash, cron, systemd timers)
- Docker and Docker Compose
- VPS and CI/CD (GitHub Actions + GitLab CI + self-hosted GitLab Runner)
- **Professional deployment track (see ADR-0004):**
  code quality gates (`pytest`, `mypy`, `ruff`, `black`, `bandit`, `pip-audit`),
  multi-registry publishing (Docker Hub, GHCR, GitLab Registry),
  observability in production (health checks, monitoring, logs)
- Technical documentation and engineering best practices

Explicitly out of scope:

- Large-enterprise infrastructure, high availability, complex clusters
- Kubernetes (only referenced, never a goal; "why not" is part of the interview defense)

### Tentative extension (optional)

As a final, optional step the student may migrate **their own real Python application**
(a product they plan to sell) to the VPS and build the complete CI/CD pipeline around it.
This is deliberately recorded as **tentative**: it only happens if the student decides to,
once the core project is finished. It never delays or depends on the core roadmap.

---

## 4. Project Story

A company hands the student a freshly installed Debian server. The student plays a Junior
Linux Administrator responsible for progressively turning that server into a modern
environment that hosts applications securely and reproducibly.

Every laboratory is a task that could exist in a professional environment. No isolated
exercises. Every laboratory leaves the server in a better state than before.

---

## 5. Philosophy

### Understand before memorizing

No command memorization. Concepts first.

### Understand before automating

No automation may hide how the system actually works.

### Learn by doing

Every concept is applied immediately in a real laboratory.

### Document everything

Nothing is finished until documented with evidence.

### Evolve one single server

One server evolves across the entire journey. No throwaway projects.

---

## 6. Initial State

The project starts with only:

- Debian installed in VirtualBox (64-bit)
- Basic Linux knowledge
- No Git installed
- No repositories
- No Docker
- No VPS
- No automation

Everything is built from zero, and every step is covered assuming nothing.

---

## 7. Resources

Initial infrastructure:

- VirtualBox + Debian VM (64-bit)
- Personal computer (Windows 10 host)

Future infrastructure:

- GitHub and GitLab (mirrored repositories)
- Docker, Docker Compose
- Free VPS (e.g., Oracle Cloud Free Tier or an equivalent available at that time)
- CI/CD pipelines

Free tools are always prioritized.

### Zero-cost principle

The student currently has no income, so the project **must stay at $0 cost** (or as close
as technically possible). Every cloud service, tool, and domain choice must be free-tier
or free. If a paid option is ever required, it must be justified, discussed with the
mentor, and explicitly approved **before** any expense. Cloud provider strategy is
recorded in ADR-0003.

---

## 8. Methodology

Every session follows the same structure:

1. Review of the previous session.
2. Validation questions.
3. Conceptual explanation (why first).
4. Professional scenario.
5. Practical laboratory.
6. Technical discussion.
7. Documentation and evidence.
8. State update and definition of the next laboratory.

Do not advance while conceptual gaps exist.

Additionally, **every day begins with a recap mini-session**: the mentor summarizes the
journey so far in the simplest possible language and validates understanding with **one
question at a time** (commands, decisions, processes) before any new progress is made.
Gaps turn the day into reinforcement instead of progress. See `AGENTS.md`.

---

## 9. Learning Architecture

Knowledge is built in layers, and each layer depends on full understanding of the
previous one:

```
Hardware
  ↓
Operating System
  ↓
Linux Administration
  ↓
Services
  ↓
Docker
  ↓
Infrastructure
  ↓
VPS
  ↓
CI/CD
```

---

## 10. Roadmap (Phases)

| # | Phase | Description |
|---|---|---|
| 0 | Planning | Documentation architecture, methodology, roles |
| 1 | VM Environment Setup | VirtualBox + Debian ready, shared folder, workspace |
| 2 | Meeting Debian | Observe the clean installation (Lab 00) |
| 3 | Version Control | Install Git early; publish to GitHub & GitLab |
| 4 | Linux Fundamentals | Filesystem, files, users, groups, permissions |
| 5 | System Administration | Processes, systemd, logs, packages, Bash, automation |
| 6 | Storage | Disks, partitions, filesystems, mount, LVM, swap |
| 7 | Networking | TCP/IP, DNS, SSH, diagnostics |
| 8 | Security | Hardening, firewall, updates, audit |
| 9 | Services | Nginx, PostgreSQL, backups |
| 10 | Docker | Engine, images, containers, volumes, Compose |
| 11 | VPS | Provision and reproduce the environment |
| 12 | CI/CD | GitHub Actions, GitLab CI, auto-deploy |
| 13 | Final Project | Full stack, HTTPS, portfolio & interview |

> Detailed checklists and current status: [`execution-plan.md`](execution-plan.md)

---

## 11. Expected Competencies

By the end of the project, the student can:

- Administer a Debian server
- Manage users, groups, and permissions
- Understand the Linux filesystem
- Administer processes and services
- Troubleshoot common problems
- Configure services
- Automate tasks
- Administer Docker
- Maintain a VPS
- Deploy applications via CI/CD
- Explain every technical decision made

---

## 12. Documentation

Professional documentation is produced for the whole project. Each lab includes, when
applicable: objective, context, procedure, technical explanation, commands used,
screenshots, problems encountered, solutions, and conclusions.

Reasoning behind decisions is captured as **Architecture Decision Records (ADRs)** in
`adr/`, making the "why" interview-ready.

---

## 13. Repositories

The project is published on **GitHub** and **GitLab** (mirrored). Version control is
introduced early — immediately after Lab 00 — so the entire evolution is visible in real
time from the clean installation onward.

Every commit represents meaningful progress. Documentation carries the same weight as
technical implementation.

---

## 14. Restrictions

- No tool is introduced before the problem it solves is understood.
- No tutorial is copied without understanding.
- No command memorization.
- No skipped documentation.
- No rushing that sacrifices understanding.

---

## 15. Success Criteria

The project is successful when there is evidence that the student can:

- Administer Linux with judgment
- Diagnose problems
- Justify technical decisions
- Document professionally
- Build a small modern infrastructure
- Deploy applications through CI/CD to a free VPS

The result must constitute a portfolio that shows the full evolution of learning and lets
an interviewer understand the technical level reached.

---

## 16. Related Documents

This project is supported by the following coherent document set:

- **`AGENTS.md`** — operating manual for any AI mentor on this repo
- **`docs/mentor-constitution.md`** — pedagogical and technical principles of the mentor
- **`docs/execution-plan.md`** — sequential execution state and checklists
- **`docs/learning-roadmap.md`** — competency map and progress
- **`docs/session-log.md`** — daily session diary
- **`docs/setup.md`** — VM environment setup

All are part of a single documentation architecture and must stay coherent with each other.

---

## 17. Tentative Extension — The Student's Own App

The student maintains a real Python application they intend to sell. As an **optional
final step**, after the VPS and CI/CD are working, the student may:

- migrate the application (containerized) to the VPS,
- build its complete pipeline: commit → build → test → deploy → rollback,
- make the VPS its permanent home.

This step is **tentative by design** — it may never happen. It is recorded in the
documentation (execution-plan Labs 44–45, marked ⭐ Optional) so the plan can absorb it
without pressure. Nothing in the core roadmap depends on it, and it costs nothing extra:
both the VPS and the CI/CD pipeline are already free-tier.

---

## Guiding Principle

> The goal of this project is not to learn Linux commands.
> The goal is to develop the technical judgment to think, act, and solve problems like a
> Junior Linux Administrator — using a real project as public evidence of that learning.
