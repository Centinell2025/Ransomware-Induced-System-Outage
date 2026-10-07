# Enterprise Environment

```
                    INTERNET
                       |
                    Firewall
                       |
                +------+------+
                |             |
               DMZ       Corporate LAN
                              |
             +----------------+----------------+
             |                |                |
          WS-FIN-07         DC-01           FILE-01
          Finance           Identity         File Server
             |                                 |
             +--------- Internal Network ------+
                              |
                           BKP-01
                       Online Backup
                              |
                       [ISOLATED VAULT]
                          VAULT-01
```

BKP-01 is operationally reachable from the corporate environment. VAULT-01 is intentionally isolated and receives controlled recovery copies.