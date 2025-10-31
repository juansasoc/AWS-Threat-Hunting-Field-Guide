# GuardDuty ↔ IAM Changes (24h Correlation)
**Why:** Connect anomalies to identity changes.

## ES|QL
```esql
FROM guardduty.findings AS gd
| JOIN (
    FROM cloudtrail
    | WHERE eventName IN ("CreateAccessKey","AttachUserPolicy","PutUserPolicy","AssumeRole")
    | WHERE eventTime >= now() - 24h
    | KEEP userIdentity.arn, eventName, eventTime, sourceIPAddress
) ON gd.resource.accessKeyDetails.userName == userIdentity.arn
| KEEP gd.severity, gd.type, eventName, gd.service.eventFirstSeen, sourceIPAddress
```
