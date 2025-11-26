# Phase 0 – Environment Setup (VMware + Windows 11 Pro)

Goal: Build a safe, repeatable Windows 11 Pro lab VM using VMware, with snapshots, lab user accounts, and basic hardening so later Sysinternals work is controlled and documentable.

This phase is about getting the environment right. No tools yet, just a clean, solid lab foundation.

---

## 1. Lab Design and Ground Rules

Before touching VMware:

- Do not use your host OS for experiments.
- Treat the VM as disposable: assume it might get messed up, so snapshots matter.
- Do not use real personal credentials or connect this VM to sensitive networks.
- Keep everything you do **documented** so the lab can be rebuilt from scratch.

**Decisions for this lab:**

- Hypervisor: VMware Workstation Pro / Player (desktop)  
- Guest OS: Windows 11 Pro (64-bit)  
- Networking: NAT by default (internet access through host), with possible Host-only later for risky tests  
- Accounts:
  - `LabAdmin` – local admin
  - `LabUser` – standard user for testing

You should update this section with the exact versions you actually use (VMware version, Windows build).

---

## 2. Prerequisites

### 2.1. VMware Installation

1. Download and install **VMware Workstation Pro** or **VMware Workstation Player** on the host machine.
2. Accept defaults unless you have a reason to change them.
3. Reboot if VMware asks for it.

Record:
- VMware product: Workstation Pro / Player
- Version: e.g., `17.x`
- Host OS: e.g., `Windows 11 Pro 64-bit`

### 2.2. Windows 11 Pro ISO

1. Download a **Windows 11** ISO from Microsoft’s official site.
2. Make sure it’s **Windows 11 Pro** or includes Pro as an option during setup.
3. Save the ISO somewhere easy to find on the host (e.g., `D:\ISOs\Win11_Pro.iso`).

Record:
- ISO filename and path
- Windows 11 edition(s) available in the ISO

---

## 3. Create the Windows 11 Pro Virtual Machine (VMware)

The exact wording varies slightly by version, but the flow is the same.

### 3.1. New VM Wizard

1. Open VMware Workstation.
2. Click **File → New Virtual Machine**.
3. When prompted for Configuration:
   - Select **Typical (recommended)**.
4. Installation media:
   - Choose **Installer disc image file (iso)**.
   - Browse to your Windows 11 ISO file and select it.
5. If VMware tries to auto-detect OS:
   - Confirm it shows something like **Windows 11 x64** or **Windows 10 and later x64**.
6. Click **Next**.

### 3.2. Name and Location

1. VM Name: for example `SysinternalsLab-Win11`.
2. Location: choose a folder with enough space, e.g. `D:\VMs\SysinternalsLab-Win11`.
3. Click **Next**.

### 3.3. Disk Configuration

1. When asked for **Maximum disk size**:
   - Use at least **60 GB** (more if you can spare it).
2. Storage options:
   - Prefer **Store virtual disk as a single file** for performance (or split if you need portability).
3. Click **Next**.

### 3.4. Customize Hardware

Before finishing, click **Customize Hardware**.

Recommended settings (adjust if your host is weaker):

- **Memory (RAM)**: 4 GB minimum, 8 GB if you can.
- **Processors**: 2 cores (or more if host allows it).
- **Network Adapter**:
  - Set to **NAT** for now (internet through host, no direct exposure of VM).
- **Display**: leave defaults.
- **Sound/USB/Printers**: leave as default unless you have a reason.

For security and Windows 11 compatibility:

- Check if VMware offers **Trusted Platform Module (TPM)** and **UEFI firmware**:
  - In some versions you can enable TPM by adding a virtual Trusted Platform Module after VM creation.
  - Windows 11 may require UEFI + Secure Boot + TPM; Workstation usually handles this during setup, but if not, you may need to:
    - Power off VM
    - Edit VM settings → Options → Advanced → ensure UEFI is used

Click **Close**, then **Finish** to create the VM.

---

## 4. Install Windows 11 Pro in the VM

### 4.1. Boot and Basic Setup

1. Power on the VM.
2. The VM should boot from the ISO.
3. Choose:
   - Language to install
   - Time and currency format
   - Keyboard or input method
4. Click **Next**, then **Install now**.

### 4.2. License and Edition

1. If prompted for a product key:
   - Click **I don’t have a product key** (you can activate later if needed).
2. When asked to choose edition:
   - Select **Windows 11 Pro**.
3. Accept the license terms.

### 4.3. Installation Type and Partitioning

1. Choose **Custom: Install Windows only (advanced)**.
2. If this is a brand new VM:
   - You will see unallocated space.
   - Select it and click **Next**.
3. Windows will create the needed partitions and begin installing.

Wait for the installation to complete; the VM will reboot several times.

---

## 5. Windows 11 OOBE (Out-of-Box Experience)

Follow the prompts after installation:

1. Region and keyboard layout.
2. Network:
   - If it insists on an online Microsoft account but you want a local lab account:
     - Sometimes you can skip by selecting **I don’t have internet** or using an offline account option.
     - If forced, you can create a throwaway Microsoft account and switch to a local account later.
3. Create an initial account (you can use this temporarily):
   - Use a simple name like `SetupUser` if the wizard won’t let you make a local admin directly how you want.
4. Disable any nonessential telemetry/features you don’t want during setup (personal choice, but note what you select).

Once you reach the desktop, proceed to post-install steps.

---

## 6. Post-Install Configuration

### 6.1. Install VMware Tools

1. In VMware menu: **VM → Install VMware Tools** (or **Update VMware Tools**).
2. Inside the VM, open **File Explorer** and go to the mounted DVD drive containing VMware Tools.
3. Run the installer and accept defaults.
4. Reboot the VM when finished.

This improves performance, mouse integration, and display scaling.

### 6.2. Windows Update

1. Open **Settings → Windows Update**.
2. Click **Check for updates** and install all important updates.
3. Reboot as needed until there are no pending critical updates.

Record:
- Update status (e.g., “Updated as of 2025-xx-xx”).

### 6.3. Basic System Tweaks

In the VM:

1. Enable file extensions:
   - Open File Explorer → **View → Show → File name extensions**.
2. Show hidden files (optional but useful):
   - **View → Show → Hidden items**.
3. Power settings:
   - **Settings → System → Power & battery**:
     - Set the VM to **never sleep** on power/plugged in to avoid interruptions during long captures.
4. Rename PC (optional):
   - **Settings → System → About → Rename this PC**.
   - Use something like `SYSINT-LAB`.

Reboot if renaming.

---

## 7. Create Lab Accounts

You want a clean local admin and standard user for experiments.

1. Open **Settings → Accounts → Other users** (or **Family & other users** depending on build).
2. Add account:

   - Click **Add account**.
   - Use **I don’t have this person’s sign-in information**, then **Add a user without a Microsoft account**.

3. Create **LabAdmin**:
   - Username: `LabAdmin`
   - Password: choose a simple lab-only password.
   - After creation, set account type to **Administrator**.
4. Create **LabUser**:
   - Username: `LabUser`
   - Password: another lab-only password.
   - Leave as **Standard User**.

Document:
- Exact usernames
- Account types
- High-level password pattern (do not store real passwords in the repo).

Log out and verify you can log in as each account successfully.

---

## 8. Networking and Isolation Check

Inside VMware:

1. With VM powered off, open **VM Settings → Network Adapter**.
2. Confirm it is set to:
   - **NAT** (recommended to start).
3. Later, for more isolation, you can:
   - Create a separate **Host-only** network adapter for offline/malware-style scenarios.
   - Disable the NAT adapter and use Host-only when you don’t need internet.

For Phase 0, the important part is:
- You know which network mode you are using.
- You record that choice in your documentation.

---

## 9. Create Lab Folders Inside the VM

In the guest OS:

1. Open File Explorer.
2. Create:

   - `C:\Lab`
   - `C:\Lab\Tools`
   - `C:\Lab\Logs`
   - `C:\Lab\Screenshots`

3. (Optional) Reserve `C:\Sysinternals` for later when you install the Sysinternals Suite in Phase 1.

These folders will be used for storing logs, exports, and screenshots from Sysinternals tools.

---

## 10. Baseline Snapshot Strategy (VMware)

Take a clean baseline snapshot so you can always revert.

### 10.1. Baseline Snapshot

1. Shut down the VM cleanly.
2. In VMware, right-click the VM → **Snapshot → Take Snapshot**.
3. Name it something like:
   - `Baseline-Clean-OS-Updated-With-Accounts`
4. Description:
   - List what’s included: Windows 11 Pro fresh install, VMware Tools, updates, LabAdmin/LabUser created, no Sysinternals tools yet.

This is your go-to “factory reset” for the lab.

### 10.2. Optional Second Snapshot

After you later install some baseline tools (like 7-Zip, a browser, etc.) you can take a second snapshot, for example:

- Name: `Baseline-With-Utilities`
- Description: OS + utilities, before any experiments.

---

## 11. What to Commit to the Repo for Phase 0

In your git repo, for Phase 0, you should add:

- This README file (`phases/phase0-environment-setup/README.md`) updated with:
  - Actual VMware version
  - Actual ISO details
  - Actual RAM/disk/network choices
  - Snapshot names and dates
- Optional documentation file, e.g.:
  - `docs/phase0-environment-notes.md` with:
    - Screenshots of VMware settings
    - Screenshot of snapshot list
    - Any issues and how you fixed them

Do **not** commit:
- ISO files
- Actual VM disk files
- Real passwords or license keys

---

## Phase 0 Completion Checklist

You are done with Phase 0 when:

- [ ] VMware is installed and working.
- [ ] Windows 11 Pro VM is created and boots successfully.
- [ ] VMware Tools are installed.
- [ ] Windows is updated.
- [ ] `LabAdmin` and `LabUser` exist and are tested.
- [ ] Network mode (NAT or other) is documented.
- [ ] Baseline snapshot is created and named.
- [ ] This README and notes are updated and committed.

Once all boxes are checked, you’re ready for **Phase 1 – Sysinternals Fundamentals**.
