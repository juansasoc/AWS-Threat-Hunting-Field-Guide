# S3 — Bucket Policy Tamper
**Why:** Backdoor access.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "s3.amazonaws.com" AND eventName == "PutBucketPolicy"
| KEEP requestParameters.bucketName, requestParameters.policy, userIdentity.arn, eventTime
```
