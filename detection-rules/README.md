# Detection Engineering: Attack & Detect Cycles

A set of attack-and-detect exercises in my home lab (Kali attacker, Windows 11 + Sysmon endpoint, Wazuh SIEM). For each attack I ran it, found the resulting events, and either wrote a custom Wazuh rule to catch it or evaluated whether the built-in detection was already sufficient. See the [home lab build](../home-lab/README.md) for the environment

All custom rules live in [local_rules.xml](local_rules.xml)

## Cycles

| # | Attack | Technique | Detection approach | Rule |
|---|---|---|---|---|
| 1 | [New admin account](admin-account-chain.md) | T1136.001 | Correlation: account created + added to Administrators by same user within 60s | 100004 (lvl 14) |
| 2 | [Scheduled task persistence](scheduled-task-persistence.md) | T1053.005 | Field match on task definition (runs as SYSTEM) | 100005 (lvl 12) |
| 3 | [Encoded PowerShell](suspicious-powershell.md) | T1059.001 | Built-in rule sufficient; found a severity-inversion tuning issue | built-in 92057 |
| 4 | [Brute-force login](brute-force.md) | T1110 | Frequency: repeated logon failures, same user + same source IP | 100006 (lvl 14) |

## What this demonstrates
- Writing custom Wazuh rules across the main rule types: correlation, field matching, and frequency/threshold
- Reading raw Windows and Sysmon events to find the right fields and parent rules to build on
- Knowing when a built-in rule is already enough, and spotting tuning problems (cycle 3's severity inversion)
- Mapping each detection to MITRE ATT&CK

## Recurring lesson
You can only detect what gets logged, and a log only becomes an alert if a rule matches it
