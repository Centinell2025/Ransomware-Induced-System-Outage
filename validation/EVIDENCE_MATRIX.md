# Evidence Coverage Matrix

This file validates challenge construction without publishing answer strings as a walkthrough.

| Investigation area | Primary artifact | Corroborating artifact |
|---|---|---|
| Initial execution | endpoint/process_activity.csv | timeline/enterprise_events.csv |
| Initial identity | endpoint/process_activity.csv | identity/authentication.csv |
| External contact | network/dns_queries.csv | network/connections.csv |
| Privileged identity anomaly | identity/privileged_activity.csv | identity/authentication.csv |
| Lateral movement | identity/authentication.csv | server/file_server_events.csv |
| Data staging | server/file_server_events.csv | timeline/enterprise_events.csv |
| Exfiltration assessment | network/connections.csv | incident/READ_ME_DEADVAULT.txt |
| Backup compromise | backup/backup_access.csv | backup/backup_jobs.csv |
| Recovery trust | backup/recovery_status.txt | backup/backup_access.csv |

Design requirement: each conclusion must be reproducible from at least one primary artifact, and major conclusions should be corroborated where possible.