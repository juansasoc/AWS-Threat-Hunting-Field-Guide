# IAM — Access Key Created
**Why:** Foothold/persistence risk.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventName == "CreateAccessKey"
| EVAL actor = userIdentity.userName, src = sourceIPAddress
| STATS count() AS events, MIN(@timestamp) AS first_seen, MAX(@timestamp) AS last_seen BY actor, src
| SORT -last_seen
```

## Sigma
```yaml
title: AWS IAM Access Key Created
id: auto-56d83bc7
status: experimental
logsource:
  product: aws
detection:
  selection:
eventName: CreateAccessKey
  condition: selection
level: medium
```

## Tuning
- Allowlist automation users; alert on human actors.

## Validation
- Confirm via IAM credential report; check subsequent API usage.
