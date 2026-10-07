# DeadVault — Complete VM Deployment Matrix

This matrix defines a reproducible **authorized defensive lab** for the DeadVault Sherlock. All addressing is private RFC1918 space. Keep the exercise isolated from production networks.

## VLAN and addressing plan

| VLAN | Zone | Subnet | Gateway | Purpose |
|---|---|---|---|---|
| 10 | USERS | 10.10.10.0/24 | 10.10.10.1 | Windows user endpoints |
| 20 | SERVERS | 10.10.20.0/24 | 10.10.20.1 | AD, file and online backup |
| 30 | SOC | 10.10.30.0/24 | 10.10.30.1 | Defensive analyst workstation |
| 40 | VAULT | 10.10.40.0/24 | 10.10.40.1 | Isolated recovery source |
| 99 | MGMT | 10.10.99.0/24 | 10.10.99.1 | Optional lab management only |

## VM deployment matrix

| VM / Node | Platform | vCPU | RAM | Disk | Network adapters | VLAN(s) | Static IP | Role | Baseline snapshot | Exercise snapshot |
|---|---|---:|---:|---:|---|---|---|---|---|---|
| EDGE-01 | Cisco IOSv | 1 | 512 MB | 2 GB max | 5 virtual NICs | 10,20,30,40,99 | .1 gateway in each VLAN | Inter-VLAN routing, ACL enforcement, telemetry | S00-EDGE-CLEAN | S10-EDGE-SEGMENTED |
| SW-CORE-01 | Cisco IOSv-L2 | 1 | 768 MB | 4 GB max | 8+ virtual NICs | 10,20,30,40,99 | 10.10.99.2 | VLAN switching/trunks and lab segmentation | S00-SW-CLEAN | S10-SW-VLANS |
| DC-01 | Windows Server | 2 | 4 GB | 60 GB | NIC1 server LAN; optional NIC2 MGMT | 20; optional 99 | 10.10.20.10 | AD DS/DNS, authentication evidence | S00-DC-BASE | S20-DC-LOGGING |
| FILE-01 | Windows Server | 2 | 4 GB | 80 GB | NIC1 server LAN; optional NIC2 MGMT | 20; optional 99 | 10.10.20.20 | Synthetic business shares and file evidence | S00-FILE-BASE | S30-FILE-PREINCIDENT |
| BKP-01 | Windows Server | 2 | 4 GB | 100 GB | NIC1 server LAN; optional NIC2 MGMT | 20; optional 99 | 10.10.20.30 | Online backup repository; intentionally reachable in scenario | S00-BKP-BASE | S30-BKP-PREINCIDENT |
| VAULT-01 | Windows Server | 2 | 4 GB | 100 GB | NIC1 vault only; optional disconnected maintenance NIC | 40 | 10.10.40.10 | Isolated validated recovery copy | S00-VAULT-BASE | S40-VAULT-VALIDATED |
| WIN-FIN-07 | Windows client | 2 | 4 GB | 64 GB | NIC1 users LAN | 10 | 10.10.10.17 | Finance endpoint and initial incident evidence source | S00-FIN-CLEAN | S30-FIN-PREINCIDENT |
| WIN-HR-03 | Windows client | 2 | 4 GB | 64 GB | NIC1 users LAN | 10 | 10.10.10.23 | Benign comparison endpoint / noise | S00-HR-CLEAN | S20-HR-NORMAL |
| WIN-ENG-12 | Windows client | 2 | 4 GB | 64 GB | NIC1 users LAN | 10 | 10.10.10.32 | Benign engineering endpoint / false-positive context | S00-ENG-CLEAN | S20-ENG-NORMAL |
| KALI-ANALYST | Kali Linux | 4 | 8 GB | 80 GB | NIC1 SOC; optional temporary NAT adapter for updates only | 30 | 10.10.30.10 | Blue-team DFIR, packet/log review, hashing, timeline analysis | S00-KALI-BASE | S20-KALI-TOOLS |

## Adapter policy

**EDGE-01:** one logical interface/subinterface per security zone. It is the only intended routing point between lab VLANs.

**Windows endpoints:** one exercise-facing adapter. Avoid dual-homing endpoints because it can bypass the segmentation exercise.

**Servers:** use the SERVER VLAN for exercise traffic. An optional MGMT adapter may be used by the instructor, but disconnect it during scored exercises if it would create an alternate route.

**VAULT-01:** connect only to VLAN 40 during the exercise. Any maintenance adapter must remain disconnected.

**KALI-ANALYST:** the SOC adapter is permanent. A NAT adapter may be enabled temporarily for package updates, then disabled before the exercise starts.

## Snapshot lifecycle

| Stage | Snapshot convention | Meaning |
|---|---|---|
| S00 | S00-<HOST>-BASE | OS installed, patched, no scenario state |
| S10 | S10-<HOST>-NETWORK | VLAN/IP/routing configuration complete |
| S20 | S20-<HOST>-LOGGING | Audit/logging and analyst tools ready |
| S30 | S30-<HOST>-PREINCIDENT | Synthetic users/data and normal activity seeded |
| S40 | S40-<HOST>-INCIDENT | Instructor-generated harmless incident telemetry present |
| S50 | S50-<HOST>-RECOVERY | Containment/recovery exercise state |
| RESET | RESET-<HOST>-KNOWN-GOOD | Tested rollback point for repeating the lab |

Do not place real malware in any snapshot. The S40 incident state should be produced with synthetic logs, harmless marker files, disposable renamed copies, and the supplied DeadVault evidence set.

## Recommended host capacity

Running every node simultaneously at the values above allocates roughly **23 vCPU and 41 GB RAM** before hypervisor overhead. A practical host target is therefore 12+ physical/logical CPU threads, 64 GB RAM, and at least 600 GB SSD/NVMe free space. On a 32 GB host, run only the required Windows comparison endpoint(s) and power down nonessential VMs.

## DNS and naming

- Lab DNS domain: deadvault.lab
- DC-01: dc01.deadvault.lab
- FILE-01: file01.deadvault.lab
- BKP-01: bkp01.deadvault.lab
- VAULT-01: vault01.deadvault.lab
- WIN-FIN-07: win-fin-07.deadvault.lab
- WIN-HR-03: win-hr-03.deadvault.lab
- WIN-ENG-12: win-eng-12.deadvault.lab
- KALI-ANALYST: kali-analyst.deadvault.lab

## Isolation requirement

The lab must not rely on access to a production network. Use host-only/internal networks for the exercise. Internet/NAT access should be temporary and controlled for updates only. Restore all systems to known-good snapshots after each run.
