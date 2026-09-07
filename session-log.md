# SESSION LOG

## Daily Diary — reverse chronological order

**Project:** Linux DevOps Labs

---

## ⛔ LESSON LEARNED — 2026-09-07

**Issue:** The agent started a session WITHOUT following the mandatory bootstrap protocol.
It skipped: (1) reminding the student about Academia Deploy Block 1, (2) giving the
daily summary, and (3) asking validation questions one at a time.

**Root cause:** The agent received the command "quiero comenzar la sesión del día" and
jumped directly to reviewing the repo status instead of following AGENTS.md Step 0.

**Fix:** Added a CRITICAL RULE section at the very top of AGENTS.md (before everything
else) with explicit, hard-to-miss instructions. The agent must NEVER skip the 3-step
protocol: Academia Deploy reminder → Summary → One-question-at-a-time validation.

**Student statement:** "de ahora en adelante cada vez que te diga, comencemos con la
sesión de hoy o algo similar lo primero siempre es seguir el proceso como se definio"

---

## 2026-09-07 — Session 08 (Lab 03 COMPLETE — Filesystem & FHS)

**Phase / Lab:** Phase 4 — Linux Fundamentals · Lab 03 — Filesystem & FHS (✅ Complete)

**Daily recap (start of day):** N/A — protocol not applied today (starts from 2026-09-08 onward per student request)

**Worked on:**
- Verified repo name discrepancy: GitHub/GitLab repos are `linux-devops-lab` (without 's'), documentation incorrectly referenced `linux-devops-labs` (with 's'). Corrected all affected files.
- Confirmed shared folder configuration: `linux-vps-project` maps to `C:\Users\XPC\Desktop\Linux VPS - Project` on host, mounted at `/mnt/host` in VM.
- Confirmed shared folder sync works in real-time (test file created from Windows, read from VM, then deleted).
- **Lab 03 completed:**
  - Explored top-level directories: `/etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt`
  - Explained FHS contract and why hierarchy exists
  - Practiced navigation: `pwd`, `cd`, `ls`, `ls -la`
  - Understood absolute vs relative paths with real examples
  - Observed symlinks: `bin -> usr/bin`, `lib -> usr/lib`, `sbin -> usr/sbin`
  - Answered all 6 mentor questions correctly

**Concepts learned / reinforced:**
- FHS is a "contract" — same structure across all Linux distributions
- `/etc` = config, `/var` = variable data, `/usr` = software, `/home` = users, `/tmp` = temporary, `/opt` = third-party
- Absolute paths start from `/`, relative paths start from current location
- `..` means "go up one level" in relative paths
- `ls -la` shows permissions, owner, size, date, and symlinks
- Symlinks (`->`) are pointers to other locations (Debian modern consolidation)

**Commands / tools used:**
| Command | Why |
|---|---|
| `ls /` | List top-level directories |
| `ls /etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt` | Explore each directory's contents |
| `pwd` | Show current location |
| `cd /`, `cd ../../home/Erick/linux-devops-labs` | Practice absolute and relative navigation |
| `ls -la /` | Detailed listing with permissions and symlinks |

**Errors encountered:**
- `ls /opt` returned empty — normal for fresh Debian install (no third-party software yet)

**Questions still open:**
- None blocking.

**Next session (target):**
- Lab 04 — Files, Inodes & Links (what a file is; inodes and metadata; hard links vs soft links; `ls -li`, `ln`, `stat`, `file`)
- **Starting from next session, the full 3-step protocol applies:** Academia Deploy reminder → Summary → One-question-at-a-time validation

**Commit / push:** Pending — student needs to copy files from `/mnt/host` to `~/linux-devops-labs` and commit + push.

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

## 2026-08-31 — Session 07 · follow-up (Repo sync diagnosis — GitHub public copy is stale)

**Phase / Lab:** Phase 3 — Version Control & Repositories · Lab 02 follow-up (repo consistency review, no new code)

**What happened after Lab 02 completion:**
- While closing the Definition of Done, the mentor noted a **gap**: the public GitHub repo
   (`linux-devops-lab`) did **not** match the progress recorded in the memory. The GitHub copy
  still showed Phase 1/2/3 as Pending and only 1 commit (the template from Session 03),
  whereas the memory (`session-log`/`execution-plan` in Windows) reflected Labs 00–02 complete.
- The student explained the environment architecture (clarified for the record):
  - `Linux VPS - Project` (**Windows**, `C:\Users\XPC\Desktop\Linux VPS - Project`) = the **project
    memory / instructions** — the files the AI edits and where progress is recorded in real time.
  - `~/linux-devops-labs` (**inside the Debian VM**) = the **real technical project/repo**, holds
    `.git`, and is what gets pushed to GitHub + GitLab.
  - The Windows folder is *mounted* into the VM (that is how the project "lives" in Debian).

**Shared-folder / mount verification (VirtualBox host side):**
- `VBoxManage showvminfo Debian` confirmed the configured shared folder:
  - Mount tag: `linux-vps-project` → host path `C:\Users\XPC\Desktop\Linux VPS - Project`.
- Inside the VM, `/mnt/host` was **empty** (`mount | grep vboxsf` returned nothing) → the shared
  folder was **not currently mounted**. It was mounted manually with:
  `sudo mount -t vboxsf linux-vps-project /mnt/host`, after which `/mnt/host` showed the Windows
  files (`AGENTS.md`, `docs`, `README.md`, `screenshots`, `scripts`, `INSTRUCCIONES SESION DIARIA - IA.txt`).

**Sync attempt and its result (key learning):**
- Tried to copy the Windows memory over the repo: `cp -r /mnt/host/* ./` inside `~/linux-devops-labs`.
  - A `cp` user error: including the `INSTRUCCIONES SESION DIARIA - IA.txt` file in the command made
    `cp` treat it as the *target*, failing with "Not a directory" (the instructions file was not copied).
  - The rest of the files copied fine.
- **Surprise finding:** `git status` showed "nothing to commit, working tree clean" — meaning the
  repo in the VM already matched the current memory. So the **local VM repo is up to date**; only the
  **published GitHub copy appeared stale during this check**. This needs a follow-up verification
  (the mentor suspects the GitHub view refreshed late, or the local repo differs from what was viewed).

**Concepts / process learnings recorded for future sessions:**
- Working directly in a VM terminal has friction for the student (untrusted long commands; copying
  output back through e-mail). **The mentor should prefer short, single-purpose, copy-paste-safe
  commands** and avoid long multi-step verification chains.
- The sync workflow (Windows memory → VM repo → push) is understood but **not executed to completion
  today**; the student preferred to close the session rather than continue the multi-step sync. The
  public-copy freshness question is deferred.

**Questions still open:**
- Why did `git status` report clean while the GitHub view seemed stale? → verify next session
  (`git log --oneline -3`, `git push github main`, `git push gitlab main` at the VM).
- Whether `/mnt/host` should stay mounted persistently (fstab) for future syncs — optional, not urgent.

**Next session (target):**
- Confirm/close the repo consistency (quick `git log` + `git push` to both) at session start;
  then proceed to Phase 4 — Lab 03 — Filesystem & FHS.

---

## 2026-08-31 — Session 07 (Lab 02 COMPLETE — Published to GitHub & GitLab)

**Phase / Lab:** Phase 3 — Version Control & Repositories · Lab 02 — Publishing to GitHub & GitLab (✅ Complete)

**Daily recap (start of day):**
- ✅ Passed. Single-question recap on SSH keys: student correctly explained key-based auth vs passwords, the public key (cerradura/lock) vs private key (llave/key), that the private key never leaves the machine, and the analogy mapping to GitHub/GitLab (put the "lock"/public key on the server; keep the "key"/private key locally).

**Worked on (VM Debian + web on both platforms):**
- **Lab 02 in full — published the project to both platforms:**
  - Added the VM's **ed25519 public key** to GitHub (Settings → SSH and GPG keys → New SSH key, titled `Debian VM`, Authentication Key). GitHub now holds two public keys: the older Windows-host key and the new VM key.
  - Validated SSH from the VM: `ssh -T git@github.com` → `Hi ericksuper8000-source! You've successfully authenticated...` (GitHub username confirmed as `ericksuper8000-source`).
  - Added the same VM public key to GitLab (Preferences → SSH Keys, titled `Debian VM`, Usage type: Authentication — Signing left off for now).
  - Validated SSH from the VM: `ssh -T git@gitlab.com` → `Welcome to GitLab, @ericksuper80!` (GitLab username confirmed as `ericksuper80`).
   - Created the **public** repository `linux-devops-lab` on **GitHub** (no auto-generated files — to avoid a first-push merge conflict).
   - Created the **public** repository `linux-devops-lab` on **GitLab** (Create blank project, empty, no README).
   - Added both remotes in the VM: `git remote add github git@github.com:ericksuper8000-source/linux-devops-lab.git` and `git remote add gitlab git@gitlab.com:ericksuper80/linux-devops-lab.git`; verified with `git remote -v` (4 lines: fetch + push for each).
  - Pushed to both: `git push -u github main` and `git push -u gitlab main` (`-u` sets the upstream tracking branch).
  - Verified both: `git push github main` + `git push gitlab main` → **Everything up-to-date**; README renders, commit history and all files visible on both platforms.

**Concepts learned / reinforced:**
- The **lock-and-key** model of SSH: the public key (lock) lives on the server (GitHub/GitLab); the private key (key) stays on the client (VM) and never leaves it.
- Validating SSH connectivity with `ssh -T git@<host>` — the "does not provide shell access" / "Welcome" messages are normal/expected.
- **Remote vs local**: a local repo is invisible to others; `git remote` points to a hosted copy; `git push` shares the history.
- **Do not let the platform auto-generate files** on a repo that already has a first commit (avoids a merge conflict on the initial push).
- Two platforms = portfolio breadth + later CI comparison (ADR-0002). GitHub username `ericksuper8000-source`, GitLab username `ericksuper80`.
- SSH key **passphrase** vs login password: the passphrase unlocks the private key (encryption on the key itself), prompted by the local SSH agent (gnome-keyring) — extra security layer.

**Commands / tools used (VM, Debian):** `cat ~/.ssh/id_ed25519.pub`, `ssh -T git@github.com`, `ssh -T git@gitlab.com`, `cd ~/linux-devops-labs`, `git remote add github ...`, `git remote add gitlab ...`, `git remote -v`, `git push -u github main`, `git push -u gitlab main`, `git push github main`, `git push gitlab main`.

**Errors encountered:**
- `ssh -T git@github.com` first prompted to unlock the private key ("Enter password to unlock the private key... application wants access to the private key ... but it is locked"). This is the **SSH passphrase** (not the Debian login password) requested by gnome-keyring. Resolved by entering the passphrase set at `ssh-keygen` time; the keyring remembers it for the session (no further prompts on subsequent commands).

**Questions still open:**
- None blocking. Optional future: SSH key **Signing** usage (GitLab) if the student later wants signed commits — not needed now.

**Next session (target):**
- Phase 4 — Linux Fundamentals: Lab 03 — Filesystem & FHS (concept-first: why a filesystem hierarchy exists; `/etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt`; navigation and inspection; absolute vs relative paths). Also remember the new Git workflow: every session now ends with commit + push to **both** remotes.

**Commit / push:** ✅ Both remotes up-to-date. Initial commit `docs: initialize linux devops labs repository` now public & visible on GitHub and GitLab.

---

## 2026-08-31 — Session 07 (Lab 01 COMPLETE — Git installed, configured, first commit)

**Phase / Lab:** Phase 3 — Version Control & Repositories · Lab 01 — Installing & Configuring Git (✅ Complete)

**Daily recap (start of day):**
- ✅ Passed. Focused on the Git concept stage from Session 06 (three states: working directory → staging area → repository; local-first Git; commit = frozen snapshot; identity; per-OS SSH keys). Student demonstrated understanding of Git add/commit/status before the practical work.

**Worked on (all inside the Debian VM, at `~/linux-devops-labs`):**
- Installed Git (`sudo apt update && sudo apt install -y git`).
- Configured identity: `user.name = Erick_Dev`, `user.email = ericksuper80@gmail.com` — **kept identical to the Windows host identity** so all commits attribute to the same person across machines.
- Set `init.defaultBranch` to `main`.
- Configured a default text editor.
- Generated an **ed25519 SSH key pair** (`ssh-keygen -t ed25519 -C "ericksuper80@gmail.com"`) inside the VM. The **public** key was copied to a host file for reference: `C:\Users\XPC\Desktop\Archivo.txt` (contains the public key only — safe, it is the key meant to be shared).
- Ran `git init` in `~/linux-devops-labs`.
- Verified `.gitignore` excludes `_archive/` and junk.
- Staged + reviewed (`git add .`, `git diff --cached`).
- Made the **first commit**: `git commit -m "docs: initialize linux devops labs repository"`.
- Confirmed history with `git log --oneline`.
- The repository `.git` lives inside the VM (`~/linux-devops-labs`); the Windows host folder has no `.git` — the host folder is the documentation/development copy mounted in the VM (`/mnt/host`).

**Concepts learned / reinforced:**
- Git three states (working tree → index → repository) and `git add` vs `git commit`.
- `git status` to inspect current state.
- Local-first Git: commit works offline, push shares (Lab 02).
- Same `user.name`/`user.email` across Windows and VM keeps authorship consistent when pushing to the same GitHub/GitLab account.
- SSH keys are per-OS: the VM generated its **own** key pair; the Windows host keeps its own. No private keys were copied between machines.

**Commands / tools used (VM, Debian):** `sudo apt update`, `sudo apt install -y git`, `git config --global user.name`, `git config --global user.email`, `git config --global init.defaultBranch`, `git config --global core.editor`, `ssh-keygen -t ed25519 -C`, `git init`, `git status`, `git add .`, `git diff --cached`, `git commit -m`, `git log --oneline`; `cat ~/.ssh/id_ed25519.pub`.

**Errors encountered:**
- None reported.

**Questions still open:**
- Next: Lab 02 — add the VM SSH **public** key to GitHub and GitLab, create the two repos, add remotes, push both.

**Next session (target):**
- Lab 02 — Publishing to GitHub & GitLab: add the SSH public key to both platforms, create public repos `linux-devops-lab` (no auto-generated files), add `github` + `gitlab` remotes, `git push -u github main` and `git push -u gitlab main`, verify README + history render on both.

**Commit / push:** First commit made in the VM (`docs: initialize linux devops labs repository`). No push yet (Lab 02).

---

## 2026-08-31 — Session 06 (Recap passed · Lab 01 started — concept: control de versiones)

**Phase / Lab:** Phase 3 — Version Control & Repositories · Lab 01 — Installing & Configuring Git (🔄 in progress: concept stage)

**Daily recap (start of day):** ✅ Passed. Academia Deploy (Bloque 1) completed first (Sesión 2: On-Premise vs IaaS, frontera de responsabilidad — verified in Academia bitácora). Linux recap topics:
1. Cuentas de sistema vs humanas (UID: 0 root, 1–999 sistema, 1000+ humanos) — answered correctly incl. least-privilege/encapsulation purpose.
2. UUID en `/etc/fstab` (Block E) — answered correctly; mentor reinforced *why* robust (device names change with hardware, UUID is fixed).
3. Carpeta compartida + `dmesg` (Fase 1, spaced repetition — was forgotten; mentor refreshed the story: `mount` only said "does not exist", `dmesg` revealed `vboxsf: Host rejected ... error -2` = VirtualBox renamed the shared folder because of spaces). Re-asked reformulated → assimilated OK.
4. Separación `/etc` vs `/usr` (Block F) — answered correctly (update software without losing config; back up `/etc` only).

**Worked on:**
- Concept antes de comandos (Lab 01): el problema que resuelve Git (historia, rollback, evidencia, red de seguridad); los tres lugares (working directory → staging area → repository) y `git add` vs `git commit`; Git es **local primero** (commit offline, push comparte, Lab 02).
- Student already has Git experience on Windows, accounts on GitHub + GitLab, and SSH keys configured on Windows.
- **Identity reference grabbed from Windows host (read-only, no private keys touched):**
  `git config --global` → `user.name=Erick_Dev`, `user.email=ericksuper80@gmail.com` (also saw `core.autocrlf=true` and a Windows-specific `core.sshcommand` — those are Windows-only and do NOT replicate to the VM).
- Clarified with student: Git in Windows and in the VM are **totally isolated** (separate config, separate SSH key files in separate OS filesystems). No conflict. VM will need its **own** SSH keys (never copied from Windows) and will use the **same identity** (Erick_Dev / ericksuper80@gmail.com) so commits attribute to the same person.

**Concepts learned / reinforced:**
- A commit = a frozen snapshot of the project at a moment in time (student's own 100→500 line Python example).
- Git is local-first; commit works offline, push shares.
- Git config and SSH keys are per-OS, fully isolated between Windows and the VM.
- Same identity across machines keeps commit authorship consistent.

**Commands / tools used (host, read-only):**
- `git config --global --list` (and `user.name`, `user.email`) — to grab identity reference. No private keys read.

**Errors encountered:**
- None.

**Questions still open:**
- SSH service not running (Lab 00 finding) → Lab 19.
- Next in Lab 01: actually install Git in the VM, configure identity, generate SSH key pair, init repo, first commit.

**Next session (target):**
- Lab 01 practical: `sudo apt install git`, set `user.name`/`user.email`/`init.defaultBranch`, generate `ed25519` SSH key, `git init` in `~/linux-devops-labs`, verify `.gitignore`, stage + first commit.

**Commit / push:** N/A — repository not created yet (Lab 01). Both memory files updated in the single project folder.

---

## 2026-08-27 — Session 05 (Lab 00 Blocks E–I completed)

**Phase / Lab:** Phase 2 — Meeting Debian · Lab 00 — Meeting Your Debian Server (🔄 in progress: Blocks A–I observed, Report pending)

**Daily recap (start of day):**
- ✅ Passed. Covered spaced-repetition topics from prior sessions:
  1. OS version importance (`/etc/os-release`, `uname -a`) — answered correctly, connected to incompatible software scenario.
  2. RAM vs disk (`free -h` vs `df -h`) — total 1.9Gi correct; minor clarification: RAM is not "temporary", it's volatile memory vs persistent storage.
  3. System accounts (UID < 1000) and least privilege — initially answered "not users"; after explanation of containment, student correctly explained encapsulation of security failures.
  4. systemctl filtering (`--type=service`, `--state=running`) — answered correctly.
  5. Tilde expansion (`~x` vs `~/x`) — correctly recalled the error from Session 03; explained that without `/` the tilde is literal.
  6. dmesg purpose — correctly identified hardware diagnostics and security restriction; minor clarification: dmesg ≠ process monitoring (that's journalctl/systemd).

**Worked on:**
- **Block E — Storage:** `lsblk -f` → sda1 ext4 root, sda5 swap; `df -h` → 28G total, 9.4G used. `tmpfs` lives in RAM, disappears on power-off. `/etc/fstab` uses UUID for robustness (device names can change with hardware changes).
- **Block F — FHS:** `/etc` = config (unique per machine), `/usr` = software (identical across installations), `/var` = variable data, `/home` = users. Symlinks: `bin -> usr/bin`, `lib -> usr/lib` (Debian modern consolidation).
- **Block G — Software:** 1600 packages installed (more than a clean install due to prior course). `dpkg` = low-level, no dependency resolution; `apt` = high-level, resolves dependencies from repositories.
- **Block H — Network:** `enp0s3` IP `10.0.2.15` (VirtualBox NAT). Gateway `10.0.2.2` translates VM traffic to host internet. `127.0.0.1` = loopback (machine talks to itself). `ss -tulpn` confirmed SSH not listening. CUPS on `127.0.0.1:631` = local-only (security).
- **Block I — Boot logs:** `journalctl -b` shows systemd dependency order (slices → sockets → services → targets). Errors: gnome-keyring, user-session-migration, gnome-software — system continued booting (error encapsulation). User not in `adm`/`systemd-journal` groups limits log visibility.

**Concepts learned / reinforced:**
- UUID in fstab is robust against hardware changes; device names are not.
- FHS separation: `/etc` (admin domain) vs `/usr` (package domain) enables sharing and safe updates.
- dpkg handles local .deb files; apt resolves dependencies from repos.
- Gateway translates private network traffic to internet; loopback is self-communication.
- 0.0.0.0 = all interfaces (risky); 127.0.0.1 = local only (secure).
- systemd boots by dependency order; non-critical service failures don't halt the system.

**Commands / tools used (all read-only):** `lsblk -f`, `df -h`, `cat /etc/fstab`, `mount`, `ls -la /`, `ls -la /etc`, `ls /var`, `ls /usr`, `ls /home`, `dpkg -l | wc -l`, `dpkg -l`, `ip a`, `ip route`, `cat /etc/hosts`, `cat /etc/resolv.conf`, `ss -tulpn`, `journalctl -b`, `journalctl -b -p err`.

**Errors encountered:**
- `ls usr` (without `/`) → "No such file or directory" → corrected to `ls /usr`. Same pattern as tilde lesson: relative vs absolute paths matter.

**Questions still open:**
- SSH not running (Lab 00 = observe only; investigate in Lab 19).
- User not in `adm`/`systemd-journal` groups → limits journalctl visibility; may need to address in Lab 05+ (user management).

**Next session (target):**
- Lab 00 — Fill Report section (8 Mentor Questions answers + self-explanation) + collect screenshots in `screenshots/lab-00/`. Then proceed to Lab 01 (Git).

**Commit / push:** N/A — repository not created yet (Lab 01). Memory files updated in single project folder.

## 2026-08-24 — Session 04 (Lab 00 in progress — Blocks A–D observed)

**Phase / Lab:** Phase 2 — Meeting Debian · Lab 00 — Meeting Your Debian Server (🔄 in progress: Blocks A–D)

**Daily recap (start of day):**
- ✅ Passed. Rotated topics from prior curriculum (Session 03 informal material):
  1. Tilde `~` vs `~/` (why `mkdir ~linux-devops-labs` made a literal folder; `~/x` = home/x). Student had FORGOTTEN this after an 11-day gap → mentor refreshed, re-asked, assimilated. Spaced-repetition note: multi-day breaks create gaps; recap must re-cover prior topics.
  2. `dmesg` / why `sudo` (kernel messages; restricted to root on modern kernels). Answered correctly, no help needed.

**Worked on:**
- 🎓 ACADEMIA DEPLOY — Bloque 1 (this AI leads it together with the Linux session, same daily flow): Sesión 1/9 completed. Topic: 7-floor deployment map + "-aaS" rule + magnetic phrase "Oye, Iré Comprando Pisos Felices Bien Seguros". Bitácora (`03-BITACORA-DE-APRENDIZAJE.md`) updated; próxima = Sesión 2. Student REJECTED the original mixed-housing analogy as unclear and CO-CREATED a new official analogy (TERRENO/property: On-Premise=terreno propio, IaaS=lote alquilado en urbanización, CaaS=casas-módulo, PaaS=casa amueblada, FaaS=hotel, BaaS=condominio, SaaS=oficina operada). Chuleta visual (`04-CHULETA-VISUAL.md`) updated to the new analogy.
- 🔧 LINUX LABS — Lab 00 Bloques A–D (observation only, no changes):
  - **A:** `cat /etc/os-release`, `uname -a`, `hostnamectl`, `uptime` → Debian 13.6 (trixie), kernel `6.12.101+deb13-amd64`, hostname `Debian`, up 1:39. Matches setup verified facts.
  - **B:** 3 CPUs; disk `sda` with partitions sda1/sda2/sda5; `/dev/sda1` ≈28G; RAM total **1.9Gi** (from `free -h`; student first looked in `df` for RAM → mentor clarified df=disk, free=RAM, and total vs available).
  - **C:** `whoami`/`id` → `Erick` UID 1000, GID 1000, groups 1000 + 100(users). `getent passwd`: `root`(0), `Erick`(1000), `Josefa`(human), `daemon` + `Debian-gdm` (system, UID<1000). Rule: system accounts UID<1000, humans ≥1000. Mentor Q2 answered: system accounts exist to run services with least privilege.
  - **D:** `systemctl list-units --type=service --state=running` → ~23 services (incl. ModemManager, colord, systemd-timesyncd). **SSH service NOT found running** (confirmed via `| grep -i ssh`, empty). Real finding vs plan assumption (install chose "SSH server"). Not fixed today (Lab 00 = observe only); flagged for its dedicated lab later. VM appears to have a GRAPHICAL desktop (`colord`/`Debian-gdm`), not headless.

**Concepts learned / reinforced:**
- Observation before action; version matters (package/command differences across versions).
- `df -h` = disk space; `free -h` = RAM (total vs available vs free).
- UID rule: <1000 system, ≥1000 human; system accounts = least privilege.
- Idle server still runs many services ("idle is not empty").
- Pipe `|` + `grep -i` to filter read-only output.

**Commands / tools used (all read-only):** `cat /etc/os-release`, `uname -a`, `hostnamectl`, `uptime`, `lscpu`, `free -h`, `lsblk`, `df -h`, `whoami`, `id`, `getent passwd|less`, `getent group|less`, `who`, `systemctl list-units --type=service --state=running`, `systemctl ... | grep -i ssh`.

**Errors encountered:**
- Student could not interpret `systemctl`/`ps` output at first → mentor error: jumped to questions without building the concept base. Corrected by explaining service/process concepts + output columns first, then a guided question. Lesson: always teach concept before command (AGENTS.md / mentor-constitution).
- SSH-not-running discrepancy → treated as observation data, not a defect to fix now.

**Questions still open:**
- Why is SSH not running? (installed but disabled? not installed?) → investigate in its dedicated lab (Lab 19). Do NOT touch during Lab 00.

**Process clarifications recorded for future sessions (mentor behavior):**
- This AI leads BOTH the Academia Deploy block AND the Linux VPS session in the same daily flow (per `05-RUTINA-DIARIA.md`). Do NOT ask the student "did you do Academia Deploy?" — the AI runs it. Flow: Bloque 1 Academia (10 min) → Bloque 2 Linux Labs (fresh).
- Chat quirk: in this OpenCode interface a leading `/` opens the internal search, so the student types `\` to escape it. Respect `\` as `/` in paths; do not flag it as an error.
- Folder consolidation (2026-08-24): the duplicate at `E:\Datos\IA\Linux VPS - Project` was removed; the single source of truth is now ONLY `C:\Users\XPC\Desktop\Linux VPS - Project` (the one mounted in the VM). No more "official/working copy" split.

**Next session (target):**
- Lab 00 — Bloques E–I (storage, FHS, software, network, boot logs) + Mentor Questions 3–8. Then fill the Lab Report, collect screenshots in `screenshots/lab-00/`, then proceed to Lab 01 (Git).

**Commit / push:** N/A — repository not created yet (Lab 01). Memory files updated in the single project folder (linked to VM); no separate official folder to sync.

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
