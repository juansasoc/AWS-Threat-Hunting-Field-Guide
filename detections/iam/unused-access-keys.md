# IAM — Unused Access Keys (>=90d)
**Why:** Attack surface.

## ES|QL
```esql
FROM iam.credential_report
| WHERE access_key_1_active == true OR access_key_2_active == true
| WHERE (now() - access_key_1_last_used) > 90d OR (now() - access_key_2_last_used) > 90d
| KEEP user, access_key_1_last_used, access_key_2_last_used
```

## Validation
- Rotate and disable unused keys; contact owners.
