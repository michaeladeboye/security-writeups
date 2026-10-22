# Security Writeups

Home lab builds, detection engineering, blue team investigations, web exploitation labs, and CTF solutions.
IS&T + Cybersecurity @ UTSA.

## Home Lab & Detection Engineering
- [Build notes](home-lab/) — Kali attacker, Windows 11 + Sysmon endpoint, Wazuh SIEM on an isolated network
- [Detection rules](detection-rules/) — 4 attack-and-detect cycles with custom Wazuh rules, mapped to MITRE ATT&CK

## Blue Team Labs (CyberDefenders)
- [Web Investigation](cyberdefenders/web-investigation.md) — PCAP analysis of a SQLi → admin login → web shell upload chain, with IOCs, ATT&CK mapping, and detection ideas

## Web Exploitation (PortSwigger Web Security Academy)
- [SQL Injection](webacademy/sql-injection/) — retrieving hidden data, login bypass
- [Cross-Site Scripting](webacademy/xss/) — reflected and stored XSS
- [Clickjacking](webacademy/clickjacking/) — framing attack against a CSRF-protected action

Each lab covers the exploit, root cause, and remediation.

## CTFs
- [OverTheWire: Bandit](bandit/) — Linux fundamentals, levels 0–33

## Incident Handler's Journal
- [Journal](incident-handler-journal.md) — incident handling, Wireshark, tcpdump

## Tools
- [domain-scanner](https://github.com/michaeladeboye/domain-scanner) — Python tool that checks domains for missing security headers (HSTS, CSP, X-Frame-Options), TLS cert expiry, and TLS 1.2+ support
