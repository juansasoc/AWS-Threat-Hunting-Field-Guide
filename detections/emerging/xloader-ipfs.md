# XLoader Payload via IPFS
**Private-ready.** Tune with internal feeds.

## ES|QL
```esql
FROM cloudwatch.logs
| WHERE message LIKE "%ipfs://%" OR message LIKE "%/ipfs/%" OR message LIKE "%/ipns/%"
| STATS COUNT() BY log_group, function_name, aws.region
```

## Sigma
```yaml
title: XLoader Payload via IPFS
id: auto-de0e0164
status: experimental
logsource:
  product: aws
detection:
  selection:
CommandLine|contains:
  - "Invoke-WebRequest"
  - "curl"
Network|domain|contains: "ipfs"
  condition: selection
level: medium
```

## Tuning
- Maintain feeds (IPFS gateways, mining pools). Exclude CI/dev hosts.

## Validation
- Capture artifacts to sandbox; verify hashes against internal IOC feeds.
