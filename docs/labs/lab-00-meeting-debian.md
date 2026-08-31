# Lab 00 — Meeting Your Debian Server

> **Phase:** Phase 2 — Meeting Debian
> **Estimated duration:** 1–2 sessions
> **Status:** ⬜ Pending
> **Prerequisites:** Phase 1 complete (VM boots, baseline snapshot exists, workspace at `~/linux-devops-labs`)

---

## Objective

Answer **one** question: *"What did we just receive?"*

This lab is pure observation. **No modifications** — no packages installed, no users
created, no configs changed. A real administrator never changes a system they do not
understand yet.

## Scenario (real world)

A company just handed you a server: "This is your new Debian server. Learn it." Your
first instinct as a professional is not to start installing things. It is to **observe**:
What version is this? Who lives here? What is already running? How is it organized? Only
then can you make safe decisions.

## Concepts (why first)

- **Observation before action.** Every change carries risk. Understanding the baseline
  lets you detect what *you* changed later and why.
- **Version matters.** Debian version → package versions, supported behavior, available
  documentation. Kernel version → hardware support. You cannot plan without this.
- **System vs human accounts.** Linux pre-creates accounts for its own components
  (`www-data`, `syslog`, …). Knowing which are "real people" vs "machinery" is the basis
  of every security decision later.
- **Idle is not empty.** A fresh server already runs processes and services. Learning to
  read them is the foundation of process and service management.
- **The filesystem has a contract.** The Filesystem Hierarchy Standard (FHS) dictates
  where things live (`/etc` = config, `/var` = variable data, `/usr` = software, `/home` =
  humans). The layout is not random — it is a convention you will rely on forever.
- **Boot logs tell a story.** The kernel and services log everything that happens at
  boot. Reading them teaches you the boot sequence before you ever study it formally.

## Pre-flight

- [ ] VM boots and you can log in.
- [ ] Baseline snapshot `baseline-clean-debian` exists (Step 5 of `docs/setup.md`).
- [ ] You know your username and the hostname.
- [ ] Your lab document is the copy in the VM:
  `~/linux-devops-labs/docs/labs/lab-00-meeting-debian.md`

> ⚠️ **Rule for this lab:** every command below is read-only. If something goes sideways,
> we have the snapshot — but the goal is to learn to observe, not to depend on undo.

---

## Observations

Run each block, read the output, and note what it tells you. Then answer the "What does
this mean?" line after each block **in your own words** (in the Report section).

### A. What are we?

```bash
cat /etc/os-release      # Debian distribution and version
uname -a                 # kernel name/version, architecture
hostnamectl              # hostname, OS, kernel, hardware (systemd summary)
uptime                   # how long the system has been up, load average
```

> What does this mean? What Debian release is this? Is it 64-bit? What hostname was
> chosen? Why does each of these facts matter for administration?

### B. What hardware do we have?

```bash
lscpu                    # CPU model, cores, architecture
free -h                  # RAM total / used / available (human-readable)
lsblk                    # block devices: disks, partitions, sizes
df -h                    # filesystems and their usage
```

> What does this mean? How many CPUs and how much RAM does the VM have? How big is the
> virtual disk? What is already using space?

### C. Who lives here?

```bash
whoami                   # who you are
id                       # your UID, GID, and groups
getent passwd | less     # every account in /etc/passwd (q to quit)
getent group | less      # every group (q to quit)
who                      # who is logged in
```

> What does this mean? Which entries look like people, which look like system machinery?
> Find `root`, your user, and at least three system accounts. Why do system accounts
> exist? Why does every account have a number (UID)?

### D. What is already running?

```bash
systemctl list-units --type=service --state=running   # services currently running
ps aux --sort=-%mem | less                             # every process, biggest first
```

> What does this mean? What services run on a brand-new server with nobody using it?
> Which one did Debian install because of your install choices (SSH server, standard
> utilities)? Pick any two processes and guess what they do.

### E. How is storage organized?

```bash
lsblk -f                 # devices with filesystem types
df -h                    # what is mounted and how full
mount | less             # all current mounts
cat /etc/fstab           # what is supposed to be mounted at boot
```

> What does this mean? Which partitions exist? What filesystem type is the root
> partition? What is in `/etc/fstab` and why does Debian put it there?

### F. How is the filesystem organized?

```bash
ls -la /                 # top-level directories
ls -la /etc | less       # configuration (first 20 lines are enough)
ls /var                  # variable data
ls /usr                  # system software
ls /home                 # human home directories
```

> What does this mean? The FHS contract: `/etc` = config, `/var` = logs and data that
> change, `/usr` = installed software, `/home` = users, `/tmp` = temporary. Why does
> this separation exist? What would break if everything lived in one folder?

### G. What software is installed?

```bash
dpkg -l | wc -l          # how many packages total (first line is a header)
dpkg -l | less           # the full package list (q to quit)
apt list --installed | less   # alternative view (q to quit)
```

> What does this mean? Roughly how many packages does a clean Debian install have? Find
> the SSH server package and the `util-linux` package. What does `dpkg` do, conceptually?

### H. How is the network configured?

```bash
ip a                    # interfaces and their IP addresses
ip route                # routing table (default gateway)
cat /etc/hosts          # static hostname mapping
cat /etc/resolv.conf    # DNS nameservers
ss -tulpn               # listening ports and sockets (sudo may add details)
```

> What does this mean? What interface exists and what IP does it have (NAT → likely
> `10.0.2.x`)? What is the default gateway? Which ports are open? Why is `ss` showing
> something listening on port 22?

### I. What does the system say about itself?

```bash
journalctl -b | less    # all logs since this boot (q to quit)
journalctl -b -p err    # only errors/worse since boot
```

> What does this mean? Even on a healthy system there are messages. What do the boot
> messages reveal about the order in which services started? Any errors worth noting?

---

## Summary Table — What Each Observation Tells You

| Area | Key command | What it tells an administrator |
|---|---|---|
| Version | `cat /etc/os-release` | What to expect for packages, support, docs |
| Hardware | `lscpu`, `free -h` | Capacity for future workloads |
| Accounts | `getent passwd` | System vs human accounts; security surface |
| Services | `systemctl list-units` | What runs on its own; attack surface |
| Storage | `lsblk -f`, `df -h` | Layout, space, growth planning |
| Filesystem | `ls -la /` | FHS contract; where things belong |
| Software | `dpkg -l` | Installed base; update/upgrade planning |
| Network | `ip a`, `ss -tulpn` | Identity on the network; exposed services |
| Logs | `journalctl -b` | Boot health; troubleshooting starting point |

---

## Mentor Questions

Answer these in the Report section before the lab is considered done:

1. What Debian release and kernel are we on? Why must you know this before changing anything?
2. Which accounts are humans and which are system accounts? How can you tell?
3. What is the difference between a service and a process?
4. Why is `/etc` separate from `/var`? Give one concrete example of each.
5. What is the default gateway and why does the VM have one?
6. What was listening on port 22, and why is that expected?
7. What is the FHS and why is it a "contract"?
8. Name one thing you observed that you cannot explain yet — and where we will find the answer later.

---

## Report (student fills after the session)

### What I did

<Summary of the observation blocks completed, in your own words.>

### How it works / why

<Your answers to the 8 Mentor Questions above.>

### Commands I used

| Command | Why I used it |
|---|---|
| `cat /etc/os-release` | Identify Debian version before anything else |
| … | … |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| … | … | … |

### Lessons learned / self-explanation

> Write 5–10 sentences explaining what a "clean Debian server" is now that you have met
> one. If you can explain it to a friend, you understood the lab.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-00/` (e.g., `01-os-release.png`, `02-users.png`, `03-running-services.png`, `04-network.png`)
- [ ] No packages installed, no users created, no config changed (verify: you changed nothing)
- [ ] Session log entry appended
- [ ] Execution plan Phase 2 checkboxes + Current Status updated
- [ ] Committed and pushed to GitHub + GitLab *(from Lab 01 onward — this is the first commit)*

> 🚀 **Next:** Lab 01 — Installing & Configuring Git, so this entire story becomes
> versioned history.
