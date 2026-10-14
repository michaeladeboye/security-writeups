## Attack
- Encoded/obfuscated PowerShell using common evasion flags:
  `powershell.exe -NoProfile -ExecutionPolicy Bypass -EncodedCommand <base64>`
- Flags: `-NoProfile` (skip profile/configs), `-ExecutionPolicy Bypass` (ignore script policy), `-EncodedCommand` (Base64-encode the command so the real text isn't visible). Decoded payload was a harmless Write-Host.

## Detection
- Caught by built-in rule 92057 (level 12): "Powershell.exe spawned a powershell process which executed a base64 encoded command"
- Wazuh already detects this technique; no custom rule needed

## Finding: severity inversion (tuning issue)
- A second rule, 92213 (level 15, "Executable file dropped in folder commonly used by malware"), also fired — triggered by PowerShell's `__PSScriptPolicyTest` temp file, not by my attack
- The side-effect rule (92213) ranks higher than the rule for the actual threat (92057) which could cause an analyst triaging by severity to look at the wrong event first
- A tuning fix would lower 92213 or scope it to exclude the `PSScriptPolicyTest` temp files


## Result
- No need for a custom rule; default was sufficient
![Detection-Result](detection-screenshots/SusPowershell.png)


## MITRE
- T1059.001 (Command and Scripting Interpreter: PowerShell)
