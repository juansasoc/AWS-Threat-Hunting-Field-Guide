# IAM — Root Account Usage
**Why:** Any root activity is high risk.

## ES|QL
```esql
FROM cloudtrail
| WHERE userIdentity.type == "Root"
| STATS count() BY eventName, sourceIPAddress
```

## Validation
- Verify if break-glass documented; rotate access keys if present.
