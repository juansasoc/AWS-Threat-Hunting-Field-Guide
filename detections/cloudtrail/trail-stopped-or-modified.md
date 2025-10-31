# CloudTrail — Trail Stopped/Modified
**Why:** Logging blind.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventName IN ("StopLogging","UpdateTrail","DeleteTrail")
| KEEP userIdentity.userName, sourceIPAddress, eventName, eventTime, requestParameters
```
