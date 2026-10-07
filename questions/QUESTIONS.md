# DeadVault — Investigation Questions

Answer from the evidence. Provide the exact artifact and relevant timestamp/event supporting each conclusion.

1. Which endpoint contains the first **confirmed malicious execution**, and what timestamp establishes it?
2. Which user account was active on that endpoint when the first confirmed malicious execution occurred?
3. What external destination is temporally associated with the suspicious execution on the initially affected endpoint?
4. Which privileged account later authenticated from a source inconsistent with its earlier legitimate administrative activity?
5. What was the first critical server reached using that privileged identity from the compromised workstation?
6. What server-side evidence indicates that data was prepared or staged before the outage?
7. Does the available evidence **prove completed data exfiltration**, or does it only establish staging plus suspicious outbound activity? Explain the evidentiary limit.
8. Which backup system was reached from the compromised workstation during the incident?
9. Why should that online backup system not be treated as a trusted recovery source?
10. Which recovery source remained isolated and passed integrity/restore validation?

## Analyst rule
Do not treat the ransom note as independent proof of data theft. Distinguish observed facts from attacker claims and from analytical inference.