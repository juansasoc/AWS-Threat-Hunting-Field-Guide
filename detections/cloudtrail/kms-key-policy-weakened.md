# KMS — Key Policy Weakened
**Why:** Crypto control risk.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "kms.amazonaws.com" AND eventName == "PutKeyPolicy"
| WHERE requestParameters.policy LIKE "%\"Principal\": \"*\"%"
| KEEP requestParameters.keyId, userIdentity.arn, eventTime
```
