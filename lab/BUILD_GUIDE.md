# Build Guide

## VM roles

### Cisco EDGE-01
Purpose: routing, VLAN separation, ACL observation, and network telemetry.
Learning objectives: identify segmentation boundaries, review permitted flows, and validate that the recovery vault cannot be reached directly from the user segment.

### Windows Server — DC-01
Purpose: lab identity services and Windows event telemetry.
Create only fictional lab users and groups.

### Windows Server — FILE-01
Purpose: shared business data and server-side evidence.
Populate it with synthetic finance/contracts documents.

### Windows Server — BKP-01
Purpose: demonstrate why an online backup reachable during an incident may become untrusted.

### Windows Server — VAULT-01
Purpose: isolated recovery source. It should accept controlled copies but reject ordinary user-segment access.

### Windows Client — WIN-FIN-07
Purpose: simulated initial affected workstation. Generate benign/synthetic events that mirror the Sherlock evidence.

### Kali Linux — KALI-ANALYST
Purpose: defensive analyst workstation for evidence review, packet/log inspection, hashing, timeline analysis, and report preparation.

## Safe incident simulation
Do not deploy real ransomware. Simulate impact by using a prebuilt dataset containing renamed copies of disposable lab files, synthetic ransom-note text, and generated logs. Preserve the original dataset so the exercise can be reset.

## Validation
The lab is complete when the analyst can reconstruct the timeline from collected artifacts and demonstrate a clean restore from VAULT-01.
