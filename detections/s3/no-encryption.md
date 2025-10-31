# S3 — No Server-Side Encryption on Uploads
**Why:** Unencrypted data at rest.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "s3.amazonaws.com" AND eventName IN ("PutObject","CompleteMultipartUpload")
| WHERE responseElements."x-amz-server-side-encryption" IS NULL
| STATS COUNT(*) BY requestParameters.bucketName
```
