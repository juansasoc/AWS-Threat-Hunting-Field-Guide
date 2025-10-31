# S3 — Object Public ACL Drift
**Why:** Object-level exposure.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "s3.amazonaws.com" AND eventName == "PutObjectAcl"
| EVAL grants = requestParameters.AccessControlPolicy
| WHERE grants LIKE "%AllUsers%" OR grants LIKE "%AuthenticatedUsers%"
| KEEP userIdentity.arn, requestParameters.bucketName, requestParameters.key, sourceIPAddress, eventTime
```
