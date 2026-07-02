# Enterprise Network Services Lab (DNS & DHCP Implementation)

**Home Lab | Sept. 2024 – Jul. 2025**

## Overview

This project simulates an enterprise network environment built on Windows Server, focused on deploying and managing core network infrastructure services. The lab was designed to replicate real-world helpdesk and network administration scenarios — including service outages, misconfigurations, and client connectivity issues — to build hands-on skills in DHCP and DNS administration, troubleshooting, and documentation.

## Architecture

- **Platform:** Windows Server (Server Manager / GUI administration)
- **Domain:** `corp.lab` (Active Directory Domain Services)
- **Server IP:** `10.0.0.4` (static)
- **Client Network:** `10.0.0.0/24`
- **Roles deployed:** AD DS, DHCP, DNS, File and Storage Services

## What Was Built

### 1. DHCP Configuration
- Authorized the DHCP server role within the AD domain
- Created scope `LAN-Scope-01` covering `10.0.0.50–10.0.0.150` (/24)
- Configured scope options: default gateway, DNS server, and lease duration
- Verified address pool and exclusions to prevent conflicts with static infrastructure IPs (e.g. the DNS/DC server at `10.0.0.4`)
- Planned reservations for consistent IP assignment on key devices (printers, servers)

### 2. DNS Configuration
- Confirmed the auto-created **Forward Lookup Zone** (`corp.lab`) provisioned by AD DS, containing SOA, NS, and Host (A) records
- Created a new **Reverse Lookup Zone** (`0.0.10.in-addr.arpa`), Active Directory–integrated, with secure dynamic updates enabled
- Added Host (A) records for simulated network devices (e.g. `workstation1` → `10.0.0.60`)
- Enabled associated PTR record creation for full forward/reverse name resolution

### 3. Troubleshooting & Fault Simulation
- Diagnosed a failed PTR record creation caused by a missing reverse lookup zone — a common real-world DNS misconfiguration
- Root-caused and resolved the issue by creating the reverse zone, then recreating the host record to confirm successful forward + reverse resolution
- Verified end-to-end resolution using `nslookup` (both `nslookup workstation1.corp.lab` and `nslookup 10.0.0.60`)
- Documented each step, including the exact warning message encountered and the fix applied

### 4. Documentation
- Maintained a running knowledge base of configuration steps, screenshots, and fixes (this repo) to support future incident response and onboarding reference

## Skills Demonstrated

- Windows Server role deployment (Server Manager)
- DHCP scope design, exclusions, and lease management
- DNS forward/reverse zone architecture
- Active Directory–integrated DNS
- Network troubleshooting using `ipconfig`, `nslookup`, and Event Viewer
- Technical documentation and incident write-ups

## Screenshots

See [`/screenshots`](./screenshots) for step-by-step configuration captures, including:
- DHCP scope creation wizard
- DHCP address pool verification
- DNS forward and reverse zone setup
- PTR record troubleshooting and resolution

## Next Steps

- [ ] Configure DHCP failover/redundancy for high availability
- [ ] Add CNAME records for service aliases
- [ ] Simulate additional fault scenarios (IP conflicts, lease exhaustion)
- [ ] Document standard operating procedures for common incidents

---

*This is a personal home lab project built for skills development and portfolio purposes.*
