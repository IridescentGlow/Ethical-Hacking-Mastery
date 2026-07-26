# Lab Status

## Current Phase

Phase 2 — Recon & Networking Fundamentals (in progress)

---

## Current Module

2.2 — Nmap (basic scanning done, version detection next)

---

## Current Lesson

Module 2.2 — Nmap version detection

---

## Current Objective

Continue Module 2.2 with Nmap version detection (moving past port-number guessing to confirmed service versions).

---

# Progress

## Completed Modules

- 1.1 — KVM/QEMU + libvirt + virt-manager installed
- 1.2 — Isolated network `labnet` created and verified active
- 1.3 — Kali VM installed, running headless via SSH
- 1.4 — Metasploitable2 converted (vmdk->qcow2), imported, running on labnet
- 2.1 — TCP/IP concepts needed for scanning (port states: open/closed/filtered, TCP vs UDP basics); tested open vs closed ports manually with netcat (nc -zv) against Metasploitable2; verified services manually (21 ftp, 22 ssh, 23 telnet open; 12345 refused)
- 2.2 (partial, in progress) — basic nmap default scan run against Metasploitable2; learned PORT/STATE/SERVICE output interpretation (service column is a port-based guess, not confirmed); researched unfamiliar services (512 exec/rexec, 53 dns, 6667 irc)

---

## Completed Labs

- Capstone 1 — PASSED. Kali<->Metasploitable2 reachable over labnet; host's real network (wlan0) confirmed separate from labnet (virbr1); host-to-VM reachability on virbr1 is expected/normal (host owns the bridge), true isolation guarantee is VM-to-internet/LAN blocking, confirmed.

---

## Completed Machines

- Kali (attacker) — running headless via SSH, on labnet
- Metasploitable2 — running, on labnet, SSH working (with legacy host-key-algorithm flags)

---

## Current Challenge

None active — Phase 1 complete, Phase 2 not yet started.

---

# Lab Infrastructure

## Host

Arch Linux, 4GB RAM (tight — run one target at a time; higher-RAM laptop earmarked for later phases, esp. Phase 6 AD lab). Shell is **zsh**. Real network: wlan0 (192.168.8.32/24) — confirmed untouched by labnet.

## Virtualization

KVM/QEMU + libvirt/virt-manager. Confirmed working.
Recurring gotcha (resolved): `virsh` CLI vs virt-manager GUI qemu:///session vs qemu:///system mismatch — permanently fixed via `LIBVIRT_DEFAULT_URI` in `~/.zshrc` (not `.bashrc` — wrong shell was the root cause).

## Networks

`labnet` — isolated, 192.168.100.0/24, active, autostart on. Host bridge interface `virbr1` (192.168.100.1). Isolation confirmed: blocks VM->internet/LAN; host->VM reachability via the bridge is normal/expected, not a leak.
Note: no internet access inside labnet — will need temporary connectivity when installing new Kali tools later.

---

# Machines

| Machine | Purpose | Status |
|----------|----------|--------|
| Kali | Attacker | Running headless via SSH, on labnet |
| Metasploitable2 | Linux target | Running, on labnet, SSH reachable |
| Kioptix-Level-1 | Leftover from prior unguided attempt | vmdk present in /var/lib/libvirt/images/, not imported/used, not part of current curriculum |
| DVWA / Juice Shop | Web targets | Planned (Phase 4) |
| Windows 10/Server eval | Windows target | Planned (Phase 5) |
| AD mini-domain (DC + hosts) | AD target | Planned (Phase 6) |

---

# Installed Tools

- Kali default toolset
- openssh-server (in Kali, enabled)
- qemu-img (vmdk->qcow2 conversion)

---

# Known Skills

- KVM/QEMU + libvirt basic admin (virsh, net-list, net-dhcp-leases)
- virt-manager VM creation via "import existing disk"
- SSH into headless VMs, including legacy hosts needing HostKeyAlgorithms/PubkeyAcceptedKeyTypes overrides
- Disk image conversion (qemu-img)
- Linux/terminal troubleshooting: faillock/sudo lockouts, libvirt storage permissions, session/system URI mismatch, bash vs zsh config file mismatch, corrupted terminal state from TERM=xterm-kitty against old SSH daemons (fix: export TERM=xterm-256color, or `reset`/new terminal)
- Basic network isolation verification (ping tests across host/VMs, reading `ip a` to distinguish real NIC from virtual bridges)

---

# Weak Areas

- Previously attempted Kioptix-Level-1 without fundamentals — copy-pasted commands blindly. Phase 2's methodology focus directly targets this.
- Terminal/shell environment fragility (kitty TERM value, zsh vs bash) not yet fully hardened — worth a permanent `~/.zshrc` cleanup pass at some point outside lesson time.

---

# Strengths

Methodical, doesn't give up on unclear errors; comfortable running diagnostic commands step by step once directed.

---

# Notes

- Host RAM 4GB — one target VM at a time recommended.
- Kali always headless via SSH.
- Old/legacy SSH targets need: `export TERM=xterm-256color` before connecting, and `-o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa` for the ssh command itself.

---

# Next Objective

Phase 2, Module 2.1: TCP/IP refresher scoped to what's needed for scanning.
