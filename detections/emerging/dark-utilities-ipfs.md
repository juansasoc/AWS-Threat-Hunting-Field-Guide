# Dark Utilities — Downloader/Exec via IPFS
**Private-ready.** Tune with internal feeds.

## ES|QL
```esql
FROM endpoint.process
| WHERE process.command_line RLIKE "Invoke-Expression|IEX|FromBase64String|curl .*ipfs|wget .*ipfs"
| KEEP host.name, process.name, process.command_line, parent.process.name
```

## Sigma
```yaml
title: Dark Utilities — Downloader/Exec via IPFS
id: auto-dd489551
status: experimental
logsource:
  product: aws
detection:
  selection:
CommandLine|contains:
  - "Invoke-Expression"
  - "IEX"
  - "FromBase64String"
Network|domain|contains: "ipfs"
  condition: selection
level: medium
```

## Tuning
- Maintain feeds (IPFS gateways, mining pools). Exclude CI/dev hosts.

## Validation
- Capture artifacts to sandbox; verify hashes against internal IOC feeds.
