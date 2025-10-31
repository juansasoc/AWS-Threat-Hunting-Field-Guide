# API Gateway — API Key Abuse
**Why:** Brute/abuse.

## ES|QL
```esql
FROM apigw.access
| WHERE requestContext.identity.apiKeyId IS NOT NULL
| STATS COUNT(*) AS calls, COUNT_DISTINCT(sourceIp) AS srcs BY requestContext.identity.apiKeyId
| WHERE srcs > 10 OR calls > 1000
```
