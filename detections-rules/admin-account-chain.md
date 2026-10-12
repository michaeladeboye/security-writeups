## Attack
- `net user hacker Password123! /add`
- `net localgroup Administrators hacker /add`

## Detection
- Produced events 4720 and 4732 respectively
- The built in rules 60109 and 60154 caught each one

## The Gap
- Neither built-in rule catches the chain and each fires on normal activity as well

## My Rules
**Rule 100002:**
```xml
 <rule id="100002" level="3">
    <if_sid>60109</if_sid>
    <description>Account created (chain tracking)</description>
    <group>attack_chain,</group>
  </rule>
```
Tags the account-creation event into the attack_chain group

- **Rule 100003:**
```xml
 <rule id="100003" level="3">
    <if_sid>60154</if_sid>
    <description>Added to Administrators (chain tracking)</description>
    <group>attack_chain,</group>
  </rule>
```
Tags the admin-group-add event into the attack_chain group

- **Rule 100004:**
```xml
  <rule id="100004" level="14" frequency="2" timeframe="60">
    <if_matched_group>attack_chain</if_matched_group>
    <same_field>win.eventdata.subjectUserName</same_field>
    <description>Windows account created and added to administrators group</description>
    <mitre><id>T1136.001</id></mitre>
  </rule>
```

Detects when both events from rules 100002 and 100003 land within 60s from the same user

## Result
Custom rule 100004 triggered at level 14 when account is created and added to admin group
![Detection Result](detection-screenshots/Rule100004.png)

## MITRE
- T1136.001
- T1098.007
