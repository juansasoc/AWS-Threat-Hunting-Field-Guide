# VPC — Egress to TOR
**Why:** Exfil/C2.

## ES|QL
```esql
FROM vpcflow
| WHERE dst_addr IN (TOR_IP_FEED) OR dst_domain IN (TOR_DOMAINS)
| WHERE action == "ACCEPT"
| STATS SUM(bytes) AS bytes_out BY src_addr, dst_addr, dst_port
| SORT -bytes_out
```

## Tuning
- Maintain current TOR feeds; exclude exit tests.
