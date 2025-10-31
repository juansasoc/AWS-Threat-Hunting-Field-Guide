# IAM — Priv-Esc via Policy Attach
**Why:** Rapid permission escalation.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventName IN ("AttachUserPolicy","AttachGroupPolicy","AttachRolePolicy")
| EVAL actor=userIdentity.userName, policy=requestParameters.policyArn
| STATS count() BY actor, policy
| SORT -count
```

## Sigma
```yaml
title: IAM Policy Attach
id: auto-91d6f956
status: experimental
logsource:
  product: aws
detection:
  selection:
eventName:
  - AttachUserPolicy
  - AttachGroupPolicy
  - AttachRolePolicy
  condition: selection
level: medium
```

## Tuning
- Allowlist CI roles; flag admin/wildcard policies.

## Validation
- Review policy diff; check for privilege increase.
