## Attack
- Brute-force against Windows from Kali.
- Hydra’s RDP modules both failed against Windows experimental RDP module, but the RDP attempts still generated the 4625 failure events

## Setup
- Opened RDP through the firewall and made a weak victim account to test on

## Detection
- Built on 60122 (single logon failure)
- Used `frequency=4`, `timeframe=10` and `same_field` on both `targetUserName` and `ipAddress`, so it only fires on repeated failures against one account from one source
- `same_field` on `ipAddress` ensures that 4 unrelated failures across the network will not trigger the rule

## The Gap
- Built in rule caught numerous login failures from the same source individually, but did not correlate them to a brute force login attempt

## My Rule
```xml
  <rule id="100006" level="14" frequency="4" timeframe="10">
    <if_matched_sid>60122</if_matched_sid>
    <same_field>win.eventdata.targetUserName</same_field>
    <same_field>win.eventdata.ipAddress</same_field>
    <description>Brute force login attempt</description>
    <mitre><id>T1110</id></mitre>
  </rule>
```

## Result
![Brute Force Detection](detection-screenshots/Rule100006.png)

## MITRE
- T1110 (Brute Force)
