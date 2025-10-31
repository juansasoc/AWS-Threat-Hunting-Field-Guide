# AWS Config — Disabled/Changed Rules
**Why:** Control blindspots.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "config.amazonaws.com" AND eventName IN ("StopConfigurationRecorder","DeleteConfigRule","PutConfigRule")
| KEEP eventTime, userIdentity.arn, eventName, requestParameters
```
