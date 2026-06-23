# Detection Use Cases

Each use case maps a threat to the Wazuh rule that detects it and the response
practiced in the lab.

| # | Use case | Data source | Rule | MITRE |
|---|----------|-------------|------|-------|
| 1 | SSH brute force | `auth.log` (Linux agents) | `100001` | T1110 |
| 2 | SSH login from outside the lab subnet | `auth.log` | `100002` | T1078 |
| 3 | New Windows account created | Windows Event 4720 | `100010` | T1136 |
| 4 | Privilege escalation on logon | Windows Event 4672 | `100011` | T1078 |
| 5 | Unauthorized file change in `/etc` | Syscheck (FIM) | built-in `550/554` | T1565 |

## Incident response flow (practiced)
1. **Triage** — alert lands on the Wazuh dashboard; confirm source host/user.
2. **Scope** — pivot on `srcip` / `agent.name` to find related alerts.
3. **Contain** — isolate host (firewall rule / disable account).
4. **Eradicate & recover** — rotate credentials, restore from known-good.
5. **Document** — write up timeline and tune the rule to reduce false positives.

## Lab layout
- 1× Wazuh single-node manager + dashboard (Docker)
- Agents on Windows 11, Ubuntu Server, and the Docker host
- Sysmon deployed on Windows for richer process/network telemetry
