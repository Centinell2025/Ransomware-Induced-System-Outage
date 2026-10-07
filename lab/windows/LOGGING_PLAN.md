# Windows Evidence and Logging Plan

Collect defensive telemetry from:
- Security log authentication events
- PowerShell operational logging
- Process creation telemetry
- File/share access events
- Service state changes
- Backup job and repository audit events
- Time synchronization status

Recommended lab roles:
- DC-01: identity/authentication evidence
- FILE-01: file/share and outage evidence
- BKP-01: backup-access evidence
- VAULT-01: isolation and restore-validation evidence
- WIN-FIN-07: endpoint/process evidence

Use only fictional accounts and disposable lab data.
