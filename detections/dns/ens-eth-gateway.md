# Route53 — ENS .eth Gateway Lookups
**Why:** Web3 staging signal.

## ES|QL
```esql
FROM route53.resolver
| WHERE query_name LIKE "%.eth.link" OR query_name LIKE "%.eth.limo" OR query_name LIKE "%.eth.xyz"
| STATS COUNT(*) BY srcaddr, query_name
```
