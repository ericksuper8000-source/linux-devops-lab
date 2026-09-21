# Lab 00 — Meeting Your Debian Server

> **Phase:** Phase 2 — Meeting Debian
> **Estimated duration:** 1–2 sessions
> **Status:** ✅ Complete
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

Completed all 9 observation blocks (A–I) of Lab 00. The goal was to observe the clean Debian server without making any changes:

- **A:** Identified the system: Debian 13.6 (trixie), kernel 6.12.101+deb13-amd64, hostname `Debian`.
- **B:** Inspected hardware: 3 CPUs, 1.9Gi RAM, disk `sda` with partitions sda1 (ext4, root) and sda5 (swap).
- **C:** Identified users and groups: `Erick` (UID 1000, human), system accounts like `root` (UID 0), `daemon`, `Debian-gdm` (UID < 1000).
- **D:** Listed running services: ~23 services active. SSH service NOT found running (confirmed). VM has a graphical desktop (GNOME).
- **E:** Analyzed storage: `lsblk -f` showed sda1 ext4 mounted at `/`, sda5 swap. `df -h` showed 28G total, 9.4G used. `tmpfs` mounts live in RAM and disappear on power-off. `/etc/fstab` uses UUID for robustness.
- **F:** Explored FHS: `/etc` = configuration (124 entries), `/var` = variable data (logs, cache), `/usr` = software (bin, lib), `/home` = users (only `Erick`). Symlinks: `bin -> usr/bin`, `lib -> usr/lib`.
- **G:** Listed software: 1600 packages installed. `dpkg` is low-level (no dependency resolution), `apt` is high-level (resolves dependencies from repos).
- **H:** Inspected network: `enp0s3` IP `10.0.2.15` (VirtualBox NAT), gateway `10.0.2.2`, DNS `8.8.8.8`/`8.8.4.4`. `ss -tulpn` showed no SSH listening. CUPS on `127.0.0.1:631` (local only).
- **I:** Reviewed boot logs: `journalctl -b` showed systemd dependency order (slices → sockets → services → targets). Errors: gnome-keyring failed, user-session-migration failed — system continued booting (error encapsulation). User not in `adm`/`systemd-journal` groups limits log visibility.

### How it works / why

**1. What Debian release and kernel are we on? Why must you know this before changing anything?**
Debian 13.6 (trixie), kernel 6.12.101+deb13-amd64. You must know the version before making changes because different versions support different packages and features. Installing something incompatible could break other programs or cause system instability.

**2. Which accounts are humans and which are system accounts? How can you tell?**
UID >= 1000 are human accounts (like `Erick`, UID 1000). UID < 1000 are system accounts (like `root`, `daemon`, `www-data`). System accounts exist to run services with the principle of least privilege — each service has its own account with only the permissions it needs, so if one service is compromised, the damage is contained and doesn't affect the rest of the system.

**3. What is the difference between a service and a process?**
A process is any program currently running on the system. A service is a process that systemd manages in the background — it keeps it running, restarts it if it fails, and controls when it starts and stops. All services are processes, but not all processes are services.

**4. Why is /etc separate from /var? Give one concrete example of each.**
`/etc` contains configuration files unique to this machine (e.g., `/etc/fstab` defines what disks to mount). `/var` contains data that changes during normal operation (e.g., `/var/log/` stores log files). The separation keeps the admin's configuration separate from the system's variable data, making backups and updates simpler.

**5. What is the default gateway and why does the VM have one?**
The default gateway is `10.0.2.2`. The VM lives on a private network (`10.0.2.x`) that doesn't exist on the internet. The gateway acts as an intermediary that translates the VM's traffic and sends it out through the host computer to reach the internet.

**6. What was listening on port 22, and why is that expected?**
Nothing was listening on port 22. This is unexpected because we selected "SSH server" during installation, but the SSH service is not running. This will be investigated in its dedicated lab (Lab 19).

**7. What is the FHS and why is it a "contract"?**
The Filesystem Hierarchy Standard (FHS) defines where different types of files live: `/etc` for config, `/var` for variable data, `/usr` for software, `/home` for users. It's called a "contract" because every Linux distribution follows the same layout, so if you learn it once, you can navigate any Linux system.

**8. Name one thing you observed that you cannot explain yet — and where we will find the answer later.**
SSH was selected during installation but is not running. We'll find the answer in Lab 19 (SSH), where we'll investigate why it's not active and how to configure it properly.

### Commands I used

| Command | Why I used it |
|---|---|
| `cat /etc/os-release` | Identify Debian version before anything else |
| `uname -a` | Get kernel version and architecture |
| `hostnamectl` | Systemd summary: hostname, OS, kernel, hardware |
| `uptime` | How long the system has been running, load average |
| `lscpu` | CPU model and core count |
| `free -h` | RAM total, used, and available (human-readable) |
| `lsblk -f` | Block devices with filesystem types and mount points |
| `df -h` | Filesystem usage (disk space) |
| `whoami` | Confirm current user |
| `id` | UID, GID, and group membership |
| `getent passwd` | List all accounts in /etc/passwd |
| `getent group` | List all groups |
| `systemctl list-units --type=service --state=running` | List active services |
| `cat /etc/fstab` | See what is configured to mount at boot |
| `mount` | See all currently mounted filesystems |
| `ls -la /` | Top-level directory structure |
| `ls -la /etc` | Configuration files |
| `ls /var` | Variable data directories |
| `ls /usr` | System software directories |
| `ls /home` | User home directories |
| `dpkg -l \| wc -l` | Count installed packages |
| `dpkg -l` | List all installed packages |
| `ip a` | Interfaces and IP addresses |
| `ip route` | Routing table and default gateway |
| `cat /etc/hosts` | Static hostname mappings |
| `cat /etc/resolv.conf` | DNS nameservers |
| `ss -tulpn` | Listening ports and sockets |
| `journalctl -b` | All logs since this boot |
| `journalctl -b -p err` | Only errors since boot |

### Problems encountered

| Problem | Investigation | Solution |
|---|---|---|
| SSH service not running despite being selected during installation | Confirmed via `systemctl` and `ss -tulpn` — no SSH process or port 22 | Observation only; will investigate in Lab 19 |
| `ls usr` returned "No such file or directory" | Forgot the leading `/` for absolute path | Corrected to `ls /usr` — same lesson as tilde: paths need correct context |
| User cannot see all journalctl messages | Hint says user not in `adm` or `systemd-journal` groups | Need to add user to those groups (covered in future user management labs) |

### Lessons learned / self-explanation

A "clean" Debian server is not empty — it already has 1600 packages, ~23 running services, a graphical desktop, and network configuration out of the box. The system is organized by the FHS contract: config in `/etc`, variable data in `/var`, software in `/usr`, users in `/home`. Every service runs under its own system account for security (least privilege). The network uses NAT through VirtualBox with a gateway to reach the internet. Boot logs show systemd starts everything by dependency order, and non-critical failures don't stop the system. The most important lesson: always observe before you change — understanding the baseline is the foundation of every safe administration decision.

### Evidence

- [ ] Screenshots saved in `screenshots/lab-00/` (e.g., `01-os-release.png`, `02-users.png`, `03-running-services.png`, `04-network.png`)
- [ ] No packages installed, no users created, no config changed (verify: you changed nothing)
- [ ] Session log entry appended
- [ ] Execution plan Phase 2 checkboxes + Current Status updated
- [ ] Committed and pushed to GitHub + GitLab *(from Lab 01 onward — this is the first commit)*

> 🚀 **Next:** Lab 01 — Installing & Configuring Git, so this entire story becomes
> versioned history.
