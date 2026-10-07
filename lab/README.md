# DeadVault Enterprise Lab

This optional lab reproduces the defensive investigation environment behind the DeadVault Sherlock.

## Platforms
- Cisco IOS/IOSv or equivalent virtual router/switch appliance
- Windows Server evaluation VMs for identity, file, and backup roles
- Windows client VM for the finance endpoint
- Kali Linux analyst workstation

## Purpose
The lab is for authorized defensive training: network segmentation, log collection, incident triage, evidence correlation, containment, backup validation, and recovery testing.

No ransomware payload is required. The incident is simulated with harmless marker files and synthetic telemetry.

## Suggested virtualization
Use an isolated hypervisor lab (VirtualBox, VMware, Hyper-V, Proxmox, or an equivalent platform). Do not bridge the attack-simulation segment to production networks.

See TOPOLOGY.md and BUILD_GUIDE.md.
