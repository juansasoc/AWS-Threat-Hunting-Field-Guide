# Lambda — Public Function URL
**Why:** Open invocation surface.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "lambda.amazonaws.com" AND eventName == "CreateFunctionUrlConfig"
| EVAL auth = responseElements.authType
| WHERE auth == "NONE"
| KEEP requestParameters.functionName, userIdentity.arn, sourceIPAddress, eventTime
```
