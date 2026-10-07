# DeadVault Lab Topology

```
                         [ Internet/NAT ]
                               |
                         [ Cisco EDGE-01 ]
                               |
                    +----------+----------+
                    |                     |
                 VLAN 10                VLAN 20
                USERS                  SERVERS
                    |                     |
              WIN-FIN-07        +---------+---------+
                                |         |         |
                              DC-01     FILE-01    BKP-01
                                |
                           VLAN 30 SOC
                                |
                           KALI-ANALYST

                         VLAN 40 VAULT
                                |
                            VAULT-01
```

## Segments
| VLAN | Name | Example subnet | Purpose |
|---|---|---|---|
| 10 | USERS | 10.10.10.0/24 | Windows workstations |
| 20 | SERVERS | 10.10.20.0/24 | AD, file and online backup |
| 30 | SOC | 10.10.30.0/24 | Analyst tooling |
| 40 | VAULT | 10.10.40.0/24 | Isolated recovery copy |

Use RFC1918 addressing only. Keep the lab isolated from business infrastructure.
