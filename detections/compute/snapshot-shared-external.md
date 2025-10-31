# EBS — Snapshot Shared Externally
**Why:** Data leakage.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "ec2.amazonaws.com" AND eventName == "ModifySnapshotAttribute"
| WHERE requestParameters.createVolumePermissionItems LIKE "%\"userId\"%"
| KEEP requestParameters.snapshotId, userIdentity.arn, eventTime
```
