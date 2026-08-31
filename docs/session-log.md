# SESSION LOG

## Daily Diary — reverse chronological order

**Project:** Linux DevOps Labs

---

## How to Write an Entry

Append every entry at the **top** of this file (under this header). One entry per session.
Keep it honest and specific: this log is the "memory" that any AI (and you) uses to resume
work instantly. The mentor reviews the latest entry at the start of every session.

### Template

```markdown
## YYYY-MM-DD — Session NN

**Phase / Lab:** Phase X — <phase name> · Lab NN — <lab title>

**Daily recap (start of day):**
- Passed ✅ / Areas to reinforce ⚠️: <what was asked and how it went>

**Worked on:**
- <what was done this session>

**Concepts learned / reinforced:**
- <concept, in your own words>

**Commands / tools used:**
- <command> — why

**Errors encountered:**
- <error> → <what you investigated> → <resolution>

**Questions still open:**
- <question> (if none, write "None")

**Next session (target):**
- <exact next checkbox to complete>

**Commit / push:** `docs(lab-00): ...` — pushed to GitHub ✅ GitLab ✅
```

---

## Entries

---

## 2026-08-13 — Session 03 (Phase 1 Completed — VM Environment Ready)

**Phase / Lab:** Phase 1 — VM Environment Setup · Setup 01–05 (all complete)

**Daily recap (start of day):**
- ⚠️ Rule clarifications from the student (recorded in AGENTS.md for all future sessions):
  1. Summaries and recap questions are tied **100%** to the Linux/DevOps technical topics
     already taught in previous sessions — nothing from planning decisions or memory files,
     and nothing not yet taught.
  2. Recap is time-boxed to **~15 minutes/day** (student works ~1.5 h/day); summaries and
     questions are **split across Mon–Fri**, always covering all topics from the beginning
     (spaced repetition) and restarting each week adding new topics.
  3. Teaching discipline: one question at a time → validate → confirm assimilation →
     continue; weak/half answers trigger reinforcement with secondary questions first.
- Since no technical topic has been taught yet (no lab completed), the question round did
  not apply today; it begins once Lab 00 produces curriculum.
- Also clarified with the student: the Windows folder is a working copy; the official folder
  is at `E:\Datos\IA\Linux VPS - Project` and is only updated by the student after each
  session (never touched by the AI). The project "real" lives in the VM (`~/linux-devops-labs`).

**Worked on:**
- Recorded recap rules in memory files (session-log + AGENTS.md) for all future sessions.
- **Setup 01 — VM verification PASSED ✅** (VirtualBox 7.2.4 r170995; VM `Debian` 64-bit, 2048 MB RAM, 3 CPUs, 30 GB VDI, NAT). Guest OS: **Debian 13 (trixie)**, kernel `6.12.101+deb13-amd64` x86-64, user `Erick`/`Debian`. Facts documented in `docs/setup.md` ("Verified Facts").
- **Setup 02 — Guest Additions ✅** (`vboxguest` module loaded).
- **Setup 03 — Shared folder ✅** mounted at `/mnt/host` (name `linux-vps-project`).
- **Setup 04 — Workspace ✅** `~/linux-devops-labs` created, template copied, structure verified with `find`.
- **Setup 05 — Baseline snapshot ✅** `baseline-clean-debian` taken (UUID 8f1f1df0-0911-4f40-b29a-6d2fba4d22e1).

**Concepts learned / reinforced (informal, no lab yet):**
- `dmesg` reads kernel messages; modern kernels restrict it to root (`sudo dmesg`).
- A failed mount's kernel message tells you *who* rejected it (`vboxsf: Host rejected mount ... error -2` = ENOENT on the host side).
- VirtualBox auto-renames shared folders (spaces → underscores); the mount tag must match exactly.
- `~` = home only with a following `/` (`~/x`); `~x` is a literal name.
- `cp -r`, `mkdir -p`, `find`, `touch`/`rm` write-test.

**Commands / tools used:**
- VM: `hostnamectl`, `cat /etc/os-release`, `uname -a`, `uptime`, `whoami`, `pwd`, `lsmod`, `sudo dmesg`, `sudo mount -t vboxsf`, `mkdir -p`, `cp -r`, `find`, `touch`, `rm`, `sudo reboot`, `sudo poweroff`.
- Host: `VBoxManage` (showvminfo, sharedfolder add/remove, controlvm acpipowerbutton, snapshot take/list).

**Errors encountered:**
- `mount: special device linux-vps-project does not exist` → investigated with `lsmod` + `dmesg` → found `vboxsf: Host rejected mount ... error -2` → root cause: the share existed but under the auto-renamed name `Linux_VPS_-_Project` → fixed via `VBoxManage sharedfolder remove` + `add` with the VM powered off.
- `~linux-devops-labs` created a folder with a literal name (tilde needs a `/`) → fixed with `rmdir` + `mkdir -p ~/linux-devops-labs`.

**Questions still open:**
- None. (ISO filename evidence still pending — the VM pre-existed.)

**Next session (target):**
- Lab 00 — Meeting Your Debian Server: observe the clean server (read-only), answer the 8 mentor questions, fill the Report, take screenshots in `screenshots/lab-00/`.

**Commit / push:** N/A — repository not created yet (Lab 01).

---

## 2026-08-10 — Session 02 (Curriculum Defined — Professional DevOps Track)

**Phase / Lab:** Phase 0/1 — Planning · Curriculum & session contract

**Daily recap (start of day):** N/A — first working session; recap protocol details
were defined in contract form (see below).

**Worked on:**
- Confirmed the **official memory folder** is `Linux VPS - Project`; updated folder
  references in `INSTRUCCIONES SESION DIARIA - IA.txt` and `docs/setup.md`
  (`linux-vps-borrador` → `linux-vps-project`).
- Confirmed a **clean Debian 64-bit VM** already exists in VirtualBox (no Git, no
  project files inside) — pending verification against `docs/setup.md`.
- Established the **fixed session structure** (recap = technical curriculum only,
  one question at a time; work session; end-of-day state update + READMEs + summary).
- As the senior mentor, audited the proposed curriculum against the 2026 market and
  defined the **Professional DevOps Junior track** (ADR-0004):
  - Linux core in strict incremental order.
  - Added: **Python-for-DevOps** prerequisite, **observability** in production,
    **quality gates** (`pytest`, `mypy`, `ruff`, `black`, `bandit`, `pip-audit`),
    **multi-registry** (Docker Hub, GHCR, GitLab Registry), **GitLab CI + self-hosted
    Runner** on the VPS, full deploy pipeline with rollback.
  - Kubernetes stays **out of scope**; Terraform stays **optional** (as an awareness
    module: learning "why not" is interview gold).
- Renumbered the roadmap (Phase 9 → Redis lab, Phase 11 → Observability, Phase 12 → 10
  sessions professional CI/CD, optional labs 44–45) and updated `execution-plan.md`,
  `learning-roadmap.md`, `project-specification.md`, `README.md`, `docs/labs/README.md`,
  ADR index, and `AGENTS.md` (recap + session Definition of Done).

**Concepts learned / reinforced:**
- The curriculum is the "study plan"; the memory files are only updated at the end of a
  session — the recap never quizzes the repo's own structure.
- A professional DevOps Junior pipeline = quality gates + multi-registry + self-hosted
  runner + observability + tested rollback.

**Commands / tools used:**
- None on the VM (planning/setup documentation only).

**Errors encountered:**
- None.

**Questions still open:**
- VirtualBox version and Debian details to be verified when the VM is first booted.

**Next session (target):**
- Phase 1 — Setup 01–05: verify the clean Debian VM (boot, hardware, SSH server),
  install Guest Additions, shared folder `linux-vps-project`, create `~/linux-devops-labs`,
  take baseline snapshot `baseline-clean-debian`.

**Commit / push:** N/A — repository not created yet (Lab 01).

---

## 2026-08-03 — Session 01 (Requirements Update)

**Phase / Lab:** Phase 0 — Planning · Documentation update

**Daily recap (start of day):** N/A — first project day.

**Worked on:**
- Defined the **daily recap & validation ritual**: a mandatory mini-session before any
  progress, with one-question-at-a-time validation (commands, decisions, processes).
- Adopted the **zero-cost principle**: no income currently, so the project must stay at
  $0 — free-tier clouds, free tools, no expenses without justification.
- Recorded a **tentative optional final step**: migrating the student's real Python app
  to the VPS with a full CI/CD pipeline (Labs 40–41, ⭐ Optional — renumbered to 44–45 in ADR-0004).
- Updated AGENTS.md, project spec, execution plan, roadmap, session-log template,
  README, and added ADR-0003 (zero-cost cloud strategy).

**Concepts learned / reinforced:**
- Interactive learning is a process, not a chat: recap → one question at a time → gate.
- Constraints (budget, real products) must be first-class citizens of the plan, not
  afterthoughts.

**Commands / tools used:**
- None (documentation update only).

**Errors encountered:**
- None.

**Questions still open:**
- None.

**Next session (target):**
- Phase 1 — Setup 01: create the Debian VM in VirtualBox (`docs/setup.md`).

**Commit / push:** N/A — repository not created yet (will be created in Lab 01).

---

## 2026-08-03 — Session 00 (Planning)

**Phase / Lab:** Phase 0 — Planning · Documentation Architecture restructure

**Worked on:**
- Reviewed all 6 original draft documents (spec, plan, constitution, agent manual, two narratives).
- Restructured the project into a professional, AI-friendly documentation architecture.
- Decided: English-only public docs, Git introduced right after Lab 00, mirrored GitHub + GitLab.
- Created the template that will be copied into the Debian VM during Setup.

**Concepts learned / reinforced:**
- A portfolio is stronger when the repository shows the *evolution*, not just the result.
- An AI mentor can recall project state instantly if a single status file is maintained.

**Commands / tools used:**
- None (host machine, planning only).

**Errors encountered:**
- None.

**Questions still open:**
- None.

**Next session (target):**
- Phase 1 — Setup 01: create the Debian VM in VirtualBox (`docs/setup.md`).

**Commit / push:** N/A — repository not created yet (will be created in Lab 01).
