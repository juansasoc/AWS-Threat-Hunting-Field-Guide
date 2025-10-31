# VPC — Rare Country Egress
**Why:** Exfil to disallowed geos.

## ES|QL
```esql
FROM vpcflow
| EVAL c = geo.country(dst_addr)
| STATS SUM(bytes) AS bytes_out BY src_addr, c
| WHERE bytes_out > 5000000 AND c IN ("RU","KP","IR","CN")
```
