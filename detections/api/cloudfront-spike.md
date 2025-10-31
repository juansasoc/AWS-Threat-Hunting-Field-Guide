# CloudFront — Spike in 4xx/5xx
**Why:** Abuse/probing.

## ES|QL
```esql
FROM cloudfront.access
| STATS COUNT_IF(status BETWEEN 400 AND 499) AS http4xx, COUNT_IF(status >= 500) AS http5xx BY edge_location, client_ip
| WHERE http4xx > 500 OR http5xx > 50
```
