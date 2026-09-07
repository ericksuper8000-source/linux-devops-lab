# Lab 04 — Files, Inodes & Links

> **Phase:** Phase 4 — Linux Fundamentals
> **Estimated duration:** 1 session
> **Status:** ✅ Complete (2026-09-07, Session 09)
> **Prerequisites:** Lab 03 complete (filesystem hierarchy understood, navigation practiced)

---

## Objective

Understand what a file really is in Linux — not just "a document" but a structure with
metadata, an inode number, and multiple types of links. This is the foundation for
understanding permissions and storage later.

## Scenario (real world)

A server has a log file that two different services need to read. Do you copy it (wasting
space and creating sync problems) or do you link it? Understanding inodes and links lets
you make the right technical decision instead of guessing.

## Concepts (why first)

- **What a file is.** A file in Linux is not just content. It is an inode (metadata +
  pointer to data blocks) and at least one directory entry (the name) that points to that
  inode. The name and the content are separate things.

- **Inodes.** Every file has an inode number. The inode stores: who owns it, permissions,
  size, timestamps, and where the data lives on disk. The name is just a label in the
  directory — you can have multiple names pointing to the same inode.

- **Hard links.** A hard link is another name for the same inode. If you create a hard
  link to a file, both names point to the exact same data. Deleting one name does NOT
  delete the data — only when the last link is gone does the data disappear. Hard links
  cannot cross filesystem boundaries.

- **Soft (symbolic) links.** A soft link is a separate file that contains the path to
  another file. It is a pointer, not a second name. If you delete the original, the soft
  link breaks (becomes a "dangling link"). Soft links CAN cross filesystem boundaries.

- **Why this matters.** Understanding the difference between a copy, a hard link, and a
  soft link prevents data duplication, broken references, and confusion when troubleshooting.

## Checklist

- [x] Explain what a file is in Linux (inode + directory entry)
- [x] Use `ls -li` to see inode numbers
- [x] Create a file and check its inode with `stat`
- [x] Create a hard link and verify it shares the same inode
- [x] Create a soft link and verify it has a different inode
- [x] Delete the original file and observe what happens to each type of link
- [x] Use `file` to identify file types
- [x] Explain the difference between a hard link and a soft link

## Mentor Questions

1. What is an inode and what information does it store?
2. If you create a hard link to a file, then delete the original, what happens to the data?
3. What is the difference between a hard link and a soft link?
4. Why can't hard links cross filesystem boundaries?
5. You have a 1GB log file and two services need to read it. Would you copy it or link it? Why?

## Report (student fills this after the session)

### What I did

Explored the concept of inodes and links in Linux. Created files, hard links, and soft links. Tested what happens when the original file is deleted. Used `stat`, `file`, and `ls -li` to inspect file metadata. Discussed real-world use cases.

### How it works / why

A file in Linux is two things: an inode (metadata + data location) and a directory entry (the name). Every file has an inode number. Hard links create another name for the same inode — both names point to the same data. Deleting one name doesn't delete the data; only when the last link is gone does the data disappear. Soft links create a separate file with its own inode that contains a path to another file. If the original is deleted, the soft link breaks.

Real-world use cases: soft links are used for shortcuts (like `bin -> usr/bin`), switching between software versions (Python 3.11 vs 3.12), and simplifying long paths. Hard links are used for space-efficient backups (no copy needed) and internally by Git to avoid duplicating files between versions.

### Commands I used

| Command | Why I used it |
|---|---|
| `echo "Hola Lab 04" > archivo-prueba.txt` | Create a test file |
| `ls -li archivo-prueba.txt` | See inode number and link count |
| `ln archivo-prueba.txt hard-link.txt` | Create a hard link |
| `ln -s archivo-prueba.txt soft-link.txt` | Create a soft link |
| `ls -li archivo-prueba.txt hard-link.txt soft-link.txt` | Compare all three |
| `rm archivo-prueba.txt` | Delete original to test link behavior |
| `ls -li hard-link.txt soft-link.txt` | Check status after deletion |
| `cat hard-link.txt` | Verify hard link still works |
| `cat soft-link.txt` | Verify soft link is broken |
| `file hard-link.txt` | Identify as "ASCII text" |
| `file soft-link.txt` | Identify as "broken symbolic link" |
| `stat hard-link.txt` | See full inode details |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| None | N/A | N/A |

### Lessons learned / self-explanation

A file is not just content — it's an inode with metadata (owner, permissions, size, timestamps, data location) and a name that points to it. Hard links share the same inode, so deleting the original doesn't affect the data. Soft links have their own inode and are just pointers — they break if the original is deleted. Soft links are common in daily Linux use (system symlinks, shortcuts, version switching). Hard links are less visible but critical for efficient backups and Git's internal storage. Understanding this prevents data loss and confusion when troubleshooting.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-04/`
- [ ] ADR written (if a decision was made): `docs/adr/NNNN-….md`
- [x] Session log entry appended
- [x] Execution plan updated
- [ ] Committed and pushed to GitHub + GitLab

> 🚀 **Next:** Lab 05 — Users & Groups
