# EXECUTION PLAN

## Sequential Execution State & Checklists

**Project:** Linux DevOps Labs
**Version:** 2.1 (2026 revision)
**Status:** In Progress

---

## How to Use This File

This is the **single source of truth** for project status. It does not contain theory or
labs — it tells you exactly where the project is and what to do next.

- **Every day starts with the recap mini-session** (see `AGENTS.md` — Daily Recap &
  Validation), then reads the **Current Status** block below.
- **Every session ends** by updating the **Current Status** block and ticking every
  checkbox completed during that session.
- A phase or lab is only marked complete when it is **understood, documented,
  evidenced, committed, and pushed** (see Definition of Done in `AGENTS.md`).
- Any AI agent joining the project reads this file first (see `AGENTS.md`).

---

## 📌 CURRENT STATUS

> **This block is updated at the end of every session.**

- **Current phase:** Phase 4 — Linux Fundamentals (🔄 in progress)
- **Current lab / task:** Lab 04 ✅ Complete. Next: Lab 05 — Users & Groups (`docs/labs/lab-05...` — pending creation)
- **Phase 1 (VM Setup):** ✅ Complete
- **Phase 2 (Meeting Debian):** ✅ Complete
- **Phase 3 (Version Control):** ✅ Complete (Labs 01–02)
- **Last completed item:** Lab 04 — Files, Inodes & Links: inodes, hard links vs soft links, `ls -li`, `stat`, `file`, practical use cases
- **Daily recap status:** N/A — protocol not applied today (starts from 2026-09-08 onward)
- **Next session target:** Lab 05 — Users & Groups (concept-first: UID/GID, `/etc/passwd`, `/etc/shadow`, `/etc/group`, primary vs secondary groups, `useradd`, `usermod`, `groupadd`, `id`, scenario: onboarding a new developer)
- **Blockers / open questions:**
  - SSH service not running — investigate in Lab 19.
- **Environment architecture (confirmed 2026-09-07):** `Linux VPS - Project` (Windows) = project memory/
  instructions (AI-edited). `~/linux-devops-labs` (VM) = real project/repo with `.git` (what gets pushed).
  Windows folder is mounted into the VM at `/mnt/host` via VirtualBox shared folder (tag `linux-vps-project`).
  Shared folder must be manually mounted: `sudo mount -t vboxsf linux-vps-project /mnt/host`.
- **Git identity (applied in VM):** `user.name = Erick_Dev`, `user.email = ericksuper80@gmail.com`. Same identity across Windows + VM. VM SSH keys generated separately. GitHub username `ericksuper8000-source`, GitLab username `ericksuper80`. VM public key added to both platforms (`Debian VM`).
- **Repo name (clarified 2026-09-07):** The repo on GitHub/GitLab is `linux-devops-lab` (WITHOUT trailing 's'). The local workspace folder is `~/linux-devops-labs` (WITH 's'). Remote URLs: `git@github.com:ericksuper8000-source/linux-devops-lab.git` and `git@gitlab.com:ericksuper80/linux-devops-lab.git`.
- **Session protocol (established 2026-09-07):** Every session starts with 3 mandatory steps: (1) Academia Deploy reminder, (2) Summary of the journey, (3) One-question-at-a-time validation. Documented in AGENTS.md CRITICAL RULE.
- **Last session:** Session 08 — Lab 03 completed (Filesystem & FHS explored, FHS contract understood, absolute/relative paths, `ls -la`, symlinks)
- **Last commit / push:** Pending — Lab 03 changes need to be committed and pushed by student.

---

## General Status

| Item | State |
|---|---|
| Project | ☒ In progress |
| Plan | ☒ Defined |
| Zero-cost policy | ☒ Active (ADR-0003) |
| Version control | ☒ Active (Git installed, repo initialized, first commit) |
| Public repositories (GitHub + GitLab) | ☒ Created & pushed (linux-devops-lab public on both) |
| Server evolution | ⬜ Not started |

---

## Phase 0 — Planning & Documentation Architecture

**Objective:** Fully define the project before touching the system.

- [x] Define the general objective
- [x] Define the methodology
- [x] Define the project philosophy
- [x] Define the mentor role
- [x] Define the student role
- [x] Create the Project Specification
- [x] Create the Execution Plan
- [x] Create the Learning Roadmap
- [x] Define the documentation strategy
- [x] Define the repository structure
- [x] Decide to version from day one (see ADR-0001)
- [x] Decide to mirror GitHub + GitLab (see ADR-0002)
- [x] Define the daily recap & validation ritual
- [x] Adopt the zero-cost principle (see ADR-0003)
- [x] Record the tentative optional final step (migrate the student's own app)
- [x] Redefine the curriculum as the Professional DevOps Junior track (see ADR-0004)

**Status:** ✅ COMPLETE

---

## Phase 1 — VM Environment Setup

**Objective:** Prepare a clean, safe, reproducible environment. Nothing learned yet — this
is pure preparation so that no later step depends on unstated assumptions.

**Estimated duration:** 1–2 sessions

- [x] **Setup 01 — Create the Debian VM in VirtualBox** (details in `docs/setup.md`)
  - [x] Verify VirtualBox is installed on the Windows host (7.2.4 r170995)
  - [x] Confirm the Debian 64-bit VM exists and boots (VM pre-existed; verified, not re-created)
  - [x] Confirm VM resources: 3 vCPU, 2048 MB RAM, 30 GB VDI, NAT
  - [x] Confirm Debian install: 13 (trixie), SSH server + standard utilities
  - [x] Log in and verify the system boots cleanly (user `Erick`, hostname `Debian`)
- [x] **Setup 02 — Install VirtualBox Guest Additions**
  - [x] Confirm Guest Additions installed (module `vboxguest` loaded)
  - [x] Reboot and confirm they load
- [x] **Setup 03 — Configure the shared folder**
  - [x] Share the host project folder with the VM (name `linux-vps-project`)
  - [x] Mount the shared folder in Debian at `/mnt/host` and verify read/write
- [x] **Setup 04 — Create the project workspace**
  - [x] Create the workspace folder in the VM (`~/linux-devops-labs`)
  - [x] Copy the project template from the shared folder
  - [x] Verify the structure matches `README.md`
- [x] **Setup 05 — Take the baseline snapshot**
  - [x] Snapshot the clean VM (rollback point for the whole project): `baseline-clean-debian`
  - [x] Document the snapshot in `session-log.md`

**Status:** ✅ COMPLETE

---

## Phase 2 — Meeting Debian

**Objective:** Understand what we received when Debian was installed. **Observe only —
no modifications.**

**Estimated duration:** 1–2 sessions

- [ ] **Lab 00 — Meeting Your Debian Server** (`docs/labs/lab-00-meeting-debian.md`) — ✅ Complete (Blocks A–I observed, Report filled, screenshots collected)
  - [x] Identify OS, kernel, and hostname (`/etc/os-release`, `uname`, `hostnamectl`)
  - [x] Inspect hardware resources (CPU, RAM, disk)
  - [x] Identify existing users and groups (`/etc/passwd`, `/etc/group`)
  - [x] Identify running services (systemd)
  - [x] Inspect disk layout and mount points (`lsblk -f`, `df -h`, `/etc/fstab`)
  - [x] Explore the directory structure (FHS)
  - [x] List installed software (`dpkg -l`)
  - [x] Inspect the initial network configuration (`ip a`, `ip route`, `ss -tulpn`)
  - [x] Review boot logs and messages (`journalctl -b`, `journalctl -b -p err`)
  - [x] Document the laboratory + collect screenshots
  - [ ] Pass the mentor validation (student explains back)

**Status:** ✅ Complete (Lab 00 done; Lab 01 next in Phase 3)

---

## Phase 3 — Version Control & Repositories

**Objective:** Start professional versioning immediately so the whole evolution is
publicly visible in real time.

**Estimated duration:** 2–3 sessions

- [x] **Lab 01 — Installing & Configuring Git** (`docs/labs/lab-01-installing-git.md`) — ✅ Complete
  - [x] Understand why version control is needed (concept before command)
  - [x] Install Git on Debian
  - [x] Configure `user.name` and `user.email`
  - [x] Choose and configure a default text editor
  - [x] Generate an SSH key pair (why: key-based auth, passwordless push)
  - [x] Initialize the repository in `~/linux-devops-labs`
  - [x] Write the initial `.gitignore` and verify ignored files
  - [x] Make the **first commit** (the whole existing documentation)
- [x] **Lab 02 — Publishing to GitHub & GitLab** (`docs/labs/lab-02-publishing-repositories.md`) — ✅ Complete
  - [x] Create the repository on GitHub (public)
  - [x] Create the repository on GitLab (public)
  - [x] Add GitHub as a remote and push
  - [x] Add GitLab as a remote and push
  - [x] Verify both repos render the README correctly
  - [x] Update `execution-plan.md` status and commit + push
  - [x] Pass the mentor validation

**Status:** ✅ COMPLETE (Labs 01 & 02 done — Project published on GitHub & GitLab)

---

## Phase 4 — Linux Fundamentals

**Objective:** Understand how Linux works internally. Concepts, not command lists.

**Estimated duration:** ~10 sessions

- [x] **Lab 03 — Filesystem & FHS**
  - [x] Why a filesystem hierarchy exists
  - [x] Purpose of top-level directories (`/etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt`)
  - [x] Navigation and inspection (`ls`, `pwd`, `cd`, `stat`)
  - [x] Absolute vs relative paths
- [x] **Lab 04 — Files, Inodes & Links**
  - [x] What a file is; inodes and metadata
  - [x] Hard links vs soft (symbolic) links
  - [x] `ls -li`, `ln`, `stat`, `file`
- [ ] **Lab 05 — Users & Groups**
  - [ ] Why users and groups exist; UID / GID
  - [ ] `/etc/passwd`, `/etc/shadow`, `/etc/group`
  - [ ] Primary vs secondary groups
  - [ ] `useradd`, `usermod`, `groupadd`, `id`
  - [ ] Scenario: onboarding a new developer
- [ ] **Lab 06 — Permissions & Ownership**
  - [ ] Why Linux needs permissions
  - [ ] rwx model for owner / group / others
  - [ ] `chmod`, `chown`, `chgrp`, numeric vs symbolic
  - [ ] `umask` and default permissions
- [ ] **Lab 07 — Special Permissions & ACLs**
  - [ ] SUID, SGID, sticky bit
  - [ ] When special bits make sense (e.g., `/tmp`)
  - [ ] ACLs with `getfacl` / `setfacl` and when they are needed

**Status:** 🔄 In Progress (Lab 03 complete)

---

## Phase 5 — System Administration

**Objective:** Think like a Linux administrator.

**Estimated duration:** ~12 sessions

- [ ] **Lab 08 — Processes**
  - [ ] What a process is; PID, PPID, lifecycle
  - [ ] `ps`, `top`/`htop`, process states
  - [ ] Signals and job control
  - [ ] Scenario: identify and investigate a runaway process
- [ ] **Lab 09 — systemd & Services**
  - [ ] What a service is; the difference between start and enable
  - [ ] Units and targets
  - [ ] `systemctl` day-to-day management
  - [ ] Scenario: recover a failed service
- [ ] **Lab 10 — Logs & journalctl**
  - [ ] Why centralized logging matters
  - [ ] `journalctl` filtering and live follow
  - [ ] Log severity levels; where classic log files live (`/var/log`)
  - [ ] Scenario: find an error using logs only
- [ ] **Lab 11 — Package Management (APT/dpkg)**
  - [ ] Why a package manager exists; dependencies
  - [ ] `apt` update / upgrade / install / remove
  - [ ] `dpkg` and when it is used
  - [ ] Repositories (`/etc/apt/sources.list`)
  - [ ] Scenario: install a tool and justify it
- [ ] **Lab 12 — Bash Scripting & Environment**
  - [ ] Environment variables and `PATH`
  - [ ] `~/.bashrc`, `~/.profile`
  - [ ] Script structure, shebang, exit codes, arguments
  - [ ] Scenario: automate a repetitive administrative task
- [ ] **Lab 13 — Automation (cron & systemd timers)**
  - [ ] What scheduling solves
  - [ ] `crontab`, cron syntax
  - [ ] systemd timers and when they are better
  - [ ] Scenario: schedule a daily task

**Status:** ⬜ Pending

---

## Phase 6 — Storage

**Objective:** Understand how Linux manages disks.

**Estimated duration:** ~6 sessions

- [ ] **Lab 14 — Disks & Partitions**
  - [ ] Disks, partitions, and partition tables
  - [ ] MBR vs GPT — why GPT won
  - [ ] `lsblk`, `fdisk`/`gdisk`, `blkid`
- [ ] **Lab 15 — Filesystems & Mounting**
  - [ ] What a filesystem is; `mkfs`
  - [ ] `mount` / `umount`, mount points
  - [ ] `/etc/fstab` and why UUIDs are used
  - [ ] Scenario: attach a new disk to the server
- [ ] **Lab 16 — LVM & Swap**
  - [ ] Why LVM exists: PV → VG → LV
  - [ ] Resize and snapshot basics
  - [ ] Swap and when it is used

**Status:** ⬜ Pending

---

## Phase 7 — Networking

**Objective:** Understand how a server communicates.

**Estimated duration:** ~8 sessions

- [ ] **Lab 17 — TCP/IP & Interfaces**
  - [ ] IP, subnet mask, gateway, addressing
  - [ ] Interfaces and `ip` commands
  - [ ] Static vs DHCP configuration
- [ ] **Lab 18 — DNS & Name Resolution**
  - [ ] Why DNS exists; how names resolve
  - [ ] `/etc/hosts`, `resolv.conf`, systemd-resolved
  - [ ] `getent`, `nslookup`, `dig`
- [ ] **Lab 19 — SSH**
  - [ ] SSH client and server; how auth works
  - [ ] Key pairs and agents
  - [ ] Basic server configuration
- [ ] **Lab 20 — Network Diagnostics**
  - [ ] Ports and sockets (`ss`)
  - [ ] `ping`, `traceroute`, `curl`, `wget`, `nc`
  - [ ] Scenario: diagnose "cannot reach the server"

**Status:** ⬜ Pending

---

## Phase 8 — Security

**Objective:** Protect the server.

**Estimated duration:** ~8 sessions

- [ ] **Lab 21 — Users & sudo Hardening**
  - [ ] Principle of least privilege
  - [ ] `sudo`, wheel group, `sudoers`
- [ ] **Lab 22 — SSH Hardening**
  - [ ] Disable root login, key-only auth
  - [ ] Optional: change port, fail2ban (justify if used)
- [ ] **Lab 23 — Firewall (UFW)**
  - [ ] What a firewall does; iptables vs UFW
  - [ ] Default-deny rules and services
- [ ] **Lab 24 — Updates & Auditing**
  - [ ] Unattended updates
  - [ ] Audit checklist for a fresh server
  - [ ] Scenario: harden a server handed to you

**Status:** ⬜ Pending

---

## Phase 9 — Services

**Objective:** Administer real services.

**Estimated duration:** ~6 sessions

- [ ] **Lab 25 — Nginx**
  - [ ] Install, configure, serve a static site
  - [ ] Virtual hosts; logs
- [ ] **Lab 26 — PostgreSQL**
  - [ ] Install, create database + user, permissions
  - [ ] Service management and logs
- [ ] **Lab 27 — Redis (as a real administered service)**
  - [ ] What a cache is and why it exists (why-first)
  - [ ] Install Redis, basic config, service management
  - [ ] Scenario: app performance problem that caching answers
- [ ] **Lab 28 — Backups & Maintenance**
  - [ ] Why backups matter; `pg_dump`, `tar`, `gzip`, `dd`
  - [ ] Automate and **test a restore** (a backup that is never restored is not a backup)

**Status:** ⬜ Pending

---

## Phase 10 — Docker

**Objective:** Understand Docker as infrastructure — only now, because the problem it
solves is real.

**Estimated duration:** ~8 sessions

- [ ] **Lab 29 — Docker Engine & CLI**
  - [ ] Containers vs VMs; images vs containers
  - [ ] Install Docker; lifecycle commands
- [ ] **Lab 30 — Images & Dockerfiles**
  - [ ] Layers, registries, tagging
  - [ ] Write a Dockerfile for an existing service
- [ ] **Lab 31 — Volumes & Networks**
  - [ ] Why containers need volumes; bind mounts
  - [ ] Container networking basics
- [ ] **Lab 32 — Docker Compose**
  - [ ] Multi-service stack: Nginx + PostgreSQL + app
  - [ ] Why each service is separated

**Status:** ⬜ Pending

---

## Phase 11 — VPS

**Objective:** Migrate the laboratory to a free VPS at **zero cost**.

**Estimated duration:** ~4 sessions

- [ ] **Lab 33 — Provisioning a Free VPS**
  - [ ] Create a cloud account (free tier only — no card charges; see ADR-0003)
  - [ ] Verify the provider's free-tier limits match our needs
  - [ ] Create the VPS; connect via SSH; firewall
- [ ] **Lab 34 — Reproducing the Environment**
  - [ ] Rebuild the setup on the VPS (user, security, Docker, services)
  - [ ] Validate services respond
- [ ] **Lab 35 — Observability (production is not "deployed and forgotten")**
  - [ ] Health checks and monitoring (CPU, RAM, disk)
  - [ ] Centralized logs and log rotation
  - [ ] Scenario: the server is down at 3 AM — how do we know and diagnose?

**Status:** ⬜ Pending

---

## Phase 12 — CI/CD (Professional Pipeline)

**Objective:** Automate deployment completely, with **quality and security gates** at
every step, exactly as a professional DevOps Junior delivers.

**Estimated duration:** ~10 sessions

- [ ] **Lab 36 — Code Quality Gates (Python)**
  - [ ] `pytest` (unit tests) — green tests gate
  - [ ] `mypy` (type checking) and `ruff` + `black` (lint/format)
  - [ ] `bandit` (security scan) and `pip-audit` (dependency vulnerabilities)
  - [ ] Why quality fails the build: CI is the last line of defense
- [ ] **Lab 37 — Multi-Registry Publishing**
  - [ ] Docker Hub, **GHCR**, and **GitLab Registry** (the same image, three homes)
  - [ ] Tagging strategy for the portfolio
- [ ] **Lab 38 — GitHub Actions**
  - [ ] Workflow fundamentals: jobs, steps, triggers
  - [ ] Build image → run quality gates → publish → deploy
- [ ] **Lab 39 — GitLab CI + Self-hosted Runner**
  - [ ] Equivalent pipeline in GitLab
  - [ ] Install a **GitLab Runner** on the VPS (professional, hands-on touch)
- [ ] **Lab 40 — Auto-Deploy & Rollback**
  - [ ] Deploy on push; health checks
  - [ ] Basic rollback strategy and a rehearsal

**Status:** ⬜ Pending

---

## Phase 13 — Final Project & Portfolio

**Objective:** A small, fully functional, documented server.

**Estimated duration:** ~4 sessions

- [ ] **Lab 41 — FastAPI Full Stack**
  - [ ] App + PostgreSQL + Nginx on the VPS
- [ ] **Lab 42 — HTTPS & Polish**
  - [ ] Let's Encrypt / Certbot
  - [ ] Final README, architecture diagram
- [ ] **Lab 43 — Portfolio & Interview Defense**
  - [ ] Walk through the repo as an interviewer
  - [ ] Rehearse "why" for every decision (including *why not* Kubernetes/Terraform)

> ### ⭐ OPTIONAL / TENTATIVE (only if the student decides — never required)
>
> The student maintains a real Python application they intend to sell. After the core
> project is complete, they *may* migrate it to the VPS and build its full pipeline.

- [ ] **Lab 44 — Migrating a Real Python App** (⭐ optional)
  - [ ] Containerize the student's own Python application
  - [ ] Deploy it on the VPS alongside the existing stack
  - [ ] Verify it runs, persists data, and is reachable
- [ ] **Lab 45 — Real App CI/CD Pipeline** (⭐ optional)
  - [ ] Full pipeline for the real app: commit → build → test → deploy → rollback
  - [ ] Exercise a real rollback with the real app
  - [ ] Decide with the mentor whether the app stays long-term on the VPS

**Status:** ⬜ Pending · ⭐ Labs 44–45 are optional/tentative

---

## Timeline (2 sessions/week, 2–3 h each)

| Phase | Months (approx.) | Sessions |
|---|---|---|
| 1 VM Setup | Month 1 | 1–2 |
| 2 Meeting Debian | Month 1 | 1–2 |
| 3 Version Control | Month 1–2 | 2–3 |
| 4 Linux Fundamentals | Month 2–4 | ~10 |
| 5 System Administration | Month 4–6 | ~12 |
| 6 Storage | Month 6–7 | ~6 |
| 7 Networking | Month 7–8 | ~8 |
| 8 Security | Month 8–9 | ~8 |
| 9 Services | Month 9–10 | ~7 |
| 10 Docker | Month 10–11 | ~8 |
| 11 VPS | Month 11 | ~4 |
| 12 CI/CD | Month 11–12 | ~10 |
| 13 Final | Month 12–13 | ~4 |

> Total ≈ 85–95 sessions ≈ 12–14 months. Cadence may be adjusted — understanding is the
> only fixed requirement.
>
> ⭐ Optional Labs 44–45 (app migration) add a few sessions only if the student decides
> to do them; they never affect the core roadmap.

---

## Session Workflow

**Daily recap mini-session (before anything else, every day):**

1. The mentor gives the simple summary of the journey so far.
2. Question round: **one question at a time** (commands, decisions, processes).
3. Gate: pass → progress; gaps → reinforcement, no new material.
4. Result recorded in `session-log.md` (passed ✅ / reinforce ⚠️).

**Start of the progress session (10 min):**

1. Read **Current Status** above.
2. Read the last entry of `session-log.md`.
3. Read the current lab document.
4. Tell the mentor what you remember from the previous session.

**During the session:**

5. Work the lab checklist. The mentor guides with questions.

**End of session (20 min):**

6. Fill the lab report section in the lab document.
7. Save screenshots/evidence in `screenshots/lab-NN/`.
8. Append an entry to `session-log.md`.
9. Tick completed checkboxes in this file and update **Current Status**.
10. Write an ADR if a meaningful decision was made.
11. Commit with a conventional message and push to **both** GitHub and GitLab.
12. Confirm the next session's target.

---

## Related Documents

- [`AGENTS.md`](../AGENTS.md) — AI operating manual & Definition of Done
- [`project-specification.md`](project-specification.md) — vision and scope
- [`mentor-constitution.md`](mentor-constitution.md) — mentoring principles
- [`learning-roadmap.md`](learning-roadmap.md) — competency map
- [`session-log.md`](session-log.md) — daily diary
- [`setup.md`](setup.md) — VM environment preparation
