# SETUP — VirtualBox + Debian Environment

**Phase:** Phase 1 — VM Environment Setup
**Objective:** Prepare a clean, safe, reproducible environment. **No Linux is learned in
this phase — this is pure preparation so no later step depends on unstated assumptions.**

**Estimated duration:** 1–2 sessions

---

## Assumptions Being Eliminated

By the end of this phase, the following are **not assumed** — they are verified facts:

- VirtualBox is installed on the Windows 10 host.
- A Debian 64-bit VM exists and boots.
- Guest Additions are installed (shared folders work).
- The project template lives inside the VM.
- A baseline snapshot exists (rollback point for the entire project).

---

## Verified Facts (2026-08-13, Setup 01)

These replace the plan's placeholders — they are the **real configuration of this machine**:

- **VirtualBox:** 7.2.4 r170995
- **VM name:** `Debian` (the plan suggested `debian-devops-labs`; the name is only a label and was kept as-is)
- **OS type:** Debian (64-bit)
- **System:** Base memory **2048 MB** · **3 processors** (plan asked 2) · Boot order: Hard Disk, Optical, Floppy · Acceleration: Nested Paging, KVM Paravirtualization
- **Display:** Video memory 16 MB · Graphics controller VMSVGA · Remote Desktop / Recording: disabled
- **Storage:** IDE controller with empty optical drive · SATA Port 0: `Debian.vdi` (Normal, **30.00 GB** — plan asked 25 GB)
- **Network:** Adapter 1 — Intel PRO/1000 MT Desktop (**NAT**)
- **Audio:** ICH AC97 (host default) · **USB:** OHCI + EHCI controllers, 0 device filters

> ISO evidence still pending: record the exact Debian ISO filename in `session-log.md` on first boot.

### Guest OS — first boot verification (2026-08-13)

- **User:** `Erick` (home: `/home/Erick`)
- **Static hostname:** `Debian`
- **OS:** Debian GNU/Linux 13 (trixie) — `VERSION_ID=13`, `DEBIAN_VERSION_FULL=13.6`
- **Kernel:** `6.12.101+deb13-amd64` — architecture **x86-64** (SMP PREEMPT_DYNAMIC)
- **Virtualization:** `oracle` (VirtualBox detected from inside the guest)
- **Chassis:** `vm` · **Hardware:** VirtualBox (innotek GmbH)
- **Uptime at check:** 10 min, 1 user, load ~1.15

---

## Step 1 — Create the Debian VM

### 1.1 Verify VirtualBox

- [ ] Open VirtualBox on Windows 10.
- [ ] Confirm the version (Help → About). Any recent 7.x is fine.

### 1.2 Download the Debian ISO

- [ ] Download the **stable** Debian 64-bit ISO (netinst recommended) from https://www.debian.org/distrib/
- [ ] Record the exact ISO file name in `session-log.md` (evidence of what was installed).

### 1.3 Create the VM

- [ ] In VirtualBox: **New**
  - [ ] Name: `debian-devops-labs`
  - [ ] Type: **Linux** · Version: **Debian (64-bit)**
  - [ ] Memory: **2048 MB** (adjust if your host has little RAM)
  - [ ] Create a virtual hard disk: **VDI, dynamically allocated, 25 GB**
  - [ ] Settings → System → Processor: **2 CPUs**
  - [ ] Settings → Network → Adapter 1: **NAT** (default; keep it simple)
- [ ] Mount the ISO and boot the installer.

### 1.4 Install Debian (no assumptions)

During installation:

- [ ] Use the **entire disk** (guided partitioning) — simple and correct for a lab.
- [ ] Profile: you choose the hostname and a normal user with `sudo` access.
- [ ] On the "software selection" screen check:
  - [ ] **SSH server**
  - [ ] **standard system utilities**
  - [ ] (A desktop environment is **optional**. A server without GUI is closer to a real
        admin environment and is recommended.)
- [ ] GRUB installed to the main disk.

### 1.5 First boot verification

- [ ] Log in with your normal user.
- [ ] Run `whoami` and `pwd` — confirm you are yourself, in your home directory.
- [ ] Run `hostnamectl` — note the OS, kernel, and hostname.
- [ ] Record these facts in `session-log.md`.

> ⚠️ If anything about the install is unclear, stop and ask the mentor. This base must be
> rock-solid because every lab builds on it.

---

## Step 2 — Install VirtualBox Guest Additions

Guest Additions provide shared folders, better video, clipboard sharing, and seamless
mouse integration. They must match the kernel of the installed system.

- [ ] From the VM menu **Devices → Insert Guest Additions CD image…**
- [ ] The VM will mount a CD. Check what was mounted (`ls /media/...` or press the eject
      auto-run). If needed:
  - [ ] `sudo apt update`
  - [ ] `sudo apt install build-essential dkms linux-headers-$(uname -r)`
- [ ] Run the installer inside the mounted CD:
  - [ ] `sudo sh /media/<mountpoint>/VBoxLinuxAdditions.run`
- [ ] Reboot: `sudo reboot`
- [ ] After reboot, verify the module is loaded:
  - [ ] `lsmod | grep vboxguest` (should show `vboxguest` / `vboxsf`)

> Take your time here. If the kernel headers step is unfamiliar, that is exactly the kind
> of thing the mentor will walk you through when we reach package management — for now,
> just follow the steps and ask questions.

---

## Step 3 — Configure the Shared Folder

The shared folder is the bridge between your Windows host (planning) and the Debian VM
(project home). Git and the repository live **inside the VM**; the shared folder lets you
copy the template in and pull evidence out.

- [ ] **On Windows:** decide the host folder to share. Recommended: `C:\Users\<you>\Desktop\Linux VPS - Project`
- [ ] In VirtualBox: **Devices → Shared Folders → Shared Folders Settings…**
  - [ ] Add → Folder path: the host folder above
  - [ ] Folder name: `linux-vps-project`
  - [ ] Check **Auto-mount**
  - [ ] (Leave "Read-only" **unchecked**)
- [ ] **In the VM:** create the mount point and mount:
  - [ ] `sudo mkdir -p /mnt/host`
  - [ ] `sudo mount -t vboxsf linux-vps-project /mnt/host`
- [ ] Verify: `ls /mnt/host` → you should see `README.md`, `AGENTS.md`, `docs/`, …
- [ ] Optional (recommended): make it persistent so you don't mount by hand every boot.
  The mentor will teach you how in the Storage labs — for now, mounting manually is fine.

> 💡 If `mount -t vboxsf` fails, Guest Additions are not loaded (Step 2). Fix Step 2 first.

---

## Step 4 — Create the Project Workspace in the VM

The real project home is `~/linux-devops-labs` inside the VM. Git will be initialized
here in Lab 01; pushes to GitHub/GitLab will originate here.

- [ ] Create the folder: `mkdir -p ~/linux-devops-labs`
- [ ] Copy the template from the shared folder (excluding the private `_archive/`):
  - [ ] `cp -r /mnt/host/README.md /mnt/host/AGENTS.md /mnt/host/.gitignore ~/linux-devops-labs/`
  - [ ] `cp -r /mnt/host/docs ~/linux-devops-labs/`
  - [ ] `mkdir -p ~/linux-devops-labs/screenshots ~/linux-devops-labs/scripts`
- [ ] Verify the structure matches `README.md`:
  - [ ] `find ~/linux-devops-labs -type f | sort`
- [ ] Confirm you can write inside it: `touch ~/linux-devops-labs/.writetest && rm ~/linux-devops-labs/.writetest`

---

## Step 5 — Baseline Snapshot

A snapshot is a frozen state of the whole VM. From here on, every experiment can be
undone by reverting. This is the safety net for the entire project.

- [ ] Close the VM (or leave it running — VirtualBox allows snapshots on live machines).
- [ ] In VirtualBox: **Machine → Take Snapshot**
  - [ ] Name: `baseline-clean-debian`
  - [ ] Description: clean Debian install, Guest Additions, shared folder, workspace created
- [ ] Reboot the VM and confirm it still boots and you can see `/mnt/host`.

---

## Definition of Done (Phase 1)

- [x] VM boots cleanly; hostname and user known (`Debian` / `Erick`).
- [x] Guest Additions loaded (`lsmod | grep vboxguest` → `vboxguest` present).
- [x] Shared folder mounted and writable (`/mnt/host` ↔ `linux-vps-project`).
- [x] Workspace `~/linux-devops-labs` mirrors the template (verified with `find`).
- [x] Baseline snapshot exists and the VM was verified after it (`baseline-clean-debian`).
- [x] Session log updated; `execution-plan.md` Phase 1 checkboxes ticked.

> Note: Git is **not** installed yet on purpose. Version control starts in **Lab 01**
> right after **Lab 00**, so that the very first commit captures the clean-server story.
