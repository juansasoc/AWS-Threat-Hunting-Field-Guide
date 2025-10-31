# EBS — Unencrypted Volume Creation
**Why:** Risk to data at rest.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "ec2.amazonaws.com" AND eventName == "CreateVolume"
| WHERE requestParameters.encrypted == false
| KEEP requestParameters.size, requestParameters.availabilityZone, userIdentity.arn, eventTime
```
