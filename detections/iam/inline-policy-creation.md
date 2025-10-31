# IAM — Inline Policy Creation
**Why:** Hard-to-track permissions.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventName IN ("PutUserPolicy","PutGroupPolicy","PutRolePolicy")
| KEEP eventTime, userIdentity.arn, requestParameters.policyName, requestParameters.policyDocument
```

## Validation
- Extract policy; review for risky actions/resources.
