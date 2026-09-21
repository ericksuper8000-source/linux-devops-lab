# Lab 05 — Users & Groups

> **Phase:** Phase 4 — Linux Fundamentals
> **Estimated duration:** 1–2 sessions
> **Status:** ✅ Complete (2026-09-14, Session 10)
> **Prerequisites:** Labs 00–04 complete (server observed, Git published, FHS + inodes understood)

---

## Objective

Answer: *"Who can do what on this server, and how does Linux tell them apart?"* Create and inspect a real user the safe way.

## Scenario (real world)

A company hires a new developer. They need their own account on the Debian server — not root, not your account — with only the access they need. You must create them, verify them, and leave the system clean and documented.

## Concepts (why first)

- **Why users exist.** Every person and every service gets its own identity so damage is contained (least privilege). You saw this in Lab 00: `root`, `Erick`, `daemon`, `Debian-gdm`.
- **UID / GID.** Linux doesn't care about names, it cares about numbers. UID = user number, GID = group number. `0` = root (all power). `1–999` = system (services). `1000+` = humans.
- **Where identities live.** `/etc/passwd` = who exists (readable by all). `/etc/shadow` = password hashes (only root can read). `/etc/group` = groups and members.
- **Primary vs secondary groups.** Each user has one primary group (owns their new files) and can be in extra secondary groups (gives extra doors, e.g. `sudo`, `adm`).
- **Creating is changing.** Unlike Lab 00 (observe only), here we modify the system — so we verify before, during, and clean up after.

## Checklist

- [x] Concept check: explain UID/GID ranges with your own words (mentor validates)
- [x] Inspect yourself: `whoami`, `id`, `groups`
- [x] List everyone: `getent passwd | less`, `getent group | less` — find root (0), you (1000), system (<1000)
- [x] Read the three files: `cat /etc/passwd`, `ls -l /etc/shadow` (why denied?), `sudo cat /etc/shadow | head` (why root only?), `cat /etc/group`
- [x] Understand one line format: `name:x:UID:GID:comment:home:shell`
- [x] Create practice group: `sudo groupadd dev-team`
- [x] Create practice user: `sudo useradd -m -s /bin/bash -g dev-team -c "Dev Nuevo" dev-nuevo`
- [x] Verify: `id dev-nuevo`, `getent passwd dev-nuevo`, `getent group dev-team`, `ls -ld /home/dev-nuevo`
- [x] Test secondary group: `sudo usermod -aG sudo dev-nuevo` then `id dev-nuevo` — explain why `-aG` (append, not replace)
- [x] Try login view: `su - dev-nuevo` then `whoami`, `id`, `exit` (no password needed from root/sudo path, explain why)
- [x] Clean up to leave server as found: `sudo userdel -r dev-nuevo`, `sudo groupdel dev-team`
- [x] Verify cleanup: `getent passwd dev-nuevo` (empty), `getent group dev-team` (empty), `ls /home`
- [x] Answer Mentor Questions below in Report

## Mentor Questions

1. What is UID and GID? Which ranges are root, system, human — and how do you tell?
2. What lives in `/etc/passwd` vs `/etc/shadow` vs `/etc/group`? Why can everyone read passwd but only root shadow?
3. What is the difference between primary and secondary group? What breaks if you forget `-a` in `usermod -G`?
4. Why do services get their own system accounts instead of running as root or as you?
5. After `userdel -r`, what disappears and what would remain if you forgot `-r`?

## Report (student fills this after the session)

### What I did

2026-09-14 Session 10: inspected my own account (Erick, UID 1000), created practice group `dev-team` (GID 1001) and user `dev-nuevo` (UID 1001), verified with `id`/`getent`, tested secondary group `sudo` (GID 27) via `-aG`, entered the account with `sudo su -`, then cleaned up with `userdel -r` + `groupdel` and verified empty results plus `/home` back to only Erick.

### How it works / why

UID 0 = root, 1–999 = system, 1000+ = humans. `passwd` is world-readable, `shadow` is root-only (hashes `$y$`, `*` = never login, `!` = locked). Primary group owns new files; secondary groups open extra doors. `-aG` appends without wiping existing groups. `su` asks for the target's password (locked account), `sudo su` uses my own password.

### Commands I used

| Command | Why I used it |
|---|---|
| `whoami` | Confirm who I am before creating anyone |
| `id` | See my UID, GID and groups |
| `getent passwd` | List all users (humans vs system) |
| `getent group` | List all groups |
| `cat /etc/passwd` | See identity file format |
| `ls -l /etc/shadow` | Prove only root can read hashes |
| `cat /etc/group` | See group membership |
| `sudo groupadd dev-team` | Create practice group |
| `sudo useradd -m -s /bin/bash -g dev-team -c "Dev Nuevo" dev-nuevo` | Create practice developer |
| `id dev-nuevo` | Verify UID/GID/groups |
| `sudo usermod -aG sudo dev-nuevo` | Add secondary group (append!) |
| `su - dev-nuevo` | Test the new account view |
| `sudo userdel -r dev-nuevo` | Remove user + home (cleanup) |
| `sudo groupdel dev-team` | Remove practice group (cleanup) |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| `userdel` warned "mail spool not found" | Normal on systems with no mailbox for the user | Expected, no action needed |
| Draft notes contained shadow hashes | Session-10 safety check: repo + GitHub grepped clean (`$y$` = 0) | Draft redacted 2026-09-14; rule: never paste shadow/keys/tokens, only `id`/`getent` |

### Lessons learned / self-explanation

I am Erick, UID 1000 / GID 1000 — a human account. Shadow stays root-only because it holds password hashes: leaking it gives attackers offline cracking material, while `passwd` only holds non-secret identity data. Primary group determines file ownership; secondary groups grant extra access, so forgetting `-a` in `usermod -G` silently strips existing doors. Onboarding uses least privilege: a new developer gets their own account with only needed groups, never root or someone else's account.

### Evidence

- [x] Outputs saved in `screenshots/lab-05/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended
- [x] Execution plan updated
- [x] Committed and pushed to GitHub + GitLab

> 🚀 **Next:** Lab 06 — Permissions & Ownership (`chmod`, `chown`, rwx, `umask`)
