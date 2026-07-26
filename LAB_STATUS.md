# Lab Status

## Current Phase

Phase 1 — Lab Foundation

---

## Current Module

1.3 complete — next: 1.4

---

## Current Lesson

Module 1.4 — Install Metasploitable2

---

## Current Objective

Add Metasploitable2 as first Linux target on labnet.

---

# Progress

## Completed Modules

- 1.1 — KVM/QEMU + libvirt + virt-manager installed
- 1.2 — Isolated network `labnet` created and verified active
- 1.3 — Kali VM installed, running headless via SSH

---

## Completed Labs

None yet (Phase 1 is infra build, capstone pending)

---

## Completed Machines

- Kali (attacker) — running, headless via SSH, on labnet

---

## Current Challenge

None active

---

# Lab Infrastructure

## Host

Arch Linux, 4GB RAM (tight — run one target at a time until more RAM available; user has a higher-RAM laptop earmarked for later phases, esp. Phase 6 AD lab)

## Virtualization

KVM/QEMU + libvirt/virt-manager. Confirmed working.
Known gotcha: `virsh` CLI can default to `qemu:///session` while virt-manager GUI uses `qemu:///system` — fixed via `LIBVIRT_DEFAULT_URI` export in `.bashrc`.

## Networks

`labnet` — isolated (no host/internet bridge), 192.168.100.0/24, active, autostart on.
Note: isolated network has no internet access — will need temporary NAT/internet reachability when installing new tools inside Kali.

---

# Machines

| Machine | Purpose | Status |
|----------|----------|--------|
| Kali | Attacker | Running, headless via SSH (192.168.100.234 at last check, DHCP) |
| Metasploitable2 | Linux target | Planned (Module 1.4, next) |
| DVWA / Juice Shop | Web targets | Planned (Phase 4) |
| Windows 10/Server eval | Windows target | Planned (Phase 5) |
| AD mini-domain (DC + hosts) | AD target | Planned (Phase 6) |

---

# Installed Tools

- Kali default toolset (via official Kali VM image)
- openssh-server (already present in Kali image, enabled)

---

# Known Skills

- KVM/QEMU + libvirt basic administration (virsh, net-list, net-dhcp-leases)
- virt-manager VM creation via "import existing disk"
- SSH into headless VM from host
- Basic Linux troubleshooting: faillock/sudo lockouts, file ownership/permission issues for libvirt storage

---

# Weak Areas

None identified yet — still in infra setup, no offensive labs run yet.

---

# Strengths

Comfortable debugging Linux system issues (sudo/faillock, libvirt URI mismatch) once pointed at the right diagnostic command.

---

# Notes

- Host RAM is 4GB — real constraint. Kali running at 1536-2048MB headless is workable; running Kali + a target simultaneously will be tight. Consider running one VM at a time for now.
- Run Kali headless (SSH) going forward — GUI desktop caused a host lockup at 4GB RAM.

---

# Next Objective

Module 1.4: Install Metasploitable2 as the first Linux target on labnet.
