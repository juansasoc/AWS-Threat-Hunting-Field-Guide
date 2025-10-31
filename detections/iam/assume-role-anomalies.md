# IAM — AssumeRole Anomalies
**Why:** Lateral movement / abuse.

## ES|QL
```esql
FROM cloudtrail
| WHERE eventName == "AssumeRole"
| EVAL actor=userIdentity.arn, role=requestParameters.roleArn
| STATS COUNT() AS uses, COUNT_DISTINCT(sourceIPAddress) AS src_ips BY role, actor
| WHERE src_ips > 3 OR uses > 100
```
