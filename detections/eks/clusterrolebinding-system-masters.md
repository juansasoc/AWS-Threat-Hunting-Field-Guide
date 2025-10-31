# EKS — ClusterRoleBinding to cluster-admin/system:masters
**Why:** Privilege escalation.

## ES|QL
```esql
FROM kubernetes.audit
| WHERE objectRef.resource == "clusterrolebindings" AND verb IN ("create","update")
| WHERE requestObject.roleRef.name == "cluster-admin" OR requestObject.subjects.name == "system:masters"
| KEEP user.username, requestObject, stageTimestamp
```
