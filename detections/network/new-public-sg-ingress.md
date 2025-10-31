# VPC — New Public SG Ingress on Critical Ports
**Why:** Exposure of SSH/RDP/SMB.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventSource == "ec2.amazonaws.com" AND eventName IN ("AuthorizeSecurityGroupIngress","RevokeSecurityGroupEgress")
| EVAL ipRanges = requestParameters.ipPermissions
| WHERE ipRanges LIKE "%0.0.0.0/0%" AND (ipRanges LIKE "%:22%" OR ipRanges LIKE "%:3389%" OR ipRanges LIKE "%:445%")
| KEEP userIdentity.arn, requestParameters.groupId, eventTime
```
