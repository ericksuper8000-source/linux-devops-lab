# Lab 03 — Filesystem & FHS

> **Phase:** Phase 4 — Linux Fundamentals
> **Estimated duration:** 1 session
> **Status:** ✅ Complete (2026-09-07, Session 08)
> **Prerequisites:** Labs 00–02 complete (server observed, Git installed, repos published)

---

## Objective

Understand **why** Linux organizes its files in a specific hierarchy and learn to
navigate it confidently. This is not about memorizing folders — it is about understanding
the contract that every Linux distribution follows.

## Scenario (real world)

A company hands you a Debian server and says: "Find the configuration file for the
network." You do not know where it is. But because Linux follows the **Filesystem
Hierarchy Standard (FHS)**, you know it must be somewhere under `/etc`. You do not
search the whole disk — you know the contract. That is what this lab teaches.

## Concepts (why first)

- **Why a hierarchy exists.** Without a standard, every distribution would organize
  files differently. The FHS is a contract: every Linux system puts configurations in
  `/etc`, variable data in `/var`, software in `/usr`, and users in `/home`. Learn it
  once, navigate any Linux system.

- **The top-level directories.** Each has a specific job:
  - `/etc` = configuration files (the admin's domain)
  - `/var` = data that changes during operation (logs, cache, mail)
  - `/usr` = installed software and libraries (the package manager's domain)
  - `/home` = personal files for each user
  - `/tmp` = temporary files (deleted on reboot)
  - `/opt` = extra software you install manually (third-party apps)

- **Absolute vs relative paths.** An absolute path starts from `/` (the root):
  `/home/Erick/documents`. A relative path starts from where you are:
  `../documents`. Using the wrong type is like giving directions from the wrong
  starting point.

- **Navigation commands.** `pwd` tells you where you are, `cd` moves you, `ls` shows
  you what is there. These are the basics of moving around any Linux system.

## Checklist

- [x] Explain why the filesystem hierarchy exists (concept before commands)
- [x] Run `ls /` and identify each top-level directory
- [x] Enter `/etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt` and observe what is inside
- [x] Explain the difference between `/etc` and `/usr` (config vs software)
- [x] Explain the difference between `/var` and `/tmp` (persistent variable data vs temporary)
- [x] Use `pwd` to confirm your current location
- [x] Use `cd` to move between directories
- [x] Use `ls` with options (`-la`) to see detailed information
- [x] Understand absolute vs relative paths with a real example
- [x] Explain what would break if everything lived in one folder

## Mentor Questions

1. What is the FHS and why is it called a "contract"?
2. If you need to change a service's configuration, where do you look? Why?
3. What is the difference between `/usr` and `/opt`?
4. What happens to files in `/tmp` when the server reboots?
5. Give me an example of an absolute path and a relative path. When would you use each?
6. What would happen if a junior administrator saved log files in `/home` instead of `/var`?

## Report (student fills this after the session)

### What I did

Explored the Linux filesystem hierarchy (FHS) to understand why files are organized the way they are. Navigated through the main directories, practiced absolute and relative paths, and observed symlinks.

### How it works / why

The FHS (Filesystem Hierarchy Standard) is a contract that every Linux distribution follows. It defines where different types of files live: configurations in `/etc`, variable data in `/var`, software in `/usr`, user files in `/home`, temporary files in `/tmp`, and third-party software in `/opt`. This standard means that knowing one Linux system means knowing all of them.

Absolute paths always start from `/` (the root) and work from anywhere. Relative paths start from your current location and only work from that specific spot. The `..` notation means "go up one level."

In Debian modern, several directories are symlinks (`bin -> usr/bin`, `lib -> usr/lib`) because historically they were separate, but now they're consolidated. The symlink points to the real location.

### Commands I used

| Command | Why I used it |
|---|---|
| `ls /` | List all top-level directories |
| `ls /etc` | See configuration files |
| `ls /var` | See variable data directories |
| `ls /usr` | See installed software |
| `ls /home` | See user directories |
| `ls /opt` | Check for third-party software (empty) |
| `ls /tmp` | See temporary files |
| `pwd` | Confirm current location |
| `cd /` | Navigate to root |
| `cd home/Erick/linux-devops-labs` | Practice relative path navigation |
| `cd ../../home/Erick/linux-devops-labs` | Practice `..` (go up levels) |
| `ls -la /` | Detailed listing with permissions and symlinks |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| `ls /opt` returned empty | Normal for fresh Debian install | No third-party software installed yet; `/opt` is for manual installs |

### Lessons learned / self-explanation

The Linux filesystem is not random — it follows a contract (FHS) that every distribution respects. `/etc` is for configuration (the admin's domain), `/var` is for data that changes during operation, `/usr` is for installed software, `/home` is for users, `/tmp` is for temporary files that disappear on reboot, and `/opt` is for third-party applications. Absolute paths work from anywhere; relative paths depend on your current location. Symlinks are pointers — Debian uses them to consolidate historical directories (`bin -> usr/bin`). Breaking the FHS contract (like saving logs in `/home`) confuses other admins who expect things in standard locations.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-03/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended
- [x] Execution plan updated
- [x] Committed and pushed to GitHub + GitLab

> 🚀 **Next:** Lab 04 — Files, Inodes & Links
