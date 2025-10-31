# S3 — Bucket Public ACL/Policy
**Why:** Data exposure.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "s3.amazonaws.com" AND eventName IN ("PutBucketAcl","PutBucketPolicy")
| EVAL acl = requestParameters."x-amz-acl", policy = requestParameters.policy
| WHERE acl IN ("public-read","public-read-write") OR policy LIKE "%\"Principal\": \"*\"%"
| KEEP userIdentity.userName, requestParameters.bucketName, acl, policy, sourceIPAddress, eventTime
```
