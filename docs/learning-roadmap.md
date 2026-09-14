# LEARNING ROADMAP

## Competency Map — "You are done when you can…"

**Project:** Linux DevOps Labs
**Version:** 1.1

---

## How to Use This Document

This is the **competency map**. For every phase it defines the questions the student must
be able to answer and the skills they must demonstrate **without help**. It complements
[`execution-plan.md`](execution-plan.md) (the *what to do*) by defining *what "done"
means for your brain*.

The mentor uses these questions to validate understanding. The student uses them to
self-assess before marking a phase complete. If you cannot answer a question fluently,
the phase is **not** complete — regardless of how many checkboxes are ticked.

Items marked ⭐ are **optional/tentative** and never gate the core roadmap.

---

## Phase 0 — Planning

- [ ] I can explain the mission of the project in 3 sentences.
- [ ] I know the 4 documents that form the project core and what each one is for.
- [ ] I understand the Definition of Done and why every session must update state.

---

## Phase 1 — VM Environment Setup

- [ ] I can explain what VirtualBox Guest Additions are and why they are needed.
- [ ] I can explain what a shared folder is and how the VM and host exchange files.
- [ ] I can explain why a baseline snapshot is taken before starting the labs.
- [ ] I can create the workspace and verify it mirrors the project template.

---

## Phase 2 — Meeting Debian

- [ ] I can list the basic facts about my server: Debian version, kernel, hostname, uptime.
- [ ] I can explain why the version matters before doing anything else.
- [ ] I can identify which users and groups are "system" and which are "human".
- [ ] I can explain what a process is and why services run on an idle server.
- [ ] I can explain the purpose of the top-level directories: `/etc`, `/var`, `/usr`, `/home`.
- [ ] I can explain what `/etc/os-release`, `/etc/passwd`, `/etc/fstab` are for.

---

## Phase 3 — Version Control & Repositories

- [ ] I can explain what a commit is and what makes a commit "meaningful".
- [ ] I can explain the difference between a working directory, staging area, and repository.
- [ ] I can explain why versioning the project from day one matters for a portfolio.
- [ ] I can create a repository, add a remote, push, and pull on both GitHub and GitLab.
- [ ] I can explain why the repositories are mirrored in two platforms.

---

## Phase 4 — Linux Fundamentals

- [x] I can explain the Filesystem Hierarchy Standard and why the layout exists.
- [x] I can explain the difference between a file, a directory, and a mount point.
- [x] I can explain what an inode is and what a hard link vs a soft link means.
- [x] I can explain what a UID and a GID are and how Linux decides access.
- [x] I can explain the difference between a primary and a secondary group.
- [ ] I can explain rwx permissions for owner/group/others and how `chmod` computes them.
- [ ] I can explain `umask`, SUID, SGID, sticky bit, and ACLs with a real example.

---

## Phase 5 — System Administration

- [ ] I can explain what a process is, its lifecycle, and how signals work.
- [ ] I can explain what a service is and the difference between starting and enabling it.
- [ ] I can explain what systemd units and targets are.
- [ ] I can find and follow an error in the logs with `journalctl`.
- [ ] I can explain why a package manager exists and how dependencies work.
- [ ] I can explain the difference between `apt` and `dpkg`.
- [ ] I can write a simple Bash script and explain exit codes and variables.
- [ ] I can schedule a task with cron and explain when to prefer a systemd timer.

---

## Phase 6 — Storage

- [ ] I can list the disks of a server and explain what each column of `lsblk` means.
- [ ] I can explain the difference between MBR and GPT and when each is used.
- [ ] I can explain the difference between a disk, a partition, and a filesystem.
- [ ] I can mount and unmount a filesystem and explain why UUIDs are preferred in fstab.
- [ ] I can explain what LVM is, why it exists, and its three layers (PV, VG, LV).
- [ ] I can explain what swap is and how Linux uses it.

---

## Phase 7 — Networking

- [ ] I can explain the role of IP, subnet mask, gateway, and DNS.
- [ ] I can explain what an interface is and how to inspect it with `ip`.
- [ ] I can explain how a hostname is resolved on Linux (`/etc/hosts`, `resolv.conf`).
- [ ] I can explain what a port is and how `ss` shows listening connections.
- [ ] I can diagnose "I cannot reach this server" step by step.
- [ ] I can explain how SSH authenticates (keys) and how to test a connection safely.

---

## Phase 8 — Security

- [ ] I can explain the principle of least privilege and apply it to users and sudo.
- [ ] I can explain why `PermitRootLogin no` is a baseline SSH hardening measure.
- [ ] I can explain what a firewall is and how UFW layers on top of iptables.
- [ ] I can explain why unattended updates matter and how to check for pending updates.
- [ ] I can enumerate the checks I would run to audit a fresh server.

---

## Phase 9 — Services

- [ ] I can install, configure, and verify a web server (Nginx) serving a site.
- [ ] I can explain the difference between Nginx and PostgreSQL and why both run as services.
- [ ] I can create a database and a user and explain the permissions involved.
- [ ] I can explain what a cache is and when Redis is the right answer.
- [ ] I can explain why backups matter and demonstrate a restore.
- [ ] I can read a service's logs to diagnose a failure.

---

## Phase 10 — Docker

- [ ] I can explain the difference between a container and a VM.
- [ ] I can explain images vs containers vs volumes vs networks.
- [ ] I can write a Dockerfile and explain what a layer is.
- [ ] I can run a multi-service stack with Docker Compose and explain each service.
- [ ] I can justify why Docker was introduced at this point of the project.

---

## Phase 11 — VPS

- [ ] I can explain the difference between a local VM and a cloud VPS.
- [ ] I can provision a free VPS and connect to it securely.
- [ ] I can reproduce the local environment on the VPS step by step.
- [ ] I can explain why the migration is a "reproduction" and not a copy-paste.
- [ ] I can set up observability: health checks, CPU/RAM/disk monitoring, and log
      rotation — production is not "deployed and forgotten".
- [ ] I can explain why the chosen cloud provider keeps costs at $0 and the limits of its
      free tier (ADR-0003).

---

## Phase 12 — CI/CD (Professional Pipeline)

- [ ] I can explain what CI and CD mean and the difference between them.
- [ ] I can explain what a quality gate is and why each tool exists:
      `pytest`, `mypy`, `ruff`, `black`, `bandit`, `pip-audit`.
- [ ] I can explain the elements of a GitHub Actions workflow (jobs, steps, triggers).
- [ ] I can explain the equivalent concepts in GitLab CI.
- [ ] I can explain how a pipeline builds, runs quality gates, publishes to multiple
      registries (Docker Hub, GHCR, GitLab Registry), and deploys automatically.
- [ ] I can explain what a self-hosted GitLab Runner is and why it matters for a
      professional touch.
- [ ] I can describe a basic rollback strategy and why it matters.

---

## Phase 13 — Final Project & Portfolio

- [ ] I can explain the final architecture end to end (user → Nginx → app → DB).
- [ ] I can explain how HTTPS was obtained and why it is non-negotiable.
- [ ] I can walk an interviewer through the repository, phase by phase.
- [ ] I can justify every major decision using the ADRs.
- [ ] I can explain why Kubernetes was kept out of scope and why Terraform stayed
      optional/deferred (a "why not" answer is as valuable as the tool itself).
- [ ] I can answer "Why did you do it this way?" for each component.
- [ ] ⭐ (Optional) I can migrate my own real Python app to the VPS, containerized.
- [ ] ⭐ (Optional) I can run the full pipeline for a real app: commit → build → test → deploy → rollback.

---

## Progress Tracker

| Phase | Self-assessment | Mentor validation | Date |
|---|---|---|---|
| 0 Planning | ✅ | ✅ | 2026-08-03 |
| 1 VM Setup | ✅ | ✅ | 2026-08-13 |
| 2 Meeting Debian | ✅ | ✅ | 2026-08-31 |
| 3 Version Control | ✅ | ✅ | 2026-08-31 |
| 4 Linux Fundamentals | 🔄 | ⬜ | 2026-09-14 (Labs 03-05 done) |
| 5 System Administration | ⬜ | ⬜ | |
| 6 Storage | ⬜ | ⬜ | |
| 7 Networking | ⬜ | ⬜ | |
| 8 Security | ⬜ | ⬜ | |
| 9 Services | ⬜ | ⬜ | |
| 10 Docker | ⬜ | ⬜ | |
| 11 VPS | ⬜ | ⬜ | |
| 12 CI/CD | ⬜ | ⬜ | |
| 13 Final Project | ⬜ | ⬜ | |
