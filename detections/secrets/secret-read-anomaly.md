# Secrets Manager — Secret Read Anomaly
**Why:** Credential access.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "secretsmanager.amazonaws.com" AND eventName IN ("GetSecretValue","BatchGetSecretValue")
| STATS COUNT(*) AS reads, COUNT_DISTINCT(userIdentity.arn) AS actors, COUNT_DISTINCT(awsRegion) AS regions BY requestParameters.secretId
| WHERE actors > 3 OR regions > 1
```
