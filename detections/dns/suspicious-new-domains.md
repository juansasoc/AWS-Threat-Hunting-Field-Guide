# Route53 — Newly Registered Suspicious Domains
**Why:** Early-stage C2/landing.

## ES|QL
```esql
FROM route53.resolver
| EVAL age_days = now() - ti.domains.first_seen(query_name)
| WHERE age_days < 14
| STATS COUNT(*) BY srcaddr, query_name
```
