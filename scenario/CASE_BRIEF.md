# DeadVault — Case Brief

## Situation
At 09:17 UTC, Northbridge Components' finance and shared-file services began failing. Within minutes, users reported inaccessible documents and a ransom note appeared on FILE-01.

The incident response team preserved telemetry from endpoints, identity services, network controls, file infrastructure, and backup systems.

## Analyst mission
Reconstruct the incident from the supplied evidence. Determine the first confirmed malicious activity, trace the movement through the environment, assess what happened to backup infrastructure, and decide whether the evidence supports the attacker's claim that data was stolen.

Do not assume that an extortion statement is true. Every conclusion must be supported by artifacts.

## Environment
- WS-FIN-07 — Finance workstation
- WS-HR-03 — HR workstation
- WS-ENG-12 — Engineering workstation
- DC-01 — Identity services
- FILE-01 — Shared file server
- BKP-01 — Online backup server
- VAULT-01 — isolated recovery vault

All names, addresses, users, organizations, events, and indicators in this challenge are synthetic.