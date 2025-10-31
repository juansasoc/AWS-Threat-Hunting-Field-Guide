# XMRig Miner Activity (Mining Pools)
**Private-ready.** Tune with internal feeds.

## ES|QL
```esql
FROM vpcflow
| WHERE dst_domain IN (KNOWN_MINING_POOLS) OR dst_addr IN (KNOWN_MINING_IP_FEED)
| STATS SUM(bytes) AS bytes_out, COUNT(*) AS conns BY src_addr, dst_domain
| WHERE bytes_out > 10000000 OR conns > 1000
```

## Sigma
```yaml
title: XMRig Miner Activity (Mining Pools)
id: auto-f4b9bc5c
status: experimental
logsource:
  product: aws
detection:
  selection:
Image|endswith:
  - "\\xmrig.exe"
  condition: selection
level: medium
```

## Tuning
- Maintain feeds (IPFS gateways, mining pools). Exclude CI/dev hosts.

## Validation
- Capture artifacts to sandbox; verify hashes against internal IOC feeds.
