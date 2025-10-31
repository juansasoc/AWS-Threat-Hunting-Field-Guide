# Lambda — Secrets in Environment Variables
**Why:** Secret leakage.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "lambda.amazonaws.com" AND eventName IN ("CreateFunction","UpdateFunctionConfiguration")
| WHERE requestParameters.environment LIKE "%AKIA%" OR requestParameters.environment RLIKE "(?i)(secret|token|password)"
| KEEP requestParameters.functionName, userIdentity.arn, eventTime
```
