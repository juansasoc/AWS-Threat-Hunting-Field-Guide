# Lambda — Unusual Invoke Pattern
**Why:** Key misuse or abuse.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "lambda.amazonaws.com" AND eventName == "Invoke"
| EVAL fn = requestParameters.functionName
| STATS COUNT() AS invocations, COUNT_DISTINCT(sourceIPAddress) AS src_ips BY fn, userIdentity.userName
| WHERE src_ips > 3 OR invocations > 1000
```
