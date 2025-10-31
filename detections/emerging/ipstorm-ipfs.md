# IPStorm Mass Download via IPFS
**Private-ready.** Tune with internal feeds.

## ES|QL
```esql
FROM vpcflow
| WHERE dst_domain IN (IPFS_GATEWAYS_FQDN_FEED)
| STATS COUNT(DISTINCT src_addr) AS unique_hosts, SUM(bytes) AS total_bytes BY dst_domain
| WHERE unique_hosts > 5 AND total_bytes > 1000000
```

## Sigma
```yaml
title: IPStorm Mass Download via IPFS
id: auto-e06c97d7
status: experimental
logsource:
  product: aws
detection:
  selection:
request.uri|contains: "/ipfs/"
  condition: selection
level: medium
```

## Tuning
- Maintain feeds (IPFS gateways, mining pools). Exclude CI/dev hosts.

## Validation
- Capture artifacts to sandbox; verify hashes against internal IOC feeds.
