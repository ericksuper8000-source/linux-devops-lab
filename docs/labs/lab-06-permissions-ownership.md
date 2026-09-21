# Lab 06 — Permissions & Ownership

> **Phase:** Phase 4 — Linux Fundamentals
> **Estimated duration:** 1–2 sessions
> **Status:** ✅ Complete (2026-09-21, Session 11)
> **Prerequisites:** Labs 00–05 complete (FHS, inodes, users/groups understood)

---

## Objective

Answer: *"We know who exists (Lab 05). Now: what can each one do?"* Control read, write
and execute on every file for owner, group and others.

## Scenario (real world)

The new developer from Lab 05 needs to **read** a config file but **not modify** it.
A deploy script must be **executable** but not editable by anyone except its owner.
The whole team shares one file without opening it to the rest of the server. Today we
learn to put those locks on.

## Concepts (why first)

- **Why permissions exist.** `/etc/shadow` is readable only by root while `/etc/passwd`
  is readable by all — observed since Lab 00. Without per-file locks, any user could
  read password hashes or delete system logs.
- **UGO are 3 classes, not 3 users.** Owner, group, others — each file answers "what
  can each class do".
- **rwx + numbers.** r=4, w=2, x=1, summed per class. 7=rwx, 6=rw-, 4=r--, 0=---.
  640 = owner rw, group r, others nothing. 644 = world-readable, owner-only writable.
- **chmod numeric vs symbolic.** Numeric sets everything at once (`chmod 640`); symbolic
  adjusts one piece (`chmod o+r`).
- **chown needs root, chgrp doesn't (mostly).** Giving files away breaks accountability
  and disk quotas, so only root reassigns owners. Group can be changed by the owner if
  they belong to that group.
- **Debian private groups.** Each user gets a same-name primary group, so new files are
  born private (`Erick:Erick`). Sharing is a deliberate act (`chgrp`).
- **umask is the birth mold.** Files are born from base 666 minus umask (002 → 664);
  directories from 777. Nothing is born too open by accident.
- **Giving away ownership demotes you.** After `chown root`, the creator falls into the
  group/others lock — experienced live as Permission denied.

## Checklist

- [x] Concept check: decode a full `ls -l` line field by field (mentor validates)
- [x] Explain UGO classes in own words (owner / group / others)
- [x] Compute 664, 640, 644 from rwx by hand
- [x] Create practice file: `echo ... > ~/permiso-test.txt`, confirm birth perms 664
- [x] `chmod 640` → mini-shadow (others stripped), explain why it protects better
- [x] `chgrp users` → change which group the middle lock serves, verify column change
- [x] `sudo chown root` → observe owner change, attempt write → Permission denied, explain why
- [x] `sudo chown Erick` → restore ownership, verify
- [x] `chmod o+r` (symbolic) → 644, compare with `/etc/passwd` model
- [x] Read `umask` (0002), explain the 666−002=664 subtraction
- [x] Why Debian files are born `Erick:Erick` (private primary group)
- [x] Real-world recipe: `chgrp dev-team` + `chmod 640` for team sharing (links Lab 05)
- [x] Clean up: `rm` test file, verify gone (leave server as found)
- [x] Answer Mentor Questions below in Report

## Mentor Questions

1. Decode `-rw-r----- 1 root shadow`: who can read `/etc/shadow` and why did Erick get Permission denied in Lab 05?
2. What changes with `chmod 640` vs `664`, and why does 640 protect better?
3. Why is a new file born `Erick:Erick`? What is a private primary group for?
4. Real case: the team must read a config but outsiders must not see it — what two commands?
5. You create a file, then `chown root` it. Can you still write to it? Why?
6. Your umask is 0002 and files are born 664 — show the subtraction. Where does 666 come from?

## Report (student fills this after the session)

### What I did

2026-09-21 Session 11: decoded `ls -l` output from Debian.txt (passwd 644, shadow 640),
created `~/permiso-test.txt` (born 664), converted it to mini-shadow (`chmod 640`),
changed its group to `users` (`chgrp`), gave it to root (`sudo chown root`) and felt
Permission denied on write, restored ownership, converted to mini-passwd (`chmod o+r`
→ 644), read `umask` (0002), then deleted the test file and verified it was gone.

### How it works / why

Every file carries owner + group + three rwx locks (UGO). Numbers are sums (r=4, w=2,
x=1): 640 = owner rw, group r, others none. chmod sets what each class can do;
chown/chgrp set who those classes are. Only root gives files away (quotas +
accountability). umask 002 subtracts others-write from the 666 birth base, so files
are born 664. Debian's private-group default keeps new files private until deliberately
shared via chgrp — the midpoint between "only me" and "everyone".

### Commands I used

| Command | Why I used it |
|---|---|
| `ls -l /etc/passwd /etc/shadow` | Observe the two real-world models (644 vs 640) |
| `ls -l ~` | See ownership of home directories |
| `echo "experimento lab 06" > ~/permiso-test.txt` | Create disposable practice file |
| `ls -l ~/permiso-test.txt` | Verify birth permissions (664) |
| `chmod 640 ~/permiso-test.txt` | Strip others → mini-shadow |
| `chgrp users ~/permiso-test.txt` | Move the middle lock to group `users` |
| `sudo chown root ~/permiso-test.txt` | Give file away (needs root) |
| `echo "sigo siendo dueño?" >> ~/permiso-test.txt` | Prove the creator lost write access (denied) |
| `sudo chown Erick ~/permiso-test.txt` | Restore ownership |
| `chmod o+r ~/permiso-test.txt` | Symbolic: give read back to others → 644 |
| `umask` | Reveal the birth mold (0002) |
| `rm ~/permiso-test.txt` | Cleanup; verify gone |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| Typed `ls` in the chat instead of the VM (typo) | Wrong window | Discarded, re-ran in VM |
| Couldn't predict resulting number for `chmod o+r` on 640 | Mentor rephrased in micro-steps (0+4=?) | Answered 644 independently, then verified live |

### Lessons learned / self-explanation

UGO are three locks, not three users: owner, group, others. Numbers are just sums —
640 means owner reads+writes, group reads, others get nothing. Changing permissions
(chmod) is half the system; deciding who fills each slot (chown/chgrp) is the other
half. Only root reassigns owners because giving away files would dodge responsibility.
Files are born 664 because umask 002 bites "write" off others from the 666 mold — and
Debian makes them born `Erick:Erick` so they start private. Sharing with a team is
deliberate: `chgrp team` + `chmod 640`.

### Evidence

- [x] Outputs saved in `screenshots/lab-06/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended
- [x] Execution plan updated
- [ ] Committed and pushed to GitHub + GitLab (pending student VM sync + push)
